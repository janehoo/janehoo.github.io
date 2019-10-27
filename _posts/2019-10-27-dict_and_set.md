---
title: Python刻意练习---Task06：字典与集合（1day）
categories:
 - deliberate-practice
tags:
 - python
---
## 字典 < dict >
字典是python中唯一的映射类型，这种类型区别于序列类型。

序列类型是通过数组的形式存储的，通过索引的方式取得相应位置的值；

而映射类型是通过键值对的形式存储的，通过键（key）映射来取得对应的值（value）。

### 创建和访问字典
字典的定义：`dict = {key1 : value1, key2 : value2, ...}`

我们先来查看一下dict的帮助文档：

执行`help(dict)`可以看到字典的创建有以下几种方式：
```
 |  dict() -> new empty dictionary
 |  dict(mapping) -> new dictionary initialized from a mapping object's
 |      (key, value) pairs
 |  dict(iterable) -> new dictionary initialized as if via:
 |      d = {}
 |      for k, v in iterable:
 |          d[k] = v
 |  dict(**kwargs) -> new dictionary initialized with the name=value pairs
 |      in the keyword argument list.  For example:  dict(one=1, two=2)
```
举几个例子：
```python
dict1 = {1:'one', 2:'two', 3:'three'}   #字典的创建方式1
dict2 = dict(((1, 'one'), (2, 'two'), (3, 'three')))    #字典的创建方式2
dict3 = dict(1='one', 2='two', 3='three')   #字典的创建方式3

dict2 = {}   #创建一个空的字典

dict1[2]    #访问字典dict1中，key=2的值
dict1[2] = '二' #修改字典dict1中，key=2的映射值（访问元素存在则对该键值对进行修改）
dict1[4] = '四' #给字典dict1，增加一对键值对（访问元素不存在则添加新的键值对）
```

### 字典的内建方法
- fromkeys(...)

该方法在文档中的说明如下：
```
 |  fromkeys(iterable, value=None, /) from builtins.type
 |      Create a new dictionary with keys from iterable and values set to value.
```
- keys(), values(), items()

文档中对以上方法的说明如下：
```
keys(...)
 |      D.keys() -> a set-like object providing a view on D's keys
```
```
values(...)
 |      D.values() -> an object providing a view on D's values
```
```
items(...)
 |      D.items() -> a set-like object providing a view on D's items
```
- get()

文档说明如下：
```
get(self, key, default=None, /)
 |      Return the value for key if key is in the dictionary, else default.
```
- clear()

文档说明如下：
```
clear(...)
 |      D.clear() -> None.  Remove all items from D.
```
- copy()

文档说明如下：
```
copy(...)
 |      D.copy() -> a shallow copy of D
```
- pop(), popitem()

文档中对以上方法的说明如下：
```
pop(...)
 |      D.pop(k[,d]) -> v, remove specified key and return the corresponding value.
 |      If key is not found, d is returned if given, otherwise KeyError is raise
```
```
popitem(self, /)
 |      Remove and return a (key, value) pair as a 2-tuple.
 |      
 |      Pairs are returned in LIFO (last-in, first-out) order.
 |      Raises KeyError if the dict is empty.
```
- setdefault()

文档说明如下：
```
setdefault(self, key, default=None, /)
 |      Insert key with a value of default if key is not in the dictionary.
 |      
 |      Return the value for key if key is in the dictionary, else default.
```
- update()

文档说明如下：
```
update(...)
 |      D.update([E, ]**F) -> None.  Update D from dict/iterable E and F.
 |      If E is present and has a .keys() method, then does:  for k in E: D[k] = E[k]
 |      If E is present and lacks a .keys() method, then does:  for k, v in E: D[k] = v
 |      In either case, this is followed by: for k in F:  D[k] = F[k]
```

## 集合 < set >

 - 集合是无序的；
 - 集合中所有的元素都是唯一的，不存在重复元素。

### 集合的创建
集合的定义：`set = {item1, item2, ...}`

我们先来查看一下dict的帮助文档：

执行`help(set)`可以看到字典的创建有以下几种方式：
```
 |  set() -> new empty set object
 |  set(iterable) -> new set object
 |  
 |  Build an unordered collection of unique elements.
```
### 集合元素的访问
- 使用`for`循环将集合中的元素逐一读出
- 使用`in`和`not in`判断一个元素是否在集合中

### 集合的常用方法
- add(), remove()

文档中对以上方法的说明如下：
```
 |  add(...)
 |      Add an element to a set.
 |      
 |      This has no effect if the element is already present.
```
```
 |  remove(...)
 |      Remove an element from a set; it must be a member.
 |      
 |      If the element is not a member, raise a KeyError.
```

### 不可变集合
使用`frozenset()`定义一个不可变集合。

执行`help(frozenset)`可以看到字典的创建有以下几种方式：
```
 |  frozenset() -> empty frozenset object
 |  frozenset(iterable) -> frozenset object
 |  
 |  Build an immutable unordered collection of unique elements.
```