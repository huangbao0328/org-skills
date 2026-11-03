---
name: paper-shaders
description: >-
  当用户要轻量 canvas 着色器背景/纹理（MeshGradient、DotOrbit 等），可用 npm 直接嵌入 React 或 vanilla 页面时使用。
---

# Paper Shaders

上游：[paper-design/shaders](https://github.com/paper-design/shaders) · 示例 https://shaders.paper.design  
本地 kit：`/home/box/agent-data/design-kits/paper-shaders`

类型：**npm 着色器库**（Apache-2.0）。包：
- React：`@paper-design/shaders-react`
- Vanilla：`@paper-design/shaders`

上游提醒：**钉版本**（0.0.x 可能破坏性变更）。

## 安装

```bash
npm i @paper-design/shaders-react
# 或
npm i @paper-design/shaders
```

## React 示例（来自上游 README）

```jsx
import { MeshGradient, DotOrbit } from '@paper-design/shaders-react';

<MeshGradient
  colors={['#5100ff', '#00ff80', '#ffcc00', '#ea00ff']}
  distortion={1}
  swirl={0.8}
  speed={0.2}
  style={{ width: 200, height: 200 }}
/>

<DotOrbit
  colors={['#d2822d', '#0c3b7e', '#b31a57', '#37a066']}
  colorBack="#000000"
  scale={0.3}
  style={{ width: 200, height: 200 }}
/>
```

## 本地参考

- 根 README：`.../paper-shaders/README.md`
- React 包：`.../packages/shaders-react/`
- 核心包：`.../packages/shaders/`
- 导出清单：Read `packages/shaders-react/src/index.ts` 与 `packages/shaders-react/src/shaders/`，**禁止臆造组件名**。

## 边界

- 适合背景/蒙版纹理，不是完整 UI 套件。
- 与 [canvas-ui](sand-workflow:canvas-ui) 叠加时注意 GPU 负载；尊重 `prefers-reduced-motion`。
