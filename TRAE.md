# TRAE.md

## Trae IDE 配置

### 工作区配置

- **工作区名称**: 打杂工具箱
- **工作区路径**: d:\LMAI\000打杂工具箱
- **项目类型**: AI辅助工作流

### 核心规则文件

| 文件 | 路径 | 说明 |
|------|------|------|
| AGENTS.md | / | 智能体定义和角色配置 |
| CLAUDE.md | / | 项目概述和工作流 |
| CLAUDE.local.md | / | 本地特定配置 |
| project_rules.md | .trae/rules/ | 项目级规则 |
| personal_rules.md | .trae/rules/ | 个人级规则 |

### 自动加载文件

以下文件会自动加载到上下文中：

1. **AGENTS.md** - 智能体定义
2. **CLAUDE.md** - 项目配置
3. **CLAUDE.local.md** - 本地配置
4. **.trae/rules/project_rules.md** - 项目规则
5. **.trae/rules/personal_rules.md** - 个人规则

### 文件监控

Trae IDE 会自动监控以下文件的变化：
- 根目录下的 `*.md` 文件
- `.trae/rules/` 目录下的所有文件
- `.trae/skills/` 目录下的所有文件

当这些文件发生变化时，会自动重新加载到上下文中。

### 技能系统

项目使用以下技能：
- **日工作记录** - `.trae/skills/日工作记录/SKILL.md`
- **周工作总结** - `.trae/skills/周工作总结/SKILL.md`
- **新闻监测** - `.trae/skills/新闻监测/SKILL.md`

### 工作流

1. **每日工作**: 工作记录 → 日工作记录 → 日总结
2. **知识萃取**: 自动更新项目库和个人知识库
3. **周总结**: 收集一周素材 → 生成周总结 → 归档

---
*版本: 1.0*
*创建日期: 2026-03-07*
