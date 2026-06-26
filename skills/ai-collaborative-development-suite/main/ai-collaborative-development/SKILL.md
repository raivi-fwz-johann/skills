---
name: ai-collaborative-development
description: 用于按 AI 协作开发流程推进软件开发任务时使用，适用于需要在设计、画图、实现、检视、验证之间顺序推进的工作；也适用于用户要求“按 SOP 做”“按完整流程推进”“按 AI 协作开发做”或未明确当前阶段但需要系统化推进的软件开发任务。
---

# AI 协作开发

本 skill 只定义流程和阶段流转规则，不包含具体实施逻辑。各阶段的实际执行应优先复用仓库内已有的相关 skills。

## Workflow

默认流程为：

1. 设计
2. 画图
3. 实现
4. 检视
5. 验证

先根据任务状态判断当前所处阶段，再进入对应阶段 skill：

- 设计阶段：`ai-collaborative-design-phase`
- 画图阶段：`ai-collaborative-drawing-phase`
- 实现阶段：`ai-collaborative-implementation-phase`
- 检视阶段：`ai-collaborative-review-phase`
- 验证阶段：`ai-collaborative-verification-phase`

如果用户没有明确当前阶段，先读取 `references/phase-selection.md`（位于本 skill 目录下）进行阶段判定，再进入对应子 skill。

## Core Rules

- 先设计，后实现；不得跳过设计直接编码。
- 各阶段实施时优先复用仓库内已有的相关 skills，本套件仅提供流程控制逻辑。
- 所有产出文档默认使用中文；代码标识符、类名、方法名保持原名。
- 小步推进、状态管理、人机确认和禁止事项的完整规则，读取 `references/workflow.md`（位于本 skill 目录下）。

## Stage Selection

读取 `references/phase-selection.md`（位于本 skill 目录下），按以下原则判断：

- **敏捷通道判定**：若评估当前任务属于单文件内的微小局部修改且无系统架构影响，优先提议用户进入“敏捷通道”，跳过设计与画图阶段直接开始实现。
- 用户要求方案、范围或验收标准：进入设计阶段
- 用户要求图示、流程图、活动图、架构图或序列图：进入画图阶段
- 用户要求实现代码：进入实现阶段
- 用户要求进行代码审查、AI 初检或人工复检：进入检视阶段
- 用户要求验证、验收或查看测试凭证：进入验证阶段

如果任务当前处于实现过程的中间状态，优先检查当前功能小步是否已经完成对应的检视与验证；若未完成，禁止推进到下一小步。

## Human Checkpoints

- 默认模式：AI 先整理信息 → 人工确认 → 确认后才流转。
- 自动模式：当用户要求“自动进行”、“自主推进”或“无需询问”时，画图、实现、检视、验证阶段由 AI 自检替代人工确认，遇阻时升级至人工确认。设计阶段始终使用人工确认。
- 整体任务结束：人工确认后才触发归档。

确认模型的完整规则见 `references/workflow.md`（位于本 skill 目录下），人机确认点参考 `references/human-ai-checkpoints.md`（位于本 skill 目录下），各阶段具体检查点见对应 skill 的 `Human Confirmation` 和 `AI Self-Review` 段落。

## Shared References

> 以下路径相对于本 skill 目录（`ai-collaborative-development/`），不是用户项目目录。

- `references/workflow.md`：完整流程、回退规则、小步推进规则
- `references/phase-selection.md`：阶段判定规则
- `references/human-ai-checkpoints.md`：各阶段人机确认点模板
