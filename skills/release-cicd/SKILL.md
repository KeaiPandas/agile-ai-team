---
name: release-cicd
description: Release Agent CI/CD 触发技能。管理持续集成和持续部署流程。触发条件：(1) 需要触发构建，(2) 部署到环境，(3) 收到"CI/CD"、"构建"、"部署"、"deploy"等指令。
---

# CI/CD 触发 Skill

管理持续集成和持续部署流程。

## 工作流程

### 1. 发布前检查

```markdown
## 发布前检查清单

### 代码检查
- [ ] 代码已合并到发布分支
- [ ] 代码审查通过
- [ ] 无未解决的冲突

### 测试检查
- [ ] QE 确认测试通过
- [ ] 单元测试覆盖率达标
- [ ] 回归测试通过

### 配置检查
- [ ] 版本号已更新
- [ ] 配置文件已更新
- [ ] 环境变量已配置

### 文档检查
- [ ] 发布日志已准备
- [ ] API 文档已更新
- [ ] 用户文档已更新
```

### 2. 版本号管理

**语义化版本：**
```
MAJOR.MINOR.PATCH

MAJOR: 不兼容的 API 变更
MINOR: 向后兼容的功能新增
PATCH: 向后兼容的问题修复
```

**更新版本：**
```bash
# npm 项目
npm version patch  # 1.0.0 → 1.0.1
npm version minor  # 1.0.0 → 1.1.0
npm version major  # 1.0.0 → 2.0.0

# Git 标签
git tag -a v1.0.1 -m "Release v1.0.1"
git push origin v1.0.1
```

### 3. CI/CD 流程

**GitHub Actions 示例：**
```yaml
# .github/workflows/deploy.yml
name: Deploy
on:
  push:
    tags:
      - 'v*'

jobs:
  build-and-deploy:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v3

      - name: Setup Node.js
        uses: actions/setup-node@v3
        with:
          node-version: '18'

      - name: Install dependencies
        run: npm ci

      - name: Run tests
        run: npm test

      - name: Build
        run: npm run build

      - name: Deploy
        run: |
          echo "Deploying to production..."
          # 部署命令
```

**触发构建：**
```bash
# 创建标签触发 CI/CD
git tag v1.0.1
git push origin v1.0.1

# 或手动触发
gh workflow run deploy.yml
```

### 4. 环境部署

**多环境部署：**
```markdown
## 环境配置

| 环境 | 用途 | 分支 | URL |
|------|------|------|-----|
| Development | 开发测试 | develop | dev.example.com |
| Staging | 预发布验证 | staging | staging.example.com |
| Production | 正式环境 | main | example.com |
```

**部署命令：**
```bash
# 部署到开发环境
npm run deploy:dev

# 部署到预发布环境
npm run deploy:staging

# 部署到生产环境
npm run deploy:prod
```

### 5. 部署验证

```markdown
## 部署验证清单

### 健康检查
- [ ] 服务启动成功
- [ ] 健康检查接口返回正常
- [ ] 数据库连接正常
- [ ] 缓存连接正常

### 功能验证
- [ ] 核心功能可用
- [ ] 登录功能正常
- [ ] 关键业务流程正常

### 监控检查
- [ ] 日志输出正常
- [ ] 监控指标正常
- [ ] 告警规则生效
```

**健康检查脚本：**
```bash
#!/bin/bash
# health-check.sh

# 检查服务状态
curl -f https://example.com/health || exit 1

# 检查数据库连接
curl -f https://example.com/api/health/db || exit 1

echo "Health check passed!"
```

### 6. 回滚操作

**回滚步骤：**
```bash
# 1. 确认要回滚的版本
git tag -l

# 2. 回滚到上一版本
git checkout v1.0.0
npm run deploy:prod

# 或使用 CI/CD 回滚
gh workflow run rollback.yml -f version=v1.0.0
```

**回滚记录：**
```markdown
## 回滚记录

**日期：** YYYY-MM-DD HH:mm
**回滚版本：** v1.0.1 → v1.0.0
**原因：** 发现严重 Bug
**影响范围：** 所有用户
**恢复时间：** 10 分钟
```

## 输出位置

```
workspace-release/releases/vX.X.X.md
workspace-release/checklists/pre-deploy.md
workspace-release/checklists/post-deploy.md
workspace-release/rollback/history.md
```

## 下一步

部署成功后，调用 `release-changelog` 生成发布日志。
