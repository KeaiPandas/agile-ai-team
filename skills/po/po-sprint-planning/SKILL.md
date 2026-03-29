---
name: po-sprint-planning
description: PO Agent Sprint 计划技能。划定 Sprint 范围，制定 Sprint 目标，选择并排序 Sprint Backlog 条目。
---

# PO Agent - Sprint 计划技能

## 概述

本技能指导 PO Agent 组织和参与 Sprint Planning 会议，划定 Sprint 范围，制定清晰的 Sprint 目标，并选择合适的工作项进入 Sprint Backlog。Sprint Planning 是每个 Sprint 的起点，一个好的计划为整个 Sprint 的成功交付奠定基础。

## 触发条件

- 开始新的 Sprint 规划
- 需要确定 Sprint 的范围和目标
- 收到"Sprint 计划"、"规划 Sprint"、"启动 Sprint"、"sprint planning"等指令
- 当前 Sprint 即将结束，需要规划下一个 Sprint
- 团队需要重新评估 Sprint 范围

## 流程

### 1. 准备阶段（Sprint Planning 前）

- 回顾上一个 Sprint 的交付情况和速度（Velocity）
- 评估当前 Backlog 中就绪（Ready）的条目
- 识别高优先级的需求和技术债
- 准备 Sprint 目标的初步设想
- 与 Scrum Master 确认团队可用容量

### 2. Sprint 目标制定

- 基于当前产品目标和优先级，提出 1-3 个 Sprint 目标
- 目标应是具体、可衡量的（如"完成用户注册和登录功能"）
- 确保目标具有挑战性但可达成
- 与团队讨论并达成共识

### 3. 选择 Sprint Backlog

- 从 Product Backlog 中选择与 Sprint 目标对齐的条目
- 考虑团队的交付速度和历史数据
- 确保选中的 Story 已细化，有明确的验收标准
- 预留一定容量（约 10-20%）给突发问题和技术债
- 记录未选入的条目及原因

### 4. 容量规划

- 评估团队成员的可用时间（考虑请假、会议等）
- 参考历史 Sprint 的完成情况
- 与开发团队确认对所选工作的估算
- 确保总工作量在团队容量范围内

### 5. 输出 Sprint 计划

- 记录 Sprint 目标
- 列出 Sprint Backlog（含每个 Story 的负责人和估算）
- 标注依赖关系和风险项
- 确定团队对计划的承诺

## 输入

- **Product Backlog**: 已排序和细化的产品待办列表
- **团队容量**: 团队的可用开发能力和历史速度
- **业务优先级**: 当前最重要的业务目标和需求
- **技术约束**: 已知的技术依赖和限制

## 输出

- **Sprint 目标**: 1-3 个明确的 Sprint 目标
- **Sprint Backlog**: 选入本 Sprint 的 User Story 列表
- **容量分配**: 团队成员的任务分配和工时估算
- **风险清单**: 已识别的风险和应对计划

## 注意事项

- **Sprint 目标比具体列表更重要**：目标是团队的共同方向，列表是实现目标的手段。
- **不要过度承诺**：宁可少选一些，保证质量交付，也不要贪多嚼不烂。
- **预留缓冲**：总会有意料之外的问题，预留 10-20% 的容量。
- **团队共同承诺**：Sprint 计划是团队协商的结果，不是 PO 单方面分配。
- **Sprint 范围一旦确定尽量不变**：频繁变更 Sprint 范围会打乱团队节奏。如有必要变更，需团队同意。
- **关注依赖关系**：合理安排 Story 的执行顺序，避免阻塞。
