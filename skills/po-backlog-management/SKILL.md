---
name: po-backlog-management
description: PO Agent Backlog 管理技能。管理产品待办列表，进行优先级排序和规划。触发条件：(1) 需要整理产品 Backlog，(2) 进行优先级排序，(3) 收到"管理 Backlog"、"优先级排序"、"整理待办"等指令。
---

# Backlog 管理 Skill

管理产品待办列表，维护优先级和状态。

## 工作流程

### 1. Backlog 结构

```markdown
# 产品 Backlog

## P0 - 核心功能（必须有）
| ID | Story | 状态 | Sprint |
|----|-------|------|--------|
| US-001 | 用户登录 | 进行中 | S1 |

## P1 - 重要功能（应该有）
| ID | Story | 状态 | Sprint |
|----|-------|------|--------|
| US-002 | 用户注册 | 待开始 | - |

## P2 - 增强功能（可以有）
| ID | Story | 状态 | Sprint |
|----|-------|------|--------|

## P3 - 未来考虑（不会有）
| ID | Story | 状态 | Sprint |
|----|-------|------|--------|
```

### 2. 优先级判断

**MoSCoW 方法：**
- **M**ust have — 没有它产品无法发布
- **S**hould have — 重要但可以变通
- **C**ould have — 有则更好
- **W**on't have — 本次不实现

**价值/复杂度矩阵：**
```
         高价值              低价值
高复杂度  | 优先评估         | 不做
低复杂度  | 优先做           | 有空再做
```

### 3. 状态管理

| 状态 | 说明 |
|------|------|
| 待开始 | 新建，未分配 |
| 已规划 | 已分配 Sprint |
| 进行中 | 开发中 |
| 待测试 | 开发完成 |
| 已完成 | 测试通过 |
| 已关闭 | 取消/延后 |

### 4. 定期维护

**Backlog 修剪：**
- 移除过时的 Story
- 调整优先级变化
- 更新估算
- 合并重复项

## 输出位置

```
workspace-po/backlog/product-backlog.md
workspace-po/backlog/user-stories/
```

## 下一步

Backlog 准备好后，调用 `po-sprint-planning` 进行 Sprint 规划。
