---
name: xiaohongshu-skills
description: >-
  当用户要求操作小红书（登录、搜索笔记、看详情、发布图文/视频/长文、评论、点赞、收藏、竞品分析、热点追踪、复合运营）时使用。基于本仓库 CLI +
  浏览器扩展 Bridge，不走外部 MCP/其他小红书工具。
---
# 小红书自动化（共用）

全组织共用技能包。根目录固定为：

`/home/box/agent-data/workflows/xiaohongshu-skills`

执行前先用 Skill 加载本技能；需要细节时再 Read 对应子技能文件：

- `skills/xhs-auth/SKILL.md` — 登录 / 检查登录 / 退出
- `skills/xhs-publish/SKILL.md` — 图文 / 视频 / 长文发布
- `skills/xhs-explore/SKILL.md` — 搜索 / 首页 / 详情 / 用户主页
- `skills/xhs-interact/SKILL.md` — 评论 / 回复 / 点赞 / 收藏
- `skills/xhs-content-ops/SKILL.md` — 竞品分析 / 热点 / 批量互动等复合流程

路径相对技能根目录。子技能正文里若写 `python scripts/cli.py`，在本机一律改为：
`cd /home/box/agent-data/workflows/xiaohongshu-skills && uv run python scripts/cli.py ...`

## 技能边界（强制）

1. **唯一执行方式**：只运行本目录下的 CLI（上式）。
2. **禁止**：调用任何外部小红书 MCP、Go 工具、其他仓库脚本，或手写替代实现绕过 CLI。
3. **输出**：CLI 返回 JSON；用白话向用户汇报，不要原样倾倒大段 JSON，除非用户要原始数据。
4. **外发确认**：发布、评论、回复必须先在对话里展示拟发内容，**等用户明确确认后再执行**。点赞/收藏也先问一句再做（用户已说「直接赞」可跳过）。
5. **频率**：操作之间留合理间隔，避免短时间刷量触发风控。

## Grok Bot / 本机适配

本包跑在共享 box 上，浏览器是 bot 桌面里的 Chrome（不是用户个人电脑）。

### 一次性准备（首次或扩展丢失时）

1. 加载 Cursor-managed `box-desktop`，再派 computerUse 完成：
   - 打开 `chrome://extensions/`，开启开发者模式
   - 「加载已解压的扩展程序」→ 选 `/home/box/agent-data/workflows/xiaohongshu-skills/extension`
   - 确认扩展 **XHS Bridge** 已启用
2. 后台启动 Bridge（若未在跑）：
   `cd /home/box/agent-data/workflows/xiaohongshu-skills && uv run python scripts/bridge_server.py`
   （默认 `ws://localhost:9333`；用 `block_until_ms: 0` 挂起）
3. 扩展需保持连接；CLI 在 bridge 未就绪时会尝试自启 server，但仍需扩展已加载并连上。

### 日常执行顺序

1. 确认依赖：项目目录已 `uv sync`（缺依赖时在根目录再跑一次）。
2. 确认 bridge server + 扩展已连接。
3. 先 `check-login`；未登录则走 `xhs-auth`（扫码或手机验证码；扫码/验证码界面用 computerUse 协助用户完成）。
4. 按用户意图路由到子技能；文件路径一律用绝对路径。
5. 任务完成后汇报结果，停下等下一步，不要擅自串联未要求的操作。

## 意图路由

| 用户意图 | 子技能 |
|---------|--------|
| 登录 / 检查登录 / 退出 / 换号 | xhs-auth |
| 发布 / 发帖 / 上传图文视频长文 | xhs-publish |
| 搜索 / 首页 / 详情 / 用户主页 | xhs-explore |
| 评论 / 回复 / 点赞 / 收藏 | xhs-interact |
| 竞品分析 / 热点 / 批量互动 / 一键创作 | xhs-content-ops |

## 常用命令速查

工作目录始终为技能根目录，前缀：`uv run python scripts/cli.py`

- 认证：`check-login` / `login` / `send-code --phone` / `verify-code --code` / `delete-cookies`
- 发现：`list-feeds` / `search-feeds --keyword` / `get-feed-detail` / `user-profile`
- 发布（须确认）：`publish` / `publish-video`
- 互动（须确认）：`post-comment` / `reply-comment` / `like-feed` / `favorite-feed`

更完整参数与失败处理以各子技能 `SKILL.md` 为准。

## 失败处理

- **未登录** → 走 xhs-auth。
- **连不上 bridge（9333）** → 检查 server 与扩展。
- **扩展未加载** → 重做一次性准备。
- **超时 / 风控** → 降频；把错误摘要告诉用户。
- **Chrome/桌面异常** → 读 `/home/box/reference/debugging-the-box.md`，必要时请用户更新 Bot 电脑。

## 来源

上游兼容 https://github.com/xpzouying/xiaohongshu-skills 。本目录为组织内安装副本。
