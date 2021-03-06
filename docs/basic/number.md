# Attack on Python - 数字 🐍














<extoc></extoc>

## 整型

在 `Python 2.7` 版本中 , `Python` 把 `int` 和 `long` 是分开的

`int` 类型的最大值是 `2147483647`  , 超过了这个值就是 `long`  类型了(长整数不过是大一些的数) ; 而在3.x中 , `int` 和 `long` 整合到一起了 , 以 `int` 来表示

```python
>>> num = 123
>>> type(num)
<class 'int'>
```

## 浮点型

float有两种表现形式 , 一种是十进制数形式 , 它由数字和小数点组成 , 并且这里的小数点是不可或缺的 ; 另一种是指数形式 , 用e(大写也可以)来表示之后可以有正负号 , 来表示指数的符号 , e就是10的幂 , 指数必须是整数

```python
>>> a = 10E2
>>> a
1000.0
>>> b = 10e2
>>> b
1000.0
>>> c = 1.1
>>> type(c)
<class 'float'>
```

小 `Tips` : 在我们工作中很多时候会需要一个无穷大 , 或者无穷小的预设值 , 就可以使用 `float` 来实现 , 无穷小和无穷大分别是 , `float('-inf')` 和 `float('inf')`

## 空值

表示该值是一个空对象 , 空值是python里一个特殊的值 , 用None表示

None不能理解为0 , 因为0是有意义的 , 而None是一个特殊的空值 ; None有自己的数据类型NoneType , 它与其他的数据类型比较永远返回False , 你可以将None复制给任何变量 , 但是你不能创建其他NoneType对象

```python
>>> type(None)
<class 'NoneType'>
>>> None == 0
False
>>> None == True
False
>>> None == False
False
```

## 布尔值

bool就是用来表征真假的一种方式

True为真 , False为假 ; Python中的值是自带bool值的 , 非0即真 , 为0即假

```python
>>> False + False
0
>>> True +  True
2
>>> True + False
1
```

## 复数

复数有实数和虚数部分组成 , 一般形式为 `x + yj` , 其中的 x 是复数的实数部分 , y是复数的虚数部分 , 这里x和y都是实数

注意 , 虚数部分不区分大小写

```python
>>> -.6545 + 0J
(-0.6545+0j)
>>> 4.53e1 - 7j
(45.3-7j)
>>> 45.j
45j
>>> 3.14j
3.14j
```

## 类型转换

```python
int(x [,base]) 将x转换为一个整数 
float(x ) 将x转换到一个浮点数 
complex(x) 将x转换为复数 
str(x) 将对象x转换为字符串 ，通常无法用eval()求值
repr(x) 将对象x转换为表达式字符串 ，可以用eval()求值
eval(str) 用来计算在字符串中的有效Python表达式,并返回一个对象 
tuple(s) 将序列s转换为一个元组 
list(s) 将序列s转换为一个列表 
chr(x) 将一个整数转换为一个字符 
unichr(x) 将一个整数转换为Unicode字符 
ord(x) 将一个字符转换为它的整数值 
hex(x) 将一个整数转换为一个十六进制字符串 
oct(x) 将一个整数转换为一个八进制字符串
```

## 数学函数

```python
abs(x)     返回数字的绝对值，如abs(-10) 返回 10
ceil(x)    返回数字的上入整数，如math.ceil(4.1) 返回 5
cmp(x, y)  如果 x < y 返回 -1, 如果 x == y 返回 0, 如果 x > y 返回 1
exp(x)     返回e的x次幂(ex),如math.exp(1) 返回2.718281828459045
fabs(x)    返回数字的绝对值，如math.fabs(-10) 返回10.0
floor(x)   返回数字的下舍整数，如math.floor(4.9)返回 4
log(x)     如math.log(math.e)返回1.0,math.log(100,10)返回2.0
log10(x)   返回以10为基数的x的对数，如math.log10(100)返回 2.0
max(x1, x2,...)    返回给定参数的最大值，参数可以为序列
min(x1, x2,...)    返回给定参数的最小值，参数可以为序列
modf(x)    返回x的整数部分与小数部分，两部分的数值符号与x相同，整数部分以浮点型表示
pow(x, y) x**y  运算后的值。
round(x [,n])   返回浮点数x的四舍五入值，如给出n值，则代表舍入到小数点后的位数
sqrt(x)     返回数字x的平方根，数字可以为负数，返回类型为实数，如math.sqrt(4)返回 2+0j
```