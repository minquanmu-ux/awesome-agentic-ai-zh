# Changelog

Last 14 days of substantive changes. Older history lives in `git log`.

Format: `YYYY-MM-DD · category · 1-line summary (commit-sha)`.

---

## 2026-06-12

- **content** · Claude Fable 5 (Mythos-class, `claude-fable-5`, GA 2026-06-09) added as the new top Claude tier across the trilingual roadmap — model tables in `CLAUDE.md` / `examples/` / stages 01·06·07·07.5·08 + glossary frontier entry; Opus 4.8 reframed as Opus-class flagship + Fable 5 safeguard-fallback. No fabricated context-window or benchmark numbers (Anthropic published none — marked "not yet published"). Also fixed a pre-existing `claude-opus-4-7` → `claude-opus-4-8` inconsistency (`12980b3`).
- **content** · Stage 5 — new **5.6 Dynamic Workflows** section after 5.5 Subagents (ecosystem-level intro + cross-link to the 7.5 deep-dive, no duplication); old 5.6 Source → 5.7, old 5.7 SDK → 5.8, all in-file refs + 7-Layer-map ranges + cross-file anchors (glossary / stages 03·06·07) relinked, tri-locale (`5044008`).
- **catalog** · `1weiho/open-slide` (★4.9k, MIT) added to §2 as an agent-native slide framework — ships Claude Code Skills, distinct from Stage 4 orchestration frameworks; tri-locale (`7d3fd5d`).
- **docs** · MCP/Skills catalog count made drift-proof — stale `62` → robust `65+`, category count reconciled to 15, across 33 files / all locales (`3782dd4`). Propagated the 7→8 stage reality into design notes / style-guide / reader docs (`39d397a`) and fixed outreach-draft count drift (`25785f0`).
- **outreach** · send-day copy-paste packages playbook for awesome-list submissions (`afd7a76`).
- **content** · per-chapter improvement audit (12-agent fan-out + skeptical filter) → 5 gap-fills, all tri-locale: Stage 3 lethal-trifecta security callout + MCP router note + glossary (`f3bde60`); Stage 1 next-token / sampling mental-model box (`1bd171f`); Stage 5 Hooks (L3 control layer) subsection (`9d2897f`); Stage 7 Loop Engineering note + glossary (`eb8e64c`).
- **catalog** · new Web Search / Retrieval category (exa-mcp + tavily-mcp) + Context7 in Dev-Collaboration; category count 15→16 (`b1718d3`).

---

## 2026-05-31

- **tooling** · pruned the ops-metric scripts that don't touch stars or URL validity (strategic-review action #1, scoped down per maintainer): removed `scripts/snapshot-traffic.py` (GitHub traffic snapshots), `scripts/refresh-outreach-status.py` (outreach-matrix drift), `scripts/check-catalog-staleness.py` (dormant-entry pinger), and the `docs/traffic/` snapshot dir. **KEPT** the weekly stars + URL auto-update (`weekly-catalog-refresh.yml` + `lint.yml`'s `star-drift` job) — the maintainer values the weekly cadence for star-count refresh and link-rot checking. All correctness + trilingual-parity guards intact (anchor / link-rot / mirror-sync / stage-template / banned-words / overclaim / zh-Hans-localize).

---

## 2026-05-26

- **ci** · `lint.yml` overclaim check expanded (P3-G from audit) — promoted from case-sensitive exact-phrase to case-insensitive (`grep -Fi`), broadened scope to include `tracks/` `examples/` `resources/` (which the previous narrower scope missed — letting 5 uppercase `Production-grade` H2 headers in `examples/` slip through the earlier sweep). Strict-blocking list now includes all style-guide §3 phrases (`首選` / `首选` / `唯一選擇` / `唯一选择` / `業界最佳` / `业界最佳` / `業界最強` / `全世界最好的` / `最緊迫` / `the most canonical`) plus English equivalents (`production-grade` / `world-class` / `best-in-class` / `cutting-edge` / `state-of-the-art` / `industry-leading`). Corpus pre-cleaned across tri-locale before flipping to strict.
- **content** · overclaim residue swept across tri-locale (18 file edits) before the lint flip — 3 × `## Production-grade …` H2 headers in `examples/stage-{6,7}/` normalized to `## Production-ready …`; 3 × inline `首選` in `stages/05` / `stages/06` / `tracks/cli/A1` softened per style-guide §3; `tracks/cli/A1` `最完整的中文社群資源` → `中文社群資源豐富` (marketing → factual).
- **tooling** · `scripts/snapshot-traffic.py` shipped — captures weekly 14-day traffic window (views / clones / referrers / paths + point-in-time totals) to `docs/traffic/snapshots/YYYY-MM-DD.json` so historical trend survives the GitHub API's 14-day visibility limit. Each file ~5 KB. First snapshot included (`docs/traffic/snapshots/2026-05-26.json`).
- **tooling** · `scripts/refresh-outreach-status.py` shipped — reads `.github/channel-partners.md`, extracts PR URLs, queries `gh pr view`, reports drift between recorded status and live PR state (merged / closed / ghosted / approved). Report-only (text / markdown / json), `--check` for CI. Closes P2-F from the 2026-05-25 audit; P2-E closed by snapshot-traffic.

---

## 2026-05-25

- **tooling** · `scripts/check-catalog-staleness.py` shipped — queries `gh api repos/<owner>/<repo>` for `pushed_at` + `archived`, flags catalog entries dormant >= N months (default 12) or archived. Report-only (text / markdown / json). Initial run on the 247-repo catalog surfaced 17 stale entries: 5 archived (incl. `langchain-ai/langserve` archived 2026-05-05 still cited as live, `RooCodeInc/Roo-Code` archived 2026-05-15 in setup-guide) + 12 dormant (oldest: `microsoft/prompt-engine` 37 mo).
- **i18n** · Stage 1 + Stage 2 mirror schema resync — `## 🎯 Curated Projects` regenerated from canonical (en hand-translated · zh-Hans via opencc tw2s + zh-hans-localize vocab); −358 lines of stale H3-card format replaced with compact-table parity to canonical. Also normalized 5 Stage 1 .zh-Hans H2 titles back to canonical wording + emoji. Eliminates the forward-schema drift across all 8 stages.

---

## 2026-05-19

- **catalog** · `microsoft/ai-agents-for-beginners` added to Stage 3 選讀/進階補充 as a parallel beginner course (explicitly *not* a substitute for the stage's hands-on practice), tri-locale (`2d83f72`, `94f2d73`).

## 2026-05-18

- **catalog** · Kimi-K2 + GLM-4.5 added to §11 中文圈專用 — neutral schema, gh-verified Stars/License, tri-locale (`fd81f31`, `ad80845`).
- **ci** · weekly catalog-refresh PR now guarded auto-merge: sanity guard (star-token-only diff, ≤150 lines, anchors pass) → squash-merge, else label `needs-manual-review` (`3dc6ecd`).

## 2026-05-17

- **docs** · per-track Capstone + 4-level self-assess rubric (`CAPSTONE`), tri-locale (`dbf1ef3`, `a31dde5`).
- **docs** · Pages unified — mkdocs at `/`, mdBook at `/book/`, one workflow; README's GitHub-only switcher stripped from rendered site (`5e59c7c`, `001d765`).
- **docs** · README positioning reframed (trilingual, English fully maintained); stale exercise-folder count corrected 27 → 23 (`b4bb862`, `24a87fe`).
- **outreach** · English-audience launch drafts — HN / Reddit / newsletters / awesome-lists (`b8f365b`).

## 2026-05-16

- **governance** · CoC + SECURITY + CITATION.cff + issue-template config added, tri-locale mirrors (`9aa2963`, `84bc58f`).
- **docs** · public ROADMAP.md + learner PROGRESS.md tracker added, tri-locale (`e5cc310`, `3e628e9`).
- **docs** · GitHub Pages site (mkdocs-material, trilingual) + live docs-site badge (`498932c`, `ea4530f`).
- **i18n** · zh-Hans mainland-localization pass + Lint gate blocking Taiwan-vocab/「」 drift (`7f73b8a`, `805ae57`).
- **visuals** · final ASCII concept blocks replaced with generated PNGs — 10/10 complete (tri-locale) (`21a2bbf`).
- **ci** · actions bumped off deprecated Node20 ahead of June 2026 forced migration (`c6a8c19`).
- **outreach** · CONTRIBUTORS — @demo112 (#14) + @Rain120 (#18) (`7040738`).

## 2026-05-15

- **content** · Stage 1 §主流 LLM 家族對比 (US 3 + China 7 + Western-OSS 4 + decision tree + benchmark + caveat) (`8f578bf`).
- **content** · Stage 5 §7-Layer Architecture Map (Claude primitives × 3 engineering disciplines) + embedded figures (`5f99bbb`, `1e5a12b`).
- **content** · subagent teaching deepened — dispatch who/how/what, vs Skill/Slash-Command disambiguation, advanced doc + figures (`009ddf9`, `21c555b`, `e8a919e`).
- **content** · 5 audience branches tableized (使用情境 / 流程 / Tier ladder) + academic-style polish, tri-locale (`184015b`, `6b7e5f6`).
- **i18n** · 97 broken outbound mirror anchors fixed + anchor-checker now enforces mirror files (`e1991a6`, `ab3a6d0`).

## 2026-05-14

- **content** · NEW Stage 7.5 — Advanced Agentic Concepts (OpenAI Harness Engineering 5 principles, Why→What→How map, work-boundary diagram) (`4a6bf18`, `e2c1d11`).
- **content** · Track A3 §6 advanced-concept playbooks for daily CLI work (`876a457`).
- **visuals** · § (513×) and 🔄 (24×) symbols stripped across all user-facing docs; concept diagrams embedded as PNG × 3 locales (`29eb774`, `d04c224`).
- **catalog** · 4 Anthropic-related resources added across stages (`0af7fbc`).
- **ci** · weekly catalog-refresh workflow + `--apply` flag (`dc91a8b`).

## 2026-05-13

- **content** · Stage 4/6/7 verified + merged to main (`cdb0ae3`); Stage 8 NEW — Agent Interfaces, §1-15 across 3 commits A/B/C (`b83c894`, `6c87a2f`, `069406f`).
- **content** · curation positioning crystallized — exercises reframed foundational/illustrative; repo = curation hub + simple cases, depth → hello-agents (`00dc046`, `0206dbc`).
- **content** · 精選 Projects consolidated to single 適合誰 tables across Stages 0-8 + Track A (`fd94d80`, `19a14a8`).
- **content** · Stage 5 expanded (§5.1-5.6: Claude Code basics, MCP/Plugin/Skill 定位, §5.5 Subagents, Harness Internals) (`2c3f1dd`, `f7de4e7`).
- **content** · Stage 6 RAG-first restructure + GraphRAG / Contextual Retrieval / Hybrid Search; 2026 frontier-model refresh (`f00e2c2`, `acbc9dc`).
- **ci** · 4 checks added — anchor validator, mirror-sync reminder, 2026 freshness, stage-template enforce (`a14c809`, `4491e6e`).
- **i18n** · 8-stage tri-locale mirror catch-up via Codex + Gemini delegation; 37 legacy anchors fixed, validator → strict (`8b39c75`, `706d257`).
- **catalog** · whale (DeepSeek terminal) + a-stock-data added to Chinese ecosystem (#14) (`3d375bd`).

## 2026-05-12

- **content** · examples/ bootstrapped — Stage 1 (6) + 2 (4) + 3 (6) + 4 (5) + 6 (5) + 7 (5) inline starters + folder examples, tri-locale (`c1fcaa7`, `8051861`, `7d2c1b7`).
- **content** · dual-path examples — Ollama (default, cost-driven) alongside Anthropic; per-stage budget + LLM recommendation list (`bc37ad8`, `3fa5410`).
- **content** · tool-calling-tutor — installable Claude Code skill + Stage 5 §5.3 meta-example (`3584669`).
- **i18n** · diagrams renamed `.zh-Hans.png` per BCP 47 / W3C convention (`78797a3`).

## 2026-05-11

- **accessibility** · `resources/setup-guide.md` (3 langs) — addresses the dev-fluency assumption gap that subagent audit flagged across 5 non-dev branches. 5 sections covering API key registration, Python install, hello-world, Claude Code first auth, SKILL.md primer (`3c88b2b`). Plus 15 branch-top callouts on all 5 audience branches. `resources/README.{en,zh-Hans}.md` created for trilingual parity.
- **accessibility** · README — promoted setup-guide pointer to top of Quick Start across all 3 langs (`ad47706`). Was buried in Related Resources where non-dev visitors hit technical walls before discovering it.
- **accessibility** · setup-guide opens with a 4-tier on-ramp (Web / Desktop / CLI / API) + official download URLs for Claude.ai, ChatGPT, Gemini, Le Chat, Claude Desktop, ChatGPT Desktop, LM Studio (`3c89952`). Replaces the abstract "decide two things" intro so non-dev readers see "just use claude.ai for free" as the first option, not "register API key → install Python".
- **accessibility** · setup-guide adds a 3rd tier between Desktop and CLI: **IDE with built-in AI** (Cursor, Windsurf, Cline, Continue, Roo Code, Zed, GitHub Copilot) with download URLs (`7e14093`). Distinguishes "AI sidekick while you write code" from "agent runs autonomous task in terminal".

## 2026-05-10

- **funnel** · Stage 1 → Stage 2 callouts added across 3 langs to address visible drop in `traffic/popular/paths` (`0ee2a3a`)
- **outreach** · 3 awesome-list targets backfilled into channel-partners matrix from launch-checklist: `travisvn/awesome-claude-skills`, `WangRongsheng/awesome-LLM-resources`, `AiHubCN/Awesome-Chinese-LLM` (`90a6ad1`)
- **outreach** · PR #6135 to `punkpeye/awesome-mcp-servers` — addressed bot `name-check`, replied to non-applicable `glama-check` + `emoji-check` (`81a7313`)
- **content** · Cookbook Recipe 6 — **Local-LLM × CLI Agent walkthrough** (`5855852`). Bridges Stage 1 (local LLM) + Stage 5 (CLI agent) end-to-end. Explicitly notes Claude Code does **not** support local LLM as backend; routes readers to OpenCode / goose / Aider / Hermes instead. Stage 5 + cli-agents-guide also gain matching pointers.
- **catalog** · Hermes Agent (`NousResearch/hermes-agent` ★142k) added as 7th major CLI agent across `cli-agents-guide`, `tracks/cli/A1`, and 5 dependent files (`698f13a`). Differentiator: cloud-VM-native, model-neutral (200+ LLMs via OpenRouter / NIM / GLM / Kimi / etc.), self-improving skill loop.
- **i18n** · `*.zh-CN.md` → `*.zh-Hans.md` migration per BCP 47 / W3C compliance (`21b653d`). 25 files renamed, ~270 markdown lines updated, tooling (`sync-language-switchers.py`, `lint.yml`, `generate-stage5-stack.py`) migrated. Thanks [@xfq](https://github.com/xfq) (W3C i18n lead) for flagging in [#9](https://github.com/WenyuChiou/awesome-agentic-ai-zh/issues/9). Added to CONTRIBUTORS (`868691d`).
- **visuals** · English README hero (`banner.en.png`), Learning Map (`learning-map.en.png`), and Branch Decision Tree (`branch-decision-tree.en.png`) refreshed to ChatGPT-rendered versions (`c7edff8`, `4be6b88`, `6c03c58`).

## 2026-05-09

- **outreach** · Day 1 PR sent: `punkpeye/awesome-mcp-servers#6135`, adding awesome-agentic-ai-zh to `## Tutorials` (`a0dc4d5`). Plan revised after upstream audit caught `hesreallyhim/awesome-claude-code` mid-reorg (Day 2 = issue not PR) (`708259c`).
- **outreach** · 8 channel-partner pitch templates created in `.github/outreach/` plus tracking matrix `.github/channel-partners.md` (`2f63745`). Targets: Datawhale, liyupi, HuggingFace, LangChain (kyrolabs), awesome-claude-code, awesome-mcp-servers, Zhipu, Moonshot.
- **catalog** · 11 中文圈專用 expanded from 2 → 7 entries: `QwenLM/Qwen-Agent`, `coze-dev/coze-studio`, `coze-dev/coze-loop`, `liaokongVFX/LangChain-Chinese-Getting-Started-Guide`, `chatchat-space/Langchain-Chatchat` (`4809039`).
- **funnel** · Stage 0 → Stage 1 callouts added (`3dfe761`).
- **ci** · zh-Hans companion files excluded from zh-TW banned-word audit (closes #7) (`3acc3f2`).

## 2026-05-08

- **content** · `for-teacher` branch expanded with 3-tier teacher AI use-case framework (Chen 2020, Mittal 2024) via @scott0127 PR #6 (`cd1cad4`).
- **content** · Stage 6 unit guide: memory + RAG overview via @scott0127 PR #5.
- **content** · Branch decision tree (zh-Hans) added, English banner added, `for-developer` branch thickened 56 → 138 lines × 3 langs.

## 2026-05-07

- **catalog** · 3 user-flagged gaps filled: `safishamsi/graphify`, `pbakaus/impeccable`, `netease-youdao/LobsterAI` + context-engineering and harness-engineering coverage.
- **content** · `resources/cookbook.md` added with 5 (now 6) step-by-step recipes covering Skill / MCP / Office / NotebookLM / Zotero / Local-LLM workflows.

## 2026-05-06

- **launch** · Repo announced to bilingual community. Star count: 0 → 519 in week one.
- **content** · `learning-map.png` polished, README hero banner placement finalized.

---

## Conventions

- Each commit SHA is clickable: `https://github.com/WenyuChiou/awesome-agentic-ai-zh/commit/<sha>`
- Categories: `content` (stages/branches/tracks) · `docs` (project meta-docs: README/ROADMAP/PROGRESS/CAPSTONE/Pages site) · `governance` (CoC/SECURITY/CITATION/issue templates) · `accessibility` (on-ramp/setup friction) · `catalog` (mcp-skills-catalog entries) · `funnel` (cross-stage navigation) · `visuals` (diagrams/banners) · `i18n` (translation/locale) · `outreach` (channel partners) · `ci` (workflows/lint) · `launch` (one-time events)
- Maintained manually; not auto-generated. Updated alongside substantive commits.
