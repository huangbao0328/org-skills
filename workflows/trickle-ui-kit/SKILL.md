---
name: trickle-ui-kit
description: >-
  当用户要纯 CSS 文字动画（打字机、瀑布、闪烁、故障、霓虹等）、要求零 framer-motion 运行时且 SSR 安全时使用。
---

# Trickle UI Kit

上游：[akaieuan/trickle-UI-kit](https://github.com/akaieuan/trickle-UI-kit) · https://tricklekit.dev  
本地 kit：`/home/box/agent-data/design-kits/trickle-ui-kit`

类型：**shadcn registry 文字动画**（纯 CSS keyframes；约 47–49 个原语）。无独立 npm 运行时包——**用 shadcn add 安装源码**。

## 安装（目标项目）

需要 Tailwind（推荐 v4）+ shadcn：

```bash
npx shadcn@latest init   # 若尚未初始化
npx shadcn@latest add https://tricklekit.dev/r/typewriter.json
```

把 `typewriter` 换成组件名。根清单：`/home/box/agent-data/design-kits/trickle-ui-kit/registry.json`。

## 已知组件名（节选）

`text-root` `typewriter` `text-reveal` `word-cascade` `char-stagger` `gradient-shift` `shiny-shimmer` `underline-draw` `aurora-text` `word-rotate` `decrypt-scramble` `glitch-split` `neon-flicker` `marquee-ribbon` `morph-swap` `ink-bleed` `shatter` `scanline` `pixelate` `confetti-text` `digital-rain` …

完整列表以 `registry.json` 的 `items[].name` 为准。

## 何时选 Trickle vs Motion Primitives

| 需求 | 选 |
|------|----|
| 营销标题出现、要轻、SSR | **Trickle** |
| 布局编排、手势、复杂时间线 | **motion-primitives** |

## 边界

- 不要为 Trickle 再装 `framer-motion`「增强」——那违背该库设计。
- 本地 docs 站可 `pnpm install && pnpm dev`（仅开发参考，非用户应用依赖）。
