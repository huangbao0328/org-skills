---
name: design-taste
description: >-
  当用户要避免「AI 味」界面、做落地页/作品集/营销站、声明设计方向，或点名 editorial-minimal、dark-tech、cinematic-motion 等风格包时使用。
---

# Design Taste

上游：[madebymustafa/design-taste](https://github.com/madebymustafa/design-taste)  
本地 kit：`/home/box/agent-data/design-kits/design-taste`（24 个 skills）

类型：**纯 Agent Skills 包**（无 npm 运行时依赖）。

## 必做顺序

1. 先 Read 核心技能并执行其流程（读 brief → 一句话 design read → Never List → 预检清单）：  
   `/home/box/agent-data/design-kits/design-taste/skills/design-taste/SKILL.md`
2. 用户点名风格或 design read 明确时，再 Read **一个** genre pack（每项目只选一个身份）：
   - `editorial-minimal` / `brutalist-industrial` / `quiet-luxury` / `dark-tech` / `playful-color`
   - `retro-print` / `japanese-minimal` / `neo-brutalism` / `corporate-trust` / `cinematic-motion`  
   路径：`.../skills/<name>/SKILL.md`
3. 需要细则时叠 craft/code 技能（可多选）：  
   `taste-typography` · `taste-color` · `taste-motion` · `taste-gsap` · `taste-accessibility` · `taste-design-system` · `taste-landing-page` · `taste-ux-copy` · `taste-brand-identity` · `taste-design-review` · `taste-code-craft` · `taste-web-performance` · `taste-code-review`
4. 对照示例（可选）：`.../examples/before.html` vs `after.html`，以及各 genre 的 html demo。

## 组合规则

- genre = 身份；craft = 细节纪律；code = 交付质量；core 始终生效。
- 不要一次加载全部 24 个正文；按任务 Read 所需文件即可。

## 边界

- 这是审美/流程指令，不替代组件安装；落地组件去 [uilayouts](sand-workflow:uilayouts) / [trickle-ui-kit](sand-workflow:trickle-ui-kit) 等。
- 政府/强合规场景优先 `corporate-trust` + `taste-accessibility`，不要强行 cinematic。
