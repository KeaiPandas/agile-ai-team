---
name: po-backlog-management
description: 维护和管理产品 Backlog，确保任务按优先级排序、状态实时更新
---

# Backlog 管理

## 概述

管理产品 Backlog 的全生命周期——维护 `backlog/product-backlog.md` 文件，确保 Task 按优先级正确排序、状态实时反映最新进展、过时内容及时清理。Backlog 是所有 Agent 的单一信息源，必须保持准确和可读。

**在流程中的位置：** 需求拆解 → **Backlog 管理** → 里程碑规划

## 触发条件

- 新 Task 被创建（来自需求拆解）
- Task 状态发生变化（被认领、完成、阻塞）
- 需要调整优先级（新需求插入、需求变更）
- 定期整理（里程碑切换时）
- 发现重复或过时的 Task

## 输入

- `backlog/product-backlog.md`（当前 backlog）
- `sprint-status.md`（当前里程碑状态，用于同步 Task 状态）
- 优先级变更请求
- 需求变更通知

## 流程

1. **读取当前 Backlog**：加载 `backlog/product-backlog.md`，了解现有内容
2. **同步状态**：对照 `sprint-status.md`，将已完成的 Task 标记为 `done`
3. **处理变更请求**：
   - 新增 Task：按优先级插入对应分组
   - 优先级调整：在分组间移动 Task
   - 需求变更：更新 Task 描述和验收标准
4. **清理过时内容**：
   - 标记废弃的 Task（状态改为 `obsolete`）
   - 合并重复的 Task
   - 删除已废弃超过 2 个里程碑的 Task
5. **确保排序正确**：每个优先级分组内按 ID 升序排列
6. **写入文件**：更新 `backlog/product-backlog.md`
7. **输出变更摘要**：报告本次变更内容

## 输出

- 更新后的 `backlog/product-backlog.md`
- 变更摘要（新增/修改/废弃的 Task 数量）

## 文件规范

### Backlog 文件格式

路径：`backlog/product-backlog.md`

```markdown
# Product Backlog

> 最后更新: YYYY-MM-DD HH:MM
> 维护者: PO Agent

## 🔴 P0 - 必须完成

| ID | Task | Size | Status | Assignee |
|----|------|------|--------|----------|
| T-001 | 实现用户登录功能 | M | done | dev |
| T-002 | 搭建项目基础架构 | L | in-progress | dev |

## 🟡 P1 - 重要

| ID | Task | Size | Status | Assignee |
|----|------|------|--------|----------|
| T-003 | 添加暗黑模式支持 | M | todo | - |
| T-004 | 优化首页加载速度 | S | todo | - |

## 🟢 P2 - 锦上添花

| ID | Task | Size | Status | Assignee |
|----|------|------|--------|----------|
| T-005 | 添加加载动画 | S | todo | - |
| T-006 | 支持 PWA 离线模式 | L | todo | - |

## 已废弃

| ID | Task | 原因 | 废弃日期 |
|----|------|------|----------|
| T-000 | 旧版登录方案 | 技术方案变更 | 2026-03-20 |
```

### Status 取值

- `todo` — 待领取
- `in-progress` — 进行中
- `review` — 待审查
- `done` — 已完成
- `blocked` — 被阻塞
- `obsolete` — 已废弃

## 注意事项

- **Backlog 是单一信息源**：所有 Task 的状态以 backlog 为准，不允许存在冲突的状态文件
- **定期整理**：每个里程碑结束后做一次全面梳理
- **保持精简**：P2 的 Task 不超过 P0+P1 总数的 50%
- **不要删除 Task**：用 `obsolete` 标记而非删除，保留历史记录
- **ID 不可复用**：废弃的 Task ID 永远不再分配给新 Task
