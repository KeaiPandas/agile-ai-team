---
name: dev-tech-docs
description: Dev Agent 技术文档生成技能。生成和维护技术文档。触发条件：(1) 需要生成技术文档，(2) 更新 API 文档，(3) 收到"写文档"、"技术文档"、"API 文档"等指令。
---

# 技术文档生成 Skill

生成清晰、实用的技术文档。

## 工作流程

### 1. 文档类型

| 类型 | 用途 | 受众 |
|------|------|------|
| API 文档 | 接口说明 | 前端/第三方 |
| 架构文档 | 系统设计 | 团队/新人 |
| 部署文档 | 运维指南 | 运维/DevOps |
| 开发文档 | 开发指南 | 开发者 |

### 2. API 文档格式

```markdown
# API 文档 - [模块名]

## 接口：[接口名称]

**路径：** `POST /api/v1/auth/login`
**描述：** 用户登录接口

### 请求参数

| 参数名 | 类型 | 必填 | 说明 |
|--------|------|------|------|
| phone | string | 是 | 手机号 |
| password | string | 是 | 密码 |

### 请求示例

```json
{
  "phone": "13800138000",
  "password": "password123"
}
```

### 响应参数

| 参数名 | 类型 | 说明 |
|--------|------|------|
| code | number | 状态码 |
| message | string | 消息 |
| data.token | string | 登录令牌 |
| data.user | object | 用户信息 |

### 响应示例

**成功：**
```json
{
  "code": 0,
  "message": "success",
  "data": {
    "token": "eyJhbGc...",
    "user": {
      "id": 1,
      "phone": "13800138000"
    }
  }
}
```

**失败：**
```json
{
  "code": 401,
  "message": "用户名或密码错误"
}
```

### 错误码

| 错误码 | 说明 |
|--------|------|
| 401 | 认证失败 |
| 400 | 参数错误 |
| 500 | 服务器错误 |
```

### 3. 架构文档格式

```markdown
# 系统架构 - [项目名]

## 概述
[一句话描述系统定位]

## 技术栈
- 前端：React + TypeScript
- 后端：Node.js + Express
- 数据库：PostgreSQL
- 缓存：Redis

## 系统架构图

```
┌─────────────┐     ┌─────────────┐
│   前端应用   │────▶│   API 服务   │
└─────────────┘     └─────────────┘
                          │
                    ┌─────┴─────┐
                    ▼           ▼
              ┌─────────┐ ┌─────────┐
              │ PostgreSQL│ │  Redis  │
              └─────────┘ └─────────┘
```

## 核心模块

### 模块一：用户认证
- 职责：处理用户登录、注册、权限
- 依赖：数据库、缓存
- 关键文件：`/src/auth/`

### 模块二：业务逻辑
...

## 数据模型

### User 用户表
| 字段 | 类型 | 说明 |
|------|------|------|
| id | bigint | 主键 |
| phone | varchar(20) | 手机号 |
| password_hash | varchar(255) | 密码哈希 |

## 部署说明
参见 [部署文档](./deployment.md)
```

### 4. 开发文档格式

```markdown
# 开发指南

## 环境要求
- Node.js >= 18
- PostgreSQL >= 14
- Redis >= 6

## 快速开始

```bash
# 安装依赖
npm install

# 配置环境变量
cp .env.example .env

# 启动开发服务器
npm run dev
```

## 项目结构

```
src/
├── auth/          # 认证模块
├── user/          # 用户模块
├── common/        # 公共模块
└── config/        # 配置文件
```

## 代码规范
- 使用 ESLint + Prettier
- 提交前运行 `npm run lint`
- 单元测试覆盖率 >= 80%

## 常见问题
参见 [FAQ](./faq.md)
```

## 输出位置

```
workspace-dev/docs/
├── api/
├── architecture/
├── deployment/
└── development/
```

## 注意事项

- 文档与代码保持同步
- 使用示例而非长篇解释
- 定期更新过时内容
