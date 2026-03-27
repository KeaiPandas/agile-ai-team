---
name: release-changelog
description: Release Agent 发布日志生成技能。自动生成清晰、规范的发布日志。触发条件：(1) 发布完成后，(2) 需要生成 Release Notes，(3) 收到"发布日志"、"changelog"、"release notes"等指令。
---

# 发布日志生成 Skill

自动生成清晰、规范的发布日志。

## 工作流程

### 1. 收集变更信息

**来源：**
- Git commits（按类型分类）
- PR 列表
- Bug 修复记录
- 功能变更说明

**收集命令：**
```bash
# 获取两个版本之间的 commits
git log v1.0.0..v1.0.1 --oneline

# 按类型分类
git log v1.0.0..v1.0.1 --pretty=format:"%s" | grep "^feat"  # 新功能
git log v1.0.0..v1.0.1 --pretty=format:"%s" | grep "^fix"   # 修复
git log v1.0.0..v1.0.1 --pretty=format:"%s" | grep "^refactor"  # 重构
```

### 2. 发布日志格式

```markdown
# Release v1.0.1

**发布日期：** YYYY-MM-DD
**发布类型：** 补丁版本

## 🎉 新功能

- 添加用户头像上传功能 (PR #42)
- 支持记住登录状态 (PR #45)

## 🐛 Bug 修复

- 修复登录页面在移动端布局异常 (PR #43)
- 修复密码找回邮件发送失败 (PR #44)

## 🔧 改进

- 优化首页加载速度，提升 30% (PR #41)
- 重构用户认证模块，提高可维护性

## 📝 文档更新

- 更新 API 文档
- 补充用户使用指南

## ⚠️ 破坏性变更

无

## 📦 升级说明

本次为补丁版本，直接升级即可，无需额外操作。

```bash
npm update my-app
```

## 🔗 相关链接

- [完整 Changelog](https://github.com/xxx/xxx/compare/v1.0.0...v1.0.1)
- [Issues 关闭](https://github.com/xxx/xxx/milestone/1?closed=1)
```

### 3. 变更分类

| 类型 | 图标 | 说明 |
|------|------|------|
| feat | 🎉 | 新功能 |
| fix | 🐛 | Bug 修复 |
| refactor | 🔧 | 重构 |
| perf | ⚡ | 性能优化 |
| docs | 📝 | 文档更新 |
| test | ✅ | 测试相关 |
| chore | 🔨 | 构建/工具 |
| breaking | ⚠️ | 破坏性变更 |

### 4. 发布类型说明

| 类型 | 版本号变化 | 说明 |
|------|-----------|------|
| 大版本 | X.0.0 | 重大更新，可能有破坏性变更 |
| 功能版本 | 0.X.0 | 新功能，向后兼容 |
| 补丁版本 | 0.0.X | Bug 修复，向后兼容 |
| 热修复 | 0.0.X | 紧急修复 |

### 5. 破坏性变更说明

**如有破坏性变更，必须包含：**
```markdown
## ⚠️ 破坏性变更

### API 变更
- `login()` 方法签名变更
  - 旧：`login(username, password)`
  - 新：`login({ phone, password })`
  - 迁移：将参数改为对象形式

### 配置变更
- 删除 `OLD_CONFIG` 配置项
  - 迁移：使用 `NEW_CONFIG` 替代

### 数据库变更
- 新增 `avatar` 字段
  - 迁移：运行 `npm run migrate`
```

### 6. 发布通知

**生成后通知相关方：**
```json
sessions_send({
  "sessionKey": "agent:main:main",
  "message": "v1.0.1 发布成功！\n\n🎉 新功能：用户头像上传\n🐛 修复：登录页面布局问题\n\n详细日志：workspace-release/releases/v1.0.1.md"
})
```

### 7. 发布归档

```markdown
## 发布历史

| 版本 | 日期 | 类型 | 主要变更 |
|------|------|------|----------|
| v1.0.1 | 2026-03-25 | 补丁 | Bug 修复 |
| v1.0.0 | 2026-03-20 | 正式 | 首次发布 |
```

## 输出位置

```
workspace-release/releases/vX.X.X.md
workspace-release/releases/history.md
```

## 注意事项

- 使用用户友好的语言，避免技术术语
- 破坏性变更必须醒目标注
- 提供清晰的升级/迁移指南
- 记录贡献者和感谢
