---
title: "API"
layout: page
date: 2017-06-02 00:00
collection: ptyon
---
[TOC]


# 字符串填充

python中有一个zfill方法用来给字符串前面补0，非常有用

```python
n = "123"
s = n.zfill(5)
assert s == "00123"
```
zfill()也可以给负数补0

```python
n = "-123"
s = n.zfill(5)
assert s == "-0123"
```

对于纯数字，我们也可以通过格式化的方式来补0

```python
n = 123
s = "%05d" % n
assert s == "00123"
```

# 随机数Random

* `random.random()`用于生成一个0到1的随机符点数: 0 <= n < 1.0。
* `random.uniform()`的函数原型为：用于生成一个指定范围内的随机符点数，两个参数其中一个是上限，一个是下限。如果a > b，则生成的随机数n: a <= n <= b。如果 a <b， 则 b <= n <= a。
```python
print random.uniform(10, 20)  
print random.uniform(20, 10)  
#---- 结果（不同机器上的结果不一样）  
#18.7356606526  
#12.5798298022
```

* `random.randint()`的函数原型为：random.randint(a, b)，用于生成一个指定范围内的整数。其中参数a是下限，参数b是上限，生成的随机数n: a <= n <= b
```python
print random.randint(12, 20)  #生成的随机数n: 12 <= n <= 20  
print random.randint(20, 20)  #结果永远是20  
```
* `random.sample()`用于从指定序列中随机获取指定长度的片断。

```python
list = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10]  
slice = random.sample(list, 5)  #从list中随机获取5个元素，作为一个片断返回  
print slice  
print list #原有序列并没有改变。  
```

* `random.choice()`从序列中获取一个随机元素

```python
print random.choice("学习Python")   
print random.choice(["JGood", "is", "a", "handsome", "boy"])  
print random.choice(("Tuple", "List", "Dict"))  
```

* random.shuffle用于将一个列表中的元素打乱。如:

```python
p = ["Python", "is", "powerful", "simple", "and so on..."]  
random.shuffle(p)  
print p  
#---- 结果（不同机器上的结果可能不一样。）  
#['powerful', 'simple', 'is', 'Python', 'and so on...']  
```