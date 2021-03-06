---
title: 机器学习实践--【第1章】机器学习基础
categories:
 - deliberate-practice
tags:
 - python
 - machine learning
---

## 关键术语

- 专家系统
- 特征
- 分类
- 训练集/训练数据
- 训练样本
- 目标变量
- 类别
- 测试数据/测试集
- 知识表示

## 主要任务

- 监督学习

>分类和回归属于监督学习，之所以称之为监督学习，是因为这类算法必须知道预测什么，即目标变量的分类信息。

1. k-临近算法——线性回归

2. 朴素贝叶斯算法——局部加权线性回归

3. 支持向量机——Ridge回归

4. 决策树——Lasso最小回归系数估计

- 无监督学习

>与监督学习相对应的是无监督学习，此时数据没有类别信息，也不会给定目标值。

1. K-均值——最大期望算法

2. DBSCAN——Parzen窗设计

- 聚类

>在无监督学习中，将数据集合分成由类似的对象组成的多个类的过程被称为聚类。

- 密度估计

>在无监督学习中，将寻找描述数据统计值的过程称之为密度估计。

## 如何选择合适的算法

- 使用机器学习算法的目的

1. 预测值？监督学习：无监督学习；

2. 确定目标变量类型。

>if(监督学习)：离散型？分类：回归。
> else if(无监督学习)：需要划分为离散组？聚类：密度估计。

- 考虑数据问题

1. 特征值是离散型变量还是连续型变量

2. 特征值中是否存在**缺失的值**，原因？  

3. 特征值中是否存在**异常值**，原因？

4. 某个特征发生的**频率**

5. ……

## 开发步骤

1. 收集数据

2. 准备输入数据

3. **分析输入数据**（p9）

4. 训练算法

5. 测试算法

6. 使用算法

## NumPy函数库基础

- 将NumPy函数库中所有模块引入当前命名空间

`>>> from numpy import *`

- 随机生成一个4X4的array

`>>> random.rand(4, 4)`

- array转换为matrix

`>>> randMat = mat(random.rand(4, 4))`

- matrix求逆

`>>> randMat.I`

- 生成4X4的单位矩阵

`>>> eye(4)`