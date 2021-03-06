#  Attack on Python - 继承 🐍












<extoc></extoc>

## 抽象与继承

**抽象** 

> 抽象是从众多的事物中抽取出共同的、本质性的特征，而舍弃其非本质的特征

比如 🍎 , 🍌 , 🍇 ,  等 , 它们共同的特性就是水果 , 我们得出水果这个概念的过程就是一个抽象的过程 , 抽象能使复杂度降低 , 好让人们能够以纵观的角度来了解许多特定的事态

有抽象就会有具体 , 我们会用抽象的对象来表示一类事物 , 而用具体的对象表示某个事物 , 比如苹果 , 香蕉 , 葡萄都是具体的对象 , 水果则是抽象的对象

**继承** 

> 继承是基于抽象的结果

抽象可以让我们来以纵观的角度了解一类事物事物 , 并且这类事物都拥有该抽象中所有的特征 , 相当于继承了该抽象中的特征 , 这样我们就可以只将这类事物不同的特征放到具体中 , 而不需要再次关心共同特征 , 所以***先有抽象后才能有继承*** 

介绍抽象的概念时利用了水果来进行说明 , 为了更好的理解 , 继承就用动物为例子

```python
'-----------抽象出动物类-----------'
# 从狗和猫中抽取共同的特征,它们都能吃,喝,睡,玩
class Animal(object):           
    # 吃                 
    def eat(self):        
        pass              
    # 喝                  
    def drink(self):      
        pass              
    # 睡                  
    def sleep(self):      
        pass           
    # 玩
    def play(self):
        pass
'------------具体动物类------------'
# 所有的类默认是继承了object类的,让'猫'类继承动物类
class Cat(Animal):
    # 抓老鼠
    def catch_mouse(self):
        pass
# 让'狗'类继承动物类
class Dog(Animal):
    # 跳墙
    def jump_wall(self):
        pass
```

我们把🌰栗子中的Animal类叫做父类 , 基类或超类 , Cat和Dog类叫做子类或派生类 

> 简单的继承方式就是在类名后面加入要继承的类

使用继承可以减少我们代码重用 , 简化代码

## 新式类与经典类

在说新式类与经典类之前 , 先说一说单继承和多继承

**单继承与多继承** 

> 单继承就是只以一个类作为父类进行继承

```python
# 定义基类
class Parent:
    pass
# 继承基类
class Subclass(Parent):
    pass
```

> 多继承就是同时以多个类做为基类进行继承

```python
# 定义第一个基类
class Parent1:
    pass
# 定义第二个基类
class Parent2:
    pass
# 定义第三个基类
class Parent3:
    pass
# 继承三个基类
class Subclass1(Parent1,Parent2,Parent3):
    pass
```

在多继承中我们需要考虑一个继承优先的问题 , 就像上面的例子 , 如果我们所定义的三个父类中 , 都拥有一个同样的方法那么Python解释器会怎么去继承父类的方法? 三个同名的方法明显只能选择其中一个进行继承 , 这就关系到经典类和新式类了

**经典类和新式类** 

经典的东西都是比较旧的 , so ,  在Python 2.x 中默认都是经典类 , 只有显示继承了object才是新式类 ; 而Python 3.x 中默认都是新式类 , 不必显示的继承object

> 经典类与新式类在声明时的区别在于 , 新式类需要加上object关键字

```python
# python 2.x 环境下
# 经典类
class A():
    pass
# 新式类
class A(object):
    pass

# python 3.x 环境下
class A:
    pass
```

> 经典类与新式类多继承顺序的区别在于 , 经典类会按照` 深度优先 ` (纵向)的方式查找 , 新式类会按照` 广度优先 ` (横向)的方式查找

**实例环境Python2** 

经典类

```python
# 经典类
class A():
    def __init__(self):
        pass
    def display(self):
        print "This is from A"
class B(A):
    def __init__(self):
        pass
class C(A):
    def __init__(self):
        pass
    def display(self):
        print  "This is from C"
class D(B,C):
    def __init__(self):
        pass
obj = D()
obj.display()
'''
执行结果: This is from A
说明:经典类深度优先,我们通过实例调用display方法时,Python解释器会先找B类,如果B类中没有就会去B类的父类(即A类)中查找,如果在所有的父类中都没有找到需要的方法,才会开始继续找下一个继承的类(即C类)
'''
```

新式类

```python
# 新式类
class A(object):
    def __init__(self):
        pass
    def display(self):
        print "This is from A"
class B(A):
    def __init__(self):
        pass
class C(A):
    def __init__(self):
        pass
    def display(self):
        print  "This is from C"
class D(B,C):
    def __init__(self):
        pass
obj = D()
obj.display()
'''
执行结果: This is from C
说明:新式类广度优先,Python解释器首先到B类进行查找,B类中没有就直接去C类中找,并不会去B类的父类(A类)中去查找,如果C类中没有才会再去B类的父类(A类)中查找,最后如果没找到就会报错
'''
```

## 派生

利用继承机制 , 新的类可以从已有的类中派生

子类继承了父类 , 父类派生了子类 , 继承是站在子类的角度 , 派生是站在父类的角度 , 我们在子类中可以添加新的属性或方法 . 但是要注意父类属性名与子类属性名相同 , 以及父类与子类中方法名的情况 , 说的有点绕了 , 通过实例进一步描述

属性名 , 方法名不发生冲突

```python
# 创建一个基类
class Person:
    # 基类属性
    country = 'China'
    # 构造方法
    def __init__(self, name, age):
        self.name = name
        self.age = age
    # 工作方法
    def work(self):
        print("I am working ...")
# 派生一个子类,继承基类中的属性和方法
class Man(Person):
    # 子类属性
    male = 'man'
    # 新增睡觉方法
    def sleep(self):
        print("I am sleepiing ...")
# 实例化子类
man = Man('Lyon', 18) 
# 调用从基类继承过来的工作方法
man.work()
# 访问从基类继承过来的国家属性
print(man.country)
# 调用子类中的睡觉方法
man.sleep()
# 访问子类中的male属性
print(man.male) 
'''
执行结果:
I am working ...
China
I am sleepiing ...
man
'''
```

属性或方法冲突 , 会按照加载顺序进行覆盖 , 定义过程就已完成

```python
# Python解释器开始执行,将Person类的名字以及类中包含的属性名方法名加载到Person类的命名空间
class Person:
    country = 'China'
    # 注意构造方法也是方法,Python解释器加载时仅仅会将__init__这个名字加载到命名空间,并不会执行内部代码
    def __init__(self, name, age):
        self.name = name
        self.age = age
    # 加载方法名
    def work(self):
        print("I am working ...")
# Python解释器将Man类的名字加载到Man的命名空间,随后由于Person类在这步之前已经完成加载,此时就会通过Person类名从Person的命名空间中取出属性和方法名加载到Man类的命名空间
class Man(Person):
    # 由于上一已完成Person类中的同名__init__的加载,此时会将其覆盖
    def __init__(self, male, country):
        self.male = male
        self.country = country
    # 同__init__,将同名work覆盖
    def work(self):
        print("I don't like working ...")
    # 加载到Man类的命名空间
    def sleep(self):
        print("I am sleepiing ...")
# 实例化Man类
man = Man('male', 'America')
# 此work为覆盖后的work即子类自己的work
man.work()
# country为父类的类属性,在实例化时被实例属性覆盖
print(man.country)
# 调用子类中的sleep方法
man.sleep()
# 打印实例属性male
print(man.male)
'''
执行结果:
I don't like working ...
America
I am sleepiing ...
male
'''
```

当然我们在使用时仅需注意一下几点:

1. 重名时 , 会以子类的方法或属性为主 , 因为父类的会被覆盖
2. 构造方法里是实例属性 , 子类如果也有构造方法 , 以子类的构造方法为主

通俗的讲 : ` 我有就用我的 , 没有就拿你的 ` 

但是上述派生中有两个问题:

1. 当子类父类都有构造方法时 , 如果子类需要父类构造方法中的实例属性怎么办 ?
2. 当子类父类都有同名方法时 , 如果子类需要用父类中的方法怎么办?

这两个问题放到下节 `super`  中解决

## super

先解决上节中的两个问题 , 既然父类中的方法被覆盖掉了 , 那么我们不妨再加载一次父类中的方法 , 将子类中的再次覆盖

解决问题1 : 子类父类构造方法中实例属性集合

```python
class Person:
    def __init__(self, name, age):
        self.name = name
        self.age = age
class Man(Person):
    # 实例属性集合也还是要传参的,只是传入后各拿各的
    def __init__(self, name, age, male):
        self.male = male
        # 通过类名.方法调用Person类中的__init__方法,即将__init__中的代码拿过来用了一遍
        Person.__init__(self, name, age)
# 实例化Man类
man = Man('Lyon', 18, 'male')
# 访问man中的name实例属性
print(man.name)
# 访问man中的age实例属性
print(man.age)
# 访问man中的male
print(man.male)
'''
执行结果:
Lyon
18
male
'''
```

解决问题2 : 使用父类中的重名方法

对于第二个问题明显不能利用问题1同样的方式了 , 因为调用就意味着执行 , 虽然我们可以以问题1中的方式执行父类的方法 , 但是子类的方法也还是会照常执行 , so , 我们得换个方式

```python
class Person:
    def work(self):
        print("I am working ...")
class Man(Person):
    def work(self):
        print("I don't like working ...")
man = Man()
# 将实例man作为self传入Person类中的work方法
# Person().work()
Person.work(man)
'''
执行结果: I am working ...
'''
```

两个问题解决了 , 但是我们发现通过这两种方式来解决会对后期修改造成非常大的麻烦 , 只要类名一变 , 那么我们就得一个个修改 , 开发中来个100个就够你改半小时了 ... 所以就有了super

> super

super只能用在新式类中 , 在经典类中则只能按照上面的方式进行处理了

截取官方文档中的一部分

```python
# 相当于super(type, obj),first argument一般是self实例本身
super() -> same as super(__class__, <first argument>)
# 返回非绑定父类对象
super(type) -> unbound super object
# 返回父类的实例
super(type, obj) -> bound super object; requires isinstance(obj, type)
# 返回父类的实例
super(type, type2) -> bound super object; requires issubclass(type2, type)
# type参数为子类
```

Python中一切皆对象 , 所以其实super是一个类 , 在我们使用super时事实上调用了super类的初始化函数 , 产生了一个super对象

首先用super的方式解决上面的问题吧

问题1

```python
class Person:
    def __init__(self, name, age):
        self.name = name
        self.age = age
class Man(Person):
    def __init__(self, name, age, male):
        self.male = male
        super().__init__(name, age)
```

问题2

```python
class Person:
    def work(self):
        print("I am working ...")
class Man(Person):
    def work(self):
        print("I don't like working ...")
man = Man()
# super的第一个参数是要找父类的那个类
super(Man,man).work()
```

但是在我们使用多继承时 , 这两者的区别就能显现出来了

使用\_\_init\_\_ 

```python
class A(object):
    def __init__(self):
        print("This is from A")

class B(A):
    def __init__(self):
        print("This is from B")
        A.__init__(self)
        print("This is from B")

class C(A):
    def __init__(self):
        print("This is from C")
        A.__init__(self)
        print("This is from C")

class D(B,C):
    def __init__(self):
        print("This is from D")
        B.__init__(self)
        C.__init__(self)
        print("This is from D")
d = D()
'''
执行结果:
This is from D
This is from B
This is from A
This is from B
This is from C
This is from A
This is from C
This is from D
'''
```

使用super

```python
class A(object):
    def __init__(self):
        print("This is from A")
class B(A):
    def __init__(self):
        print("This is from B")
        super().__init__()
        print("This is from B")
class C(A):
    def __init__(self):
        print("This is from C")
        super().__init__()
        print("This is from C")
class D(B,C):
    def __init__(self):
        print("This is from D")
        super().__init__()
        print("This is from D")
d = D()
'''
执行结果:
This is from D
This is from B
This is from C
This is from A
This is from C
This is from B
This is from D
'''
```

用\_\_init\_\_ 和 super我们得到的结果是不一样的 , 因为super是一个类名 , super( ) 事实上调用了super类的初始化函数 , 产生了一个super对象 , 所以使用super可以避免父类被重复调用

PS : super的查找方式遵循MRO表中的顺序 , MRO表后续文章中在研究

## 抽象类与接口

Python本身不提供抽象类和接口机制

抽象类

> 在Java中抽象类的定义是这样的 : 由abstract 修饰的类叫抽象类 , 该类不能被实例化 , 并且仅支持单继承

在Python中如果要实现抽象类 , 需要借助abc模块 .  ABC是Abstract Base Class的缩写

在abc模块中有一个用来生成抽象类的元类 ` ABCMeta ` 

生成抽象类

```python
# 导入抽象元类和抽象方法
from abc import ABCMeta,abstractmethod
class Abstract_class(metaclass=ABCMeta):
    # 使用抽象方法进行约束
    @abstractmethod
    # 父类可以简单实现,子类必须实现
    def func(self):
        print('hello func')
```

抽象类提供了继承的概念 , 它的出发点就是为了继承 , 否则它没有存在的任何意义 , 所以说定义的抽象类一定是用来继承的

接口

> 在Java中接口是一个抽象类型 , 是抽象方法的集合 , 接口通常以interface来声明 . 一个类通过继承接口的方式 , 从而来继承接口的抽象方法 , 达到约束的目的

在Python中默认是没有的 , 所以我们如果要使用接口 , 有两种方法 , 第一种就是我们在抽象类的基础上进行定义 , 第二种则是借助第三方模块 ` zope.interface ` 

这里我们只说第一中方法

```python
# 导入抽象元类和抽象方法
from abc import ABCMeta,abstractmethod
class Abstract_class(metaclass=ABCMeta):
    # 使用抽象方法进行约束
    @abstractmethod
    # 父类不能实现,子类必须实现
    def func(self):
        pass
```

与抽象类中的例子比较 , 因为在Python中抽象类与接口类这两者区分并不清晰 , 我们在对于方法是否实现上 , 修改之后基本就实现了一个接口

> 什么时候使用抽象类与接口

- 当几个子类的父类,有相同的功能需要被实现的时候,就使用` 抽象类 `
- 当几个子类,有相同的功能,但是实现各不相同的时候,就使用` 接口` (接口归一)

接口归一实例

```python
from abc import ABCMeta, abstractmethod
# 定义接口
class Payment(metaclass = ABCMeta):
    @abstractmethod
    def pay(self, money): pass
# 继承接口
class Applepay(Payment):
    def pay(self, money):
        print('The payment method is Applepay , {}'.format(money))
# 继承接口
class Zhifubao(Payment):
    def pay(self, money):
        print('The payment method is Zhiwubaopay , {}'.format(money))
# 继承接口
class Wexin(Payment):
    # 没有接口中的pay方法,实例化时就报错
    def fuqian(self, money):
        print('The payment method is Wexinpay , {}'.format(money))
# 接口归一
def payment(obj,money):
    obj.pay(money)
# 实例化就报错,没有pay方法
# wexin = Wexin()
zhifubao = Zhifubao()
apple = Applepay()
payment(zhifubao,100)
payment(apple,1000)
```

***总结*** 

1. 抽象类与接口都不能被实例化 (抽象方法约束)  , 所以必须被继承才能使用
2. 抽象类中的方法能够被实现 , 接口中的方法不能被实现
3. 抽象类中可以有构造方法 , 接口中不可有
4. 抽象类最好不要用多继承 , 而接口类可以


## isinstance 和 issubclass

isinstance(obj, cls) 检查obj是否是类cls的对象

```python
class Foo:
    pass
obj = Foo()
print(isinstance(obj, Foo))
print(isinstance(obj, object))
print(isinstance(obj, type))
'''
执行结果:
True  #obj是类Foo的对象
True  #obj是object的对象,Foo类继承了object类
False #object类是有type类的实例
'''
```

issubclass(sub, super) 检查sub类是否是super类的派生类

```python
class A:
    pass
class B(A):
    pass
print(issubclass(B, B))
print(issubclass(B, A))
print(issubclass(B, object))
print(issubclass(B, type))
'''
执行结果:
True  #B类是自己的派生类
True  #B类是A类的派生类
True  #B类是object类的派生类,因为A类继承了object类
False #B类不是type类的派生类,type类实例化产生了object类
'''
```
