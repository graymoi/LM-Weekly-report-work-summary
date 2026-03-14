# 文件夹管理 Skill

## 概述

自动化文件夹结构检查、命名规范验证和常见问题修复，确保文件夹结构的一致性和规范性。

---

## 核心功能

### 1. 文件夹结构检查
- 检查文件夹是否存在
- 检查文件夹结构是否符合规范
- 检查文件夹命名是否符合规范
- 生成文件夹结构报告

### 2. 命名规范验证
- 检查文件夹名称中是否包含非法字符
- 检查文件夹名称是否符合命名约定
- 提供命名建议
- 自动重命名不符合规范的文件夹

### 3. 常见问题修复
- 修复文件夹命名问题
- 修复文件夹结构问题
- 修复文件夹嵌套问题
- 生成修复报告

### 4. 自动化检查
- 定期检查文件夹结构
- 自动修复常见问题
- 生成检查报告
- 发送预警通知

---

## 触发条件

### 显式触发

- "检查文件夹"、"检查文件夹结构"
- "整理文件夹"、"文件夹整理"
- "验证文件夹命名"、"命名规范检查"
- "修复文件夹"、"修复文件夹结构"

### 自动触发

- Git 提交前（pre-commit hook）
- 定期检查（cron job）
- 检测到文件夹结构变化

---

## 工作流程

```
文件夹结构检查
  ↓
  ├── 检查文件夹是否存在
  ├── 检查文件夹结构
  ├── 检查文件夹命名
  └── 生成检查报告
  ↓
命名规范验证
  ↓
  ├── 检查非法字符
  ├── 检查命名约定
  ├── 提供命名建议
  └── 自动重命名
  ↓
常见问题修复
  ↓
  ├── 修复命名问题
  ├── 修复结构问题
  ├── 修复嵌套问题
  └── 生成修复报告
  ↓
输出结果
```

---

## 文件夹命名规范

### 禁止使用的字符

| 字符 | 说明 | 替代方案 |
|------|------|---------|
| `/` | 斜杠（路径分隔符） | 使用 `-` 或 `_` |
| `\` | 反斜杠（路径分隔符） | 使用 `-` 或 `_` |
| `:` | 冒号 | 使用 `-` 或 `_` |
| `*` | 星号 | 使用 `-` 或 `_` |
| `?` | 问号 | 使用 `-` 或 `_` |
| `"` | 双引号 | 使用单引号或不使用 |
| `<` | 小于号 | 使用 `-` 或 `_` |
| `>` | 大于号 | 使用 `-` 或 `_` |
| `|` | 竖线 | 使用 `-` 或 `_` |

### 推荐的命名方式

| 类型 | 示例 | 说明 |
|------|------|------|
| 中文 | `技能发现` | 使用中文，清晰易懂 |
| 英文 | `SkillDiscovery` | 使用英文，符合编程规范 |
| 混合 | `技能发现_SkillDiscovery` | 中英文混合，便于理解 |
| 下划线 | `技能发现` | 使用下划线代替特殊字符 |
| 连字符 | `技能发现` | 使用连字符代替特殊字符 |

### 命名约定

1. **使用有意义的名称**: 文件夹名称应该清晰表达其用途
2. **避免特殊字符**: 不要使用 `/`, `\`, `:`, `*`, `?`, `"`, `<`, `>`, `|`
3. **使用一致的命名风格**: 选择一种命名风格并保持一致
4. **避免过长的名称**: 文件夹名称不宜过长（建议不超过 20 个字符）

---

## 常见问题

### 1. 文件夹名称包含非法字符

**问题描述**: 文件夹名称中包含 `/`, `\`, `:`, `*`, `?`, `"`, `<`, `>`, `|` 等非法字符

**示例**:
```
A/B测试/        ❌ 包含 /
技能:发现/      ❌ 包含 :
技能*发现/      ❌ 包含 *
```

**修复方案**:
```
AB测试/         ✅ 使用 AB 代替 A/B
技能发现/       ✅ 移除 :
技能发现/       ✅ 移除 *
```

### 2. 文件夹结构不一致

**问题描述**: 文件夹结构不一致，部分文件夹有子文件夹，部分没有

**示例**:
```
.trae\skills\
├── 技能发现\
│   └── SKILL.md
├── 技能评估\
│   └── SKILL.md
└── 技能生成\      ❌ 缺少 SKILL.md
```

**修复方案**:
```
.trae\skills\
├── 技能发现\
│   └── SKILL.md
├── 技能评估\
│   └── SKILL.md
└── 技能生成\      ✅ 添加 SKILL.md
    └── SKILL.md
```

### 3. 文件夹嵌套过深

**问题描述**: 文件夹嵌套过深，影响可读性和维护性

**示例**:
```
.trae\skills\
└── A\
    └── B测试\
        └── SKILL.md    ❌ 嵌套过深
```

**修复方案**:
```
.trae\skills\
└── AB测试\
    └── SKILL.md        ✅ 减少嵌套层级
```

---

## 输出格式

### 检查报告模板

```markdown
# 文件夹结构检查报告

生成时间: YYYY-MM-DD HH:MM:SS

---

## 检查结果

### ✅ 正常的文件夹

- 文件夹1
- 文件夹2
- ...

### ❌ 需要修复的文件夹

| 文件夹 | 问题 | 修复建议 |
|--------|------|---------|
| 文件夹1 | 问题描述 | 修复建议 |
| 文件夹2 | 问题描述 | 修复建议 |

---

## 修复建议

### 自动修复

- 文件夹1: 自动修复
- 文件夹2: 自动修复

### 手动修复

- 文件夹3: 需要手动修复
  - 原因: ...
  - 步骤: ...

---

## 总结

- 正常文件夹: X 个
- 需要修复的文件夹: Y 个
- 可以自动修复: Z 个
- 需要手动修复: W 个
```

### 修复报告模板

```markdown
# 文件夹结构修复报告

生成时间: YYYY-MM-DD HH:MM:SS

---

## 修复结果

### ✅ 自动修复成功

| 文件夹 | 修复前 | 修复后 |
|--------|--------|--------|
| 文件夹1 | 修复前名称 | 修复后名称 |

### ❌ 修复失败

| 文件夹 | 失败原因 | 建议 |
|--------|---------|------|
| 文件夹1 | 失败原因 | 建议 |

---

## 总结

- 成功修复: X 个
- 修复失败: Y 个
- 需要手动修复: Z 个
```

---

## PowerShell 脚本

### 检查文件夹结构

```powershell
# 检查文件夹结构
function Check-FolderStructure {
    param (
        [string]$Path
    )

    $illegalChars = @('/', '\', ':', '*', '?', '"', '<', '>', '|')
    $folders = Get-ChildItem -Path $Path -Directory

    $report = @{
        NormalFolders = @()
        ProblemFolders = @()
    }

    foreach ($folder in $folders) {
        $hasProblem = $false
        $problem = ""

        # 检查非法字符
        foreach ($char in $illegalChars) {
            if ($folder.Name -like "*$char*") {
                $hasProblem = $true
                $problem = "包含非法字符 '$char'"
                break
            }
        }

        # 检查嵌套过深
        $depth = ($folder.FullName -split '\\').Count - ($Path -split '\\').Count
        if ($depth -gt 2) {
            $hasProblem = $true
            $problem = "嵌套过深（深度: $depth）"
        }

        if ($hasProblem) {
            $report.ProblemFolders += @{
                Folder = $folder.Name
                Path = $folder.FullName
                Problem = $problem
            }
        } else {
            $report.NormalFolders += $folder.Name
        }
    }

    return $report
}

# 使用示例
$report = Check-FolderStructure -Path ".trae\skills"
Write-Host "正常的文件夹: $($report.NormalFolders.Count)"
Write-Host "有问题的文件夹: $($report.ProblemFolders.Count)"
```

### 自动修复文件夹命名

```powershell
# 自动修复文件夹命名
function Repair-FolderNaming {
    param (
        [string]$Path
    )

    $illegalChars = @('/', '\', ':', '*', '?', '"', '<', '>', '|')
    $folders = Get-ChildItem -Path $Path -Directory -Recurse

    $report = @{
        RepairedFolders = @()
        FailedFolders = @()
    }

    foreach ($folder in $folders) {
        $newName = $folder.Name
        $hasIllegalChar = $false

        # 替换非法字符
        foreach ($char in $illegalChars) {
            if ($newName -like "*$char*") {
                $hasIllegalChar = $true
                $newName = $newName -replace [regex]::Escape($char), '_'
            }
        }

        if ($hasIllegalChar) {
            try {
                $newPath = Join-Path -Path $folder.Parent.FullName -ChildPath $newName
                Rename-Item -Path $folder.FullName -NewName $newName -ErrorAction Stop

                $report.RepairedFolders += @{
                    OldName = $folder.Name
                    NewName = $newName
                    OldPath = $folder.FullName
                    NewPath = $newPath
                }
            } catch {
                $report.FailedFolders += @{
                    Folder = $folder.Name
                    Path = $folder.FullName
                    Error = $_.Exception.Message
                }
            }
        }
    }

    return $report
}

# 使用示例
$report = Repair-FolderNaming -Path ".trae\skills"
Write-Host "成功修复: $($report.RepairedFolders.Count)"
Write-Host "修复失败: $($report.FailedFolders.Count)"
```

---

## Git 集成

### Pre-commit Hook

```bash
#!/bin/bash
# .git/hooks/pre-commit

# 检查文件夹命名规范
echo "检查文件夹命名规范..."

# 检查 .trae/skills 文件夹
illegal_chars='[/\\:*?"<>|]'
if find .trae/skills -type d -name "[$illegal_chars]" 2>/dev/null | grep -q .; then
    echo "错误: 发现包含非法字符的文件夹名称"
    echo "非法字符: /, \\, :, *, ?, \", <, >, |"
    exit 1
fi

echo "✅ 文件夹命名规范检查通过"
exit 0
```

### Post-commit Hook

```bash
#!/bin/bash
# .git/hooks/post-commit

# 生成文件夹结构报告
echo "生成文件夹结构报告..."

# 运行检查脚本
powershell.exe -File ".trae\scripts\check-folder-structure.ps1"

echo "✅ 文件夹结构报告已生成"
exit 0
```

---

## 使用示例

### 检查文件夹结构

```
用户: 检查文件夹结构

AI: 正在检查文件夹结构...

✅ 正常的文件夹: 12 个
❌ 有问题的文件夹: 1 个

问题详情:
- A/B测试/: 包含非法字符 '/'

修复建议:
- 重命名为: AB测试/

是否自动修复？(y/n)
```

### 修复文件夹命名

```
用户: 修复文件夹命名

AI: 正在修复文件夹命名...

✅ 成功修复: 1 个
- A/B测试/ → AB测试/

❌ 修复失败: 0 个

修复完成！
```

---

## 注意事项

1. **备份重要数据**: 在修复文件夹命名前，先备份重要数据
2. **测试修复脚本**: 在正式使用前，先在测试环境中测试修复脚本
3. **逐步修复**: 对于大量文件夹，建议逐步修复，避免一次性修复太多
4. **验证修复结果**: 修复后，验证文件夹结构是否正确
5. **更新相关引用**: 修复文件夹命名后，更新所有相关的引用

---

## 相关文档

- [Git 工作流](.trae\docs\Git工作流.md)
- [优化评估标准](.trae\docs\优化评估标准.md)
- [技能发现报告](输出成果\技能发现报告_文件夹整理.md)

---

*版本: 1.0*
*创建日期: 2026-03-07*
*适用范围: 文件夹管理*
