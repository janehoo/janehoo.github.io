---
title: Python刻意练习---Task04：字符串与序列（1day）
date: 2019-10-24 23:02:26
categories:
 - 刻意练习
tags:
 - python
---

### 字符串

#### 字符串的相关方法
执行`dir(str)`，得到：
```
['__add__', '__class__', '__contains__', '__delattr__', '__dir__', '__doc__', '__eq__', '__format__', '__ge__', '__getattribute__', '__getitem__', '__getnewargs__', '__gt__', '__hash__', '__init__', '__init_subclass__', '__iter__', '__le__', '__len__', '__lt__', '__mod__', '__mul__', '__ne__', '__new__', '__reduce__', '__reduce_ex__', '__repr__', '__rmod__', '__rmul__', '__setattr__', '__sizeof__', '__str__', '__subclasshook__', 'capitalize', 'casefold', 'center', 'count', 'encode', 'endswith', 'expandtabs', 'find', 'format', 'format_map', 'index', 'isalnum', 'isalpha', 'isascii', 'isdecimal', 'isdigit', 'isidentifier', 'islower', 'isnumeric', 'isprintable', 'isspace', 'istitle', 'isupper', 'join', 'ljust', 'lower', 'lstrip', 'maketrans', 'partition', 'replace', 'rfind', 'rindex', 'rjust', 'rpartition', 'rsplit', 'rstrip', 'split', 'splitlines', 'startswith', 'strip', 'swapcase', 'title', 'translate', 'upper', 'zfill']
```
执行`help(str)`,将打印字符串所有方法的说明：

其中，对方法`capitalize`的说明如下：
```
capitalize(self, /)
Return a capitalized version of the string.
More specifically, make the first character have upper case and the rest lower case.
```
即，该方法使字符串首字母大写，其余字母小写。

用这种方法，我们可以查询所有字符串相关方法的详细说明。

#### 字符串的**format**方法
`format()`使用举例：
```python
str1 = '{0} love {1} {2}'.format('I', 'love', 'python')
print(str1)
```
```python
str2 = '{0} love {b} {c}'.format('I', b = 'love', c = 'python')
print(str2)
```
```python
str3 = '{a} love {b} {0}'.format(a = 'I', b = 'love', 'python')
print(str3)
```
打印`str3`时会报错，因此，这是一种错误的`format()`使用方法。当格式化的位置被key定义后，就不能再使用序号来定义位置了。

```python
str4 = '{0:.1f}{1}'.format(27.658, 'GB')
print(str4)
```
打印结果是：
```
27.7GB
```
`:`后的`.1f`表示，格式化为小数点后保留1位的浮点数。

#### 字符串格式化符号(使用%进行字符串格式化)

`%c`表示格式化字符和ASCII码；

`%s`表示格式化字符串；

`%d`表示格式化整数；

`%o`表示格式化无符号八进制数；

`%x`表示格式化无符号十六进制数；

`%X`表示格式化无符号十六进制数（大写）；

`%f`表示格式化浮点数，且可指定精度；

`%e`表示用科学计数法格式化浮点数；

`%E`表示用科学计数法格式化浮点数，作用同`%e`；

`%g`表示根据值的大小决定使用`%f`或`%e`；

`%G`表示根据值的大小决定使用`%f`或`%e`，作用同`%g`。

举个例子：
```python
str5 = '%f' % 3.1415926 #使用%和格式化符号对字符串进行格式化操作
```

#### 格式化操作符辅助指令

`m.n` m为显示的最小总宽度，n是小数点后的位数；

`-` 用于左对齐；

`+` 在正数前显示加号；

`#` 在八进制数前面显示`0o`，在十六进制数前显示`0x`或`0X`；

`0` 显示的数字前面添加`0`取代空格。

举个例子：
```python
str6 = '%-10f' % 5  #辅助指令用在格式化符号的%和字母中间
```

#### 字符串转义字符

### 序列

####  列表、元组和字符串的共同点
列表，元组和字符串统称为序列。它们：
- 都可以通过索引得到每一个元素
- 默认索引值总是从0开始
- 可以通过分片的方式得到一个范围内的元素的集合
- 有很多共同的操作符（重复操作符、拼接操作符、成员关系操作符）

##### `list()`方法
```
list() -> new empty list
list(iterable) -> new list initialized from iterable's item
```

##### `tuple()`方法
```
tuple(iterable=(), /)

Built-in immutable sequence.
If no argument is given, the constructor returns an empty tuple.
If iterable is specified the tuple is initialized from iterable's items.
If the argument is a tuple, the return value is the same object.
```

##### `str()`方法
```
str(object='') -> str
str(bytes_or_buffer[, encoding[, errors]]) -> str

Create a new string object from the given object. If encoding or
errors is specified, then the object must expose a data buffer
that will be decoded using the given encoding and error handler.
Otherwise, returns the result of object.__str__() (if defined)
or repr(object).
encoding defaults to sys.getdefaultencoding().
errors defaults to 'strict'.
 ```

##### `len()`方法
```
len(obj, /)

Return the number of items in a container.
```

##### `max()`方法
```
max(...)
max(iterable, *[, default=obj, key=func]) -> value
max(arg1, arg2, *args, *[, key=func]) -> value
    
With a single iterable argument, return its biggest item. The
default keyword-only argument specifies an object to return if
the provided iterable is empty.
With two or more arguments, return the largest argument.
```

##### `min()`方法
```
min(...)
min(iterable, *[, default=obj, key=func]) -> value
min(arg1, arg2, *args, *[, key=func]) -> value
    
With a single iterable argument, return its smallest item. The
default keyword-only argument specifies an object to return if
the provided iterable is empty.
With two or more arguments, return the smallest argument.
```

##### `sum()`方法
```
sum(iterable, start=0, /)
Return the sum of a 'start' value (default: 0) plus an iterable of numbers
    
When the iterable is empty, return the start value.
This function is intended specifically for use with numeric values and may
reject non-numeric types.
```

##### `sorted()`方法
```
sorted(iterable, /, *, key=None, reverse=False)
Return a new list containing all items from the iterable in ascending order.
    
A custom key function can be supplied to customize the sort order, and the
reverse flag can be set to request the result in descending order.
```

##### `reversed()`方法
```
reversed(sequence, /)
   
Return a reverse iterator over the values of the given sequence.
```

##### `enumerate()`方法
```
enumerate(iterable, start=0)
   
Return an enumerate object.
 ```

##### `zip()`方法
```
zip(iter1 [,iter2 [...]]) --> zip object
   
Return a zip object whose .__next__() method returns a tuple where
the i-th element comes from the i-th iterable argument.  The .__next__()
method continues until the shortest iterable in the argument sequence
is exhausted and then it raises StopIteration.
```