---
name: superdesign-skill
description: >-
  当用户要设计/改版页面、功能流、设计系统、幻灯片或海报封面，需要在 Superdesign 画布上找方向、出多方案并迭代（而不是直接堆默认 shadcn）时使用。
---

# Superdesign Skill

上游：[superdesigndev/superdesign-skill](https://github.com/superdesigndev/superdesign-skill)  
本地 kit：`/home/box/agent-data/design-kits/superdesign-skill`（本目录 `vendor/` → 同路径）

这是 **Agent Skill + CLI 产品**，不是组件库。完整流程以 vendor 技能为准。

## 必做顺序

1. **加载完整配方**：Read  
   `/home/box/agent-data/design-kits/superdesign-skill/skills/superdesign/SKILL.md`  
   以及它引用的 `references/*.md`（按任务选 INIT / SUPERDESIGN / PRESENTATION / GRAPHIC 等）。
2. **CLI 预检**（每个会话先跑一次）：
   ```bash
   npx --yes @superdesign/cli@latest
   ```
   若未登录：`npx --yes @superdesign/cli@latest login`（或全局装 `@superdesign/cli` 后 `superdesign login`）。无账号则停在说明，引导用户去 https://superdesign.dev，**不要假装已经出稿**。
3. 有真实前端仓库时：按 vendor 的 init / resume 路径写 `.superdesign/` 上下文；空沙箱则先问清产品/受众/风格再走 brand-new project。
4. 用 CLI 搜风格、抽网站 DNA、建 draft、迭代（replace vs branch 按 vendor ITERATION MODE）。

## 常用 CLI（一律用 npx 最新）

```bash
npx --yes @superdesign/cli@latest search-prompts --query "<keyword>"
npx --yes @superdesign/cli@latest extract-website --url https://example.com --design-md
```

更多命令以 vendor SKILL 与 README 为准。

## 边界

- 不要与「只抄一个组件库」混淆；本技能管设计判断与画布草稿。
- 需要落地 React 组件时，再配合 [uilayouts](sand-workflow:uilayouts) / [motion-primitives](sand-workflow:motion-primitives) / [better-design](sand-workflow:better-design)。
- 归因：上游 MIT；产品能力依赖 Superdesign 云端服务。
