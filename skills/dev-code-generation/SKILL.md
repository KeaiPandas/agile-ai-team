---
name: dev-code-generation
description: Dev Agent 代码生成技能。使用 Claude Code 或其他编码工具生成高质量代码。触发条件：(1) 需要编写新代码，(2) 实现功能需求，(3) 收到"写代码"、"实现功能"、"开发"、"编码"等指令。
---

# 代码生成 Skill

使用编码工具生成高质量代码。

## 工作流程

### 1. 理解需求

开发前确认：
- [ ] User Story 是否清晰
- [ ] 验收标准是否明确
- [ ] 技术栈是否确定
- [ ] 是否有设计稿/API 文档

### 2. 技术方案设计

**设计要点：**
- 架构模式（MVC、Clean Architecture 等）
- 数据结构设计
- API 设计（如有）
- 错误处理策略
- 测试策略

### 3. 代码生成方式

**方式一：使用 coding-agent skill（推荐）**
```
sessions_spawn({
  "agentId": "coding-agent",
  "task": "实现用户登录功能：\n- 技术栈：React + TypeScript\n- 需求：手机号+密码登录\n- 包含表单验证"
})
```

**方式二：直接编写**
```javascript
// 使用 read/write/edit 工具直接编写代码
```

### 4. 代码质量标准

**必须满足：**
- [ ] 符合项目代码规范
- [ ] 有适当的注释
- [ ] 错误处理完善
- [ ] 无明显的性能问题
- [ ] 无安全漏洞

**代码规范示例：**
```javascript
/**
 * 用户登录
 * @param phone 手机号
 * @param password 密码
 * @returns 登录结果
 */
async function login(phone: string, password: string): Promise<LoginResult> {
  // 参数验证
  if (!validatePhone(phone)) {
    throw new ValidationError('手机号格式错误');
  }

  // 业务逻辑
  const user = await userRepository.findByPhone(phone);
  if (!user || !user.validatePassword(password)) {
    throw new AuthenticationError('用户名或密码错误');
  }

  // 返回结果
  return { token: generateToken(user), user };
}
```

### 5. 自测清单

提交前自测：
- [ ] 功能是否正常工作
- [ ] 边界条件是否处理
- [ ] 错误情况是否覆盖
- [ ] 代码是否通过 Lint
- [ ] 单元测试是否通过

## 输出位置

```
workspace-dev/code/
```

## 下一步

代码完成后：
1. 调用 `dev-code-review` 进行代码审查
2. 调用 `dev-git-operations` 提交代码
