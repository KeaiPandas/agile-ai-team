---
name: dev-git-operations
description: 管理 Git 操作，包括分支管理、提交规范、PR 创建和合并
---

# Git 操作

## 概述

Dev Agent 管理项目的 Git 操作，确保代码版本控制规范统一。包括分支命名、提交信息格式、PR 创建和合并策略。每个 Task 对应独立的 feature 分支，通过 PR 合并到主分支。

**在流程中的位置：** 贯穿整个开发流程，代码生成后提交 → 代码审查通过后合并

## 触发条件

- 代码生成完成后需要提交
- Task 审查通过后需要创建 PR 并合并
- 里程碑发布后需要打 tag
- 需要回滚或修复

## 输入

- Task ID（`T-XXX`）
- 代码变更文件列表
- PR 模板（如有）

## 流程

1. **创建功能分支**：
   - 从 `main` 或 `develop` 分支拉取最新代码
   - 创建命名规范的分支：`feature/T-XXX-task-description`
   - 修复分支：`fix/T-XXX-bug-description`

2. **提交代码**：
   - 使用规范的 commit message
   - 每个 Task 至少一个 commit，复杂 Task 可拆分多个 commit
   - Commit message 格式：`T-XXX: 简要描述`
   - 每次提交前确认 lint 和类型检查通过

3. **推送到远程**：
   - 推送功能分支到远程仓库
   - 触发 CI 流水线（如有）

4. **创建 PR**：
   - PR 标题：`[T-XXX] Task 描述`
   - PR 描述包含：变更说明、关联 Task、验收标准检查
   - 设置审查者（如有）

5. **合并 PR**：
   - 审查通过后合并（Squash Merge 优先）
   - 合并后删除功能分支
   - 更新 `sprint-status.md` 中 Task 状态

6. **版本标签**：
   - 里程碑完成后打 tag：`v<里程碑版本号>`
   - 推送 tag 触发部署流程

## 输出

- Git 分支和提交记录
- PR 链接（如有远程仓库）
- 更新后的 `sprint-status.md`

## 文件规范

### Commit Message 格式

```
T-XXX: 简要描述（50 字以内）

详细说明（可选）：
- 改动点 1
- 改动点 2
```

### PR 模板

```markdown
## 关联 Task
- T-XXX: Task 描述

## 变更说明
简要描述本次变更的内容。

## 验收标准
- [x] 标准 1
- [x] 标准 2

## 测试
- [x] 单元测试通过
- [x] 本地功能验证通过
```

### 分支命名规范

```
feature/T-XXX-简短描述    # 功能开发
fix/T-XXX-简短描述        # Bug 修复
refactor/T-XXX-简短描述   # 重构
```

## 注意事项

- **一个 Task 一个分支**：避免在同一个分支上开发多个 Task
- **提交前检查**：确保 lint 和类型检查通过再提交
- **不要 force push**：除非确认不会影响其他人
- **保持 main 分支稳定**：只有通过审查的代码才能合并到 main
- **Commit 信息可追溯**：每个 Commit 关联 Task ID，方便回溯
