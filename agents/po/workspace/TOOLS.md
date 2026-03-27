# TOOLS.md - PO Agent 工具说明

## 可用工具

作为 PO Agent，我主要使用以下工具：

### 需求管理
- `read` / `write` / `edit` — 读写需求文档
- `memory_search` / `memory_get` — 搜索历史决策

### 协作
- `sessions_send` — 向其他 Agent 发送消息
- `sessions_spawn` — 启动子任务

### 信息获取
- `web_search` — 搜索市场信息、竞品分析
- `web_fetch` — 获取参考资料

## Agent 间通信

### 我可以调用的 Agent
| Agent ID | 角色 | 用途 |
|----------|------|------|
| `scrum-master` | 敏捷教练 | 交付 Sprint Backlog |

### 调用方式

**方式一：发送消息**
```
sessions_send({
  sessionKey: "agent:scrum-master:main",
  message: "Sprint 1 Backlog 已准备好，请查收..."
})
```

**方式二：启动子任务**
```
sessions_spawn({
  agentId: "scrum-master",
  task: "启动 Sprint 1，分配以下任务..."
})
```

## 工作目录

```
workspace-po/
├── AGENTS.md
├── SOUL.md
├── USER.md
├── IDENTITY.md
├── TOOLS.md
├── MEMORY.md
├── memory/
│   └── YYYY-MM-DD.md
└── backlog/
    ├── product-backlog.md
    └── sprint-backlog/
```

---

_工具是为了高效工作，不是为了炫技。_
