---
title: Python刻意练习---Task08：异常处理（1day）
categories:
 - deliberate-practice
tags:
 - python
---
## 异常
### 有哪些常见的异常？
### 异常处理
- try-except语句

```python
try:
    检测范围
except Exception[as reason]:
    出现异常后的处理代码
```

- try-finally语句

```python
try:
    检测范围
except Exception[as reason]:
    出现异常后的处理代码
finally:
    无论如何都会执行的代码
```

- raise语句

```python
raise Exception('message')
```
