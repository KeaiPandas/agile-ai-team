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

### 团队流程图

```
产品总监（用户）
    │
    ▼
┌─────────────┐
│  PO Agent 📋 │  需求拆解 / Backlog 管理 / Sprint 计划
└──────┬──────┘
       │
       ▼
┌──────────────────┐
│ Scrum Master 🏃  │  Sprint 启动 / 每日站会 / 障碍清除
└──────┬───────────┘
       │
       ▼
┌─────────────┐
│ Dev Agent 💻 │  代码生成 / Code Review / Git 操作 / 技术文档
└──────┬──────┘
       │
       ▼
┌─────────────┐
│ QE Agent 🔬 │  测试用例 / 自动化测试 / Bug 报告 / 回归测试
└──────┬──────┘
       │
       ▼
┌─────────────────┐
│ Release Agent 🚀 │  CI/CD 流水线 / 发布日志 / 部署管理
└─────────────────┘
```

### Agent 通信矩阵

| 发送方 | 接收方 | 通信内容 |
|--------|--------|----------|
| PO Agent | Scrum Master | Sprint Backlog |
| Scrum Master | Dev Agent | 开发任务 |
| Scrum Master | QE Agent | 测试任务 |
| Dev Agent | QE Agent | 代码提交通知 |
| QE Agent | Dev Agent | Bug 反馈 |
| QE Agent | Release Agent | 发布就绪确认 |

## 👥 Agent 角色介绍

### 📋 PO Agent — 产品负责人
负责将产品愿景转化为可执行的需求，维护产品 Backlog，划定 Sprint 范围。

### 🏃 Scrum Master — 敏捷教练
保障敏捷流程顺利执行，组织 Sprint 启动、每日站会，清除团队障碍。

### 💻 Dev Agent — 全栈开发者
将需求转化为高质量代码，负责代码生成、Code Review、Git 操作和技术文档编写。

### 🔬 QE Agent — 质量工程师
保障产品质量，负责测试用例设计、自动化测试、Bug 记录和回归测试。

### 🚀 Release Agent — 发布工程师
管理产品交付的最后关卡，负责 CI/CD 流水线、环境部署和发布日志生成。

## 🛠 Skills 体系（16 个）

| Agent | Skills | 说明 |
|-------|--------|------|
| PO | `po-requirement-breakdown` | 需求拆解为 User Story |
| | `po-backlog-management` | Backlog 管理与优先级排序 |
| | `po-sprint-planning` | Sprint 范围划定与计划 |
| Scrum Master | `scrum-sprint-kickoff` | Sprint 启动与任务分配 |
| | `scrum-standup` | 每日站会与进度跟踪 |
| | `scrum-blocker-resolution` | 障碍识别与解决 |
| Dev | `dev-code-generation` | 高质量代码生成 |
| | `dev-code-review` | 代码审查与改进建议 |
| | `dev-git-operations` | Git commit / PR / 分支管理 |
| | `dev-tech-docs` | 技术文档生成与维护 |
| QE | `qe-test-case-gen` | 测试用例设计 |
| | `qe-automation-test` | 自动化测试脚本编写与执行 |
| | `qe-bug-report` | Bug 记录与跟踪 |
| | `qe-regression-test` | 回归测试与修复确认 |
| Release | `release-cicd` | CI/CD 流水线管理 |
| | `release-changelog` | 发布日志自动生成 |

## 📁 项目结构

```
agile-ai-team/
├── README.md
├── .gitignore
├── agents/
│   ├── po/                    # PO Agent — 产品负责人
│   │   └── workspace/
│   │       ├── AGENTS.md      # 工作指令与流程
│   │       ├── SOUL.md        # 性格与边界
│   │       ├── IDENTITY.md    # 身份定义
│   │       ├── TOOLS.md       # 工具与通信说明
│   │       ├── MEMORY.md      # 长期记忆
│   │       └── HEARTBEAT.md   # 心跳配置
│   ├── scrum-master/          # Scrum Master — 敏捷教练
│   ├── dev/                   # Dev Agent — 全栈开发者
│   ├── qe/                    # QE Agent — 质量工程师
│   └── release/               # Release Agent — 发布工程师
└── skills/
    ├── po-requirement-breakdown/
    ├── po-backlog-management/
    ├── po-sprint-planning/
    ├── scrum-sprint-kickoff/
    ├── scrum-standup/
    ├── scrum-blocker-resolution/
    ├── dev-code-generation/
    ├── dev-code-review/
    ├── dev-git-operations/
    ├── dev-tech-docs/
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

1. **角色隔离** — 每个 Agent 有明确的职责边界，不越权、不重叠
2. **记忆独立** — 每个 Agent 维护独立的记忆系统，模拟真实团队成员的认知
3. **人格化** — 每个 Agent 有独特的性格定义，影响其沟通风格和决策方式
4. **流程驱动** — 基于敏捷 Scrum 框架设计完整的工作流
5. **可扩展** — 可根据需要添加新的 Agent 角色或 Skills

## 📄 License

MIT
