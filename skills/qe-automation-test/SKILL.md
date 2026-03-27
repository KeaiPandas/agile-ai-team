---
name: qe-automation-test
description: QE Agent 自动化测试技能。编写和执行自动化测试脚本。触发条件：(1) 需要编写自动化测试，(2) 执行测试脚本，(3) 收到"自动化测试"、"e2e"、"测试脚本"等指令。
---

# 自动化测试 Skill

编写和执行自动化测试脚本。

## 工作流程

### 1. 选择测试框架

| 类型 | 推荐框架 |
|------|----------|
| 单元测试 | Jest, Vitest |
| E2E 测试 | Playwright, Cypress |
| API 测试 | Supertest, Axios |

### 2. 单元测试示例

```typescript
// login.test.ts
import { login } from './auth';

describe('登录功能', () => {
  test('正常登录应该成功', async () => {
    const result = await login('13800138000', 'password123');
    expect(result.token).toBeDefined();
    expect(result.user.phone).toBe('13800138000');
  });

  test('密码错误应该抛出异常', async () => {
    await expect(
      login('13800138000', 'wrongpassword')
    ).rejects.toThrow('用户名或密码错误');
  });

  test('手机号为空应该抛出异常', async () => {
    await expect(
      login('', 'password123')
    ).rejects.toThrow('手机号不能为空');
  });
});
```

### 3. E2E 测试示例

```typescript
// login.spec.ts (Playwright)
import { test, expect } from '@playwright/test';

test.describe('登录功能', () => {
  test.beforeEach(async ({ page }) => {
    await page.goto('/login');
  });

  test('正常登录流程', async ({ page }) => {
    // 输入手机号
    await page.fill('[data-testid="phone-input"]', '13800138000');

    // 输入密码
    await page.fill('[data-testid="password-input"]', 'password123');

    // 点击登录
    await page.click('[data-testid="login-button"]');

    // 验证跳转
    await expect(page).toHaveURL('/home');

    // 验证用户信息显示
    await expect(page.locator('[data-testid="user-phone"]')).toHaveText('13800138000');
  });

  test('密码错误提示', async ({ page }) => {
    await page.fill('[data-testid="phone-input"]', '13800138000');
    await page.fill('[data-testid="password-input"]', 'wrongpassword');
    await page.click('[data-testid="login-button"]');

    // 验证错误提示
    await expect(page.locator('[data-testid="error-message"]')).toHaveText('用户名或密码错误');
  });
});
```

### 4. API 测试示例

```typescript
// auth.api.test.ts
import request from 'supertest';
import app from './app';

describe('登录 API', () => {
  test('POST /api/v1/auth/login', async () => {
    const response = await request(app)
      .post('/api/v1/auth/login')
      .send({
        phone: '13800138000',
        password: 'password123'
      });

    expect(response.status).toBe(200);
    expect(response.body.code).toBe(0);
    expect(response.body.data.token).toBeDefined();
  });
});
```

### 5. 执行测试

```bash
# 单元测试
npm test

# E2E 测试
npx playwright test

# 测试覆盖率
npm test -- --coverage

# 指定文件
npm test login.test.ts
```

### 6. 测试报告

```markdown
## 测试报告 - YYYY-MM-DD

### 概要
- 测试框架：Jest + Playwright
- 用例总数：XX
- 通过：XX
- 失败：XX
- 跳过：XX
- 覆盖率：XX%

### 详细结果

| 模块 | 用例数 | 通过 | 失败 |
|------|--------|------|------|
| 登录 | 10 | 9 | 1 |
| 注册 | 8 | 8 | 0 |

### 失败用例
1. TC-005: 手机号格式验证
   - 原因：预期抛出异常，实际返回 null
   - 截图：[链接]
```

## 输出位置

```
workspace-qe/scripts/
workspace-qe/reports/
```

## 下一步

测试失败时，调用 `qe-bug-report` 提交 Bug。
