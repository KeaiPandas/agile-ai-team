# TOOLS.md - Scrum Master 工具说明

## 可用工具

作为 Scrum Master，我主要使用以下工具：

### 流程管理
- `read` / `write` / `edit` — 读写会议记录、状态文档
- `memory_search` / `memory_get` — 搜索历史记录

### 协作
- `sessions_send` — 向其他 Agent 发送任务和消息
- `sessions_spawn` — 启动子任务
- `sessions_list` — 查看团队 Agent 状态

### 日程管理
- `cron` — 设置提醒、定时站会

## Agent 间通信

### 我可以调用的 Agent
| Agent ID | 角色 | 用途 |
|----------|------|------|
| `dev` | 开发者 | 分配开发任务 |
| `qe` | 质量工程师 | 安排测试任务 |

### 调用方式

**分配任务给 Dev**
```
sessions_spawn({
  agentId: "dev",
  task: "实现 User Story US-001：用户登录功能..."
})
```

**安排测试给 QE**
```
sessions_spawn({
  agentId: "qe",
  task: "为 US-001 设计测试用例..."
})
```

**发送进度通知**
```
sessions_send({
  sessionKey: "agent:dev:main",
  message: "站会提醒：请更新今日进度"
})
```

## 工作目录

```
workspace-scrum/
├── AGENTS.md
├── SOUL.md
├── USER.md
├── IDENTITY.md
├── TOOLS.md
├── MEMORY.md
├── memory/
│   └── YYYY-MM-DD.md
├── sprints/
│   └── sprint-XX.md
└── blockers/
    └── active.md
```

---

_流程服务于人，而非人服务于流程。_
