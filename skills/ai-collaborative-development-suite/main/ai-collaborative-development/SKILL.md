---
name: ai-collaborative-development
description: 总控路由节点(Router)。用于按意图切分研发流程。严禁级联加载子技能，按需挂载。
---

# AI 协作开发 [仅限路由]

[机制: 动态上下文加载]
- [必须] 严禁将所有阶段 SKILL 一次性全部加载到系统提示词中。
- [必须] 仅加载当前处于活跃阶段的 `SKILL.md`。
- [必须] 发生阶段切换时，立即卸载上一阶段的 `SKILL.md` 以节省 Token。

## 1. 阶段选择 (路由逻辑)
读取 `references/phase-selection.md` 识别意图 -> 映射到对应阶段。

## 2. 共享引用
- `references/workflow.md`: 全局状态与约束。
- `references/human-ai-checkpoints.md`: 全局确认模式。

[禁止事项]
- 在此路由 SKILL 内执行具体的阶段代码任务。
- 绕过设定的阶段流转顺序。
