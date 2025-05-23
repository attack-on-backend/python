#  Attack on Python - 生成器 🐍








<extoc></extoc>

## 介绍

生成器 , 又称为 "半协程" , 它与迭代器 , 协程都有着亲密的关系

## 生成器

生成器非常类似于返回数组的函数 , 都是具有参数、可被调用、产生一系列的值 , 但是生成器不是构造出数组包含所有的值并一次性返回 , 而是每次产生一个值 , 因此生成器看起来像函数 , 但行为像迭代器

因此我们可以利用生成器进行惰性求值 , 不提前存储 , 每次都是通过计算

在 `Python` 中 , 生成器是用来实现迭代器的 , 所以生成器实际上是迭代器的构造器

虽然迭代器是由生成器构造 , 但是生成器同样是可迭代对象 , 自然生成器也可以算是迭代器 , 至少在 `Python` 中我们可以这样来判断

```python
from collections import Iterator
print(isinstance((i for i in range(10)), Iterator))
```

## 生成器函数 

一个函数调用时返回一个迭代器 , 那么这个函数就叫做生成器函数

利用生成器做一个range( 2.x中的xrange ) 的功能

```python
# 定义生成器
>>> def range(n):
...		start = 0
... 	while start < n:
... 		yield start
...			start += 1
>>> obj = range(5)
>>> obj.__next__()
>>> obj.__next__()
>>> obj.__next__()
>>> obj.__next__()
>>> obj.__next__()

# 也可以使用()定义生成器
range = (i for i in range(5))
```

`yield` 的作用 :  `yield` 的作用是中断函数的执行并记录中断的位置 , 等下次重新调用这个函数时 , 就会接着上次继续执行

PS : 调用生成器函数时 , 仅仅会返回一个生成器 , 并不会执行函数的内容 , 生成器只能由 `next()`  进行调用执行 , 实质上`next()` 方法就是调用的` __next__() `  方法

**yield from**

```python
def func1():
    for i in 'AB':
        yield i
    for j in range(3):
        yield j
print(list(func()))

def func2():
    yield from 'AB'
    yield from range(3)
    
print(list(func2()))
```

除了通过 `yield` 和 `yield from` 语句 , 我们还可以通过生成器表达式来定义 , 也就是 `(i for i in range(10))` 这种方式 , 而其他的推导式则是使用 `()` 之外的定义 

```python
# 列表推导式
l = [i for i in range(10)]
# 字典推导式
d = {i:i for i in range(10)}
# 集合推导式
s = {i for i in range(10)}
```

## 应用

监听文件

```python
import time
def tail(filename):
    # 打开文件
    f = open(filename,encoding='utf-8')
    # 从文件末尾算起
    f.seek(0, 2) 
    while True:
        # 读取文件中新的文本行
        line = f.readline()  
        if not line:
            time.sleep(0.1)
            continue
        yield line
tail_g = tail('tmp')
# 生成器也是可迭代对象
for line in tail_g:
    print(line)
```

计算动态平均值

```python
def averager():
	total = 0
    count = 0
    average = None
    while True:
        term = yield average
        total += term
        count += 1
        average = total/count
# 生成生成器
g_avg = averager()
# 激活生成器,不激活无法send
next(g_avg)
# send相当于先传参,后调用next()
print(g_avg.send(10))
print(g_avg.send(30))
print(g_avg.send(50))
```

当然在我们工作中更多的是利用生成器来实现惰性计算

**生成器进阶可见 [《生成器》](https://attack-on-backend.github.io/tornado/#/generator)** 
