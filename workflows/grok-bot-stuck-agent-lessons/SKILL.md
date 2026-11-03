---
name: grok-bot-stuck-agent-lessons
description: >-
  当某个 Grok Bot 出现「Bot 未能回复」、新回合起不来、peer 叫醒无新 transcript、或要向 support@x.ai
  报障/跟进工单时使用：区分卡点类型、平台恢复阶梯、邮件通道与勿 Reset Computer。
---
# Grok Bot 单 Agent 卡死报障与恢复（可复用经验）

来源：2026-10-21 小战（Agent ID 示例形态 `20b13d26-…`）实战，工单 **T-I1219**。清单编号 **A018**。

---

## 0. 先定性：不是「内容卡住」，是「新回合起不来」

| 信号 | 含义 |
|------|------|
| UI 显示「Bot 未能回复」/ Bot failed to reply | 客户端已判定本回合失败 |
| `ReadTranscript` 最后一条成功回复之后，用户新消息或 peer wake **没有新 assistant 回合** | 调度/ harness 未起回合 |
| 同账号其他 Bot 仍正常 | 多半是**单 Agent 会话**问题，不是全账号额度或电脑桌面坏了 |
| 卡在某次工具调用中途、反复同一 tool | 才是 mid-tool stall；处理不同 |

定性后再选恢复路径；不要一上来 Reset Bot's Computer。

---

## 1. 客户端自助阶梯（轻 → 重）

1. **短重试**：在该 Bot 聊天发极短一句「在吗」。
2. **查用量**：设置 → 用量；周额度/积分触顶时整条链路可能起不了新回合。
3. **更新 App + 完全退出重开**：修客户端，不修服务端 Temporal/会话本身。
4. **一般不要** Update / Reset Bot's Computer：官方支持明确——对**单个**静默 Bot 无效，还可能弄丢仍正常 Bot 的近期工作。
5. **最后手段**：侧栏右键 Delete 该 Bot 再重建（对话历史一起没）；没有「只清会话、保留人设」的官方按钮。

没有「一键恢复某个 Bot」的开关；真正修会话调度要走**平台侧 / support**。

---

## 2. 跨 Bot 诊断（管理层 Bot 可做）

- 用 `ReadTranscript` 看目标 Agent 是否停在某一成功 `SendToUser` 之后。
- `SendToAgent` priority 叫醒：投递成功但 transcript 仍无新回合 → 强化「runtime 不起回合」判断。
- 业务交付可先由仍正常的 Bot **代写**（如 Notion 附录），不阻塞用户主线。

---

## 3. 向 support@x.ai 报障（通道很关键）

### 3.1 不要指望 Grok Bot 邮箱直达

- 从 `*@mail.grokbot.com` 发往 `support@x.ai` 可能被 **Amazon SES suppression（5.1.1）** 打回，看起来「已发送」实则未达。
- **优先用用户已连接的 Gmail/Outlook** 发到 `support@x.ai`；用 `DraftExternalMessage` 卡片让用户确认后再发。

### 3.2 Gmail 连接器权限

- 读信可用、发卡后点发送报缺权限 → **重连 Gmail 并勾选全部权限**（`AuthenticateMcpServer` + `force_reauth`，须用户同意）。
- 重连后再挂同一封草稿发送。

### 3.3 首封可极简，第二封补齐 Sam 清单

支持常先回工单号（如 T-I1219）并追问：

1. 静默 Bot ID（iPhone：个人资料 → … → Copy ID）；最好再给一个仍正常的对照 Bot ID  
2. 大致最后成功回复时间；是否有 scheduled routines  
3. 已尝试步骤（重开 App、短重试、peer wake 等）；**不要** Reset Computer  
4. 是否仅 iPhone，还是桌面也「未能回复」/ transcript 停更  

补齐后对方常回「已转内部支持，先用其他 Bot」——进入等待态，待办记「等后台修复」。

---

## 4. 跟进与关闭

- 待办写入共享 `todos.md`，靠「每日待办清单提醒」暴露即可，不必另建专用 cron（除非用户明确要更高频）。
- **确认该 Bot 又能正常起新回合后**再划掉待办。
- 支持明确前：继续禁止对单 Bot Reset Computer。

---



## 6. 健康巡检补记（2026-10-26）

- **2026-10-25 大G老师**：偶发「未能回复」，peer 叫醒即回——偏客户端偶发，非 10-21 小战式硬卡。
- 反馈通道：继续禁止 `*@mail.grokbot.com`→`support@x.ai`（SES suppression）；走 Gmail/应用内。
- 清单 A018 备注已同步。

## 5. 非目标

- 不把「删重建」当默认第一刀。
- 不把 Grok Bot 原生邮箱当 support 唯一通道。
- 不把用量触顶、单 Bot harness 卡死、mid-tool stall 混为一谈。
