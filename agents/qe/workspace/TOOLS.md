# TOOLS.md - QE Agent 工具说明

## 可用工具

作为 QE Agent，我主要使用以下工具：

### 测试管理
- `read` / `write` / `edit` — 读写测试用例、报告
- `memory_search` / `memory_get` — 搜索历史测试记录

### 执行测试
- `exec` — 运行测试脚本、命令行工具
- `process` — 管理测试进程

### 协作
- `sessions_send` — 向其他 Agent 发送 Bug 报告、测试结果
- `sessions_spawn` — 启动测试子任务

### 信息获取
- `web_search` — 搜索测试方法、工具文档

## Agent 间通信

### 我可以调用的 Agent
| Agent ID | 角色 | 用途 |
|----------|------|------|
| `dev` | 开发者 | 反馈 Bug |
| `release` | 发布工程师 | 确认发布就绪 |

### 调用方式

**反馈 Bug 给 Dev**
```
sessions_send({
  sessionKey: "agent:dev:main",
  message: "发现 Bug BUG-003：登录页面在移动端布局异常..."
})
```

**确认发布就绪**
```
sessions_spawn({
  agentId: "release",
  task: "Sprint 1 所有测试通过，可以发布 v1.0.0..."
})
```

## 常用命令

### 运行测试
```bash
npm test
npm run test:e2e
npm run test:coverage
```

### 生成报告
```bash
npm run report
```

## 工作目录

```
workspace-qe/
├── AGENTS.md
├── SOUL.md
├── USER.md
├── IDENTITY.md
├── TOOLS.md
├── MEMORY.md
├── memory/
│   └── YYYY-MM-DD.md
├── test-cases/
│   └── module/
├── bug-reports/
│   └── BUG-XXX.md
└── reports/
    └── YYYY-MM-DD.md
```

---

_测试是灯塔，照亮质量之路。_
