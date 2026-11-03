---
name: ui-design-stack
description: >-
  当用户要做/改网页或产品 UI、落地页、设计系统、动效、着色器背景、鼠标特效、文字动画，或说「顶尖 UI / 别做成 AI 味 / 用设计栈 / 设计网页
  / 产品界面」时使用（全员自动启用，无需再点名）。先路由到对应子技能，再动手。
---
# UI Design Stack（伞技能）

全组织共用设计能力路由。清单 **A020**；组织规则 **A031**。本地 kit 根目录：

`/home/box/agent-data/design-kits/`

## 全员自动启用（2026-10-22）

凡用户提到「设计网页 / 产品界面 / 落地页 / UI 改版 / 别做成 AI 味」及同类意图：**先 Skill 加载本技能**，再按意图路由子技能；无需用户再说「用设计栈」。禁止跳过伞技能凭记忆乱抄组件。

执行前用 Skill 加载本技能；选定子技能后再 Skill 加载对应文件夹的 `SKILL.md`。

## 先定意图，再选工具

| 用户意图 | 加载技能 | kit 路径 |
|---------|---------|----------|
| 在画布上出方案 / 改界面 / 幻灯片 / 海报，要设计判断 | [superdesign-skill](sand-workflow:superdesign-skill) | `design-kits/superdesign-skill` |
| 按 Linear/Stripe 等成品设计系统搭 UI + 自查 a11y | [better-design](sand-workflow:better-design) | `design-kits/better-design` |
| 反 AI 味审美、选风格包、落地页/作品集调性 | [design-taste](sand-workflow:design-taste) | `design-kits/design-taste` |
| 液体/玻璃/力场等 canvas 创意特效罩在真实 DOM 上 | [canvas-ui](sand-workflow:canvas-ui) | `design-kits/canvas-ui` |
| MeshGradient 等轻量着色器背景/纹理 | [paper-shaders](sand-workflow:paper-shaders) | `design-kits/paper-shaders` |
| 现代创意布局与交互组件（轮播、上传、sparkles 等） | [uilayouts](sand-workflow:uilayouts) | `design-kits/uilayouts` |
| 高级沉浸动效（粒子、图迹、全屏导航等） | [hyperiux-components](sand-workflow:hyperiux-components) | `design-kits/hyperiux-components` |
| 文字/面板/视差等 motion 基础原语 | [motion-primitives](sand-workflow:motion-primitives) | `design-kits/motion-primitives` |
| 自定义鼠标指针动画 | [cursify](sand-workflow:cursify) | `design-kits/cursify` |
| 纯 CSS 文字动画（零 motion 运行时） | [trickle-ui-kit](sand-workflow:trickle-ui-kit) | `design-kits/trickle-ui-kit` |

## 推荐组合（默认工作流）

1. **定调**：`design-taste`（声明 design read + 禁 LLM 默认）→ 需要成品系统时加 `better-design`。
2. **出稿**：复杂产品页/多方案用 `superdesign-skill`；简单页面可直接写代码。
3. **组件**：布局/交互用 `uilayouts` 或 `motion-primitives`；文字动效用 `trickle-ui-kit`（优先）或 motion 文字组件。
4. **氛围**：背景着色器用 `paper-shaders`；整页 canvas 特效用 `canvas-ui`；更炫沉浸用 `hyperiux-components`；指针用 `cursify`（克制，勿每页都上）。

## 强制纪律

1. **先读再抄**：安装/复制组件前，Read 对应子技能与 kit 内 README；不要凭记忆编造 API。
2. **尊重现有品牌**：已有 design tokens / 组件库时，不要擅自换成 catalog 里另一个系统，除非用户明确要求换皮。
3. **账号墙**：Superdesign CLI 需登录；Hyperiux 需 `~/.hyperiux/auth.json` 或 `HYPERIUX_TOKEN`；Better Design 推荐连 MCP。无账号时：用本地 kit 源码/文档继续，并告知用户缺什么登录。
4. **更新 kit**：`cd /home/box/agent-data/design-kits/<name> && git pull --ff-only`（shallow clone 可再 `git fetch --depth 1 && git reset --hard origin/HEAD`）。
5. **归因**：上游仓库与许可证见各子技能；商业再分发前核对 Commons Clause / Pro 等限制（尤其 Canvas UI、Hyperiux Pro）。

## 与 anatomy / slides 的边界

- 等距技术图解 → 用现有 [anatomy](sand-workflow:anatomy)，不要硬套本栈。
- PPT/幻灯片优先 slides/office-pptx 技能；仅当用户明确要 Superdesign 出演示稿时才走 `superdesign-skill`。
