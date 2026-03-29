---
name: release-changelog
description: 基于已完成的 Task 自动生成发布日志
---

# 发布日志

## 概述

Release Agent 根据里程碑中已完成的 Task 自动生成发布日志（Changelog）。Changelog 记录本次发布的所有变更，面向使用者和开发者，是版本发布的重要组成部分。

**在流程中的位置：** 里程碑所有 Task 完成并通过测试 → **生成发布日志** → CI/CD 部署

## 触发条件

- 里程碑所有 Task 状态为 `done`
- QE 全量回归测试通过
- 准备发布新版本
- 用户要求生成变更记录

## 输入

- `sprint/sprint-status.md`（里程碑状态和完成的 Task 列表）
- `backlog/tasks/T-XXX.md`（各 Task 的详细描述）
- `sprint/tasks/T-XXX/work-log.md`（各 Task 的工作记录）
- `bugs/bug-summary.md`（修复的 Bug 列表）
- 上一个版本的 `CHANGELOG.md`

## 流程

1. **收集变更信息**：
   - 从 `sprint-status.md` 获取本次里程碑完成的全部 Task
   - 从各 Task 文件获取变更描述和实现细节
   - 从 Bug 汇总获取修复的 Bug
2. **分类整理**：
   - **新功能（Features）**：新增的功能和特性
   - **修复（Bug Fixes）**：修复的问题
   - **优化（Improvements）**：性能优化、体验改进
   - **重构（Refactors）**：代码重构（不影响功能）
   - **文档（Docs）**：文档更新
3. **确定版本号**：
   - 遵循语义化版本（SemVer）
   - 新功能 → 小版本号 +1
   - Bug 修复 → 补丁版本号 +1
   - 破坏性变更 → 大版本号 +1
4. **生成 Changelog**：按时间倒序追加到 `CHANGELOG.md`
5. **输出摘要**：向团队报告本次发布内容

## 输出

- 更新后的 `CHANGELOG.md`
- 发布摘要

## 文件规范

### Changelog 格式（Conventional Changelog 风格）

路径：`CHANGELOG.md`

```markdown
# Changelog

## [0.2.0] - 2026-03-29

### 新功能
- **T-001** 用户登录功能 — 支持邮箱密码登录和 JWT 认证
- **T-003** 首页展示 — 实现响应式首页布局

### 修复
- **T-005** 修复登录页面在移动端的样式问题
- **BUG-001** 修复空邮箱输入未校验的问题

### 优化
- **T-004** 首页加载速度优化，首屏加载时间从 3s 降至 1.5s

### 文档
- **T-006** 新增 API 接口文档

## [0.1.0] - 2026-03-20

### 新功能
- **T-000** 项目初始化 — 搭建基础框架和开发环境
```

## 注意事项

- **面向用户的语言**：Changelog 是给使用者和开发者看的，避免内部术语
- **每个变更关联 Task ID**：方便追溯详细实现
- **保持格式一致**：遵循约定俗成的 Changelog 格式
- **不要遗漏**：每个已完成的 Task 都应体现在 Changelog 中
- **版本号严格遵循 SemVer**：不要随意跳版本号
