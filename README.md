# 🤖 Agile AI Team — 基于 OpenClaw 的多 Agent 敏捷开发系统

> 用 AI Agent 模拟完整敏捷开发团队，实现从需求到发布的全流程自动化协作。

## 📌 项目简介

本项目设计并实现了一套完整的 **多 Agent 协作系统**，模拟敏捷开发团队中的核心角色。每个 Agent 拥有独立的性格、职责边界、记忆系统和工作流程，通过 Agent 间通信实现端到端的产品交付。

**技术亮点：**
- 🔗 **Agent 间通信机制** — Agent 通过消息传递实现跨角色协作
- 📋 **完整的敏捷流程** — 覆盖需求拆解、Sprint 规划、开发、测试、发布全链路
- 🧠 **独立记忆系统** — 每个 Agent 拥有独立的长期记忆和每日日志
- 🎭 **人格化设计** — 每个 Agent 有独立的性格定义和协作边界
- 🛠 **16 个专业 Skills** — 为每个角色定制的技能模块

## 🏗 架构设计

### 角色合并策略

为了简化团队结构、减少沟通层级，本项目对传统 Scrum 角色进行了合并：

- **PO Agent** = 产品负责人 + Scrum Master — 需求管理的同时负责流程调度
- **Quality Agent** = QE + Release — 质量保障与发布流程合并为一体化交付关卡

### 团队流程图

```
产品总监（用户）
    │
    ▼
┌──────────────────┐
│  PO Agent 📋🏃   │  需求拆解 / Backlog 管理 / Sprint 计划 / 站会 / 障碍清除
└──────┬───────────┘
       │
       ├──────────────┐
       ▼              ▼
┌─────────────┐  ┌──────────────────┐
│ Dev Agent 💻 │  │ Quality Agent 🔬🚀 │
│              │  │                    │
│ 代码生成     │  │ 测试用例 / 自动化  │
│ Code Review  │  │ Bug 报告 / 回归    │
│ Git 操作     │  │ CI/CD / Changelog  │
│ 技术文档     │  │ 发布部署           │
└──────┬──────┘  └────────┬──────────┘
       │                  │
       └────────┬─────────┘
                ▼
          交付给用户 ✅
```

### Agent 通信矩阵

| 发送方 | 接收方 | 通信内容 |
|--------|--------|----------|
| PO Agent | Dev Agent | 开发任务分配 |
| PO Agent | Quality Agent | 测试任务分配 |
| Dev Agent | Quality Agent | 代码提交通知 |
| Quality Agent | Dev Agent | Bug 反馈与改进建议 |
| Quality Agent | PO Agent | 测试报告 / 进度汇报 |

## 👥 Agent 角色介绍

### 📋🏃 PO Agent — 产品负责人 + 流程调度

负责将产品愿景转化为可执行的需求，维护产品 Backlog，划定 Sprint 范围。同时承担 Scrum Master 职责，组织 Sprint 启动、每日站会，清除团队障碍。

### 💻 Dev Agent — 全栈开发者

将需求转化为高质量代码，负责代码生成、Code Review、Git 操作和技术文档编写。

### 🔬🚀 Quality Agent — 质量守护师 + 发布工程师

综合保障产品的质量、安全和发布流程。负责测试用例设计、自动化测试、Bug 记录、回归测试，以及 CI/CD 流水线管理、发布日志生成和部署交付。

## 🛠 Skills 体系（16 个）

Skills 按所属角色分组管理，Scrum Master 技能归入 PO，Release 技能归入 Quality。

| Agent | Skills | 说明 |
|-------|--------|------|
| PO | `po-requirement-breakdown` | 需求拆解为 User Story |
| | `po-backlog-management` | Backlog 管理与优先级排序 |
| | `po-sprint-planning` | Sprint 范围划定与计划 |
| | `scrum-sprint-kickoff` | Sprint 启动与任务分配 |
| | `scrum-standup` | 每日站会与进度跟踪 |
| | `scrum-blocker-resolution` | 障碍识别与解决 |
| Dev | `dev-code-generation` | 高质量代码生成 |
| | `dev-code-review` | 代码审查与改进建议 |
| | `dev-git-operations` | Git commit / PR / 分支管理 |
| | `dev-tech-docs` | 技术文档生成与维护 |
| Quality | `qe-test-case-gen` | 测试用例设计 |
| | `qe-automation-test` | 自动化测试脚本编写与执行 |
| | `qe-bug-report` | Bug 记录与跟踪 |
| | `qe-regression-test` | 回归测试与修复确认 |
| | `release-cicd` | CI/CD 流水线管理 |
| | `release-changelog` | 发布日志自动生成 |

## 📁 项目结构

```
agile-ai-team/
├── README.md
├── .gitignore
├── agents/
│   ├── po/                    # PO Agent — 产品负责人 + Scrum Master
│   │   └── workspace/
│   │       ├── AGENTS.md      # 工作指令与流程
│   │       ├── SOUL.md        # 性格与边界
│   │       ├── IDENTITY.md    # 身份定义
│   │       ├── TOOLS.md       # 工具与通信说明
│   │       ├── MEMORY.md      # 长期记忆
│   │       └── HEARTBEAT.md   # 心跳配置
│   ├── dev/                   # Dev Agent — 全栈开发者
│   │   └── workspace/
│   └── quality/               # Quality Agent — 质量守护 + 发布工程
│       └── workspace/
└── skills/
    ├── po/                    # PO 相关技能（含 Scrum Master）
    │   ├── po-requirement-breakdown/
    │   ├── po-backlog-management/
    │   ├── po-sprint-planning/
    │   ├── scrum-sprint-kickoff/
    │   ├── scrum-standup/
    │   └── scrum-blocker-resolution/
    ├── dev/                   # Dev 相关技能
    │   ├── dev-code-generation/
    │   ├── dev-code-review/
    │   ├── dev-git-operations/
    │   └── dev-tech-docs/
    └── quality/               # Quality 相关技能（含 Release）
        ├── qe-test-case-gen/
        ├── qe-automation-test/
        ├── qe-bug-report/
        ├── qe-regression-test/
        ├── release-cicd/
        └── release-changelog/
```

## 🔧 技术栈

- **Agent 框架：** [OpenClaw](https://github.com/openclaw/openclaw) — 多 Agent 运行时框架
- **LLM：** GLM 系列（智谱 AI）
- **通信协议：** Agent-to-Agent 消息传递
- **记忆系统：** 文件持久化（MEMORY.md + 每日日志）
- **技能系统：** OpenClaw AgentSkills 规范

## 💡 设计理念

1. **角色精简** — PO 融合 Scrum Master，Quality 融合 Release，减少沟通层级
2. **角色隔离** — 每个 Agent 有明确的职责边界，不越权、不重叠
3. **记忆独立** — 每个 Agent 维护独立的记忆系统，模拟真实团队成员的认知
4. **人格化** — 每个 Agent 有独特的性格定义，影响其沟通风格和决策方式
5. **流程驱动** — 基于敏捷 Scrum 框架设计完整的工作流
6. **可扩展** — 可根据需要添加新的 Agent 角色或 Skills

## 📄 License

MIT
