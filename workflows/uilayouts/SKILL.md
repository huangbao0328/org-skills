---
name: uilayouts
description: >-
  当用户要现代创意布局与交互组件（轮播、文件上传、sparkles、时间线、图片 ripple/mousetrail、按钮等）且基于 React + Tailwind + motion 时使用。
---

# UI Layouts

上游：[ui-layouts/uilayouts](https://github.com/ui-layouts/uilayouts) · 站点 https://www.ui-layouts.com  
本地 kit：`/home/box/agent-data/design-kits/uilayouts`

类型：**开源创意组件 monorepo**（文档站 + packages）。安装方式以站点「复制/CLI」与源码为准，不是单一 npm UI 包名冒充。

## 目标项目依赖（上游 README）

```bash
npm install motion clsx tailwind-merge
```

并提供 `cn` 工具与可选 `useMediaQuery`（全文见 kit README）。

## 怎么取组件

1. 在 https://www.ui-layouts.com/components 选定组件。
2. 对照本地源码（优先）：
   - `packages/ui/`、`packages/blocks/`、`packages/shadcn/`
   - 文档应用：`apps/ui-layout/`
3. 把所需 tsx 与依赖拷进用户项目，按项目别名改 import；不要整仓 `npm install` 本 monorepo 当依赖。

## 高频方向（站点命名）

R3F Blob、Image Ripple、File Upload、Password、Range Slider、Motion Number、Embla Carousel、Sparkles、Drag Items、Timeline Animation、Clip Path、Buttons、Image Mousetrail、Image Reveal 等。

## 边界

- 与 [motion-primitives](sand-workflow:motion-primitives) 重叠时：uilayouts 偏整段创意区块；motion-primitives 偏可组合原语。
- Labs：https://www.ui-layouts.com/labs
