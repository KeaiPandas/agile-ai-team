# TOOLS.md - Dev Agent 工具说明

## 可用工具

作为 Dev Agent，我主要使用以下工具：

### 代码开发
- `read` / `write` / `edit` — 读写代码文件
- `exec` — 运行命令（git、npm、build 等）
- `process` — 管理后台进程

### 协作
- `sessions_send` — 向其他 Agent 发送消息
- `sessions_spawn` — 启动编码子任务（Claude Code 等）

### 代码审查
- `read` — 读取代码进行审查
- `edit` — 直接修改代码

### 信息获取
- `web_search` — 搜索技术问题、文档
- `web_fetch` — 获取 API 文档

## Agent 间通信

### 我可以调用的 Agent
| Agent ID | 角色 | 用途 |
|----------|------|------|
| `qe` | 质量工程师 | 提交代码测试 |

### 调用方式

**提交代码给 QE 测试**
```
sessions_spawn({
  agentId: "qe",
  task: "请测试 feature/login 分支的登录功能..."
})
```

**发送代码完成通知**
```
sessions_send({
  sessionKey: "agent:qe:main",
  message: "US-001 代码已完成，PR #42 已提交，请安排测试"
})
```

## 常用命令

### Git 操作
```bash
git status
git add .
git commit -m "type(scope): message"
git push origin branch
git checkout -b feature/xxx
```

### 项目构建
```bash
npm install
npm run build
npm test
```

## 工作目录

```
workspace-dev/
├── AGENTS.md
├── SOUL.md
├── USER.md
├── IDENTITY.md
├── TOOLS.md
├── MEMORY.md
├── memory/
│   └── YYYY-MM-DD.md
├── code/              # 代码目录
└── docs/
    └── technical/     # 技术文档
```

---

_工欲善其事，必先利其器。_
