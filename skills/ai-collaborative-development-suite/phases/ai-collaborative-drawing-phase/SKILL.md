---
name: ai-collaborative-drawing-phase
description: 基于设计输出 PlantUML 图示。
---

# 画图阶段

[目标]
将设计转化为可视化的 PlantUML 模型。

[准入条件]
- 设计阶段已完成。
- 存在 `推荐图示清单`。

[退出条件]
- 已生成/更新合法的 `.puml` 源码。
- 更新 `TASK_STATE.md`。

[执行步骤]
1. 读取 `推荐图示清单`。
2. [必须] 必须通过工具 (如 `grep_search` 或 `view_file` 查找 `skills/plantuml-from-design-or-code/templates/*.puml`) 动态搜索与读取所需的模板文件。严禁依赖 AI 静态内置记忆。
3. 生成 `.puml` 文件。
4. 自动验证语法与渲染情况。
5. 自动模式 -> 直接放行。手动模式 -> 等待人工确认。

[禁止事项]
- 凭空臆造设计或代码中不存在的组件。
- 将冗长的画图模板硬编码在 AI 的系统提示词中。
