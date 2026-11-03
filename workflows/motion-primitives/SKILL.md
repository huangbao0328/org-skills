---
name: motion-primitives
description: >-
  当用户要 React 界面动效基础组件（文字 morph/shimmer/scramble、in-view、dock、spotlight、magnetic、accordion 等）时使用。
---

# Motion Primitives

上游：[ibelick/motion-primitives](https://github.com/ibelick/motion-primitives) · CLI `motion-primitives`  
本地 kit：`/home/box/agent-data/design-kits/motion-primitives`

类型：**动效原语 + CLI 复制进项目**（文档站即本仓库）。

## 安装（目标项目）

```bash
npx motion-primitives list
npx motion-primitives add <component-name>
# 例：
npx motion-primitives add text-morph
```

也可 `npm install -g motion-primitives` 后用同名命令。CLI 会写入组件并安装所需依赖。

## 本地组件清单（core）

目录：`/home/box/agent-data/design-kits/motion-primitives/components/core/`

含：`text-morph` `text-shimmer` `text-scramble` `text-effect` `text-loop` `text-roll` `spinning-text` `animated-number` `sliding-number` `in-view` `infinite-slider` `carousel` `dock` `magnetic` `spotlight` `glow-effect` `progressive-blur` `scroll-progress` `tilt` `accordion` `dialog` `morphing-dialog` `morphing-popover` `disclosure` `border-trail` `animated-background` `animated-group` `cursor` `image-comparison` `toolbar-*` `transition-panel` 等。

**先 `list` 或 ls 该目录再 add**，不要编造组件名。

## 用法注意

- 与 [trickle-ui-kit](sand-workflow:trickle-ui-kit) ：只要「营销页文字出现」且要零 JS 动画运行时 → 优先 Trickle；要编排/手势/复杂交互 → Motion Primitives。
- CLI README：`.../cli/README.md`

## 边界

- 遵守 `prefers-reduced-motion`；避免每段文字都上 scramble。
