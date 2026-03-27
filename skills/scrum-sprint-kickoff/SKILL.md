---
name: scrum-sprint-kickoff
description: Scrum Master Sprint 启动技能。组织 Sprint 启动，分配任务给开发者。触发条件：(1) 收到 PO 的 Sprint Backlog，(2) 需要启动新 Sprint，(3) 收到"启动 Sprint"、"开始 Sprint"、"分配任务"等指令。
---

# Sprint 启动 Skill

组织 Sprint 启动，分配任务给开发团队。

## 工作流程

### 1. 接收 Sprint Backlog

从 PO 接收确认的 Sprint Backlog，确认：
- [ ] Sprint 目标是否清晰
- [ ] Story 验收标准是否明确
- [ ] 故事点估算是否合理

### 2. 任务分配原则

**分配考虑因素：**
- 开发者技能匹配
- 工作量平衡
- 技术依赖关系
- 学习成长机会

**任务分配表：**
```markdown
## Sprint XX 任务分配

| Story | 负责人 | 协助人 | 预计完成 |
|-------|--------|--------|----------|
| US-001 | Dev-A | Dev-B | Day 3 |
| US-002 | Dev-B | - | Day 5 |
```

### 3. 通知开发者

**启动子任务：**
```json
sessions_spawn({
  "agentId": "dev",
  "task": " Sprint XX 任务分配：\n\nStory: US-001 用户登录\n故事点: 3\n截止: Day 3\n\n验收标准:\n- 支持手机号登录\n- 支持密码登录\n- 登录失败有明确提示\n\n请开始开发。"
})
```

### 4. Sprint 启动检查清单

- [ ] 所有 Story 已分配
- [ ] 开发者已确认任务
- [ ] 依赖关系已梳理
- [ ] 风险已识别并记录

## 输出位置

```
workspace-scrum/sprints/sprint-XX.md
workspace-scrum/sprints/sprint-XX-tasks.md
```

## 下一步

Sprint 启动后，使用 `scrum-standup` 进行每日站会跟踪。
