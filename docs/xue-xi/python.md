# python3学习笔记

>### [廖雪峰python教程学习笔记](https://www.liaoxuefeng.com/wiki/0014316089557264a6b348958f449949df42a6d3a2e542c000)

1. 直接运行py文件
  - 在文件第一行添加注释：```#!/usr/bin/env python3```
  - 给文件赋权：```chmod a+x hello.py```
  - 运行py文件：```./hello.py```
- 输出：```print()```

  - 多个字符串用逗号隔开，输出时，遇到**逗号会自动输出一个空格**
- 输入：```input()```
  - 例1：```name = input()```
  - 例2：```name = input('please input your name:')```
- 源码文件以 **UTF-8** 编码，所有字符串都是 **unicode** 字符码。
- 标识符对 **大小写敏感**。
- 多行内容：用一对```'''```包含内容
  - 例：
  ```python
  print('''line1
  line2
  line3''')
  ```
- 布尔值：```True```、```False```<font color=red>（注意：首字母是大写）</font>
- 逻辑运算符：```and```、```or```、```not```
- 空值：```None```
- 除法
  - /：结果为浮点数；
  - //：结果为整数（向下取整）
  - %：取余
- 整数没有大小限制
- 浮点数没有大小限制，超出范围会表示为```inf```（无限大）
- 字符编码
  - ASCII编码：定长，1个字节
  - Unicode编码：定长，通常是2个字节
  - UTF-8：变长，1-6个字节
- 源码文件以 **UTF-8** 编码。
- Numbers: 
    - int | float | bool | complex(复数)
    - <font color=red>除法：2/4 = 0.5;2//4=0;</font>
    - <font color=red>乘方：2**5 = 32</font>
    - 在混合计算时，Pyhton会把整型转换成为浮点数。
- 字符串
  - 字符串以 **unicode** 编码
  - ord()：获取字符的整数表示，字符 → 整数
  - chr()：把编码转换为字符，整数 → 字符
  - len()：计算字符串长度，例：
  ```python
  >>> len('ABC')
  3
  ```
  - int()：str转int
- bytes
  - ```bytes```类型的数据用带```b```前缀的单引号或双引号表示：```x = b'ABC'```
  - encode()：将以Unicode表示的```str```编码为指定的bytes，例：
  ```python
  >>> 'ABC'.encode('ascii')
  b'ABC'
  >>> '中文'.encode('utf-8')
  b'\xe4\xb8\xad\xe6\x96\x87'
  ```
  - decode()：bytes 转 str
    - 例：
    ```python
    >>> b'ABC'.decode('ascii')
    'ABC'
    >>> b'\xe4\xb8\xad\xe6\x96\x87'.decode('utf-8')
    '中文'
    ```
  - errors='ignore'：忽略 decode() 转换报错，例：
  ```python
  b'\xe4\xb8\xad\xff'.decode('utf-8', errors='ignore')
  ```
- 查看对象类型：```type()```
  - 例：
  ```python
  print(type(x))
  ```
- 为了让解释器按UTF-8编码读取源文件，我们通常在文件开头写上这两行：
```python
#!/usr/bin/env python3
# -*- coding: utf-8 -*-
```
  - 第1行：告诉Linux/OS X系统，这是一个Python可执行程序，Windows系统会忽略这个注释
  - 第2行：告诉Python解释器，按照UTF-8编码读取源代码
- 格式化输出
  - 例：
  ```python
  >>> 'Hello, %s' % 'world'
  'Hello, world'
  ```
  ```python
  >>> 'Hi, %s, you have $%d.' % ('Michael', 1000000)
  'Hi, Michael, you have $1000000.'
  ```
  <table style='border: 1px solid black'>
    <tr style='text-align:center'><th>占位符</th><th>替换内容</th></tr>
    <tr><td>%d</td><td>整数</td></tr>
    <tr><td>%f</td><td>浮点数</td></tr>
    <tr><td>%s</td><td>字符串</td></tr>
    <tr><td>%x</td><td>十六进制整数</td></tr>
  </table>
  - 整数补零：
    - ```%03d```：3位整数，补零
    - ```%3d```：3位整数，不补零，但会占位
  - 浮点数设置小数位数

    - ```%.2f```：保留2位小数
  - %%：对```%```转义
  - format()：用传入的参数依次替换字符串内的占位符
    - 例：
    ```python
    >>> 'Hello, {0}, 成绩提升了 {1:.1f}%'.format('小明', 17.125)
    'Hello, 小明, 成绩提升了 17.1%'
    ```
- list：列表，有序
```python
classmates = ['Michael', 'Bob', 'Tracy']
# 获取元素个数
len(classmates)
# 取最后一个元素
classmates[-1]
# 追加元素
classmates.append('Adam')
# 在指定位置插入元素
classmates.insert(1, 'Jack')
# 删除末尾的元素
classmates.pop()
# 删除指定位置的元素
classmates.pop(1)
# list里面的元素的数据类型可以不同
L = ['Apple', 123, True]
# list元素也可以是另一个list
s = ['python', 'java', ['asp', 'php'], 'scheme']
# 空list
L = []
```
- tuple：元组，有序，初始化后不能修改（指向不变）
```python
classmates = ('Michael', 'Bob', 'Tracy')
# 定义一个空的tuple
t = ()
# 定义只有一个元素的tuple
t = (1,)
```
- 条件判断
```python
age = 3
if age >= 18:
    print('adult')
elif age >= 6:
    print('teenager')
else:
    print('kid')
```
- for 循环
```python
names = ['Michael', 'Bob', 'Tracy']
for name in names:
    print(name)
```
- while 循环
```python
# 计算100以内所有奇数之和
sum = 0
n = 99
while n > 0:
    sum = sum + n
    n = n - 2
print(sum)
```
- break：提前结束循环
- continue：跳过本次循环
- dict：字典，等同于java的map，<font color=red>key必须是不可变对象
</font>
```python
d = {'Michael': 95, 'Bob': 75, 'Tracy': 85}
#多次对一个key放入value，后面的值会把前面的值冲掉
#
#判断key是否存在
#方式一：in
'Thomas' in d
#方式二：get()，如果key不存在，可以返回None，或者自己指定的value
d.get('Thomas')
d.get('Thomas', -1)
#
#删除
d.pop('Bob')
```
- set：无序不重复
```python
s = set([1, 2, 3])
#追加元素
s.add(4)
#删除元素
s.remove(4)
#集合运算
s1 = set([1, 2, 3])
s2 = set([2, 3, 4])
# 交集
s1 & s2
# 并集
s1 | s2
```
- 导入函数
```python
#从abstest.py中导入my_abs函数
from abstest import my_abs
```
- 空函数
```python
def nop():
    # pass用作占位符
    pass
```
- 如果没有 return 语句，函数执行完毕后也会返回结果，只是结果为 None 。
- 检查参数类型，抛异常
  例：
  ```python
  def my_abs(x):
    if not isinstance(x, (int, float)):
        raise TypeError('bad operand type')
    if x >= 0:
        return x
    else:
        return -x
  ```
- 函数可以同时返回多个值，但其实就是一个 tuple 。
- **默认参数**：参数有默认值
  ```python
  def enroll(name, gender, age=6, city='Beijing'):
    print('name:', name)
    print('gender:', gender)
    print('age:', age)
    print('city:', city)
  # 调用
  >>> enroll('Sarah', 'F')
  name: Sarah
  gender: F
  age: 6
  city: Beijing
  # 不按顺序提供部分默认参数时，需要指定参数名
  >>> enroll('Adam', 'M', city='Tianjin')
  ```
- <font color=red>定义默认参数要牢记一点：默认参数必须指向不变对象！</font>
- **可变参数**：参数前加 *，在函数调用时自动组装为一个tuple
  ```python
  def calc(*numbers):
    sum = 0
    for n in numbers:
      sum = sum + n * n
    return sum
  # 调用
  >>> calc(1, 2)
  5
  # 把list或tuple的元素变成可变参数传递时，在前面加 *，即表示把集合的所有元素作为可变参数传进去
  >>> nums = [1, 2, 3]
  >>> calc(*nums)
  14
  ```
- **关键字参数**：参数前加 **，在函数内部自动组装为一个dict
  ```python
  def person(name, age, **kw):
    print('name:', name, 'age:', age, 'other:', kw)
  # 调用
  >>> person('Adam', 45, gender='M', job='Engineer')
  name: Adam age: 45 other: {'gender': 'M', 'job': 'Engineer'}
  # dict作为参数传递
  >>> extra = {'city': 'Beijing', 'job': 'Engineer'}
  >>> person('Jack', 24, **extra)
  name: Jack age: 24 other: {'city': 'Beijing', 'job': 'Engineer'}
  ```
- **命名关键字**：用于限制关键字参数的名字
  ```python
  # 命名关键字参数前使用 * 分割，* 后面的参数被视为命名关键字参数
  def person(name, age, *, city, job):
    print(name, age, city, job)
  # 调用
  >>> person('Jack', 24, city='Beijing', job='Engineer')
  Jack 24 Beijing Engineer
  # 如果函数定义中已经有了一个可变参数，后面的命名关键字参数就不需要 * 分割
  def person(name, age, *args, city, job):
    print(name, age, args, city, job)
  # 命名关键字参数必须传入参数名
  ```
- **参数组合**：顺序必须为-必选参数、默认参数、可变参数、命名关键字参数和关键字参数
- 对于任意函数，都可以通过类似```func(*args, **kw)```的形式调用它，无论它的参数是如何定义的。
- 迭代
  ```python
  # 判断是否可迭代
  from collections import Iterable
  >>> isinstance('abc', Iterable) # str是否可迭代
  True
  >>> isinstance([1,2,3], Iterable) # list是否可迭代
  True
  >>> isinstance(123, Iterable) # 整数是否可迭代
  False
  #
  # dict 的迭代
  # 迭代key
  for key in dict:
    print(key)
  # 迭代value
  for value in dict.values():
    print(value)
  # 迭代key和value
  for k,v in dict.items():
    print(k,v)
  #
  # 下标循环迭代
  list = ['A', 'B', 'C']
  for i, value in enumerate(list):
    print(i, value)
  ```
- 列表生成式：用来创建list的生成式
```python
>>> [x * x for x in range(1, 11)]
[1, 4, 9, 16, 25, 36, 49, 64, 81, 100]
>>> [x * x for x in range(1, 11) if x % 2 == 0]
[4, 16, 36, 64, 100]
>>> [m + n for m in 'ABC' for n in 'XYZ']
['AX', 'AY', 'AZ', 'BX', 'BY', 'BZ', 'CX', 'CY', 'CZ']
```
- 生成器：一边循环一边计算，是可迭代对象
```python
# 创建一个generator
# 1. 把列表生成式的[]改成()
g = (x * x for x in range(10))
# 2. 如果一个函数定义中包含yield关键字，这个函数就是generator
# 
# 通过next()函数获得generator的下一个返回值，或通过for循环来迭代它
# 没有更多的元素时，抛出 StopIteration 的错误
```

----

- 注释：**单行注释** 以#开头，**多行注释** 用三个单引号（'''）或者三个双引号（"""）将注释括起
- 自然字符串， 通过在字符串前加 **r** 或 **R** 。 如 r"this is a line with \n" 则\n会显示，并不是换行。
- 复合赋值：a,b = 0,1
- 变量不需要声明。每个变量 **在使用前都必须赋值**，变量**赋值以后该变量才会被创建**。
- 变量就是**变量**，它**没有类型**，我们所说的**"类型"是**变量所指的内存中**对象的类型**。
  - Numbers: 
    - int | float | bool | complex(复数)
    - <font color=red>除法：2/4 = 0.5;2//4=0;</font>
    - <font color=red>乘方：2**5 = 32</font>
    - 在混合计算时，Pyhton会把整型转换成为浮点数。
  - String: myStr = 'ilovepython'
    - 字符串**不能被改变**
    - 用*运算符重复
    - 索引：①从左往右，从0开始依次增加；②从右往左，从-1开始依次减少
    - 截取/切片：myStr[1:5]
    - 转义：反斜杠可以用来转义，使用r可以让反斜杠不发生转义。
  - List: a = [1, 2, 3, 4, 5, 6]
    - 列表中的元素**可变**
    - 列表中元素的类型可以不相同
    - 串联操作：使用+操作符
  - Tuple(元组): a = (1991, 2014, 'physics', 'math')
    - 元组的元素**不能修改**
    - 字符串是一种特殊的元组
    - 只含一个元素需要在元素后添加逗号：tup = (20,)
#####<font color=red>string、list和tuple都属于sequence（序列）</font>
  - Sets: student = {'Tom', 'Jim', 'Mary', 'Tom', 'Jack', 'Rose'} # 重复的元素被自动去掉
    - 是一个**无序不重复**元素的集
    - 创建一个空集合必须用 set() 而不是 { }
    - 集合运算：- 差集，| 并集，& 交集，^ 多个集合不同时存在的元素
  - Dictionaries(字典)：dic = {}  # 创建空字典	tel = {'Jack':1557, 'Tom':1320, 'Rose':1886}
    - 无序键值对集合
    - 关键字必须使用不可变类型
    - 同一个字典中，关键字必须互不相同
    - 内置函数：如clear()、keys()、values()等
- 运算符
  - 逻辑运算符：a 为 10, b 为 20
    - and：(a and b) 返回 20——布尔"与"，如果 a 为 False，a and b 返回 False，否则它返回 b 的计算值。
    - or：(a or b) 返回 10——布尔"或"，如果 a 是 True，它返回 a 的值，否则它返回 b 的计算值。
    - not：not(a and b) 返回 False——布尔"非"，如果 x 为 True，返回 False 。如果 x 为 False，它返回 True。
  - 成员运算符：
    - in：a in list
    - not in：a not in list
  - 身份运算符：
    - is：x is y, 如果 id(x) 等于 id(y) , is 返回结果 1——判断两个标识符是不是引用自一个对象
    - is not：x is not y, 如果 id(x) 不等于 id(y). is not 返回结果 1——是判断两个标识符是不是引用自不同对象
- 在交互模式中，表达式结果被默认赋值给变量 \_。 \_ 变量为只读变量。不要显式地给它赋值——这样您将会创建一个具有相同名称的独立的本地变量，并且屏蔽了这个内置变量的功能。
- Python **字符串不能被改变**，向一个索引位置赋值会导致错误。