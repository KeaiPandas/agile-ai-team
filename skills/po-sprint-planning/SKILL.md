---
name: po-sprint-planning
description: PO Agent Sprint 计划技能。划定 Sprint 范围，制定 Sprint 目标和 Backlog。触发条件：(1) 开始新的 Sprint 规划，(2) 确定 Sprint 范围，(3) 收到"Sprint 计划"、"规划 Sprint"、"启动 Sprint"等指令。
---

# Sprint 计划 Skill

制定 Sprint 目标和 Sprint Backlog。

## 工作流程

### 1. 确定 Sprint 信息

```markdown
## Sprint XX 计划

**时间范围：** YYYY-MM-DD ~ YYYY-MM-DD
**Sprint 目标：** [一句话描述本次 Sprint 要达成什么]
**团队容量：** [可用人数 × 天数 × 效率系数]
```

### 2. 选择 Story

**选择原则：**
- 优先选择 P0/P1 Story
- 总故事点不超过团队容量
- 考虑技术依赖关系
- 平衡风险和确定性

**Story 选择检查：**
- [ ] 是否符合 Sprint 目标？
- [ ] 是否有明确验收标准？
- [ ] 是否可估算？
- [ ] 是否有足够容量？

### 3. Sprint Backlog 格式

```markdown
# Sprint XX Backlog

## Sprint 信息
- **Sprint 编号：** XX
- **开始日期：** YYYY-MM-DD
- **结束日期：** YYYY-MM-DD
- **Sprint 目标：** [目标描述]
- **总故事点：** XX

## Story 列表

| ID | Story | 故事点 | 负责人 | 状态 |
|----|-------|--------|--------|------|
| US-001 | 用户登录 | 3 | Dev | 待开始 |
| US-002 | 用户注册 | 5 | Dev | 待开始 |

## 风险项
- [风险描述] - [应对措施]
```

### 4. 交付给 Scrum Master

Sprint Backlog 确定后，通知 Scrum Master：

```json
sessions_send({
  "sessionKey": "agent:scrum-master:main",
  "message": "Sprint XX Backlog 已准备好，请启动 Sprint..."
})
```

## 输出位置

```
workspace-po/backlog/sprint-backlog/sprint-XX.md
```

## 注意事项

- 每个 Sprint 保持专注，不要贪多
- 预留 10-20% 缓冲时间
- 记录未入选的原因，方便后续回顾
