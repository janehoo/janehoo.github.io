---
title: Python刻意练习---Task10：类与对象（2day）
categories:
 - deliberate-practice
tags:
 - python
---
## 对象 < object >

`对象 = 属性 + 方法`
- 类名约定以大写字母开头

## 面向对象的特征

- 封装
- 继承
- 多态

## 封装

### self是什么

### python的魔法方法：`__init__`

### 公有和私有
- 在python中定义私有变量只需要在变量名或函数名前加上`__`（双下划线）。

## 继承

A类继承自B类
```
class A(B):
    pass
```

如果子类中定义与父类同名的方法或属性，则会自动覆盖父类对应的方法或属性。

想要在子类中继承父类方法，可以在重写父类方法时：
1. 调用未绑定的父类方法
2. 使用super函数

## 多重继承

A类继承B、C、D类
```
class A(B, C, D):
    pass
```

## 组合
把多个类的实例化放到一个新类里面得到一个组合。

## Mixin

## 类、类对象和实例对象
```python
class A:
    def methondA():
        #do something

A.methondA()

a = A()
a.methondA()
```
其中，class A中，A为类名；

A.methondA()中，A为类对象；

a为实例对象。

注意：若类定义中，属性名和方法名相同，则属性名覆盖方法名。

## 什么是绑定？
python严格要求方法需要有实例才能被调用这种限制，即为绑定。