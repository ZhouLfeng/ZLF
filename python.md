#### 注释的使用：

#(单行) 和‘’‘  ’‘’(多行)

#### 变量命名规范：

以数字、字母和下划线组成，数字不能作开头，不能使用关键字，要做到顾名思义

#### 数据类型：

int,float,str,bool,tuple,set,list,dict

#### 输出语句：

print()

#### 输入语句：

input()

#### 占位符：

%d,%s,%f,{}和.format搭配使用

#### 数据类型转换：

在变量前加上数据类型进行转换

#### 进制转换：

int(数据，进制)

#### 字符串

##### 输出:print(%s)

##### 输入:python中默认为字符串输入

##### 索引:可以通过下标来取出各个值

###### 切片:通过变量名后的[:]来进行切片

[1:3]表示取出下标为1到3的值，不包含第3个

[1:]表示从下标为1取到最后

[:3]表示从下标为0取到3，不包含第3个

[1:5:2]从下标为1取到5，每两个取一次，不包含第5个

[7:5:-1]从下标为7倒着往前取，取到下标为5

##### 常用方法

获取长度:len

查找内容:

find,rfind:不存在返回-1

index,rindex:不存在报异常

判断:

startswith：判断开头

endswith：判断结尾

isalpha：判断是否纯字母

isdigit：判断是否纯数字

isalnum：判断是否由数字、字母组成

isspace：判断是否全是空格

计算出现次数:count

替换内容:

replace：可修改指定长度（原字符，新字符，修改次数）

切割字符串:

split,rsplit：返回一个列表存放切割开的数据，不包含切割字符

splitlines：按行分割，返回一个列表

partition,rpartition：返回一个元组，包含切割字符

修改大小写:capitalize,title,upper(全大写),lower(全小写)

空格处理:

补空格---ljust,rjust,center(两边空格补齐)

删空格---lstrip,rstrip,strip(删除两端空格)

字符串拼接:join

#### 元组

tuple

元组无法修改

方法:index和count

index:查找数据，找不到报错

count:计算数据出现的次数

#### 字典

字典通过一对键值对来储存数据，一个键对应一个值

字典通过键来查看存放的值，同样也是通过键来修改存放的值

字典可以通过**变量名['键'] = 数据**来添加数据，只要这个键没有在字典中出现过。

##### 删除：

del：del(字典名(键名))

clear：清空字典

##### 字典遍历：

for i in a.keys:              遍历键

for i in a.values:           遍历值

for i in a.items:             遍历键值对



#### enumerate的使用：

字典中enumerate是用来遍历键值对的

列表，元组和字符串中是用来遍历下标和值的

for i,j in enumerate(dict)            I,j为键值对

for i,j in enumerate(list\str\tuple)        i为下标，j为下标对应的值



#### set的使用

set是一个不重复的无序序列，创建格式为{1，2，3}或set（）

##### set方法:

| 方法                          | 描述                                                         |
| ----------------------------- | ------------------------------------------------------------ |
| add()                         | 为集合添加元素                                               |
| clear()                       | 移除集合中的所有元素                                         |
| copy()                        | 拷贝一个集合                                                 |
| difference()                  | 返回多个集合的差集                                           |
| difference_update()           | 移除集合中的元素，该元素在指定的集合也存在。                 |
| discard()                     | 删除集合中指定的元素                                         |
| intersection()                | 返回集合的交集                                               |
| intersection_update()         | 删除集合中的元素，该元素在指定的集合中不存在。               |
| isdisjoint()                  | 判断两个集合是否包含相同的元素，如果没有返回 True，否则返回 False。 |
| issubset()                    | 判断指定集合是否为该方法参数集合的子集。                     |
| issuperset()                  | 判断该方法的参数集合是否为指定集合的子集                     |
| pop()                         | 随机移除元素                                                 |
| remove()                      | 移除指定元素                                                 |
| symmetric_difference()        | 返回两个集合中不重复的元素集合。                             |
| symmetric_difference_update() | 移除当前集合中在另外一个指定集合相同的元素，并将另外一个指定集合中不同的元素插入到当前集合中。 |
| union                         | 返回两个集合的并集                                           |
| update()                      | 给集合添加元素                                               |

#### 列表

通过下标获取列表内的值

##### 增加：

append(末尾)，insert(指定位置)，extend(合并列表)

##### 修改：

通过下标控制

##### 查找：

in，not in

index:查找元素位置----index(需要查找的数据，范围)

count:查找数据出现的次数

##### 删除：

del:通过下标删除

pop:删除最后一个元素

remove:根据元素的值进行删除

##### 排序：

sort:直接将列表进行排序，不需要变量接收返回值

​		格式：sort(列表，key =)，key值是列表排序的根据

sorted:将列表进行排序，需要一个变量来接收排好序的列表

reverse:将列表逆置

##### 遍历：

通过循环语句来控制下标进行列表的遍历

只插入偶数下标

a=[]
for i in range(0,10):
    if i%2 ==0:
        a.insert(i,input("请输入"))
    else:
        a.insert(i,0)
print(a)



冒泡排序：

for i in range(len(a)-1):

​		for j in range(len(a)-1-i):

​						if a[j]>a[j-1]:

  							a[j],a[j-1] = a[j-1],a[j]

##### 列表嵌套：

类似于二维数组，在列表中在嵌套一个列表，通过他所在的下标位置再加一个[]来控制嵌套的那个列表的下标。

#### 函数

##### 定义

def 函数名:

​		pass

##### 调用

函数名()

##### 局部变量

函数中定义的变量为局部变量，如果想引用全局全量。需要声明，即global 变量名

##### 返回值

函数返回值只有一个，若函数中有多个return语句，则只有一个return语句有效

##### 拆包

当函数返回多个值时，可用多个变量来提取结果，简称拆包

##### 函数参数

###### 缺省参数：带默认值的参数

调用函数时，缺省参数的值如果没有传入，则取默认值

缺省参数一定要在参数列表后面

###### 不定长参数

加了星号（*）的变量args会存放所有未命名的变量参数，args为元组

而加**的变量kwargs会存放命名参数，即形如key=value的参数， kwargs为字典.

###### 缺省参数在*args后面

如果很多个值都是不定长参数，那么这种情况下，可以将缺省参数放到 *args的后面， 但如果有\*kwargs的话，*kwargs必须是最后的

##### 可变类型和不可变类型

可变类型(修改数据，内存地址不会发生变化)有： 列表、字典、集合

不可变类型(修改数据，内存地址必定发生变化)有： 数字、字符串、元组

##### 参数值传递

Python中函数参数是传递引用，也就是数据的内存地址

对于不可变类型，修改形参，不影响实参

对于可变类型来说，修改形参，会影响实参

传带*号的排序

def is_sort(*a):
    a = list(a)
    t = len(a)
    for i in range(0, t):
        for j in range(0, t - i - 1):
            if a[j] > a[j + 1]:
                a[j], a[j + 1] = a[j + 1], a[j]
    return a

print(is_sort(1, 2, 3, 5, 4, 8, 6, 9))



#### 递归函数

递归函数通过自己来调用自己，函数中一定要有截止点

#### 匿名函数

lambda 参数列表: 运算表达式

> > > def makeActions():

```
    acts = []

    for i in range(5): # Use defaults instead

        acts.append(lambda x, i=i: i ** x) # Remember current i

    return acts
```

acts = makeActions()

acts[0](2) # 0 ** 2

结果：0

acts[1](2) # 1 ** 2

结果：1

acts[2](2) # 2 ** 2

结果：4

acts[4](2) # 4 ** 2

结果：16



def makeActions():

```
    acts = []
    for i in range(5): 
        acts.append(lambda x: i ** x) 
    return acts
```

acts = makeActions()

acts[0](2) 

结果：16

acts[1](2)

结果：16

acts[2](2) 

结果：16

acts[4](2) 

结果：16

#### 列表推导式

通过循环来控制，往列表中逐个添加数据

#### 高阶函数

既然变量可以指向函数，函数的参数能接收变量，那么一个函数就可以接收另一个函数作为参数，同样，我们还可以把一个函数当做另一个函数的返回值。这种函数的使用方式我们称之为高阶函数。

同样，函数可以作为形参，也可以作为返回值

#### 嵌套函数

在函数里面还可以定义函数，可以嵌套多层，执行需要被调用。

#### 闭包

将函数作为一个整体赋给变量，通过变量+（）可调用函数

#### 装饰器

使用装饰器实现权限

def outer_check(base_permission):
    def check_permission(action):
        def do_action(my_permission):
            if my_permission & base_permission:
                return action(my_permission)
            else:
                return '对不起，您不具有该权限'
        return do_action
    return check_permission

READ_PERMISSION = 1
WRITE_PERMISSION = 2
EXECUTE_PERMISSION = 4

@outer_check(base_permission=READ_PERMISSION)
def read(my_permission):
    return '读取数据'

@outer_check(base_permission=WRITE_PERMISSION)
def write(my_permission):
    return '写入数据'

@outer_check(base_permission=EXECUTE_PERMISSION)
def execute(my_permission):
    return '执行程序'

print(read(5))

###### 一般格式：

def w1(func):
    def inner():
        # 验证1
        # 验证2
        # 验证3
        func()
    return inner

@w1
def f1():
    print('f1')
@w1
def f2():
    print('f2')
@w1
def f3():
    print('f3')
@w1
def f4():
    print('f4')

def a(b):
    def c(d):
        return b(d)
    return c

修饰器不带参数的，第一层修饰器名+函数名参数，第二层自己定义的函数名+变量参数。如果需要执行被修饰程序，调用函数名参数（变量参数），其中函数名参数就是被修饰的函数名，变量参数就是被修饰函数的传参，最后return第二层函数名。
修饰器带参数的，第一层为修饰器名+参数，参数为修饰器语句传递过来，第二层和第三层和不带参数的修饰器第一层和第二层差不多，最后返回在第一层返回第二层的函数名，第二层中返回第三层的函数名



#### 文件操作

##### 文件打开：

file = open("文件名",“打开方式”)

file.close()

with open("文件名",“打开方式”) as file:    (不需要关闭文件)

##### 打开方式：

r:只读方式打开

w:只写方式打开，打开后会清除原数据，若无打开文件，会新建

a:追加方式打开

三种方式后面加b为二进制打开方式

#### 文件读写

f.write:文件写入

f.read:文件读

f.readline:文件按行读取

f.readlines:文件读出所有行

#### 指针定位

tell():显示当前位置指针

seek(offset,whence):重新设定指针位置

​	offset:表示偏移量

​	whence:只能传入012中的一个数字。

​		0表示从文件头开始

​		1表示从当前位置开始

​		2 表示从文件的末尾开始

#### 文件的序列化与反序列化

导入pickle包，文件必须要二进制打开

pickle.dump可将文件序列化写入文件

pickle.load可将文件反序列化读出

#### 面向对象

##### 类和对象

类：对事物和行为的总称，类规定了一个对象所拥有的事物和行为

对象：通过引用类来完成事件

##### 基本语法

dir(参数)：查看对象类中的所有方法

\_\_init\_\_:对象初始化时会自动调用

_\_del\_\_:对象被删除时自动调用

_\_str\_\_:返回对象描述信息，print函数输出使用

_\_new\_\_:给实例化对象生成一个内存，至少要有一个参数cls，代表要实例化的类

##### 定义类

class 类名:

​		def 方法名(self,参数):

​						pass0

##### 创建实例对象

对象变量名= 类名()

##### 添加属性

对象变量名.变量 = 一个数据，若变量在类中没有定义，则会自动添加一个类变量，尽量不要使用，会引起混乱

### 深拷贝与浅拷贝

内存保存变量是由一个内存地址保存变量名，再由另一个内存地址来保存变量中的数据，也就是说是阶级性的，一层指向一层

不可变类型：字符串、int、float、元组
可变类型：列表、字典

不可变数据就是在他的内存地址上修改不了数据
可变数据就是在他的内存地址上可修改数据，因为可变数据是通过可变数据这一个整体的内存地址来控制的，里面的数据是由一个个不可变数据组和的，总而言之就是通过这一个整体来调用内存中存放他的各个数据的内存地址，所以当你修改时，也就相当于修改了他所调用的内存地址，所以拷贝数据和原数据才都会做出改变

== 调用__eq__方法，is比较内存地址
id(变量)——显示内存地址

python传递变量全是传递的内存地址
例：
a=[1,2,3,4,5,6]
b=a
b[0]=7
当输出a列表和b列表时第0个位置更改为7
即  a-->7，2，3，4，5，6
     b-->7，2，3，4，5，6
就是a和b共享同一个内存地址

浅拷贝copy：复制变量的内存数据，保存在不同的内存中，但内存中的数据所待的内存不变

若数据为不可变，拷贝的数据修改后，不会改变原数据，原数据指向内存地址，修改后的数据指向不同的内存地址，因为是不可变的，所以每一块内存只存一个不可变数据，拷贝的内存地址就得修改，但原数据的内存地址并不修改，所以原数据不变

若数据可变，拷贝的数据修改后，原数据会被修改，因可变数据指向同一个内存地址，再加上是可变的，所以一旦修改则全部改变。

copy可以浅拷贝数据，但指向不同的内存地址

a=[1,2,[3,4],5,6]
b=a.copy
b[1][0]=7
b[0]=8
当输出a列表不变，b列表时第0个位置更改为7
即  a-->1，2，[7，4]，5，6
     b-->8，2，[7，4]，5，6

深拷贝deepcopy:不可变数据和浅拷贝差不多，但可变数据和浅拷贝不同
深拷贝把原数据的可变数据和拷贝后的可变数据分别存放在不同的内存中，当其中有一个可变数据被修改，不会牵连拷贝或者原数据。

内存中每一个地址都存放一个基层数据，基层数据都为不可变的，浅拷贝和深拷贝都不会重新创建一个内存地址来存放相同的基层数据，也就是所以的拷贝中，如果数据类型都不可变，当修改数据，内存只会重新创建一个内存地址来保存修改后的数据，这样深拷贝和浅拷贝中修改后的数据指向的内存地址会进行改变，原数据不变。

##### 私有属性和方法

在变量前或方法名前添加两个_,会变为私有属性，只能由类内部自我调用，外部变量调用不了，实例化对象也无法调用

##### 继承

创建类时在类名后的括号内添加已定义的类名即为继承，会拥有父类的所有属性及方法，但私有方法无法继承

py中也可以多继承，拥有多个类的属性及方法

super().函数名(参数)
父类名.函数名(self,参数)

##### 方法的重写

子类继承父类后，如果子类和父类都拥有同一个方法，则子类中的方法会把父类中的方法重写，调用只会使用子类的方法

### 面向对象的三大特性：

- 封装：这是定义类的准则，根据对象的特点，将行为和属性抽象出来，封装到一个类中。
- 继承：这是设计类的技巧。父类与子类，主要体现在代码的重用，不需要大量的编写重复代码。
- 多态：不同的子类调用相同的父类方法，产生不同的执行结果，可以增加代码的外部灵活度。多态是以继承和重写父类方法为前提的，它是一种调用方法的技巧，不会影响到类的内部设计。

##### 类方法

第一个形参是类对象的方法

需要用装饰器`@classmethod`来标识其为类方法，对于类方法，第一个参数必须是类对象，一般以`cls`作为第一个参数。

类方法调用类里面的函数，在前面添加@classmethod
可直接类名.函数名调用

```python
class Dog(object):
    __type = "狗"

    # 类方法，用classmethod来进行修饰
    @classmethod
    def get_type(cls):
        return cls.__type
print(Dog.get_type())
```

##### 静态方法

需要通过装饰器`@staticmethod`来进行修饰，静态方法既不需要传递类对象也不需要传递实例对象（形参没有self/cls）。

静态方法 也能够通过 实例对象 和 类对象 去访问。

```python
class Dog(object):
    type = "狗"

    def __init__(self):
        name = None

    # 静态方法    
    @staticmethod
    def introduce():  # 静态方法不会自动传递实例对象和类对象
        print("犬科哺乳动物,属于食肉目..")

dog1 = Dog()
Dog.introduce()    # 可以用 实例对象 来调用 静态方法
dog1.introduce()    # 可以用 类对象 来调用 静态方法
```

##### 单例模式

一个类只有一个实例化对象称为单例模式

### 异常

常见异常：

NameError	尝试访问一个没有申明的变量

ZeroDivisionError	除数为0

SyntaxError	语法错误

indexError	                索引超出序列范围

KeyError	                请求一个不存在的字典关键字

IOError	                输入输出错误（比如你要读的文件不存在）

AttributeError	尝试访问未知的对象属性

异常处理常见格式：

try：
	语句		（对语句进行错误检测）
except     	错误名称：	（有错误，判断错误，执行语句）
	语句
except     	错误名称：
	语句
...
else：			（没有错误，执行语句）
	语句
finally：			（无论有没有错误，finally都会执行，属于收尾）
	语句



一般简写：
try：			（对语句进行错误检测）
	语句		
except			（有错误，执行语句）
	语句
else：			（没有错误，执行语句）
	语句
finally：			（无论有没有错误，finally都会执行，属于收尾）
	语句

自定义异常(raise后面的异常名可带参数，参数直接传至异常类中)

class 异常名(Exception):
    def __init__(self):
        pass
    def __str__(self):
        return 

def 函数名(参数):
    if 条件:
        raise 异常名
    else:
        print("输入正确")

变量= input("请输入密码：")
try:
    函数名(变量)
except 异常名 as e:
    print(e)

### 模块

#### 模块导入方式：

import 模块名

from 模块名 import 功能名

from 模块名 import *

import 模块名 as 别名

from 模块名 import 功能名 as 别名

##### 常见模块

pickle模块(文件序列化与反序列化):dumps、dump、load、loads、

随机数产生
import random
变量 = random.randint(a,b)           生成[a,b]的整数
变量 = random.randrange(a,b)      生成[a,b)的整数
变量 = random.random()               生成[0,1)的小数
random.choice()                            随机选择

random.sample                               随机选择不重复的数

import math
math.ceil()     向上取整，有小数加1
math.floor()   向下取整，有小数去小数
math,fabs()    取绝对值

##### 模块中的all

\_\_all_\_ = ["Test","test2"]  # 有Test类和test2方法，没有test1方法

all中没有指定的方法，无法导入

### 正则表达式

基本：
	re.search(r'\d+', b).group()

compile用法
	regex = re.compile(r'd\d+m')
	regex.search(a)



()		括号表达式
[]		表示一段区间，判断中间的数是否在该区间内
{}		规定前面的字符串出现的次数
. 		表示除了换行\n 以外的任意字符
\ 		表示转义字符串
\d 		表示的数字，等价于  [0-9]
\D  		表示的是非数字
\w 		表示的数字、字母和下划线  等价于 [0-9a-zA-Z_]
\W  		表示非数字、字母下划线   等价于[^0-9a-zA-Z_]
\s 		表示空白字符    
\S  		非空白字符
[\u4e00-\u9fa5]  	匹配中文区间
^ 		指定开头判断
$ 		指定结尾判断

- 表示前面的字符出现0次或者多次  等价于  {0,}

- 表示前面的字符出现1次或者多次  等价于  {1,}
  ? 		表示前面的字符出现0次或者1次  等价于{0,1}

re.I		修饰符用来忽略大小写
re.M		多行匹配，影响^$匹配结果
re.S 		点能够匹配到换行

正则替换
re.sub

贪婪算法和非贪婪算法：
贪婪算法就是尽可能的取，比如说文件名，(.*)(\..+)可以取出文件名和后缀，不管文件名中有多少个.都可以取到
非贪婪算法：最少可能的取，(.*)?(\..+)只取第一个.之前的字符，不会疯狂的往后取，这种更类似于用符号分完组后，取出第一个组

### 迭代器

只要类中有__iter__函数即为可迭代对象
如果一个类要成为迭代器，必须重写__iter__和__next__
迭代器停止: raise StopIteration

```python
class MyIter(object):
    def __init__(self, n):
        self.n = n
        self.a = 1
        self.b = 1
        self.count = 0

    def __iter__(self):
        return self

    def __next__(self):
        if self.count < self.n:
            self.count += 1
            c = self.a
            d = self.b
            self.a = d
            self.b = c + d
            return c
        raise StopIteration


f = MyIter(20)
for i in f:
    print(i, end=' ')

```

###  生成器(输出数列)
def fibonacci(n):
    a = 1
    b = 1
    count = 0
    while count < n:
        yield a
        a, b = b, a + b
        count += 1

gen = fibonacci(10)
for i in gen:
    print(i, end=' ')
print()

协程:send

### 加密方法

##### MD5和SHA加密

```python
# MD5 和 SHA加密的方法都在hashlib模块里

import hashlib

# help(hashlib)
# print(hashlib.__doc__)
m5 = hashlib.md5()

# 计算了 hehe 它的 md5 值，并且把值保存到m5对象上了
m5.update('hehe'.encode('utf-8'))
# 获取m5对象上的hehe的md5十六进制值
print(m5.hexdigest())

# s224 = hashlib.sha224()
# s224.update('good morning'.encode('utf-8'))
# print(s224.hexdigest())
print(hashlib.sha224('abcdhehehehe'.encode('utf-8')).hexdigest())
print(hashlib.sha256('abcdhehehehe'.encode('utf-8')).hexdigest())
print(hashlib.sha512('abcdhehehehe'.encode('utf-8')).hexdigest())

```

##### HMAC加密

```python
import hmac

# h = hmac.new('hehe'.encode('utf-8'), 'good'.encode('utf-8'))
# print(h.hexdigest())

# hexdigesth = hmac.new('hehe'.encode('utf-8'))
# h.update('good'.encode('utf-8'))
# print(h.hexdigest())

h = hmac.new('hehe'.encode('utf-8'))
user_password = '7ecf78fd96d522f5526e527305bc5e10'

input_pwd = input('请输入您的密码')
h.update(input_pwd.encode('utf-8'))
if h.hexdigest() == user_password:
    # if hmac.compare_digest(h.hexdigest(), user_password):
    print('欢迎登录')

```

#### property的使用

##### 作为装饰器使用

```python
class Person(object):
    def __init__(self, name, age):
        self.name = name
        self.age = age
        self.__money = 2000

    def get_money(self):
        return self.__money

    @property
    def money(self):
        print('查询余额了！！！！')
        return self.__money

    @money.setter
    def money(self, qian):
        print('存取款了！！！！')
        self.__money += qian

    @money.deleter
    def money(self):
        print('呵呵')
        del self.__money


p = Person('张三', 18)
print(p.name)
print(p.age)

print(p.get_money())

# @property 可以让一个函数像是属性一样被调用
print(p.money)
p.money = 2000
print(p.money)

del p.money

print(p.money)

```

##### 作为类属性使用

```python
class Foo(object):
    def get_bar(self):
        print("getter...")
        return 'laowang'

    def set_bar(self, value):
        """必须两个参数"""
        print("setter...")
        return 'set value' + value

    def del_bar(self):
        print("deleter...")
        return 'laowang'

    BAR = property(fget=get_bar, fset=set_bar, fdel=del_bar, doc="description...")


obj = Foo()
# obj.get_bar()
# obj.set_bar()
# obj.del_bar()

obj.BAR  # 自动调用第一个参数中定义的方法：get_bar
obj.BAR = "alex"  # 自动调用第二个参数中定义的方法：set_bar方法，并将“alex”当作参数传入
desc = Foo.BAR.__doc__  # 自动获取第四个参数中设置的值：description...
print(desc)
del obj.BAR  # 自动调用第三个参数中定义的方法：del_bar方法

```

#### 类中的常见魔法方法

```python
   # 迭代器，需要返回一个迭代器
    # 如果一个类重写了这个方法，它就是一个可迭代对象
    # def __iter__(self):

    # 迭代对象时，自动调用的方法
    # def __next__(self):

    # def __ge__(self, other):
    # def __lt__(self, other):
    # def __le__(self, other):
    # def __ne__(self, other):

    # 位运算相关
    # def __and__(self, other):
    # def __or__(self, other):
    # def __xor__(self, other):

    # 算数运算相关
    # def __add__(self, other):
    # def __sub__(self, other):
    # def __mul__(self, other):
    # def __truediv__(self, other):
    # def __floordiv__(self, other):
```

### 线程、进程和协程

```
进程在大规模计算中使用
线程在网络IO中使用
协程在网络IO中使用
```

#### 线程

导入threading模块，利用threading.Thread（target=函数名）可将函数线程化，多个线程可同时进行，只需要调用start（）函数

在一个进程内的所有线程共享全局变量，很方便在多个线程间共享数据，缺点就是线程是对全局变量随意遂改可能造成多线程之间对全局变量的混乱（即线程非安全）

当多个线程同时调用同一个变量时，可利用线程锁来控制，即threading.Lock()

创建锁

mutex = threading.Lock()

锁定

mutex.acquire()

释放

mutex.release()

##### 线程通信

```python
import threading
import time
from queue import Queue

def producer(queue):
    for i in range(100):
        print('{}存入了{}'.format(threading.current_thread().name, i))
        queue.put(i)
        time.sleep(0.1)
    return

def consumer(queue):
    for x in range(100):
        value = queue.get()
        print('{}取到了{}'.format(threading.current_thread().name, value))
        time.sleep(0.1)
        if not value:
            return

if __name__ == '__main__':
    queue = Queue()
    t1 = threading.Thread(target=producer, args=(queue,))
    t2 = threading.Thread(target=consumer, args=(queue,))
    t3 = threading.Thread(target=consumer, args=(queue,))
    t4 = threading.Thread(target=consumer, args=(queue,))
    t6 = threading.Thread(target=consumer, args=(queue,))
    t1.start()
    t2.start()
    t3.start()
    t4.start()
    t6.start()
```

#### 进程

导入multiprocessing包中的Process，通过Process（target=函数名）进程化，若函数需要形参，则引用列表和字典传递

```python
p = Process(target=run_proc, args=('test',18), kwargs={"m":20})
```

进程不能共享数据

##### 进程通信

```python
from multiprocessing import Queue
q=Queue(3) #初始化一个Queue对象，最多可接收三条put消息
q.put("消息1") 
q.put("消息2")
print(q.full())  #False
q.put("消息3")
print(q.full()) #True

#因为消息列队已满下面的try都会抛出异常，第一个try会等待2秒后再抛出异常，第二个Try会立刻抛出异常
try:
    q.put("消息4",True,2)
except:
    print("消息列队已满，现有消息数量:%s"%q.qsize())

try:
    q.put_nowait("消息4")
except:
    print("消息列队已满，现有消息数量:%s"%q.qsize())

#推荐的方式，先判断消息列队是否已满，再写入
if not q.full():
    q.put_nowait("消息4")

#读取消息时，先判断消息列队是否为空，再读取
if not q.empty():
    for i in range(q.qsize()):
        print(q.get_nowait())
```

### 生产者消费者模式

```python
import threading
from queue import Queue
import time


def producer():
    for i in range(20):
        queue.put(i)
        print('存入了商品{}'.format(i))
        time.sleep(0.5)


def cosumer():
    for i in range(10):
        p = queue.get()
        print('消费了商品{}'.format(p))
        time.sleep(0.5)


queue = Queue()
t1 = threading.Thread(target=producer)
t2 = threading.Thread(target=producer)

t3 = threading.Thread(target=cosumer)
t4 = threading.Thread(target=cosumer)
t5 = threading.Thread(target=cosumer)

t1.start()
t2.start()

t3.start()
t4.start()
t5.start()

```

### socket

发送数据

```python
import socket

s = socket.socket(socket.AF_INET, socket.SOCK_DGRAM)
s.sendto("= =".encode("utf-8"), ('10.11.55.223', 9000))

```

接收数据

```python
import socket

s = socket.socket(socket.AF_INET, socket.SOCK_DGRAM)

bind_addr = ("0.0.0.0", 8000)
s.bind(bind_addr)


data, addr = s.recvfrom(1024)
data = data.decode('utf-8')
print("IP:{},端口号：{}，发送来的信息：{}".format(addr[0], addr[1], data))

# s.close()

```

### TCP

发送数据

```python
import socket

s = socket.socket(socket.AF_INET, socket.SOCK_STREAM)

s.connect(('127.0.0.1', 9000))
s.send("123".encode('utf-8'))

print(s.recv(1024).decode('utf-8'))
s.close()


```

接收数据

```python
import socket

s = socket.socket(socket.AF_INET, socket.SOCK_STREAM)

s.bind(('0.0.0.0', 9000))

s.listen(128)
# result = s.accept()
# print(result)
client_socket, client_addr = s.accept()
msg = client_socket.recv(1024).decode('utf-8')
print(msg)

client_socket.send("gun".encode('utf-8'))

s.close()

```

### 客户端下载数据

文件下载客户端

```python
import socket

s = socket.socket(socket.AF_INET, socket.SOCK_STREAM)

file_name = input("请输入文件名：")
s.connect(('127.0.0.1', 9000))
s.send(file_name.encode('utf-8'))
content = b''
while True:
    msg = s.recv(1024)
    if not msg:
        break
    content += msg

with open('1.txt', 'wb') as file:
    file.write(content)
s.close()

```

文件下载

```python
import socket
import os

s = socket.socket(socket.AF_INET, socket.SOCK_STREAM)

s.bind(('0.0.0.0', 9000))
s.listen(128)
while True:
    client_socket, client_addr = s.accept()
    file_name = client_socket.recv(1024).decode('utf-8')
    if not os.path.exists(file_name):
        client_socket.send('对不起，你要下载的文件不存在'.encode('utf-8'))
    else:
        with open(file_name,'rb')as file:
            msg = b''
            while True:
                content = file.read(1024)
                msg += content
                if not content:
                    break
            client_socket.send(msg)
    client_socket.close()

```

### 实现通话性能

A

```python
import socket
import threading


def send_msg(udp_socket):
    """获取键盘数据，并将其发送给对方"""
    # 1. 从键盘输入数据
    msg = input("\n请输入要发送的数据:")
    # 2. 输入对方的ip地址
    dest_ip = input("\n请输入对方的ip地址:")
    # 3. 输入对方的port
    dest_port = int(input("\n请输入对方的port:"))
    # 4. 发送数据
    udp_socket.sendto(msg.encode("utf-8"), (dest_ip, dest_port))


def recv_msg(udp_socket):
    """接收数据并显示"""
    while True:
        # 1. 接收数据
        recv_msg = udp_socket.recvfrom(1024)
        # 2. 解码
        recv_ip = recv_msg[1]
        recv_msg = recv_msg[0].decode("gbk")
        # 3. 显示接收到的数据
        print(">>>%s:%s" % (str(recv_ip), recv_msg))


def main():
    # 1. 创建套接字
    udp_socket = socket.socket(socket.AF_INET, socket.SOCK_DGRAM)
    # 2. 绑定本地信息
    udp_socket.bind(("", 7890))

    # 3. 创建一个子线程用来接收数据
    t = threading.Thread(target=recv_msg, args=(udp_socket,))
    t.start()
    # 4. 让主线程用来检测键盘数据并且发送
    send_msg(udp_socket)

if __name__ == "__main__":
    main()

```

B

```python
import socket
import threading


def send_msg(udp_socket):
    """获取键盘数据，并将其发送给对方"""
    # 1. 从键盘输入数据
    msg = input("\n请输入要发送的数据:")
    # 2. 输入对方的ip地址
    dest_ip = input("\n请输入对方的ip地址:")
    # 3. 输入对方的port
    dest_port = int(input("\n请输入对方的port:"))
    # 4. 发送数据
    udp_socket.sendto(msg.encode("utf-8"), (dest_ip, dest_port))


def recv_msg(udp_socket):
    """接收数据并显示"""
    while True:
        # 1. 接收数据
        recv_msg = udp_socket.recvfrom(1024)
        # 2. 解码
        recv_ip = recv_msg[1]
        recv_msg = recv_msg[0].decode("gbk")
        # 3. 显示接收到的数据
        print(">>>%s:%s" % (str(recv_ip), recv_msg))


def main():
    # 1. 创建套接字
    udp_socket = socket.socket(socket.AF_INET, socket.SOCK_DGRAM)
    # 2. 绑定本地信息
    udp_socket.bind(("", 8000))

    # 3. 创建一个子线程用来接收数据
    t = threading.Thread(target=recv_msg, args=(udp_socket,))
    t.start()
    # 4. 让主线程用来检测键盘数据并且发送
    send_msg(udp_socket)

if __name__ == "__main__":
    main()

```



### pygame模块常用方法

import pygame
pygame.Rect（顶部坐标,长宽）                                  生成矩形

pygame.draw.rect（screen,填充颜色,生成的矩形）      绘制矩形

绘制直线
pygame.draw.line（screen,填充颜色,(起始像素点),(截止像素点)) 

绘制图形参数：
rect 矩形、polygon 多边形（三个及三个以上的边）、circle 圆、ellipse 椭圆、arc 圆弧、line 线、lines 一系列的线、aaline 一根平滑的线、aalines 一系列平滑的线

关闭窗口事件类型。 用常量 pygame.QUIT 来标识这种类型。如果 event.type == pygame.QUIT 为真的话，意味着程序收到了关闭窗口事件。代码1的第27行代码的作用是退出程序——这正是关闭窗口事件的响应处理。
键盘按下事件类型。 用常量 pygame.KEYDOWN 来标识这种类型。如果 event.type == pygame.KEYDOWN 为真的话，意味着程序收到了键盘上任意一个按键按下的事件。
键盘松开事件类型。 用常量 pygame.KEYUP 来标识这种类型。如果 event.type == pygame.KEYUP 为真的话，意味着程序收到了先前按下的键松开的事件。有人会问，为啥要区分按下和松开两种情形呢？这是为了达成精细的控制。我们的俄罗斯方块程序只需要响应键盘按下事件，但有的程序还需要响应按键松开事件。

### 函数变量作全局变量：

```python
def a():
    a.b = 10
    return a.b


print(a())
print(a.b)
```

#### zip

zip函数可以将两个列表或元组类型的数据变成和字典类型差不多的键值对，即第一个列表的第一个数对应第二个列表的第一个数

例：zip([123],[456])--->[(1,4),(2,5),(3,6)]