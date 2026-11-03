---
name: canvas-ui
description: >-
  当用户要液体、玻璃、破碎、力场、解密显现等 canvas/WebGL/WebGPU 创意特效罩在真实可点 DOM 上（React/Vue/Svelte 等）时使用。
---

# Canvas UI

上游：[DavidHDev/canvas-ui](https://github.com/DavidHDev/canvas-ui) · 文档 https://canvasui.dev  
本地 kit：`/home/box/agent-data/design-kits/canvas-ui`

类型：**shadcn 兼容 registry 组件库**（约 35+ 特效；copy 进仓库，不装成黑盒包）。许可证：**MIT + Commons Clause**（再分发/卖组件前读 `LICENSE.md`）。

## 安装（目标项目内）

先确保项目已 `npx shadcn@latest init`，然后：

```bash
npx shadcn@latest add @canvas-ui/liquid-react
```

把 `liquid` 换成组件名；`react` 可换 `solid` / `preact` / `vue` / `svelte` / `vanilla`。  
WebGPU 变体加后缀：`@canvas-ui/liquid-react-webgpu`。

源码落入 `components/canvasui/`。

## 用法模式

```tsx
import { Liquid } from "@/components/canvasui/Liquid";

export default function Page() {
  return (
    <Liquid>
      <YourEntirePage />
    </Liquid>
  );
}
```

多数组件是 **包裹子树**：子树保持可选中/可点击，特效画在上层。

## 本地参考

- README：`/home/box/agent-data/design-kits/canvas-ui/README.md`
- 站点组件目录：https://canvasui.dev/components
- 需要 AI 检索安装时可按其文档做 MCP：`npx shadcn@latest mcp init --client ...`

## 边界

- 性能与无障碍：提供减弱动效/无 GPU 回退；不要默认每页套重特效。
- 与 [paper-shaders](sand-workflow:paper-shaders) 区别：Canvas UI 偏整页交互失真；Paper 偏轻量背景着色器。
