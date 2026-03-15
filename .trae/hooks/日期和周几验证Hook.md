---
name: 日期和周几验证Hook
description: |
  在生成工作总结时自动验证日期和周几的对应关系，提供JavaScript验证工具。
author: Claude Code
version: 2.0.0
date: 2026-03-15
---

# 日期和周几验证Hook

## Hook目的

在生成工作总结时自动验证日期和周几的对应关系，防止日期和周几错误。

---

## 触发条件

| 触发场景 | 触发时机 |
|---------|---------|
| 生成工作总结 | 总结生成前、中、后 |
| 修改工作总结 | 内容修改时 |
| 检查工作总结 | 用户手动触发 |

---

## 执行逻辑

本Hook自动执行以下规则文件中定义的内容：

**规则文件**: [.trae\rules\日期和周几验证规则.md](file:///d:/LMAI/000打杂工具箱/.trae/rules/日期和周几验证规则.md)

### 验证流程

```
触发验证
    │
    ├── 生成前：验证日期范围
    │
    ├── 生成时：验证日期和周几对应关系
    │
    └── 生成后：逐行检查内容
```

---

## 验证工具（JavaScript）

### 1. 日期和周几验证函数

```javascript
function validateWeekday(year, month, day, expectedWeekday) {
  const weekdays = ['周日', '周一', '周二', '周三', '周四', '周五', '周六'];
  const d = new Date(year, month - 1, day);
  const actualWeekday = weekdays[d.getDay()];

  if (actualWeekday !== expectedWeekday) {
    console.error(`❌ 日期和周几不匹配！`);
    console.error(`  日期: ${year}年${month}月${day}日`);
    console.error(`  预期周几: ${expectedWeekday}`);
    console.error(`  实际周几: ${actualWeekday}`);
    return false;
  }

  console.log(`✅ ${year}年${month}月${day}日: ${actualWeekday}`);
  return true;
}
```

### 2. 日期范围验证函数

```javascript
function validateDateRange(startDate, endDate) {
  const start = new Date(startDate.year, startDate.month - 1, startDate.day);
  const end = new Date(endDate.year, endDate.month - 1, endDate.day);

  if (start > end) {
    console.error(`❌ 日期范围无效！`);
    console.error(`  开始日期: ${startDate.year}年${startDate.month}月${startDate.day}日`);
    console.error(`  结束日期: ${endDate.year}年${endDate.month}月${endDate.day}日`);
    return false;
  }

  console.log(`✅ 日期范围有效`);
  return true;
}
```

### 3. 工作总结内容验证函数

```javascript
function validateContent(content, dateWeekdayMap) {
  const errors = [];
  const regex = /周[一二三四五六日][（(](\d+)月(\d+)日[）)]/g;
  let match;

  while ((match = regex.exec(content)) !== null) {
    const weekday = match[0].substring(0, 2);
    const month = parseInt(match[1]);
    const day = parseInt(match[2]);

    const key = `${month}月${day}日`;
    const expectedWeekday = dateWeekdayMap[key];

    if (expectedWeekday && expectedWeekday !== weekday) {
      errors.push({
        text: match[0],
        expected: expectedWeekday,
        actual: weekday,
      });
    }
  }

  if (errors.length > 0) {
    console.error(`❌ 发现${errors.length}处日期和周几不匹配！`);
    errors.forEach(error => {
      console.error(`  ${error.text}`);
      console.error(`    预期: ${error.expected}`);
      console.error(`    实际: ${error.actual}`);
    });
    return false;
  }

  console.log(`✅ 工作总结内容验证通过`);
  return true;
}
```

### 4. 快速验证脚本

```javascript
// 验证指定日期
function quickValidate(year, month, day) {
  const weekdays = ['周日', '周一', '周二', '周三', '周四', '周五', '周六'];
  const d = new Date(year, month - 1, day);
  return weekdays[d.getDay()];
}

// 使用示例
console.log(quickValidate(2026, 3, 2));  // 输出: 周一
console.log(quickValidate(2026, 3, 8));  // 输出: 周日
```

---

## 错误处理

| 错误类型 | 错误信息 | 处理步骤 |
|---------|---------|---------|
| 日期周几不匹配 | `❌ 日期和周几不匹配！` | 停止 → 检查 → 修正 → 重验 |
| 日期范围无效 | `❌ 日期范围无效！` | 停止 → 检查范围 → 修正 → 重验 |
| 内容有错误 | `❌ 发现N处不匹配！` | 停止 → 检查内容 → 修正 → 重验 |

---

## 注意事项

### JavaScript Date对象

| 要点 | 说明 |
|------|------|
| 月份 | 从0开始（0=1月，11=12月） |
| getDay() | 0=周日，1=周一，...，6=周六 |
| 时区 | 使用本地时区 |

### 验证时机

| 时机 | 验证内容 |
|------|---------|
| 生成前 | 日期范围 |
| 生成时 | 日期和周几对应关系 |
| 生成后 | 工作总结内容 |

---

## 与规则文件的关系

```
规则文件（定义"做什么"）
    │
    ├── 规则目的
    ├── 日期周几对应表
    ├── 验证步骤
    ├── 常见错误
    └── 应急处理
         │
         ▼
Hook文件（定义"什么时候做" + "工具实现"）
    │
    ├── 触发条件
    ├── 验证流程
    ├── JavaScript工具 ←── 独特价值
    └── 错误处理
```

---

## 相关文档

- **规则文件**: [.trae\rules\日期和周几验证规则.md](file:///d:/LMAI/000打杂工具箱/.trae/rules/日期和周几验证规则.md)
- **时间处理Hook**: [.trae\hooks\时间信息处理.md](file:///d:/LMAI/000打杂工具箱/.trae/hooks/时间信息处理.md)

---

*版本: 2.0*
*创建日期: 2026-03-08*
*更新日期: 2026-03-15*
*更新内容: 重构为引用规则文件，保留JavaScript验证工具作为独特价值*
