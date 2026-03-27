# TOOLS.md - Release Agent 工具说明

## 可用工具

作为 Release Agent，我主要使用以下工具：

### 发布管理
- `read` / `write` / `edit` — 读写发布日志、配置文件
- `memory_search` / `memory_get` — 搜索历史发布记录

### CI/CD 操作
- `exec` — 执行构建、部署命令
- `process` — 管理发布进程

### 协作
- `sessions_send` — 向其他 Agent 发送发布状态
- `cron` — 定时发布任务

### 信息获取
- `web_search` — 搜索部署文档、最佳实践

## Agent 间通信

### 我可以调用的 Agent
（Release 是流程终点，无下游 Agent）

### 我接收的消息来源
| Agent ID | 角色 | 发送内容 |
|----------|------|----------|
| `qe` | 质量工程师 | 测试通过确认 |

### 通知发布完成
```
sessions_send({
  sessionKey: "agent:main:main",
  message: "v1.0.0 发布成功！"
})
```

## 常用命令

### 构建与部署
```bash
npm run build
npm run deploy
npm run rollback
```

### 版本管理
```bash
npm version patch/minor/major
git tag -a vX.Y.Z -m "Release vX.Y.Z"
git push --tags
```

### 健康检查
```bash
curl -f http://localhost:3000/health
```

## 工作目录

```
workspace-release/
├── AGENTS.md
├── SOUL.md
├── USER.md
├── IDENTITY.md
├── TOOLS.md
├── MEMORY.md
├── memory/
│   └── YYYY-MM-DD.md
├── releases/
│   └── vX.Y.Z.md
├── checklists/
│   ├── pre-deploy.md
│   └── post-deploy.md
└── rollback/
    └── history.md
```

---

_发布是一门艺术，更是一门科学。_
