# Skills

本目录包含 AI 协作开发所使用的 skills 集合。

## 目录结构

```
skills/ (仓库根目录)
├── README.md
└── skills/                               # 技能库文件夹
    ├── ai-collaborative-development-suite/   # 流程控制 suite
    │   ├── main/
    │   │   └── ai-collaborative-development/ # 总控技能（流程路由）
    │   │       ├── SKILL.md
    │   │       ├── agents/
    │   │       │   └── openai.yaml
    │   │       └── references/
    │   │           ├── workflow.md            # 流程、确认模型、状态管理（权威来源）
    │   │           ├── phase-selection.md     # 阶段判定规则
    │   │           └── human-ai-checkpoints.md # 各阶段人机确认与自检点模板
    │   └── phases/
    │       ├── ai-collaborative-design-phase/        # 设计阶段
    │       ├── ai-collaborative-drawing-phase/       # 画图阶段
    │       ├── ai-collaborative-implementation-phase/ # 实现阶段
    │       ├── ai-collaborative-review-phase/        # 检视阶段
    │       └── ai-collaborative-verification-phase/  # 验证阶段
    │
    └── plantuml-from-design-or-code/          # PlantUML 绘图 skill
        ├── SKILL.md
        ├── templates/                         # RISC-V 定制化绘图模板库
        ├── agents/
        │   └── openai.yaml
        └── references/
            └── ai-workflow.md
```

## Skills 概览

### ai-collaborative-development-suite

**定位**：流程控制框架，仅定义阶段流转规则，不包含具体实施逻辑。

**标准流程**：设计 → 画图 → 实现 → 检视 → 验证

**核心特性**：
- 小步推进：`实现 → 检视 → 验证` 以功能小步为单位成组推进，每小步验证通过后执行 git commit
- 双模式确认：默认执行人工确认，当用户要求“自动进行”时切换为 AI 自主检查确认
- 状态管理：通过 `ai-task/TASK_STATE.md` 跨会话保持上下文
- 敏捷通道：微小修改可跳过设计和画图阶段
- 各阶段实施时优先复用仓库内已有的相关 skills

### plantuml-from-design-or-code

**定位**：专用绘图技能，根据设计文档、源码或两者结合生成 PlantUML 图示。

**核心特性**：
- 支持 C4 架构图、类图、流程图、活动图、序列图、状态图、波形图(时序图)、部署图与产物依赖图
- 内置针对 RISC-V C++ 模拟器深层架构定制的高质量模板库
- 事实来源策略：design-doc / source-code / hybrid
- 描述性文字默认中文，代码标识符保持原名

## 通用约定

- **语言**：所有产出文档默认使用中文；代码标识符、类名、方法名保持原名
- **画图格式**：默认使用 PlantUML
- **过程文档**：设计文档和图示存入项目的 `ai-task/` 目录，不提交到代码仓库
- **Agent 配置**：各 skill 的 `agents/openai.yaml` 定义平台展示信息，使用 `interface:` 嵌套格式
