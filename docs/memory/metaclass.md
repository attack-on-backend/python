#  Attack on Python - 元类 🐍












<extoc></extoc>

## 介绍

[元类](https://zh.wikipedia.org/wiki/%E5%85%83%E7%B1%BB) ( metaclass ) , 是一种实例是类的类 

普通的类定义的是特定对象的行为 , 元类定义的则是特定的类及其对象的行为 , 不是所有面向对象编程语言都支持元类

## type

元类在 Wiki 中的解释已经说的很明确了 , 它是一种实例是类的类 , 这也就意味着元类可以创造类

这么说你可能会不太清晰 , 我们从问题出发 , 在 Python 中是谁创建了类 , 也就是说 Python 中的元类是谁?

如果你看过 Python 这一部分的源码 , 那么想必你对这个问题肯定了然于心 , 没错就是 `type` 类

```python
>>> object.__class__
<class 'type'>
```

至于 `type` 类为什么是元类 , 你可以从我的另一篇文章中获得答案 [《对象的创建》](<https://lyonyang.github.io/blogs/01-Python/09-In-Depth/02-Python%20-%20%E5%AF%B9%E8%B1%A1%E7%9A%84%E5%88%9B%E5%BB%BA.html>) 

看下面的例子 : 

```python
>>> class Foo:
...     pass
...
>>> f = Foo()
```

在这个例子中 , `Foo()` , 也就是调用 `Foo` 的 `__call__` 方法 , 它会做两件事情 : 

1. 调用 `__new__` , 创建对象
2. 调用 `__init__` , 初始化对象

但是注意 , 这个 `__call__` 是 `object` 类的 , 因为 Python 3 中所有的类都默认继承了 `object` , 至于 Python 2 没什么好谈的 , 相信你查查就能知道

我们本就可以通过重载 `__new__` 来控制对象的创建 , 如下 : 

```python
def new(cls):
    x = object.__new__(cls)
    x.attr = 100
    return x

Foo.__new__ = new

f = Foo()
print(f.attr)

g = Foo()
print(g.attr)
"""
执行结果如下: 
100
100
"""
```

但是不同的是 , 你对 `type` 不能这么干 , Python 也不允许你这么干 , 如果唯一的元类都被动了 , 那就乱套了

```python
def new(cls):
    x = type.__new__(cls)
    x.attr = 100
    return x

type.__new__ = new

"""
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
TypeError: can't set attributes of built-in/extension type 'type'
"""
```

所以你从这里也可以知道 , `type` 和 `object` 的区别就在于 : 

- `type` 的 `__new__` , 返回了一个类
- `object` 的 `__new__` , 返回了一个对象实例

如果我们要定义一个元类 , 只需要如下 : 

```python
class Meta(type):
    def __new__(cls, name, bases, dct):
        x = super().__new__(cls, name, bases, dct)
        x.attr = 100
        return x
```

当然你也看出来了 , 这只是继承 , 要让它真正成为元类 , 你还需要如下 :

```python
class Foo(metaclass=Meta):
    pass

print(Foo.attr)
```

我们再看看这个 `Foo` 和普通的对象有什么不同 : 

```python
class Meta(type):
    def __new__(cls, name, bases, dct):
        x = super().__new__(cls, name, bases, dct)
        x.attr = 100
        return x
    
class Foo(metaclass=Meta):
    pass

class Bar(Foo):
    pass

print(type(Meta))
print(type(object))
print(type(Foo))
print(type(Bar))

"""
执行结果如下:
<class 'type'>
<class 'type'>
<class '__main__.Meta'>
<class '__main__.Meta'>
"""
```

当指定了 `metaclass` 之后 , 类的创建将不再由 `type` 负责 , 而是由元类 `Meta` 负责 , 也就是说 `type` 类与这类的 `Meta` 类都是元类 , 大家是同一级

## 元类的作用

元类可以用来改变类的行为 , 这和类并没有什么差别 , 因为我们定义类也可以改变对象的行为 , 我们来看一个例子

```python
class Foo:
    pass

# 调用__call__
f = Foo()

# 如果我们想改变 () 也就是 __call__的行为要怎么做?
# 当然不可能是在Foo类中重载 __call__ 因为那是控制 Foo 实例化出来的对象的
# 所以我们需要用元类来控制它

# 单例模式直接用metaclass来实现, 而且它是线程安全的
class SingletonMeta(type):
    _instances = {}

    def __call__(self, *args, **kwargs):
        if self not in self._instances:
            self._instances[self] = super(SingletonMeta, self).__call__(*args, **kwargs)
        return self._instances[self]


class Singleton(metaclass=SingletonMeta):
    pass

a = Singleton()
b = Singleton()
c = Singleton()
d = Singleton()
e = Singleton()
```

如果你想要改变类的行为 , 除了 Python 默认提供的一个魔术方法 (`__new__`) , 你必须通过元类来改变

**因为 `__new__` 是唯一一个第一个参数不是 `self` 而是 `cls` 的魔术方法**

所以上面这个例子 , 除了用元类 , 你也可以通过覆盖 `__new__` 来实现  

元类其实就是一个类工厂 , 而类则是对象工厂 , 但是实际上我们不需要使用元类同样可以达到生产的目的 , 因为通常我们不会需要去改变类的行为 , 需要改变的是对象的行为

看下面几个例子

**继承**

```python
>>> class Base:
...     attr = 100
...

>>> class X(Base):
...     pass
...

>>> class Y(Base):
...     pass
...

>>> class Z(Base):
...     pass
...

>>> X.attr
100
>>> Y.attr
100
>>> Z.attr
100
```

**类装饰器**

```python
>>> def decorator(cls):
...     class NewClass(cls):
...         attr = 100
...     return NewClass
...
>>> @decorator
... class X:
...     pass
...
>>> @decorator
... class Y:
...     pass
...
>>> @decorator
... class Z:
...     pass
...

>>> X.attr
100
>>> Y.attr
100
>>> Z.attr
100
```

总而言之 , 元类的作用就是用来创造类的 , 我们通常更多的是使用继承 (也就是利用抽象) 的方式来达到我们的目的

Python 之禅中这么说到 : 元类是深层次的魔术代码 , 99% 的用户都不需要关心它 , 如果你好奇你是否需要 , 那你就不需要 , 真正需元类的人 , 是很清楚他们需要的 , 并且 , 不需要一个理由来解释

简单的说 , 元类不适合在生产的代码中使用 , 它更适合用来设计 , 比如 Django , SQLAlchemy 中 , 你就能发现它的身影 , 总而言之 , **元类控制类 , 类控制对象**

