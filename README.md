# org-skills

组织**自建**可复用工作流与技能镜像（源：Grok Bot 盒机 `/home/box/agent-data/workflows`）。

## 同步口径（Bob 2026-11-03）

- **只上传我们自己制作的 skills**
- **配置/安装的外部 skills 不上传**（设计 kit 薄封装、getnote / IMA / 微信读书等厂商包、anatomy 等第三方）
- 权威白名单：根目录 `MIRROR_ALLOWLIST`（一行一个 skill-id）
- 双周巡检（大全 Ambient B）：仅对比白名单；仓内白名单外目录应删除

## 结构

- `workflows/<skill-id>/` — 白名单内每个技能一目录（含 `SKILL.md` 与附属文件）
- 不含 `.venv` / 嵌套 `.git` / `__pycache__` / `node_modules`
- Cursor 平台只读技能不在此仓

## 关联

- 飞书「内部应用与Skill清单」
- 组织规则手册（`workflows/org-rules-handbook`）
