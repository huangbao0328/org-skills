# Grok Bot / 本组织使用说明

- Skill 根目录：`/home/box/agent-data/workflows/anatomy/`（全助手共享）
- 上游：https://github.com/wheresryan22/anatomy （MIT）
- 本机已有：Node.js、Google Chrome（验证脚本可用 `CHROME_PATH=/usr/bin/google-chrome`）
- 触发：用户要等距图、技术原理示意图、交互 explainer、Linear 风格技术插图，或说「用 anatomy」「画一台能解释某某机制的机器」
- 执行前先 Read 本目录 `SKILL.md`，需要时再打开 `references/` 与最近的 `examples/`
- 产出放 `/workspace/anatomy-out/<slug>/`，避免污染 skill 目录
- 完整图可能很慢；先对齐要解释的概念与真实数字（预注册四态可选用）
