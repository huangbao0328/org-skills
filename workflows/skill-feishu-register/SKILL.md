---
name: skill-feishu-register
description: >-
  当新建或实质性改写组织可复用 Skill（Memory M2）时使用：用 lark-cli 取下一 A
  编号（或更新已有行）写入飞书「内部应用与Skill清单」。
---
# skill-feishu-register

把组织可复用 Skill（Memory **M2**）同步进飞书「内部应用与Skill清单」（**M1**）。手册规则 19 / 4 编号闸门。

## 何时用

- 刚 `UpdateSkill` 写入或大改了 `/home/box/agent-data/workflows/<slug>/` 下的**组织共用** Skill
- Bob 要求「可复用做法进清单」

**不必用：** Cursor 插件只读 Skill；一次性私聊草稿；仅改错别字且清单行已存在且口令未变。

## 常量

- base：`XMXmbeLB0aDBfJs8Nw6caYnYnTg`
- table：`tblPtlpjeJGRoLpB`
- 飞书一律 `lark-cli`（不用飞书 MCP）

## 步骤

1. **导出编号列**（禁止凭记忆顺延）：
   ```bash
   lark-cli base +record-list \
     --base-token XMXmbeLB0aDBfJs8Nw6caYnYnTg \
     --table-id tblPtlpjeJGRoLpB \
     --field-id 编号 --field-id 名称 --field-id 使用入口/口令 \
     --format ndjson --output /tmp/feishu-skill-sync.ndjson --overwrite
   ```
2. **Python 判定**：读 ndjson；取最大 `A###`；若「名称」或口令里已含本 Skill 的 `slug` / 路径，记下 `record_id` 走更新，否则 `next = max+1` → `A{next:03d}`（或按现网位数）。
3. **组装字段**（至少）：
   - `编号`：新建时用 next；更新时不动编号
   - `名称`：`{slug}｜一句话用途`
   - `使用入口/口令`：触发词 + `Skill：{slug}` + 路径 `/home/box/agent-data/workflows/{slug}/`
   - 若表有且可知：`类型`=`["Skill"]`；`维护人`；`上次更新`（Asia/Shanghai）；`是否过期/备注`=`有效`
4. **写入**：
   - 新建：`lark-cli base +record-upsert --base-token … --table-id … --json '{...}'`（**无** `--record-id`）
   - 更新：同上加 `--record-id <id>`
5. **回报**：编号、名称、新建/更新、record_id。撞号则改号重试，不得并存两行同号。

## 反模式

- 凭记忆分配 A 号
- 用飞书 MCP
- 只写 Skill 不跑本配方（违反手册规则 19）
- 把插件 Skill / 私聊草稿强行入库刷号
