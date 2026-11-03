# org-skills

组织可复用工作流与技能镜像（源：Grok Bot 盒机 `/home/box/agent-data/workflows`）。

## 结构

- `workflows/<skill-id>/` — 每个技能一目录（含 `SKILL.md` 与附属文件）
- 不含 `.venv` / 嵌套 `.git` / `__pycache__`
- Cursor 平台只读技能不在此仓；本仓仅组织自建 / 已安装到 workflows 的技能

## 同步约定

- 首轮与后续巡检由大全例程执行：对比盒机 `workflows` 与本仓，有新增或内容变更则提交并开/更新 PR
- 两周巡检一次；无变更则静默
- 秘钥与 App Secret 禁止入库

## 关联

- 飞书「内部应用与Skill清单」
- 组织规则手册（`workflows/org-rules-handbook`）
