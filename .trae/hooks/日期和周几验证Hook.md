---
name: 日期和周几验证Hook
description: |
  在生成工作总结时自动验证日期和周几的对应关系。
author: Claude Code
version: 1.0.0
date: 2026-03-08
---

# 日期和周几验证Hook

## Hook目的

在生成工作总结时自动验证日期和周几的对应关系，防止日期和周几错误。

## 触发条件

- 生成工作总结时
- 修改工作总结时
- 检查工作总结时

## Hook内容

### 1. 触发时机

#### 时机1：生成工作总结前
- 检查工作总结的日期范围
- 确认日期和周几的对应关系

#### 时机2：生成工作总结时
- 使用JavaScript Date对象计算日期对应的周几
- 验证计算结果与对应关系表是否一致
- 如果不一致，立即停止并检查

#### 时机3：生成工作总结后
- 逐行检查工作总结中的日期和周几
- 确保所有日期和周几的对应关系正确
- 如果发现错误，立即修正

### 2. 验证逻辑

#### 逻辑1：日期和周几对应关系验证

```javascript
// 日期和周几验证函数
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

#### 逻辑2：工作总结日期范围验证

```javascript
// 工作总结日期范围验证函数
function validateDateRange(startDate, endDate) {
  const start = new Date(startDate.year, startDate.month - 1, startDate.day);
  const end = new Date(endDate.year, endDate.month - 1, endDate.day);

  if (start > end) {
    console.error(`❌ 日期范围无效！`);
    console.error(`  开始日期: ${startDate.year}年${startDate.month}月${startDate.day}日`);
    console.error(`  结束日期: ${endDate.year}年${endDate.month}月${endDate.day}日`);
    return false;
  }

  console.log(`✅ 日期范围有效: ${startDate.year}年${startDate.month}月${startDate.day}日 - ${endDate.year}年${endDate.month}月${endDate.day}日`);
  return true;
}
```

#### 逻辑3：工作总结内容验证

```javascript
// 工作总结内容验证函数
function validateContent(content, dateWeekdayMap) {
  const errors = [];

  // 查找所有日期和周几的匹配
  const regex = /周[一二三四五六日][（(](\d+)月(\d+)日[）)]/g;
  let match;

  while ((match = regex.exec(content)) !== null) {
    const weekday = match[0].substring(0, 2);
    const month = parseInt(match[1]);
    const day = parseInt(match[2]);

    const key = `${month}月${day}日`;
    const expectedWeekday = dateWeekdayMap[key];

    if (expectedWeekday !== weekday) {
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

### 3. 验证流程

#### 流程1：生成工作总结前

1. 检查工作总结的日期范围
2. 确认日期和周几的对应关系
3. 如果日期范围无效，停止生成

#### 流程2：生成工作总结时

1. 使用JavaScript Date对象计算日期对应的周几
2. 验证计算结果与对应关系表是否一致
3. 如果不一致，立即停止并检查

#### 流程3：生成工作总结后

1. 逐行检查工作总结中的日期和周几
2. 确保所有日期和周几的对应关系正确
3. 如果发现错误，立即修正

### 4. 错误处理

#### 错误1：日期和周几不匹配

**错误信息**：
```
❌ 日期和周几不匹配！
  日期: 2026年3月2日
  预期周几: 周一
  实际周几: 周日
```

**处理步骤**：
1. 立即停止生成
2. 检查日期和周几的对应关系
3. 修正错误
4. 重新验证

#### 错误2：日期范围无效

**错误信息**：
```
❌ 日期范围无效！
  开始日期: 2026年3月8日
  结束日期: 2026年3月2日
```

**处理步骤**：
1. 立即停止生成
2. 检查日期范围
3. 修正日期范围
4. 重新验证

#### 错误3：工作总结内容有错误

**错误信息**：
```
❌ 发现1处日期和周几不匹配！
  周一（3月2日）
    预期: 周日
    实际: 周一
```

**处理步骤**：
1. 立即停止生成
2. 检查工作总结内容
3. 修正错误
4. 重新验证

## 使用说明

### 何时使用

- 生成工作总结时
- 修改工作总结时
- 检查工作总结时

### 如何使用

1. Hook自动触发
2. 按照验证流程执行
3. 发现错误时按照错误处理步骤处理
4. 验证通过后继续生成

## 注意事项

### 1. JavaScript Date对象注意事项

- **月份从0开始**：0=1月，1=2月，...，11=12月
- **getDay()返回值**：0=周日，1=周一，...，6=周六
- **时区问题**：JavaScript Date对象使用本地时区

### 2. 验证时机

- **生成前**：验证日期范围
- **生成时**：验证日期和周几对应关系
- **生成后**：验证工作总结内容

### 3. 错误处理

- **立即停止**：发现错误时立即停止生成
- **查找原因**：检查是文件名错误、内容错误，还是计算错误
- **修正错误**：根据正确信息修正错误
- **重新验证**：修正后重新验证所有日期和周几

## 版本历史

- **v1.0.0** (2026-03-08): 初始版本
