# 组织安装说明（Grok Bot 盒机）

- 来源：https://github.com/eze-is/web-access （v2.6）
- Skill：`/home/box/agent-data/workflows/web-access`（飞书 A066，record `reczz28SkQrQKzJK`）
- 用户数据：`~/.web-access/config.env`、`~/.web-access/site-patterns/`
- Node：`~/.local/node/current`（v22.21.0），PATH 已写入 `~/.bashrc`
- 浏览器：`WEB_ACCESS_BROWSER=/home/box/chrome-profile/Fork-3`，`WEB_ACCESS_CDP_PORT=9225`
- 本地补丁：`scripts/cdp-proxy.mjs` 的 `discoverUrl` 在无 wsPath 时改走 `/json/version` 取完整 `webSocketDebuggerUrl`（否则只拼 `/devtools/browser` 会 non-101）
- 与现网：盒机 GUI 默认仍走 `box-desktop`；小红书等走既有共用 Skill。web-access 作 CDP/联网策略增强备用
- 状态（2026-10-28）：`check-deps` 通过；CDP Proxy `:3456` `connected:true`
