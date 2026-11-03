---
name: xiaohongshu-ops-lessons
description: >-
  做小红书采集/登录/详情拉取前必读：会话卫生、设备登录超限、check-login 误伤、手机登录≠方框 Chrome、详情重试纪律。与
  xiaohongshu-skills（A012）配套；提到小红书操作踩坑、登录墙、电脑设备登录超限、get-feed-detail 失败时使用。
---
# 小红书操作踩坑与会话卫生（可复用经验）

配套 Skill：[xiaohongshu-skills](sand-workflow:xiaohongshu-skills)（清单 A012）。**唯一执行面**仍是该仓库 CLI + Bridge `:9333` + Chrome 扩展 XHS Bridge；本技能只沉淀「怎么少踩坑」，不另起 MCP 或自写爬虫。

根目录：`/home/box/agent-data/workflows/xiaohongshu-skills`  
入口：`cd … && uv run python scripts/cli.py <子命令>`

---

## 0. 硬约束（组织规则）

1. 凡「去小红书搜索 / 发小红书 / 登录 / 点赞收藏评论」→ **只用** A012，禁止其他小红书 MCP 或临时 scrape。
2. **发布与评论**须先经负责人确认后再执行。
3. 密钥、cookies、二维码原图路径可本地暂存，**不明文写入 Memory**。

---

## 1. 登录与会话（最高频翻车点）

### 1.1 `check-login` 会副作用

- 未登录或会话飘忽时，`check-login` 常会 **打开/刷新登录页、弹出二维码**，甚至把已可用会话搅乱。
- **会话已证明可用后**（`search-feeds` / `get-feed-detail` 已成功返回）：
  - **禁止**再跑 `check-login` / `get-qrcode` / `wait-login` / `delete-cookies`「再确认一下」。
  - 用业务命令成败当登录探针，比反复 check 更安全。

### 1.2 手机网页登录 ≠ 方框 Chrome 已登录

- 用户在 **手机浏览器**扫码/验证码登录，登录的是手机侧会话，**不会**自动落到 Bot 方框里的 Chrome + Bridge。
- 正确做法：在 **方框桌面 Chrome**（已装 XHS Bridge）上出现登录模态时，用小红书 App 扫 **该模态里的二维码**；必要时把桌面画面交给用户扫。
- 二维码会过期；过期后只刷新 **同一 Chrome 会话** 的码，不要换端「随便登一下」。

### 1.3 「电脑设备登录超限」

- 症状：登录页提示设备数超限、反复 QR、详情/搜索 461 或导航失败。
- **不要**硬重试登录循环或 `delete-cookies` 清了再登（易加重风控）。
- 先停登录类命令；请用户在小红书 App / 账号安全里退出不用的电脑设备，再在方框 Chrome **单次**扫码。
- 超限未解除前：**不要**批量 `get-feed-detail` 硬重试。

### 1.4 Bridge / 扩展

- CLI 依赖本机 Bridge `9333` + 扩展注入；扩展未就绪时不要改用「免登录公开页抓取」当替代方案。
- 扩展/Bridge 挂了：按 A012 文档重启 Bridge、确认扩展启用，再试一条轻量 `search-feeds`。

---

## 2. 搜索 → 精选 → 详情

### 2.1 工作流

1. `search-feeds` 多关键词（视频/最多点赞等）→ 落盘 JSON。
2. 人工或脚本 **精选**（均衡口岸/主题），写出 `selected.json`：至少 `id` + `xsecToken`。
3. `get-feed-detail --feed-id … --xsec-token …` **逐条**拉正文；`id` 与 `xsec_token` 必须来自同一次搜索配对。

### 2.2 详情拉取纪律（实战有效）

- 间隔 **10–15 秒**；失败最多再试 **1** 次。
- 详情阶段 **禁止**穿插 `check-login`。
- 列表标题可写调研骨架；**旁白/流程口播以详情 `desc` 为准**（不少笔记正文极短，几乎只有话题标签）。
- 交付脚本末尾可附 explore 链接（Agent 内复开用）：`https://www.xiaohongshu.com/explore/{id}?xsec_token={token}&xsec_source=pc_search`。
- **给人点开（重要，A086）**：`/explore/…?xsec_token=…` 网页直链对外常进登录墙或 404，**不要当「可点交付」**。优先：① 完整标题 + 作者（手机 App 内搜）；② 已登录方框 Chrome 打开笔记 → 分享 → **复制链接**（短链如 xhslink）再发人。设备超限时先别抄短链，先发搜词救急，再私聊扫码。

### 2.3 失败分类

| 现象 | 优先动作 |
|------|----------|
| 登录墙 / 没有 feeds | 停搜索风暴；按 §1 修方框会话后再搜 |
| 详情 461 / 导航失败 | 停批量；确认未在 check-login；会话稳后再短间隔重试 |
| token 无效 | 用该条搜索结果里的原 `xsecToken` 重配，勿拼错源 |
| 设备超限 | §1.3，不硬重试 |

---

## 3. 内容合规（通关/口岸类）

- 边检、闸机、证件页：**口播可以，实拍不要**；脚本里写明禁拍区。
- 时间、费用、班次以官方/本人实测为准；参考笔记数字只作旁白素材，**勿逐字照搬**。

---

## 4. 交付物建议结构

- `research-notes.md`：关键词、条数、限制说明、精选表
- `details/{id}.json` + `_index.md`
- 脚本方案：分镜 + 来自正文的旁白素材 + **文末参考链接清单**

---

## 5. 一页口令（给人看）

**只用 A012 → 方框 Chrome 扫码 → 会话可用后别再 check-login → 搜索配对 token → 详情慢拉少重试 → 超限先清设备再登 → 发布评论先问人。**
