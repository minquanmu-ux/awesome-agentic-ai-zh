> **繁體中文** | [简体中文](./README.zh-Hans.md) | [English](./README.en.md)

# 練習 5：Error Handling + Retry wrapper

對應 [Stage 1 — LLM 基礎](../../../stages/01-llm-basics.md) 練習 5。

## 為什麼這題重要

Stage 3-7 的 production agent 一定會碰到 API 錯誤：
- Rate limit（429）→ Anthropic 訂閱階級不一樣、隨時可能撞到
- 網路抖（connection reset）→ 跨機房 / VPN 是日常
- API key 過期（401）→ rotate 沒同步
- Context 過長（400）→ 你給太多歷史對話

**有些錯誤該 retry（rate limit / 網路）、有些不該（key 錯、context 滿）**。沒分清楚 = 寫 production agent 的常見坑。

## 怎麼跑

```bash
pip install -r requirements.txt
export ANTHROPIC_API_KEY=sk-ant-...
python starter.py
```

預期看到（樣本）：

```
[情境 1] 故意用壞 API key
  ✅ 抓到 AuthenticationError: 401
  💡 production 處理: 立刻 alert、stop retry（key 不會自己變對）

[情境 2] 正常 call、with_retry 包裝
  ✅ 成功、第一次就過: 👋

[情境 3] Prompt 超過 context window
  ✅ 抓到 APIStatusError: 400
  💡 production 處理: 在 client 端先 count token、超過就拒、別浪費 API call

✅ 練習 5 通過 — 你已了解 3 種錯誤如何 raise、知道何時該 retry 何時該 stop
```

## 不花錢驗證程式邏輯（不需真的斷網）

```bash
python test.py
```

6 個 test 都用 `unittest.mock` 構造假錯誤 + 假 sleep（時間 0 秒）、驗證 retry 邏輯：

```
✅ test_no_retry_when_success_first_time
✅ test_retry_on_connection_error_then_success
✅ test_retry_on_rate_limit
✅ test_raise_after_max_attempts
✅ test_no_retry_on_auth_error
✅ test_exponential_backoff_delays

🎉 全部通過 — retry wrapper 邏輯正確（RETRIABLE 才 retry、exponential backoff 有效）
```

## 程式結構走查

| 段 | 在做什麼 |
|---|---|
| `RETRIABLE = (APIConnectionError, RateLimitError)` | 白名單：只 retry 這兩種、其他直接 raise |
| `with_retry(fn, ...)` | exponential backoff wrapper：1s, 2s, 4s, 8s + jitter |
| `demo_bad_key()` | 故意用假 key、看 AuthenticationError 屬性 |
| `demo_with_retry()` | 正常 call 包 with_retry、預期 1 次成功 |
| `demo_too_long_prompt()` | 1.5M token prompt、看 APIStatusError 怎麼 raise |

## 常見坑

1. **無腦 retry 所有 exception**：你會把 AuthenticationError 也 retry 一遍、浪費 4 倍時間最後 still 401。RETRIABLE 白名單是核心
2. **Backoff 不加 jitter**：1000 個 worker 同時被 rate limit、同時 1s 後重試、再次 rate limit → 死循。加 `random.uniform(0, 0.3)` 打散
3. **max_attempts 太高**：retry 8 次 = 1+2+4+8+16+32+64+128 = 255 秒、user 早就 give up。`max_attempts=4` 通常夠
4. **沒記錄 attempt count**：production 一定要把 retry 次數加進 metric、超過 threshold 該 alert
5. **rate limit response 帶 `Retry-After` header**：API 告訴你等多久、Anthropic SDK 已自動處理，但自寫 wrapper 別忽略這個 hint

## 延伸

- **加 jitter strategy**：除了 uniform、可試 [decorrelated jitter](https://aws.amazon.com/blogs/architecture/exponential-backoff-and-jitter/)（更穩）
- **加 circuit breaker**：連續 N 次 retry 失敗、暫時 stop call（避免 wave-after-wave 打死下游）
- **改用 [tenacity](https://github.com/jd/tenacity)** library：production 不要自己寫 retry、用成熟 lib（這份 starter 只是給你看裡面是什麼）
- **錯誤分類更細**：依 status code（429 / 503 / 502 / 500）給不同 backoff strategy
