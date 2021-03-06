#  Attack on Python - 函数进阶 🐍








<extoc></extoc>

## 介绍

接下来我们会介绍一些函数更高级的用法

## 嵌套函数

嵌套函数即函数里面再套一个函数 , 如下 : 

```python
# 全局变量name
name = "Lyon_1"
def func():
    # 第一层局部变量name
    name = "Lyon_2"
    print("第1层打印",name)
    
    #嵌套
    def func2():
        # 第二层局部变量name
        name = "Lyon_3"
        print("第2层打印", name)
        
        # 嵌套
        def func3():
            # 第三层局部变量
            name = "Lyon_4"
            print("第3层打印", name)
        # 调用内层函数
        func3()     
    # 调用内层函数
    func2()  
func()
print("最外层打印", name)
'''
执行结果:
第1层打印 Lyon_2
第2层打印 Lyon_3
第3层打印 Lyon_4
最外层打印 Lyon_1
'''
```

嵌套函数不能越级调用 , 也就是说我们不能在`func2` 的外部去调用`func3` , 当然反过来我们的代码就进入无限递归了

当然我们有时需要的就是在嵌套函数中 , 使用上一层的变量 , 那么我们可以使用`nonlocal` 语句

`nonlocal` 的作用就是改变变量的作用域 , 但是不会扩展到全局变量 , 即只能在函数内部改变 ; nonlocal声明之后 , 会从上层开始找并返回第一个变量 , 没找到则会报错

```python
def func(arg):
    n = arg
    def func1():
        n = 2
        def func2():
            nonlocal n      # n = 2
            n += 1
        func2()
        print(n)        # n = 3
    func1()
    print(n)
func(10)
'''
执行结果:
3
10
'''
```

## 高阶函数

高阶函数就是将一个函数以参数的形式传入另一个函数

```python
# 定义一个主函数,并设置一个参数func
def main_func(func):
	# 返回func的值
    return func

# 定义一个函数作为参数传入主函数
def func():
    # 返回"Lyon"给func()
    return "Lyon"

# res接收main_func的返回值,将func()的返回值作为参数传入main_func函数    
res = main_func(func())
print(res)
'''
执行结果:
Lyon
'''
```

## 闭包

闭包是一个结构体 , 闭包必须是内部定义的函数 (嵌套函数) , 该函数包含对外部作用域而不是全局作用域名字 (命名空间) 的引用

```python
def foo():
    # 局部变量name
    name = 'Lyon'
    # 内部定义的函数
    def bar():
        # 引用了外部定义的变量name,即内部函数使用外部函数变量,这一行为就叫闭包
        print("I am",name)
        return "In the bar"
    # 调用bar并打印结果
    print(bar())
    return "In the foo"
# 调用foo并打印结果
print(foo())
'''
执行结果:
I am Lyon
In the bar
In the foo
'''
```

我们可以通过查看函数对象的 `__closure__` 属性来显示的查看是否有闭包

```python
def foo():
    # 局部变量name
    name = 'Lyon'
    def bar():
        print("I am",name)
        return "In the bar"
    print(bar.__closure__)
foo()
'''
执行结果:
(<cell at 0x7f9a88272fa8: str object at 0x7f9a88167730>,)
'''
```

1. 闭包的这种引用方式 , 我们完全可以把闭包当做一个局部的 `"全局命名空间"` , 也就是说它只是在闭包的作用域中是可见的 , 对外并不可见 , 且闭包只有调用时才会创建 , 所以每个闭包都是完全独立的 , 拥有自己的环境

2. 而且在闭包中被引用的变量的生命周期将会得到提升 , 只要有一个闭包引用了这个变量 , 它就会一直存在

我们来用两个例子加深一下印象

我们可以利用上面第一条所说的来实现一个累加器

```python
# 利用闭包实现一个累加器
def add():
    count = [0]
    def inner():
        count[-1] += 1
        return count[-1]
    return inner

adder1 = add() # 实例化第一个累加器
adder2 = add() # 实例化第二个累加器
print(adder1())
print(adder1())
print(adder1())
print(adder2())
'''
执行结果:
1
2
3
1
'''
```

可以看到两个累加器互不干扰 , 这就像对象的实例化 , 所以你应该知道了 , 闭包可以用来实现对象系统

我们再看看生命周期提升的好处

```python
# 方式一, 利用闭包
def func():
    name = "Lyon"
    def inner():
        hello_name = 'Hello' + name
    [inner() for _ in range(10)]

# 方式二, 不利用闭包
def func():
    def inner():
        name = "Lyon"
        hello_name = 'Hello' + name
    [inner() for _ in range(10)]

func()
"""
首先我们不讨论这段代码是否有实际意义, 只讨论它们的执行方式
我们对比一下方式1和方式2, 它们两者的区别在于 name = "Lyon" 一个在inner外部, 一个在内部
当func执行时
方式1: 创建name变量, 然后执行10次inner函数
方式2: 执行10次inner函数, 每次执行inner函数中, 创建name变量
"""
```

通过代码 , 很明显 , 方式1只需要创建1次 `name` , 而方式2会创建10次 , 原因就在于当一个函数执行完毕 , Python 的垃圾回收机制会将无用的对象进行销毁

虽然从这里可以看出 , 闭包的使用可以提升某些时候的性能 , 但是同时 , 由于生命周期的提升 , 它将永远都不会被销毁 , 这不见得是一件好事 , 所以使用闭包还是需要注意不要滥用

我们再留一个思考 , 思考一下下面这道面试题的结果会是什么呢

```python
s = [lambda x: x + i for i in range(10)]
print(s[0](10))
print(s[1](10))
print(s[2](10))
print(s[3](10))
```

## 装饰器

装饰器即给原来的函数进行装饰的工具

装饰器由函数去生成 , 用于装饰某个函数或者方法 (类中的说法) , 它可以让这个函数在执行之前或者执行之后做某些操作

装饰器其实就是上一节闭包中的应用 , 而 `Python` 为了方便我们使用就创造出一个语法糖来方便我们使用

语法糖 : 指那些没有给计算机语言添加新功能 , 而只是对人类来说更"甜蜜"的语法 , 语法糖主要是为程序员提供更实用的编码方式 , 提高代码的可读性 , 并有益于更好的编码风格

语法糖如下 : 

```python
# 装饰器函数
def decorator(func):
    def inner():
        # 我们可以在func执行前, 干一些别的事情
        # 引用外部传入的func, 一般是一个函数对象
        func()
        # 当然也可以在func执行后, 干一些别的事情
	return inner

# 语法糖版本,@ 函数名
@decorator 
def func():
	pass

# 闭包调用版本
func = decorator(func)
```

该语法糖只是将我们闭包中最后自己处理的部分进行处理了 , 如下 : 

```python
@decorator
	↓ 等价
func = decorator(func)
```

实例

```python
def decorator(func):
    def inner():
        print("I am decorator")
        func()   
    return inner
@decorator    # → func = decorator(func)
def func():
    print("I am func")
    return func
func()
'''
执行结果:
I am decorator
I am func
'''
```

多个装饰器装饰同一个函数

```python
def decorator1(func):
    def inner():
        return func()
    return inner

def decorator2(func):
    def inner():
        return func()
    return inner

@decorator1
@decorator2
def func():
    print("I am func")
func()
```

被装饰函数带有参数

```python
def decorator(func):
    def inner(*args,**kwargs):
        return func(*args,**kwargs)
    return inner

@decorator
def func(name):
    print("my name is %s" % name)
func("Lyon")
```

带参数的装饰器

```python
F = False
def outer(flag):
    def decorator(func):
        def inner(*args,**kwargs):
            if flag:
                print('before')
                ret = func(*args,**kwargs)
                print('after')
            else:
                ret = func(*args, **kwargs)
            return ret
        return inner
    return decorator

@outer(F)      # outer(F) = decorator(func)
def func():
    print('I am func')
```

我们利用装饰器虽然功能达到了 , 但是注意原函数的元信息却没有赋值到装饰器函数内部 , 比如函数的注释信息 , 如果我们需要将元信息也赋值到装饰器函数内部 , 可以使用 `functools` 模块中的`wraps()`方法 , 如下 :

```python
import functools
def outer(func):
    @functools.wraps(func)
    def inner(*args, **kwargs):
        print(inner.__doc__)
        return func()
    return inner
@outer
def func():
    """
    I am func
    """
    return None
func()
```

我们也可以自己手动修改 , 比如 `inner.__qualname__ = func.__qualname__` , `inner.__doc__ = func.__doc__`
