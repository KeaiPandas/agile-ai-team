---
name: scrum-sprint-kickoff
description: 扫描 Backlog，按优先级选取 Task 分配给对应 Agent，创建里程碑状态文件
---

# 里程碑启动

## 概述

Scrum Master Agent 扫描 Backlog，根据里程碑计划选取 Task，分配给对应的 Agent（dev/qe），并创建 `sprint-status.md` 状态文件。这是里程碑正式开始执行的信号——状态文件就绪后，各 Agent 即可通过读取状态文件领取和执行 Task。

**在流程中的位置：** 里程碑规划（PO）→ **里程碑启动** → 代码生成（Dev）/ 测试用例生成（QE）

## 触发条件

- PO Agent 完成里程碑计划（`sprint/milestone-plan.md` 已就绪）
- 新里程碑需要启动
- 当前里程碑需要重新规划分配

## 输入

- `sprint/milestone-plan.md`（里程碑计划，包含目标 Task 列表）
- `backlog/product-backlog.md`（Backlog 完整信息）
- 可用 Agent 列表和各自能力

## 流程

1. **读取里程碑计划**：加载 `sprint/milestone-plan.md`，确认包含的 Task
2. **检查依赖关系**：确认每个 Task 的前置依赖已满足或已包含在范围内
3. **分配 Task 到 Agent**：
   - 开发类 Task → `dev` Agent
   - 测试类 Task → `qe` Agent
   - 文档类 Task → `dev` Agent（如有专人可分配）
   - 注意负载均衡，避免单个 Agent 同时承担过多 L 级 Task
4. **确定执行顺序**：按依赖关系排出推荐执行顺序
5. **创建状态文件**：写入 `sprint/sprint-status.md`
6. **更新 Backlog**：将已分配的 Task 状态改为 `in-progress`，更新 Assignee
7. **发出启动通知**：向相关 Agent 广达里程碑已启动，状态文件已就绪

## 输出

- `sprint/sprint-status.md` — 里程碑状态文件（核心产出）
- 更新后的 `backlog/product-backlog.md`（Task 状态同步）
- 启动通知摘要

## 文件规范

### Sprint Status 文件格式

路径：`sprint/sprint-status.md`

```markdown
# Milestone Status - <里程碑名称>

**开始日期:** YYYY-MM-DD
**目标:** <一句话目标>
**状态:** active / completed / cancelled

## 进度

| Task | Assignee | Status | 更新时间 |
|------|----------|--------|----------|
| T-001 | dev | in-progress | 2026-03-29 |
| T-002 | dev | todo | 2026-03-29 |
| T-003 | qe | todo | 2026-03-29 |

## 推荐执行顺序
1. T-001 → 2. T-002 → 3. T-003（依赖 T-001/T-002）

## 阻塞项
- 无

## 备注
- dev Agent 优先完成 T-001，T-002 可并行启动
```

## 注意事项

- **状态文件是唯一协调机制**：Agent 不需要会议同步，全部通过读写状态文件协调
- **启动前确认计划就绪**：不要在里程碑计划未完成时启动
- **预留缓冲**：建议里程碑内的 Task 总量不超过 Agent 容量的 80%
- **阻塞项初始为空**：启动时不应有已知阻塞，如有需在启动前解决
