---
name: dev-git-operations
description: Dev Agent Git 操作技能。执行 commit、branch、PR、merge 等 Git 版本控制操作，维护代码仓库的整洁和规范。
---

# Dev Agent - Git 操作技能

## 概述

本技能指导 Dev Agent 执行各类 Git 操作，确保版本控制的规范性和代码仓库的整洁。良好的 Git 操作习惯不仅让项目历史清晰可追溯，还能有效避免代码冲突和丢失。Dev Agent 应成为团队的 Git 最佳实践守护者。

## 触发条件

- 需要提交代码变更（commit）
- 需要创建或管理分支（branch）
- 需要创建 Pull Request / Merge Request
- 收到"commit"、"push"、"PR"、"git"、"合并"、"分支"等指令
- Sprint 结束需要合并代码到主分支
- 需要解决代码冲突

## 流程

### 1. 分支管理

- **分支命名规范**: 遵循团队约定的命名规则，如 `feature/xxx`、`bugfix/xxx`、`hotfix/xxx`
- **创建分支**: 从最新的 develop/main 分支创建功能分支
- **保持分支更新**: 定期将主分支的变更合并到功能分支，减少冲突

### 2. Commit 规范

- 使用语义化 commit message，推荐格式：
  ```
  <type>(<scope>): <subject>

  <body>
  ```
- **type 类型**: feat | fix | docs | style | refactor | perf | test | chore
- **subject**: 简明扼要描述变更内容（不超过 50 字符）
- **body**: 详细说明变更原因和影响（如有必要）
- 每次提交保持原子性：一个 commit 只做一件事

### 3. Pull Request 创建

- PR 标题清晰描述变更内容
- PR 描述包含：变更目的、主要改动、测试方式、关联 Issue
- 确保本地测试通过后再创建 PR
- 添加合适的 label 和 reviewer

### 4. 代码合并

- 合并前确认 CI 通过、Review 通过
- 选择合适的合并策略：merge / squash merge / rebase
- 合并后及时删除功能分支
- 同步更新本地仓库

### 5. 冲突解决

- 识别冲突文件
- 理解双方变更意图
- 与相关开发者沟通确认解决方案
- 解决后运行测试确保功能正常

## 输入

- **代码变更**: 需要提交或合并的代码修改
- **任务上下文**: 关联的 User Story 或 Issue
- **团队规范**: 分支命名、commit 格式等团队约定

## 输出

- **规范的 Git 提交记录**: 清晰、语义化的 commit history
- **PR/MR**: 格式规范的 Pull Request
- **合并完成**: 代码成功合并到目标分支

## 注意事项

- **不要直接 push 到 main/master**: 始终通过 PR 合并到主分支。
- **commit 前检查 diff**: 提交前仔细检查变更内容，避免提交调试代码或敏感信息。
- **不要 force push 公共分支**: 仅在自己的功能分支上使用 force push。
- **敏感信息不入库**: API Key、密码等敏感信息绝不提交到仓库。
- **定期清理分支**: 合并后的功能分支及时删除，保持仓库整洁。
- **写好 commit message**: 未来回头看时，commit message 是最好的文档。
- **大功能拆分 PR**: 如果变更很大，拆分为多个小 PR，便于 Review 和回滚。
