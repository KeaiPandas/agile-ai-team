---
name: dev-git-operations
description: Dev Agent Git 操作技能。执行 commit、PR、分支管理等 Git 操作。触发条件：(1) 需要提交代码，(2) 创建 PR，(3) 收到"commit"、"push"、"PR"、"git"等指令。
---

# Git 操作 Skill

执行 Git 相关操作，管理代码版本。

## 工作流程

### 1. 分支策略

**分支命名规范：**
```
feature/US-XXX-description  # 功能分支
bugfix/BUG-XXX-description  # Bug 修复分支
hotfix/XXX-description      # 紧急修复
release/vX.X.X              # 发布分支
```

**创建分支：**
```bash
# 从 main 创建功能分支
git checkout main
git pull origin main
git checkout -b feature/US-001-user-login
```

### 2. Commit 规范

**Commit 消息格式：**
```
<type>(<scope>): <subject>

<body>

<footer>
```

**Type 类型：**
| Type | 说明 | 示例 |
|------|------|------|
| feat | 新功能 | feat(auth): 添加用户登录功能 |
| fix | Bug 修复 | fix(auth): 修复登录验证逻辑 |
| refactor | 重构 | refactor(auth): 优化登录流程 |
| docs | 文档 | docs(readme): 更新安装说明 |
| test | 测试 | test(auth): 添加登录单元测试 |
| chore | 构建/工具 | chore(deps): 更新依赖版本 |

**Commit 示例：**
```
feat(auth): 添加用户登录功能

- 实现手机号+密码登录
- 添加表单验证
- 添加登录错误提示

Closes #42
```

### 3. 提交流程

```bash
# 查看变更
git status
git diff

# 添加文件
git add .

# 提交
git commit -m "feat(auth): 添加用户登录功能"

# 推送
git push origin feature/US-001-user-login
```

### 4. 创建 PR

**PR 描述模板：**
```markdown
## 变更说明
实现用户登录功能，支持手机号+密码登录。

## 关联 Issue
Closes #42

## 变更类型
- [x] 新功能
- [ ] Bug 修复
- [ ] 重构
- [ ] 文档更新

## 测试情况
- [x] 单元测试通过
- [x] 本地功能测试通过
- [x] Lint 检查通过

## 截图
[如有 UI 变更，附上截图]

## 检查清单
- [x] 代码符合规范
- [x] 已添加必要注释
- [x] 已更新相关文档
```

**创建 PR 命令：**
```bash
# 使用 GitHub CLI
gh pr create --title "feat(auth): 添加用户登录功能" --body-file pr-template.md
```

### 5. 常用命令

```bash
# 查看状态
git status

# 查看日志
git log --oneline -10

# 合并分支
git merge feature/US-001-user-login

# 回滚
git revert <commit-hash>
git reset --soft HEAD~1  # 撤销最近一次 commit，保留变更

# 解决冲突
git status  # 查看冲突文件
# 手动解决冲突后
git add <resolved-files>
git commit
```

## 输出位置

代码提交到远程仓库。

## 下一步

代码提交后，通知 QE Agent 进行测试：

```json
sessions_spawn({
  "agentId": "qe",
  "task": "PR #42 已提交，请测试用户登录功能..."
})
```
