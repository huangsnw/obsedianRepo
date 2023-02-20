# Python解释器
## 源文件的字符编码
默认情况下，Python源文件的编码是UTF-8。如果不使用默认编码，则要声明文件的编码，文件的第一行要写成特殊注释。
```python
# -*- coding: encoding -*-
```
但是也有例外，如果第一行已经写了编译器配置，则将编码配置写在第二行。
```python
#!/usr/bin/env python3
# -*- coding: cp1252 -*-
```
# 变量和简单数据类型
Python的变量不需要预先声明。Python的变量在被使用时会有两个动作：一是开辟地址空间，二是赋予指定的变量值。在Python中，变量在指定的时，必须强制赋予初始值，否则就会报错。
## 变量的赋值
变量的命名规则和大多数的编程语言一样。
>单个变量赋值
```python
a="Hello World!"
```
>多个变量赋值
```python
a=b=c="Hello World!"

// 或者
a,b,c = 10,20,30
```
多个变量同时赋值时，在内存中会指向同一个地址，获取同一个值。
## 变量的类型
Python的变量类型只有在赋值之后才能被*隐性*确认。
Python的变量类型包括字符串（String）、数字（Numeric）、列表（List）、元组（Tuple）、
字典（Dictionary）五大类。
### 字符串
字符串（String）由单引号（' '）、双引号（" "）或者三引号（''' '''）组成。
⚠️三引号字符串可以保留格式。
>字符串值的读取
```python
a = "Hello World!"

# 读取下标
print(a[1])

# 切片 [1,2)
print(a[1:2])
print(a[:3])
print(a[3:])
print(a[1:-3])
```
>字符串值的合并
```python
first_name="San"
last_name="Zhang"
name=last_name+" "+first_name
print(name)
```
>字符串值修改
```python
str="Hello World!"
str_1=str[:6]
res=str_1+"世界！"
print(res)
```
字符串的值本身不能修改，但是可以使用切片对它进行拼接重组。
>字符串值的删除
```python
str="Hello World!"
del(str)
```
>获取字符串的长度
```python
str="Hello World!"
len(str)
```
>原始字符串
```python
str=r"Hi, I'm ZhangSan. \n \n"
print(str)
```
原始字符串会忽视转译符号。
>重复输出字符串
```python
str="Hahaha "
print(str*3)
```
>格式化字符串
```python
age=10
print("ZhangSan's age is %d"%(age))
```
|符号|描述|
|--|--|
|%C|格式化字符及其ASCII码|
|%s|格式化字符串|
|%d|格式化整数|
|%u|格式化无符号整型|
|%o|格式化无符号八进制数|
|%X|格式化无符号十六进制数|
|%X|格式化无符号十六进制数(大写)|
|%f|格式化浮点数字，可指定小数点后的精度|
|%e|用科学计数法格式化浮点数|
|%E|作用同%e，用科学计数法格式化浮点数|
|%g|%f和%e的简写|
|%G|%F和%E的简写|
|%p|用十六进制数格式化变量的地址|
### 数字和运算符
Python中数字又可分为整数（Integer）、浮点数（Float）、复数（Complex）、布尔（Boolean）。
算术运算符中需要注意的是，除法（/）、取模（%）、幂（\*\*）、取整数（//）。
Python中的布尔值使用*True*和*False*表示，也可以使用1和0标识，布尔值可以直接用于算术运算。
Python的逻辑运算符包括*and*、*or*和*not*。
身份运算符
1. `is`判断两个标识符号是不是引用自同一个对象；
2. `is not`判断两个标识符号不是引用自同一个对象；
## 数据类型转换
1. int()：将浮点数转化为整数，方式是舍弃小数部分；
2. float()：将整数转换为浮点数；
3. complex()：转换为复数；
4. str()：转换为字符串；
5. bin()：转换为二进制；
6. oct()：转换为八进制；
7. hex()：转换为十六进制；
8. chr()：把十进制转换为ASCII字符；
9. ord()：把ASCII字符转换为十进制；
# 条件分支与循环
## if条件分支
```python
a=3
if a>0 and a<3:
	print("A")
elif a==3:
	print("B")
else:
	print("C")
```
## while循环
```python
a=1
while a<10:
	print(a,end=" ")
	a+=1
```
## for循环
python的for循环遍历的是数值，想要遍历下标则可以使用`range(len(list))`的方式，遍历索引则可以使用函数`enumerate(iterable)`。
```python
list1=[1,2,3,4,5,6]
for a in list1:
	print(a,end=" ")
```
## 循环控制语句
1. break
2. continue
3. pass
## match语句
`match`在python 3.10之后才能使用
```python
def http_error(status):
	match status:
		case 400:
			return "Bad request"
		case 404:
			return "Not found"
		case 418:
			return "I'm a teapot"
		case _:
			return "Something's wrong with the internet"
```
`match`也可以使用多条件
```python
case 401 | 403 | 404:
    return "Not allowed"
```
# 列表与元组
列表（List）是一个可变序列。Python的列表元素可以是不同的元素。
```python
list1=[1,2,3,"Hello World",2.3,3.45]
```
List有以下的方法：
![Pasted image 20230102233919 列表的方法](https://article.biliimg.com/bfs/article/85540f2ce6f062bdbf9b48611c7827269e6cd8d3.png)
元组（Tuple）是一个不可改变的序列。Python同样允许元组有不同的元素。
```python
tu=(1,2,3,4,"123",4.56)
print(tu)
```
Tuple有以下的方法：
![[Pasted image 20230102234428 元组的方法.png]]
# 字典
字典（Dict）是可变的无序集合。
```python
dic = {"name":"张三","age":18,"address":"江苏省南京市"}
print(dic.get("name"))
```
Dictionary有以下方法：
![Pasted image 20230102234808 字典的方法](https://article.biliimg.com/bfs/article/475048c0f92bf65eb7857033a809100183c1e1ee.png)
字典的key要保持唯一性。
# 函数
## 各种类型的函数
>不带参数的函数
```python
def Print():
	return "Hello World!"

print(Print())
```
>带参数的函数
```python
def Add(a,b):
	return a+b
	
print("a + b = %d"%Add(10,20))
```
>函数文档
```python
def Add(a,b):
	"""This is a add function."""
	return a+b
```
>关键字参数
```python
def Add(a,b):
	return a+b

Add(a=1,b=2)
```
为了避免传值错误，可以指明参数。
>默认值
```python
def Add(a,b=10):
	return a+b

Add(1)
Add(1,2)
```
默认值可以省略传参，但是当传值后，默认值失效。
>不定长参数
```python
# 传递任意数量的参数
def Add(a, *b):
	for i in b:
		a+=i
	return a

print(Add(1,2,3,4,5,6))

# 传递任意数量的键值对
def Add(a, **b):
	print(a)
	print(b)
	
print(Add("Tom",age=18,gender="男"))
```
>传递元组、列表、字典
```python
# 列表
def Print(nameList):
	for i in nameList:
		print(i,end=" ")

Print(["Tom1","Tom2","Tom3","Tom4","Tom5"])

# 元组 
def Print(nameList):
	for i in nameList:
		print(i,end=" ")
		
Print(("Tom1","Tom2","Tom3","Tom4","Tom5"))

# 字典
def Print(key):
	print(key)
	
Print({"Name":"张三","Age":19})
```
## 值传递和引用传递
Python函数普通传值方式是值传递，而传递列表、字典则属于引用传递。
```python
# 值传递
def change(a):
	a+=1
	print("In function, value is: %d"%a)

a = 10
change(a)
print("Out function, value is: %d"%a)

# 引用传递
def change(a):
	for i in range(len(a)):
		a[i]+=10

a = [1,2,3,4,5]
change(a)
print(a)
```
## 变量的作用域
Python的变量作用于和其它语言一样，也可以分为全局变量（Global Variable）和局部变量（Local Variable）。
```python
a = 10

def change():
	b = 1
	b = a + b
	print(b)

change()
print(a)
```
上面的代码中，a为全局变量，b为局部变量。在函数`change()`不能修改全局变量a的值，只能使用它。b是局部变量，它的值可以在函数中进行修改。
全局变量默认只读，如果想要修改则需要声明为`global`。
```python
a = 10

def change():
	b = 1
	global a
	a = a + b
	print(b)
	
change()
print(a)
```
## 闭包
```python
i = 10

def change():
	j = 1
	def change_son():
		k = i + j
		return k
	return change_son()
	
print(change())
```
如果想要修改上述代码中k的值，则需要在`change_son()`方法中使用关键字`nonlocal`。
```python
i = 10

def change():
	j=1
	def change_son():
		nonlocal j
		j = i + j
		return j
	return change_son()

print(change())
```
## 匿名函数
Python使用lambda来创建匿名函数。
```python
a1=lambda a,b:a+b
print(a1(1,2))
```
# 类
## 创建类
```python
class Car():
	# 构造函数
	def __init__(self):
		self.name = "宝马mini"
		self.color = "Green"
		self.price = "20w"

	# 类函数，想要被实例调用，必须有self
	def toString(self):
		print(self.name,self.color,self.price)
		
c = Car()
c.toString()
```
和Java不一样，Python类的属性是在构造函数`_init_()`里面创建的。
当然，也可以在创建实例的时候定义。
```python
class Car():
	def __init__(self,name,color,price):
		self.name=name
		self.color=color
		self.price=price
		
	def toString(self):
		print(self.name,self.color,self.price)

c = Car("1","2","3")
c.toString()
```
## 属性值修改
可以直接使用属性修改，也可以使用类里的函数修改。
```python
class Car():
	def __init__(self,name,color,price):
		self.name=name
		self.color=color
		self.price=price

	def toString(self):
		print(self.name,self.color,self.price)

	def setColor(self,color):
		self.color=color

c = Car("1","2","3")
c.name="哪吒汽车"
c.setColor("五颜六色")
c.toString()
```
类的组合关系可以这么写：
```python
class Wheel():
	def __init__(self,size):
		self.size=size

	def toString(self):
		print(self.size)

class Car():
	def __init__(self,name,color,price,wheel):
		self.name=name
		self.color=color
		self.price=price
		self.wheel=wheel

	def toString(self):
		print(self.name,self.color,self.price,self.wheel.size)

	def setColor(self,color):
		self.color=color

wheel=Wheel(10)
car=Car("小鹏汽车", "蓝色", 2200000, wheel)
car.toString()
```
## 继承
```python
# 父类
class People():
	def __init__(self,name):
		self.name=name
	
	def toString(self):
		print(self.name)
	
	def P(self):
		print("Print str: %s"%(self.name))

# 子类
class Student(People):
	def __init__(self,name,age):
		# super().__init__(name)
		self.name=name
		self.age=age

	def toString(self):
		print(self.name,self.age)

s=Student("张三", 10)
s.toString()
s.P()
```
若父类构造函数有参数，则在子类的构造函数要写父类的属性。
在子类构造函数里可以使用`super()`函数，实现父类和子类的关联。
Python可以实现多级继承。
子类可以重写父类的函数。
## 私有
Python的私有属性是在属性前面使用`__`表示。
```python
class Car():
	def __init__(self,name,address):
		self.name=name
		self.__address=address

	def toString(self):
		print(self.name,self.__address)

c=Car("宝马","中国")
c.toString()
```
## 静态类
可以创建实例的类是*动态类*，不支持创建实例的类是*静态类*。
>静态类和动态类的区别
1. 静态类内部没有`self`关键字，也就是不能被实例化；
2. 静态类不能通过类名传递参数；
3. 静态类不支持`__init__()`初始化函数；
4. 静态类不能被真正实例化，但它可以集成变量或函数，是一个带结构的数据类型。
```python
class StaticCar():
	name="宝马"
	color="绿色"
	
	def a():
		print(StaticCar().name,StaticCar().color)
		
StaticCar.a()
```
# 标准库
## Python标准知识库
### datetime
```python
from datetime import *

t = datetime.now()
print("当天时间和日期",t)
print("当天日期",datetime.date(t))
print("当天时间",datetime.time(t))
print("格式化时间",datetime.ctime(t))
print("UTC时间",datetime.utcnow())
print("时间戳",datetime.timestamp(t))
# 等等 
```
### math
```python
from math import *
```
### random
```python
from random import *
```
### os
```python
from os import *
```
### sys
```python
from sys import *
```
### time
```python
from time import *
```
# 异常
## 捕获异常
```python
try:
	# 代码块
except:
	# 代码块
finally:
	# 代码块
```
## 抛出异常
```python
raise ValueError
```
# 文件处理
没有写。
# 线程和进程
Python多线程模块包括`_thread`、`threating`、`queue`模块等。
`_thread`在3.X被放弃了，取而代之的是`threating`。
>示例
```python
#!/usr/bin/env python3
# -*- coding: UTF-8 -*-
import time
import threading
  
class MyThread(threading.Thread):
	def run(self):
		for i in range(5):
		print('thread {}, @number: {}'.format(self.name, i))
		time.sleep(1)

	def main():
		print("Start main threading")
		# 创建三个线程
		threads = [MyThread() for i in range(3)]
		# 启动三个线程
		for t in threads:
			t.start()
		print("End Main threading")

if __name__ == '__main__':
	main()
```










# 测试和打包