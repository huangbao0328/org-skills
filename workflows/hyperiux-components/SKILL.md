---
name: hyperiux-components
description: >-
  当用户要高级沉浸动效（粒子、图迹、银河、全屏导航、文字揭示等）并用 Hyperiux CLI/MCP 装进 Next.js 项目时使用。
---

# Hyperiux Components（Vault）

上游：[Hyperiux-Immersion-Labs/hyperiux-components](https://github.com/Hyperiux-Immersion-Labs/hyperiux-components) · https://vault.hyperiux.com  
本地 kit：`/home/box/agent-data/design-kits/hyperiux-components`

类型：**CLI（`hyperiux`）+ MCP（`hyperiux-mcp-server`）效果库**；源码安装进项目。Free 约 50+，Pro 约 90+（需订阅）。

## 安装流程（目标项目）

```bash
npx hyperiux init
npx hyperiux login          # 免费账号也要登录
npx hyperiux list
npx hyperiux add <effect>   # 例：rectangular-text-reveal / phantom-image-trail
```

```jsx
import RectangularTextReveal from "@/components/effects/rectangular-text-reveal";
export default function Page() {
  return <RectangularTextReveal>Hello, world.</RectangularTextReveal>;
}
```

常用：`add` / `outdated` / `versions` / `diff`；`-y` 跳过确认，`--dry-run` 预览。

## MCP（可选）

```json
{
  "mcpServers": {
    "hyperiux": {
      "command": "npx",
      "args": ["-y", "hyperiux-mcp-server"]
    }
  }
}
```

本地包路径：`packages/cli`、`packages/mcp-server`。说明见 kit 内 `MCP-OVERVIEW.md`。

## 无登录时

不要伪造效果源码。可：展示 `media/effects/` 演示 gif、读 README/AGENTS.md 列效果名，并请用户完成 `npx hyperiux login`。Free 有日配额。

## 边界

- Pro 效果未订阅不要绕过付费墙。
- 许可证：根 `LICENSE` + `LICENSE_EFFECTS`；安装进项目后用户拥有所装源码，再分发按上游条款。
