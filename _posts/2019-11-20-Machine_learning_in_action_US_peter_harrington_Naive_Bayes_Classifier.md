---
title: 机器学习实践--【第4章】基于概率论的分类方法：朴素贝叶斯
date: 2019-11-20 16:05:26
categories:
 - deliberate-practice
tags:
 - python
 - machine learning
---
## 朴素贝叶斯

>优点:在数据较少的情况下仍然有效，可以处理多类别问题。 
>
>缺点:对于输入数据的准备方式较为敏感。 
>
>适用数据类型:标称型数据。

- 贝叶斯决策理论的核心思想，即选择具有最高概率的决策.因此，计算元素属于某分类的`条件概率`成为解决问题的关键。

- `条件概率`：事件A在另外一个事件B已经发生条件下的发生概率。表示为：`P(A|B)`。

- `贝叶斯准则`：

![](https://wikimedia.org/api/rest_v1/media/math/render/svg/87c061fe1c7430a5201eef3fa50f9d00eac78810)

## 使用朴素贝叶斯进行文档分类
- 朴素贝叶斯是贝叶斯分类器的一个扩展，是用于文档分类的常用算法。
- 朴素贝叶斯分类器中的另一个假设是，每个特征同等重要。

- 朴素贝叶斯的一般过程：
>(1) 收集数据:可以使用任何方法。本章使用RSS源。
>
>(2) 准备数据:需要数值型或者布尔型数据。
>
>(3) 分析数据:有大量特征时，绘制特征作用不大，此时使用直方图效果更好。
>
>(4) 训练算法:计算不同的独立特征的条件概率。
>
>(5) 测试算法:计算错误率。
>
>(6) 使用算法:一个常见的朴素贝叶斯应用是文档分类。可以在任意的分类场景中使用朴素贝叶斯分类器，不一定非要是文本。

### 1. 准备数据：从文本中构建向量
### 2. 训练算法：从词向量计算概率
伪代码：
```
计算每个类别中的文档数目
  对每篇训练文档:
对每个类别:
如果词条出现在文档中→ 增加该词条的计数值 增加所有词条的计数值
    对每个类别:
      对每个词条:
        将该词条的数目除以总词条数目得到条件概率
    返回每个类别的条件概率
```

```python
from numpy import *

def loadDataSet():
    '创建实验样本。 postingList：词条切分后的文档集合；classVec：类别标签集合'
    postingList = [['my', 'dog', 'has', 'flea', 'problems', 'help', 'please'],
                   ['maybe', 'not', 'take', 'him' 'to', 'dog', 'park', 'stupid'],
                   ['my', 'dalmation', 'is', 'so', 'cute', 'I', 'love', 'him'],
                   ['stop', 'posting', 'stupid', 'worthless', 'garbage'],
                   ['mr', 'licks', 'ate', 'my', 'steak', 'how', 'to', 'stop', 'him'],
                   ['quit', 'buying', 'worthless', 'dog', 'food', 'stupid']]
    classVec = [0,1,0,1,0,1]    #1 代表侮辱性文字，0代表正常言论
    return postingList, classVec

def createVocabList(dataSet):
    '创建一个包含在所有文档中出现的不重复词的列表'
    vocabSet = set([])
    for document in dataSet:
        vocabSet = vocabSet | set(document)     #取并集
    return list(vocabSet)


def setOfWords2Vec(vocabList, inputSet):
    '将词汇转为词向量'
    returnVec = [0] * len(vocabList)
    for word in inputSet:
        if word in vocabList:
            returnVec[vocabList.index(word)] = 1
        else: print("the word： %s is not in my Vocabulary!" % word)
    return returnVec


def trainNB0(trainMatrix, trainCategory):
    'trainMatrix: 文档矩阵；trainCategory：由每篇文档类别标签所构成的向量'
    numTrainDocs = len(trainMatrix)
    numWords = len(trainMatrix[0])
    pAbusive = sum(trainCategory)/float (numTrainDocs)
    p0Num = zeros(numWords)
    p1Num = zeros(numWords)
    p0Denom = 0.0
    p1Denom = 0.0
    for i in range(numTrainDocs):
        if trainCategory[i] == 1:
            p1Num += trainMatrix[i]
            p1Denom += sum(trainMatrix[i])
        else:
            p0Num += trainMatrix[i]
            p0Denom += sum(trainMatrix[i])
    p1Vect = p1Num/p1Denom
    p0Vect = p0Num/p0Denom
    return p0Vect, p1Vect, pAbusive

```