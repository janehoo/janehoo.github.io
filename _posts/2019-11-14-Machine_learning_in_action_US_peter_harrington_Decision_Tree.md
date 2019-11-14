---
title: 机器学习实践--【第3章】决策树
date: 2019-11-14 11:33:26
categories:
 - deliberate-practice
tags:
 - python
 - machine learning
---
## 构建决策树

感觉下面的翻译有些问题，但是有不知道怎么
>在构造决策树时，我们需要解决的第一个问题就是，当前数据集上哪个特征在划分数据分类时起决定性作用。为了找到决定性的特征，划分出最好的结果，我们必须评估每个特征。完成测试之后，原始数据集就被划分为几个数据子集。这些数据子集会分布在第一个决策点的所有分支上。如果某个分支下的数据属于同一类型，则当前分支已经正确地划分数据分类，无需进一步对数据集进行分割。如果数据子集内的数据不属于同一类型，则需要重复划分数据子集的过程。如何划分数据子集的算法和划分原始数据集的方法相同，直到所有具有相同类型的数据均在一个数据子集内。

### 创建分支
`createBranch()`伪代码：

```
检测数据集中的每个子项是否属于同一分类: 
If so return 类标签;
Else
      寻找划分数据集的最好特征
      划分数据集
      创建分支节点
for 每个划分的子集调用函数createBranch并增加返回结果到分支节点中
return 分支节点
```
### 划分数据集

- 原则：将无序的数据变得更加有序。
- 信息增益：英文：information gain，在划分数据集之前之后信息发生的变化称为信息增益。**获得信息增益最高的特征就是最好的选择。**
- 香农熵/熵：英文：entropy，一种集合信息的度量方式，**香农熵/熵**，即**信息的期望值。**（另一种度量集合无序程度的方法是**基尼不纯度**）
- 信息的定义：
<img src="http://chart.googleapis.com/chart?cht=tx&chl= l\left ( x_{i} \right )=- \log _{2} p\left ( x_{i} \right )" style="border:none;">
- 熵的计算：
<img src="http://chart.googleapis.com/chart?cht=tx&chl=H=-\sum_{i=1}^{n} \log _{2}p\left ( x_{i} \right )" style="border:none;">

其中，n是分类的数目。

#### 计算给定数据集的香农熵
 ```python
from math import log

def calcShannonEnt(dataSet):
    '计算给定数据集的香农熵'
    numEntries = len(dataSet)   #返回数据集的长度
    labelCounts = {}    #定义 类别：数量 字典
    for featVec in dataSet:
        currentLabel = featVec[-1]  #这里，选择数据最后一位元素作为目标特征
        if currentLabel not in labelCounts.keys():
            labelCounts[currentLabel] = 0
        labelCounts[currentLabel] += 1
    shannonEnt = 0.0
    for key in labelCounts:
        prob = float(labelCounts[key])/numEntries
        shannonEnt -= prob * log(prob, 2)
    return shannonEnt
 ```
 执行结果
 ```python
>>> import trees
>>> myDat,labels=trees.createDataSet()
>>> myDat
[[1, 1, 'yes'], [1, 1, 'yes'], [1, 0, 'no'], [0, 1, 'no'], [0, 1, 'no']]
>>> trees.calcShannonEnt(myDat)
0.9709505944546686
 ```

#### 划分数据集
 ```python
def splitDataSet(dataSet, axis, value):
    '划分数据集：返回数据集中数据第axis元素为value的新数据集,新数据集中不包含原数据集中第axis元素'
    retDataSet = []
    for featVec in dataSet:
        if featVec[axis] == value:
            reduceFeatVec = featVec[:axis]
            reduceFeatVec.extend(featVec[axis+1:])
            retDataSet.append(reduceFeatVec)
    return retDataSet
 ```
 执行结果：
 ```python
>>> import imp
>>> imp.reload(trees)
<module 'trees' from '/Users/janehoo/work/python/trees.py'>
>>> myDat, labels = trees.createDataSet()
>>> trees.splitDataSet(myDat, 0, 1)
[[1, 'yes'], [1, 'yes'], [0, 'no']]
 ```
#### 找到最好的特征划分方式
```python
def chooseBestFeatureToSplit(dataSet):
    numFeatures = len(dataSet[0]) - 1
    baseEntropy = calcShannonEnt(dataSet)
    bestInfoGain = 0.0
    bestFeature = -1
    for i in range(numFeatures):
        featList = [example[i] for example in dataSet]  #保存原数据集第i个元素组成的新集合，用于后续循环
        uniqueVals = set(featList)
        newEntropy = 0.0
        for value in uniqueVals:
            subDataSet = splitDataSet(dataSet, i, value)
            prob = len(subDataSet)/float(len(dataSet))
            newEntropy += prob * calcShannonEnt(subDataSet)
        infoGain = baseEntropy - newEntropy
        if (infoGain > bestInfoGain):
            bestInfoGain = infoGain
            bestFeature = i
    return bestFeature
```
#### 构建决策树


## 练习遇到的问题
