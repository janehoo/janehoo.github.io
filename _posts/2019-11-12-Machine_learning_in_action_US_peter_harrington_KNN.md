---
title: 机器学习实践--【第2章】k-近邻算法(KNN)
categories:
 - deliberate-practice
tags:
 - python
 - machine learning
---

## 工作原理
>存在一个样本数据集合，也称作训练样本集，并且样本集中每个数据都存在标签，即我们知道样本集中每一数据与所属分类的对应关系。输入没有标签的新数据后，将新数据的每个特征与样本集中数据对应的特征进行比较，然后算法提取样本集中特征最相似数据(最近邻)的分类标签。一般来说，我们只选择样本数据集中前k个最相似的数据，这就是k-近邻算法中k的出处，通常k是不大于20的整数。 最后，选择k个最相似数据中出现次数最多的分类，作为新数据的分类。

简言之，所谓K近邻算法，即是给定一个训练数据集，对新的输入实例，在训练数据集中找到与该实例最邻近的K个实例（也就是上面所说的K个邻居）， 这K个实例的多数属于某个类，就把该输入实例分类到这个类中。

>优点:精度高、对异常值不敏感、无数据输入假定。
> 
>缺点:计算复杂度高、空间复杂度高。 
>
>适用数据范围:数值型和标称型。

## 实例
>(1) 收集数据:可以使用任何方法。
>
>(2) 准备数据:距离计算所需要的数值，最好是结构化的数据格式。
>
>(3) 分析数据:可以使用任何方法。
>
>(4) 训练算法:此步骤不适用于k-近邻算法。
>
>(5) 测试算法:计算错误率。
>
>(6) 使用算法:首先需要输入样本数据和结构化的输出结果，然后运行k-近邻算法判定输
入数据分别属于哪个分类，最后应用对计算出的分类执行后续的处理。

### 导入数据
### 实施kNN算法
伪代码：
```
对未知类别属性的数据集中的每个点依次执行以下操作: 
(1) 计算已知类别数据集中的点与当前点之间的距离;
(2) 按照距离递增次序排序;
(3) 选取与当前点距离最小的k个点;
(4) 确定前k个点所在类别的出现频率;
(5) 返回前k个点出现频率最高的类别作为当前点的预测分类。
```
kNN.py 代码如下：

```python
from numpy import *
import operator


def createDataSet():
    '创建数据集和标签'
    group = array([[1.0, 1.1], [1.0, 1.0], [0, 0], [0, 0.1]])
    labels = ['A', 'A', 'B', 'B']
    return group, labels


def classify0(inX, group, labels, k):
    '分类算法：k-近邻算法'
    # 距离计算
    dataSetSize = group.shape[0]
    diffMat = tile(inX, (dataSetSize, 1)) - group
    sqDiffMat = diffMat ** 2
    sqDistances = sqDiffMat.sum(axis=1)
    distances = sqDistances ** 0.5
    # 距离排序
    sortedDistIndicies = distances.argsort()
    ## argsort(),返回排序后的元素角标
    classCount = {}
    ## classCount用于存储前k个近邻中各种类别分别对应的数量
    for i in range(k):
        voteIlabel = labels[sortedDistIndicies[i]]
        classCount[voteIlabel] = classCount.get(voteIlabel, 0) + 1
    sortedClassCount = sorted(classCount.items(), key=operator.itemgetter(1), reverse=True)

    return sortedClassCount[0][0]
```
执行过程及结果：

```python
>>> group, labels = kNN.createDataSet()
>>> group
array([[1. , 1.1],
       [1. , 1. ],
       [0. , 0. ],
       [0. , 0.1]])
>>> labels
['A', 'A', 'B', 'B']
>>> kNN.classify0([0,0], group, labels, 3)
'B'
```

## 练习中遇到的问题
- 错误提示：`ModuleNotFoundError: No module named 'numpy'`

>解决办法：安装`numpy`
>
>在shell中执行：`python3 -m pip install numpy`

- numpy.tile函数

>[点击查看：python numpy-tile函数](https://www.jianshu.com/p/4b74a367833c)

- 错误提示：`AttributeError: 'dict' object has no attribute 'iteritems'`

>原因：python3中`dict`的`iteritems`方法被`items`替代