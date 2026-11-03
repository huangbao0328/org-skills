---
name: cursify
description: >-
  当用户要自定义鼠标指针动画（霓虹、气泡、磁吸、轨迹、雪花、故障风等）且基于 React + Tailwind + motion 时使用。
---

# Cursify

上游：[ui-layouts/cursify](https://github.com/ui-layouts/cursify)  
本地 kit：`/home/box/agent-data/design-kits/cursify`

类型：**鼠标指针效果文档站 + registry 源码**（与 UI Layouts 生态相近）。

## 目标项目依赖

```bash
npm install motion clsx tailwind-merge
```

并加入 `cn`（及可选 `useMediaQuery`），同 kit README。

## 怎么取组件

1. 浏览文档内容：`content/components/*-cursor.mdx`（如 `neon-cursor` `bubble-cursor` `magnetic-cursor` `trail-cursor` `fairy-dust` 等命名）。
2. 复制实现：`registry/components/cursor/<name>/`（例：`neoncursor/index.tsx`）。
3. 按项目路径改 import；触控设备提供关闭/降级。

## 纪律

- **默认不要全站替换系统光标**；用于营销英雄区或创意作品集局部。
- 必须保留可点击性与键盘可达；提供「关闭特效」开关。
- 与 [canvas-ui](sand-workflow:canvas-ui) 的指针类特效二选一，避免叠两层指针逻辑。

## 本地参考

- README：`.../cursify/README.md`
- registry：`.../cursify/registry/components/cursor/`
