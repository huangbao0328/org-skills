---
name: transcript-healthcheck
description: >-
  Use when scanning fleet chat transcripts for org friction (skill | bot |
  routine proposals), the Monday 「等 Bob」阻塞周拉, Memory layer / 原则疑似共享闸门 / M3查重抽查,
  S7 规则25任务经验漏写当场派修, S8 跨岗禁纯私聊, and S3 交验收无检查项抽查, especially the
  transcript-healthcheck routine. Prefer search-index.db over Cursor-style
  agent-transcripts paths.
---
# Transcript healthcheck

Scan recent multi-agent chat for **org friction worth proposing**, plus a Monday **「等 Bob」阻塞周拉**, **S7 规则25 任务经验漏写 → 当场派修**, **S8 跨岗禁纯私聊**, and **S3/21.a 交验收无检查项**. Output suggestions only for friction/bot/routine. For S7 漏写：**当场点名负责人补写**（小O 派活盯闭环，**禁止代写**）。Do **not** create/edit skills, bots, or routines until the owner picks an item（S7 补写飞书行除外——属规则25已批纪律）。

## Ambient Scope（试点 · 小O｜至约 2026-11-13）

跑本技能前先读 `/workspace/org/ambient-scope-xiaoO-routines-v0.1.md` → **transcript-healthcheck** 节。出 Scope 先停再问；禁止「为你好」扩权。线上例行正文若未贴 Scope，以该文件 + 本岗 profile Memory 为准。

## Source of truth (Grok Bot)

Primary index: `/home/box/agent-data/search-index.db` (also mirrored at `/home/box/sand-data/search-index.db`).

- Table `messages`: `agent_id`, `entry_id`, `role` (`user`|`assistant`), `timestamp_ms`, `body`, `seq`
- There is **no** `/home/box/agent-data/agent-transcripts/` on this platform — do not look for it
- Map `agent_id` → display name via `/home/box/agent-data/agents/<id>/profile.json` (`name` / `title`)
- Optional deepen: `ReadTranscript` with `agent_id` for a single agent when the index body is too short

## Window

- Since last **successful** run of this healthcheck, else last **24h**
- Convert `timestamp_ms` to the owner's timezone when reporting times

## Steps

1. Resolve window start/end; note it in a short scratch `manifest` under `/workspace/transcript-healthcheck-YYYY-MM-DD/` if useful for the run
2. Pull messages in-window from `search-index.db` (SQL/Python). Skip empty agents
3. Mine for friction signals (examples, not exhaustive):
   - Routine woke but blocked / empty output (missing URL, connector, board, credential)
   - Repeated redo, contradiction then correction, unclear ownership
   - Role overlap / 串味 across bots
   - Skill missing or recipe path wrong for this platform
   - Attention tax: noisy digests, filler when nothing changed
   - **P3 拍板回写抽查（手册规则 18）**：窗口内若出现「Bob 拍板 / 群内定稿 / 原则确认」类结论，检查是否已回写绑定 Skill、飞书清单或手册；跨岗接棒是否只在私聊完成而未进 L2/L3（产品链默认「产品交付协作」）。未回写或纯私聊接棒 → 记一条 `skill | bot` 提案，勿自动回写
   - **L3 Owner 主报抽查（S2）**：产品交付协作群内是否多人同答同一澄清 / 非 Owner 刷进度；有则记一条提案，勿自动改群
   - **Memory 分层监督（规则 19 · 原则疑似共享闸门）**：窗口内若 Bot 写入或声称「记得」类内容，抽查是否错层——① 全员硬规则只进 M4；② 教训长故事灌 M3；③ **疑似原则相关却不准备进 M3、且未主动问 Bob 就只落 M4**（破坏闸门）；④ 可复用做法只留 journal 不写 M2；⑤ **写 M3 不查重 / M3 长篇堆砌**。有证据 → 记 `skill | bot` 提案（勿代写 Memory、勿替 Bob 筛共享层）。口径见 `/workspace/org/memory-principle-ask-bob-v0.1.md` 与 `/workspace/org/memory-layers-v0.1.md`
4. **S1「等 Bob」周拉（手册监督补丁）**：从窗口内聊天抽出**仍阻塞在人**的事项（等 Bob 拍板、等确认 URL/验收、等付钱/改权限等）。格式一行一条：`事项｜等谁｜已等约 N 天`。只列证据明确的阻塞；勿把进行中进度表塞进来。无阻塞 → 本节不报。全文口径见 `/workspace/org/supervision-reporting-v0.1.md`
5. **S7 规则25 任务经验派修（Bob 2026-11-01）**：抽查窗口内是否有明确 **T1 采纳签字** 或 **与 Bob 搁置** 证据，却无飞书 `任务经验` 对应行。有漏 → **当场点名**负责人（执行岗／群 Owner）按 [task-experience](sand-workflow:task-experience) 补写；报告格式：`漏写｜负责人｜证据一句｜已派修`。小O **禁止代写**；不把「是否写库」再拖成等 Bob。无触发证据 → 本节静默（勿造假经验）。口径 `/workspace/org/supervision-reporting-v0.1.md` S7。
6. **S8 跨岗禁纯私聊（Bob 2026-11-02）**：窗口内已跨岗接棒却全程只私聊、或绕过 Owner 直捅执行 → 记 `事项｜私聊双方｜应进现场｜建议`；可点名 Owner 补进群，**禁止代写交接正文**。合法例外见 supervision S8。无证据 → 本节静默。
7. **S3/21.a 检查项抽查（Bob 2026-11-02）**：窗口内已交非代码验收（brief/原型/分析/编制）却无检查项+证据 → 记 `skill | bot` 提案一行，勿代写检查项。网页/WebQ 不在本项。无证据 → 本节静默。
8. Rank; keep only items worth the owner's bandwidth
9. Report as `skill | bot | routine` proposals；S1 / S7 / S8 / 21.a 可各成一节
10. **Stay quiet** if nothing worth proposing **and** no S1 阻塞 **and** no S7 漏写 **and** no S8 **and** no 21.a 漏项 — no filler
11. Hard stop: friction 类只报等 Bob 点；**S7 派修可立刻 SendToAgent 点名**（不代写）；S8 可点名 Owner 补进群（不代写）

## Anti-jobs

- Do not auto-create skills, bots, or routines from the report
- Do not modify another bot's profile/routines without explicit owner OK
- Do not invent friction or 阻塞; cite concrete message evidence
- Do not turn S1 into a full status digest
- Do not auto-migrate Memory layers or decide M3 for Bob; only propose
- Do not turn Memory 抽查 into a full Memory audit of every bot
- Do not 代写任务经验行；S7 只派修
- Do not 代写跨岗交接正文或检查项清单；S8/21.a 只提案或点名

## Companion

Pair with `routine-healthcheck` for schedule/token waste. This skill is about **conversation friction + 等 Bob 可拉 + Memory 分层抽查 + 规则25 派修 + S8 跨岗禁纯私聊 + 21.a 检查项**, not cron inventory alone.
