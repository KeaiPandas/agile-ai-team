---
name: qe-regression-test
description: QE Agent 回归测试技能。确认修复后功能正常，无新引入问题。触发条件：(1) Bug 修复后验证，(2) 发布前验证，(3) 收到"回归测试"、"验证"、"regression"等指令。
---

# 回归测试 Skill

确认修复后功能正常，无新引入问题。

## 工作流程

### 1. 回归测试范围

**全量回归：**
- 所有测试用例
- 适用于：大版本发布、核心模块变更

**部分回归：**
- 受影响模块的用例
- 适用于：Bug 修复、小功能更新

**冒烟测试：**
- 核心功能的 P0 用例
- 适用于：快速验证、热修复

### 2. Bug 验证清单

```markdown
## BUG-XXX 回归验证

**Bug 描述：** 登录页面系统错误
**修复版本：** vX.X.X
**验证人：** QE Agent
**验证时间：** YYYY-MM-DD

### 验证步骤

- [ ] 1. 验证原 Bug 已修复
  - 测试步骤：[复现步骤]
  - 预期结果：[正确行为]
  - 实际结果：✅ 通过 / ❌ 失败

- [ ] 2. 验证关联功能正常
  - 关联功能：注册、密码找回
  - 测试结果：✅ 通过

- [ ] 3. 验证边界场景
  - 边界场景：空手机号、错误密码
  - 测试结果：✅ 通过

### 回归范围

| 模块 | 用例数 | 通过 | 失败 |
|------|--------|------|------|
| 登录 | 5 | 5 | 0 |
| 注册 | 3 | 3 | 0 |
| 首页 | 2 | 2 | 0 |

### 结论
- [ ] ✅ 验证通过，可以关闭
- [ ] ❌ 验证失败，重新打开
- [ ] ⚠️ 有新问题，创建新 Bug

### 备注
[补充说明]
```

### 3. 回归测试矩阵

```markdown
## 回归测试矩阵

| Bug ID | 关联功能 | 验证用例 | 状态 |
|--------|----------|----------|------|
| BUG-001 | 登录 | TC-001~005 | ✅ 通过 |
| BUG-002 | 注册 | TC-010~015 | ✅ 通过 |
| BUG-003 | 支付 | TC-020~025 | ❌ 失败 |
```

### 4. 自动化回归

**执行自动化测试：**
```bash
# 运行所有测试
npm test

# 运行指定模块
npm test -- login

# 运行 E2E 测试
npx playwright test

# 生成覆盖率报告
npm test -- --coverage --reporter=html
```

**CI 集成示例：**
```yaml
# .github/workflows/regression.yml
name: Regression Test
on: [push, pull_request]
jobs:
  test:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v3
      - uses: actions/setup-node@v3
      - run: npm ci
      - run: npm test
      - run: npm run test:e2e
```

### 5. 回归测试报告

```markdown
## 回归测试报告 - YYYY-MM-DD

### 测试概要
- 测试类型：Bug 回归 / 发布回归
- 测试范围：登录模块
- 测试版本：vX.X.X
- 测试人员：QE Agent

### 测试结果

| 指标 | 数量 |
|------|------|
| 用例总数 | XX |
| 通过 | XX |
| 失败 | XX |
| 阻塞 | XX |
| 通过率 | XX% |

### Bug 验证结果

| Bug ID | 状态 | 备注 |
|--------|------|------|
| BUG-001 | ✅ 已修复 | - |
| BUG-002 | ✅ 已修复 | - |
| BUG-003 | ❌ 未修复 | 新问题 |

### 新发现问题
1. TC-XXX: [问题描述]
   - 状态：新建 Bug BUG-XXX

### 结论
- [ ] ✅ 可发布
- [ ] ⚠️ 有风险，建议修复后发布
- [ ] ❌ 不可发布

### 建议
[改进建议]
```

### 6. 发布就绪确认

回归测试通过后，通知 Release Agent：

```json
sessions_spawn({
  "agentId": "release",
  "task": "Sprint XX 回归测试已完成，通过率 100%，可以发布 v1.0.0"
})
```

## 输出位置

```
workspace-qe/reports/regression-YYYY-MM-DD.md
```

## 注意事项

- 回归测试要覆盖修复点和关联模块
- 关注是否有新引入问题
- 记录测试环境和数据
- 自动化回归提高效率
