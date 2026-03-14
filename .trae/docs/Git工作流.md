# Git 初始化脚本

## 概述

此脚本用于初始化 Git 仓库，配置分支策略和提交规范。

---

## 快速开始

### 1. 初始化 Git 仓库

```powershell
# 在项目根目录执行
git init
```

### 2. 添加所有文件

```powershell
git add .
```

### 3. 首次提交

```powershell
git commit -m "chore: 初始化项目，添加基础配置和 Skills"
```

### 4. 创建主分支

```powershell
git branch -M main
```

### 5. 添加远程仓库（可选）

```powershell
git remote add origin <你的远程仓库地址>
git push -u origin main
```

---

## 分支策略

### 主分支

```
main - 稳定版本，生产环境使用
```

### 优化分支

```
optimize/规则优化 - 规则优化实验
optimize/skills优化 - Skills 优化实验
optimize/钩子优化 - 钩子优化实验
optimize/全面优化 - 全面优化实验
```

### 功能分支

```
feature/新功能名称 - 新功能开发
```

### 修复分支

```
fix/问题描述 - 问题修复
```

---

## 提交规范

### 提交格式

```
[类型] 简短描述

详细描述（可选）
```

### 提交类型

| 类型 | 说明 | 示例 |
|------|------|------|
| `chore` | 构建/工具/配置变更 | `chore: 更新 .gitignore` |
| `feat` | 新功能 | `feat: 添加深度研究 Skill` |
| `fix` | 问题修复 | `fix: 修复日工作记录触发问题` |
| `docs` | 文档更新 | `docs: 更新 CLAUDE.md` |
| `style` | 代码格式（不影响功能） | `style: 格式化代码` |
| `refactor` | 重构（不是新功能也不是修复） | `refactor: 优化规则匹配逻辑` |
| `perf` | 性能优化 | `perf: 优化 Skills 执行速度` |
| `test` | 测试相关 | `test: 添加优化测试` |
| `optimize` | 优化相关 | `optimize: 优化规则使用率` |

### 提交示例

```powershell
# 新增 Skill
git commit -m "feat: 添加自我优化 Skill"

# 优化规则
git commit -m "optimize: 优化日工作记录触发词"

# 修复问题
git commit -m "fix: 修复新闻监测去重问题"

# 更新文档
git commit -m "docs: 更新优化评估标准"
```

---

## 优化工作流

### 1. 创建优化分支

```powershell
# 规则优化
git checkout -b optimize/规则优化

# Skills 优化
git checkout -b optimize/skills优化

# 钩子优化
git checkout -b optimize/钩子优化

# 全面优化
git checkout -b optimize/全面优化
```

### 2. 应用优化

```powershell
# 修改相应文件
# ...

# 查看变更
git status

# 添加变更
git add .

# 提交变更
git commit -m "optimize: 优化日工作记录触发词"
```

### 3. 推送分支

```powershell
git push -u origin optimize/规则优化
```

### 4. 创建 Pull Request

```powershell
# 在 Git 平台（GitHub/GitLab）创建 PR
# 从 optimize/规则优化 合并到 main
```

### 5. 审核和合并

```powershell
# 人工审核
# 确认优化效果

# 合并到主分支
git checkout main
git merge optimize/规则优化

# 推送
git push origin main

# 删除优化分支
git branch -d optimize/规则优化
git push origin --delete optimize/规则优化
```

---

## 常用 Git 命令

### 查看状态

```powershell
git status
```

### 查看日志

```powershell
# 简洁日志
git log --oneline

# 详细日志
git log

# 图形化日志
git log --graph --oneline --all
```

### 查看差异

```powershell
# 查看未暂存的变更
git diff

# 查看已暂存的变更
git diff --staged

# 查看两个提交的差异
git diff <commit1> <commit2>
```

### 撤销操作

```powershell
# 撤销未暂存的变更
git checkout -- <file>

# 撤销已暂存的变更
git reset HEAD <file>

# 撤销最后一次提交（保留变更）
git reset --soft HEAD~1

# 撤销最后一次提交（丢弃变更）
git reset --hard HEAD~1

# 回滚到指定提交
git reset --hard <commit>
```

### 分支操作

```powershell
# 查看所有分支
git branch -a

# 创建新分支
git branch <branch-name>

# 切换分支
git checkout <branch-name>

# 创建并切换分支
git checkout -b <branch-name>

# 删除本地分支
git branch -d <branch-name>

# 删除远程分支
git push origin --delete <branch-name>
```

### 标签操作

```powershell
# 创建标签
git tag -a v1.0 -m "版本 1.0"

# 查看标签
git tag

# 推送标签
git push origin v1.0

# 推送所有标签
git push origin --tags
```

---

## Git 配置

### 用户配置

```powershell
# 设置用户名
git config --global user.name "你的名字"

# 设置邮箱
git config --global user.email "你的邮箱"
```

### 别名配置

```powershell
# 简化提交命令
git config --global alias.ci "commit"
git config --global alias.st "status"
git config --global alias.co "checkout"
git config --global alias.br "branch"
git config --global alias.lg "log --graph --oneline --all"
```

### 配置示例

```powershell
# 查看配置
git config --list

# 编辑配置
git config --global --edit
```

---

## 最佳实践

### 1. 提交频率

- **小步快跑**: 频繁提交，每次提交一个逻辑单元
- **原子提交**: 每次提交只做一件事
- **清晰描述**: 提交信息要清晰描述做了什么

### 2. 分支管理

- **主分支稳定**: main 分支始终保持稳定
- **分支隔离**: 每个功能/优化在独立分支进行
- **及时清理**: 合并后及时删除分支

### 3. 代码审查

- **PR 审查**: 所有合并都通过 PR
- **自动化测试**: 合并前必须通过测试
- **人工审核**: 重要变更需要人工审核

### 4. 版本管理

- **语义化版本**: 使用语义化版本号（v1.0.0）
- **标签管理**: 重要版本打标签
- **变更日志**: 维护 CHANGELOG.md

---

## 故障排除

### 问题1：.gitignore 不生效

```powershell
# 清除缓存
git rm -r --cached .

# 重新添加
git add .
git commit -m "fix: 修复 .gitignore"
```

### 问题2：换行符问题

```powershell
# 配置 Git 自动转换
git config --global core.autocrlf true

# 查看换行符
git ls-files --eol
```

### 问题3：合并冲突

```powershell
# 查看冲突文件
git status

# 手动解决冲突
# 编辑冲突文件，标记冲突解决

# 添加解决后的文件
git add <file>

# 继续合并
git commit
```

---

## 相关文档

- **自我优化 Skill**: `.trae\skills\自我优化\SKILL.md`
- **优化评估标准**: `.trae\docs\优化评估标准.md`
- **Git 配置**: `.gitignore`, `.gitattributes`
- **项目规则**: `.trae\rules\project_rules.md`

---

*版本: 1.0*
*创建日期: 2026-03-07*
*适用范围: Git 初始化和工作流*
