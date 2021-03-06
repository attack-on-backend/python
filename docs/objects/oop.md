#  Attack on Python - 面向对象 🐍












<extoc></extoc>

## 介绍 

编程范式

编程是程序员用 特定的语法 + 数据结构 + 算法组成的代码来告诉计算机如何执行任务的过程 , 而实现一个任务的方式有很多种不同的方式 ,  对这些不同的编程方式的特点进行归纳总结得出来的编程方式类别，即为编程范式

- 面向过程编程  Procedural Programming

面向过程编程就是程序从上到下一步步执行 , 基本设计思路就是程序一开始是要着手解决一个大的问题 , 然后把一个大问题分解成很多个小问题或子过程 , 这写子过程再执行的过程再继续分解直到小问题足够简单到可以在一个小步骤范围内解决

在Python中 , 我们通过把大段代码拆成函数 , 通过一层一层的函数调用 , 就可以把复杂任务分解成简单的任务 , 这种分解可以称之为面向过程的程序设计 . 函数就是面向过程的程序设计的基本单元

- 函数式编程  Functional Programming

函数式编程就是一种抽象程度很高的编程范式 , 纯粹的函数式编程语言编写的函数没有变量 , 函数式编程的一个特点就是 , 允许把函数本身作为参数传入另一个函数 , 还允许返回一个函数  , Python对函数式编程提供部分支持 . 由于Python允许使用变量 , 因此 , Python不是纯函数式编程语言

- 面向对象编程  Object Oriented Programming

面向对象编程是利用"类"和"对象"来创建各种模型来实现对真实世界的描述 , 使用面向对象编程的原因一方面是因为它可以使程序的维护和扩展变得更简单 , 并且可以大大提高程序开发效率 , 另外 , 基于面向对象的程序可以使它人更加容易理解你的代码逻辑 , 从而使团队开发变得更从容

## 类与实例

类的语法

```python
class 类名:
    pass
```

一个栗子🌰

```python
# 创建一个人的'类',首字母要大写
class Person(object):
    # 构造函数,初始化属性
    def __init__(self,name):
        self.name = name
	# 人可以吃饭
    def eat(self):
    	print("I am eatting")
# 创造了一个叫做'Lyon'的人        
p = Person('Lyon')
# 执行吃饭功能
p.eat()
# 执行结果: I am eatting
```

* 类 (class)  

类就是 `对现实生活中一类具有共同特征事物的抽象` 

类起到一个模板的作用 , 当我们创建一个类时 , 就相当于创建了一个初始的'模型' , 我们可以通过这个'模型' 来创建出一个个具有相同特征或功能的事物 , 来帮助我们更好的处理问题

在上述栗子中类名Person 后有一个` (object) ` , 这是新式类的写法 , 而在python3.x 以上的版本中 , 默认为新式类 , 所以也可直接 ` class Person: ` 

我们创建类时 , 都默认继承了object类 , object详解见后期文章

* 实例 (instance)

我们知道类是一个抽象 , 既然是抽象那就是不可操作的 , 所以我们如果进行操作 , 就需要将这一抽象的概念变成具体的事物 , 这个过程我们称为实例化

实例化: ` 由抽象的类转换成实际存在的对象的过程 `

实例: ` 由类进行实例化所得到的对象 `  , 上述栗子中的 ` p ` 就是一个实例

## 属性与方法

属性是实体的描述性质或特征 , 比如人有名字 , 年龄 , 性别等 . 当然还有人所能做的事情也是一种属性 , 比如吃饭 , 睡觉 , 喝水等 . 对于这两种属性 , 一种是表示特征的 , 叫做静态属性 , 另一种则是表示功能的 , 叫做动态属性

在Python中 , 我们将**静态属性** 就称为` 属性 `  , 将**动态属性** 就称为` 方法  `  , 并且以变量来表示属性 , 以函数表示方法 , 

**PS:类中的函数已经不叫函数了 , 而叫做方法**


调用方式: `类名.属性名`

```python
class Person:
    # 类变量
    role = 'student'
    # 构造函数
    def __init__(self,name):
        # 实例变量
        self.name = name
```


调用方式: 类名 . 方法名( )

```python
class Person:
    # 普通方法
    def eat(self):
        pass
```

***特殊的类属性***

| 属性名            | 说明                |
| -------------- | ----------------- |
| \_\_dict\_\_   | 查看类或对象成员 , 返回一个字典 |
| \_\_name\_\_   | 查看类的名字            |
| \_\_doc\_\_    | 查看类的描述信息 , 即注释部分  |
| \_\_base\_\_   | 查看第一个父类           |
| \_\_bases\_\_  | 查看所有父类 , 返回一个元组   |
| \_\_module\_\_ | 查看类当前所在模块         |
| \_\_class\_\_  | 查看对象通过什么类实例化而来    |

PS:对于属性和方法 , 在网上分类各种各样的都有 , 比如字段 , 还有菜鸟教程中的一些 , 其实本质上都是一个东西

## 构造函数

在上述例子中 , 可以看到有一个\_\_init\_\_ 方法 , 这个方法叫做构造方法 , 用于初始化属性 , 所以如果我们要设置属性 , 那么构造方法是必须要的

> ***self*** 

我们直接通过实例来说明

```python
class Foo:
    def __init__(self,name):
        self.name = name
    def func(self):
        print(id(self))
a = Foo('Lyon')
# 打印实例a的内存地址
print(id(a))
# 调用类中的func方法,即打印self的内存地址
a.func()
'''
执行结果:
1703689404544
1703689404544
结果分析:
我们发现a的内存地址和self的内存地址是一样的,也就是说self其实就是实例本身
那么在我们进行实例化的时候,self.name = name 就是给实例添加一个name属性,该属性的值就是我们在实例化时传入的'Lyon'
所以如果我们需要给对象添加属性的话,可以直接通过 对象.属性名 = 属性值 的方式进行添加
'''
```

将上栗子中的构造函数再换个姿势看看

```python
a = Foo('Lyon')
# 等价于如下,用类名调用类中的方法
Foo.__init__(a,'Lyon')
```

## 命名空间

在函数中 , Python解释器在执行时 , 会将函数名称依次加载到命名空间 , 类当然也一样

我们创建一个类时 , Python解释器一执行就会创建一个类的命名空间 , 用来存储类中定义的所有名称( 属性和方法 ) , 而我们进行实例化时 , Python解释器又会为我们创建一个实例命名空间 , 用来存放实例中的名称

当我们利用 ` 对象. 名称 `  来访问对象属性 ( 静态与动态 ) 时 , Python解释器会先到该对象的命名空间中去找**该名称**  , 找不到就再到类 ( 该对象实例化之前的类 ) 的命名空间中去找 , 最后如果都没找到 , 那么就抛出异常了 

命名空间的本质是一个字典 , 我们可以访问对象的 `__dict__` 属性得到命名空间

访问属性实例

```python
class A(object):
    """
    这是一个类
    """
    pass
a = A()
# 访问实例a的__doc__属性
print(a.__doc__)
'''
执行结果:

    这是一个类
    
'''
```

## 嵌套组合

对象交互

```python
class Person:
    def __init__(self, name):
        self.name = name
    def attack(self,per):
        print("{} attacked {}".format(self.name, per.name))
lyon = Person("Lyon")
kenneth = Person("kenneth")
lyon.attack(kenneth)
# 执行结果: Lyon attacked kenneth
```

类的组合

传参时组合

```python
class BirthDate:
    def __init__(self, year, month, day):
        self.year = year
        self.month = month
        self.day = day
class Person:
    def __init__(self, name, birthdate):
        self.name = name
        self.birthdate = birthdate
p = Person('Lyon', BirthDate(2000, 1, 1))
```

定义时组合

```python
class BirthDate:
    def __init__(self, year, month, day):
        self.year = year
        self.month = month
        self.day = day
class Person:
    def __init__(self, name, year, month, day):
        self.name = name
        self.birthdate = BirthDate(year, month, day)
p = Person('Lyon', 2000, 1, 1)
```
