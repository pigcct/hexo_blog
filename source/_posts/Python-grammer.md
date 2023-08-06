---
title: Python基础语法
author: 苦逼小码农
tags:
  - 语法
categories:
  - Python
mathjax: true
date: 2023-05-16 14:36:27
---

# Python基础语法



## 1. 标识符，关键字和保留字

### 1.1 标识符

在 Python 中，标识符是用来给变量、函数、类等命名的。Python 中的标识符需遵循以下规则:

1. 标识符由字母、数字和下划线组成。
2. 标识符第一个字符必须是字母或下划线。
3. 标识符不能是 Python 的关键字（如：if、else、while 等）。
4. 标识符对大小写敏感，例如：age 和 Age 是两个不同的标识符。

例如，以下是有效的标识符：

```python
my_name
_name
name_1
value2
```

以下是无效的标识符：

```python
1name # 以数字开头
if # 是Python的关键字
my-name # 中间有横线
```



### 1.2 关键字

| False    | def     | if       | raise  |
| -------- | ------- | -------- | ------ |
| False    | def     | if       | raise  |
| None     | del     | import   | return |
| True     | elif    | in       | try    |
| and      | else    | is       | while  |
| as       | except  | lambda   | with   |
| assert   | finally | nonlocal | yield  |
| break    | for     | not      |        |
| class    | from    | or       |        |
| continue | global  | pass     |        |



### 1.3 保留字

Python 没有保留字（Reserved Words）的概念，但是有一些特殊用途的标识符，应当避免使用它们作为变量、函数名等标识符。这些特殊用途的标识符包括：

- `_`（单下划线）：一般用作临时变量、不重要的变量、表示国际化文本中的占位符等。
- `__`（双下划线）：用于类中的私有属性和方法，Python 会自动将属性名改为 `_类名__属性名` 的形式。
- `__xxx__`（双下划线开头和结尾）：Python 中的特殊方法，如 `__init__`、`__str__` 等。





## 2. 变量

### 2.1 定义变量

```python
变量名 = 值
eg ： a = 1
```

标识符命名规则是Python中定义各种名字的时候的统一规范，具体如下：

- 由数字、字母、下划线组成
- 不能数字开头
- 不能使用内置关键字
- 严格区分大小写

### 2.2 命名习惯

- 见名知义。
- 大驼峰：即每个单词首字母都大写，例如：`MyName`。
- 小驼峰：第二个（含）以后的单词首字母大写，例如：`myName`。
- 下划线：例如：`my_name`。



## 3. 数据类型

### 3.1 基础数据类型

{% asset_img 1.png %}

```python
# 这里介绍的是python中的数据类型
a = 1 # int 整形
b = 3.14 # float 浮点型
c = True # bool 布尔型
d = 'LOVE' # str 字符串
e = ['good'] # list 列表
f = (10, 20, 30) # tuple 元组
g = {'Tom'} # set 集合
h = {'name' : 'Tom', 'age' : '18'} # 字典

print(type(a))
print(type(b))
print(type(c))
print(type(d))
print(type(e))
print(type(f))
print(type(g))
print(type(h))
```

### 3.2 数据类型的转换

{% asset_img 3.png %}



**代码示例：**

```pytho
# python中数据的输入(input)
# python中输入的用户输入的数据都是当做字符串str来处理
password = input('请输入您的密码：')
print(f'您输入的密码是{password}')

print(type(password))  # 数据类型为：str
print(type(int(password))) # 将数据类型转换为 int型

list1 = [10, 20, 30] # 列表 list
print(list1)         # 列表 list [10, 20, 30]
print(tuple(list1))  # 元组 tuple (10, 20, 30)
print(set(list1))    # 集合 set  {10, 20, 30}
print(type(list1))   # 若未标明转换的数据类型，则仍然输出原始的数据类型
```





## 4. 运算符

### 4.1 算数运算符

> 💡 **混合运算优先级顺序：()高于 \** 高于 \* / // % 高于 + -**



{% asset_img 2.png%}

*** 这里是和C语言不同的算数运算符***

```python
x = 11 // 2  # 相当于int型的整数除法
y = 2 ** 4   # 这里是求2的4次方
print(x, y)
```

### 4.2 逻辑运算符

| 运算符 | 逻辑表达式 | 描述                                                     | 示例                                 |
| ------ | ---------- | -------------------------------------------------------- | ------------------------------------ |
| and    | x and y    | 布尔"与":如果×为False，x and y返回False，否则它返回y的值 | True and False，返回False。          |
| or     | x or y     | 布尔"与":如果×为False，x and y返回False，否则它返回y的值 | False or True，返回True。            |
| not    | not x      | 布尔"与":如果×为False，x and y返回False，否则它返回y的值 | not True返回False, not False返回True |

```python
# 多个变量赋值
um1, float1, str1 = 10, 0.5, 'hello world'
print(um1,  float1,  str1)

a = b = c = d = 10
print(a, b, c, d)

aa = 4
bb = 6
cc = 4
dd = 0
print(aa > bb)  # 输出False
print(aa == cc) # 输出True

# 逻辑运算 和(and)  或(or)
print(aa > bb) and (aa == cc) # 输出False
print(aa == cc) or (aa > bb)  # 输出True

print(aa and dd) # 不成立 输出0
print(aa and bb) # 成立 输出的是较大的数 bb = 6
print(aa or dd)  # 成立 输出的是较大的数 aa = 4
```

### 4.3 补充知识

**数字之间的逻辑运算**

```python
a = 0
b = 1
c = 2

# and运算符，只要有一个值为0，则结果为0，否则结果为最后一个非0数字
print(a and b)  # 0
print(b and a)  # 0
print(a and c)  # 0
print(c and a)  # 0
print(b and c)  # 2
print(c and b)  # 1

# or运算符，只有所有值为0结果才为0，否则结果为第一个非0数字
print(a or b)  # 1
print(a or c)  # 2
print(b or c)  # 1
```





## 5. 控制语句



### 5.1 while循环

```python
while 条件:
    条件成立重复执行的代码1
    条件成立重复执行的代码2
    ......
```

**示例代码：**

```python
# Python中的while循环
n = 10
while n:
    print("I'm a good boy")
    n -= 5
# 求1——100的累加和
i = 1
result = 0
while i <= 100:
    result += i
    i += 1

# 输出5050
print(result)
```





### 5.2 for循环

```cpp
# for循环
'''
(切记 " : " 这个符号)
for 临时存储变量 in 序列：
    if 条件 :
'''

str = 'Hello world'
for i in str:
    if i == 'l':
        continue
    print(i)
# 使用for循环遍历输出列表中的值
cars = ['bwn', 'audi', 'bens', 'toyota']

for car in cars:
    if car == 'bens':
        print(car.upper())
    else:
        print(car.title())
```

### 5.3 循环的嵌套

#### 5.3.1  while循环嵌套

```python
while 条件1:
    条件1成立执行的代码
    ......
    while 条件2:
        条件2成立执行的代码
        ......
```

**示例代码：**

```python
# 重复打印9行表达式
j = 1
while j <= 9:
    # 打印一行里面的表达式 a * b = a*b
    i = 1
    while i <= j:
        print(f'{i}*{j}={j*i}', end='\\t')
        i += 1
    print()
    j += 1
```





####  5.3.2 while…else…语句

> 💡 所谓else指的是循环正常结束之后要执行的代码，即如果是break终止循环的情况，else下方缩进的代码将不执行,都是continue语句结束可以执行else语句。

**语法：**

```python
while 条件:
    条件成立重复执行的代码
else:
    循环正常结束之后要执行的代码
```

**示例代码：**

```python
i = 1
while i <= 5:
    print('Hello World')
    i += 1
else:
    print('执行完毕')
```





#### 5.3.3  for…else… 语句

> 💡 所谓else指的是循环正常结束之后要执行的代码，即如果是break终止循环的情况，else下方缩进的代码将不执行,都是continue语句结束可以执行else语句。

**语法：**

```python
for 临时变量 in 序列:
    重复执行的代码
    ...
else:
    循环正常结束之后要执行的代码
```





### 5.4 跳出循环

> 💡  break和continue是循环中满足一定条件退出循环的两种不同方式。

```python
# break实例
i = 1
while i <= 5:
    if i == 4:
        print(f'吃饱了不吃了')
        break
    print(f'吃了第{i}个苹果')
    i += 1
```



## 6. 操作列表（数组）

```python
# python中的列表就相当于C语言中的数组
bicycles = ['trek', 'cannon dale', 'redline', 'specialized']
print(bicycles[0]) # 输出：trek
```



## 7. 字典（键值对）

### 7.1 字典的定义及字典元素的输出

> 💡 **在Python中键和值之间用冒号分隔，而键—值对之间用逗号分隔。**

```cpp
#字典就是给每个集合中的么个值一个关键字，简称键值对
girlfriend = {'tall' : 160, 'type' : 'cute'}

print(girlfriend['tall']) # 160
print(girlfriend['type']) # cute
```

**添加键值对**

```python
girlfriend = {'tall' : 160, 'type' : 'cute'}
print(girlfriend['tall'])
print(girlfriend['type'])

girlfriend['love'] ='DD' # 在字典的尾部添加一个键值对
girlfriend['intersted'] = 'aiai'# 字典的尾部插入一个键值对
print(girlfriend)
```

**创建一个新的字典**

```python
# 创建一个新的字典
boyfriend = {}
boyfriend['name'] = 'HCD'
boyfriend['fun'] = 'basketball'
print(boyfriend)
```

**修改字典中的值**

```python
boyfriend = {}
boyfriend['name'] = 'HCD'
boyfriend['fun'] = 'basketball'
print(boyfriend) # {'name': 'HCD', 'fun': 'basketball'}

# 修改字典中的值
boyfriend['fun'] = 'computer'
print(boyfriend) # {'name': 'HCD', 'fun': 'computer'}
```

**输出键值对（del语句）**

```python
# 删除键值对
boyfriend1 ={'name' : 'HCD', 'fun' : 'computer', 'type' : 'sun'}
del boyfriend1['fun'] # 删除使用 del 语句
print(boyfriend1) # {'name': 'HCD', 'type': 'sun'}
```

**类似对象组成的字典（方便观看和查找键值对）**

```python
# 类似对象的键值对
favorite_languages = {
    'jen': 'python',
    'sarah': 'c',
    'edward': 'ruby',
    'phil': 'python',
}

# jen favorite langeuages is Python.
print(f'jen favorite langeuages is '+ favorite_languages['jen'].title() + '.')
```

### 7.2 遍历字典

遍历字典需要使用for循环，需要声明两个变量，可用于作为存储键值对的关键字，for语句的第二部分包含字典名和方法items()，它返回一个键—值对列表。

```python
# 遍历字典的for循环方法（需要用到items()方法）
for 变量1, 变量2 in 字典名称 . items():
 # 这里是需要遍历的字典
favorite_languages = {
    'jen': 'python',
    'sarah': 'c',
    'edward': 'ruby',
    'phil': 'python',
}

# 遍历字典
for name, language in favorite_languages.items():
    print('\\nname : ' + name)
    print('language : ' + language)

# 下面是输出的语句
'''
name : jen
language : python

name : sarah
language : c

name : edward
language : ruby

name : phil
language : python
'''
```

**遍历字典中的所有键（ key()方法 ）**

```python
 # 这里是需要遍历的字典
favorite_languages = {
    'jen': 'python',
    'sarah': 'c',
    'edward': 'ruby',
    'phil': 'python',
}

# 遍历字典中的所有键
for name in favorite_languages.keys():
    print(name.title())

# 输出
'''
Jen
Sarah
Edward
Phil
'''
```

**按顺序遍历字典中的所有键**

要以特定的顺序返回元素，一种办法是在for循环中对返回的键进行排序。为此，可使用函数sorted()来获得按特定顺序排列的键列表的副本。

```python
# 这里是需要遍历的字典
favorite_languages = {
    'jen': 'python',
    'sarah': 'c',
    'edward': 'ruby',
    'phil': 'python',
}

# 按顺序遍历字典中的所有键
for name in sorted(favorite_languages.keys()):
print(name.title())

# 输出
'''
Edward
Jen
Phil
Sarah
'''
```

**遍历字典中的所有值（ values()方法 ）**

```python
 # 这里是需要遍历的字典
favorite_languages = {
    'jen': 'python',
    'sarah': 'c',
    'edward': 'ruby',
    'phil': 'python',
}

# 遍历字典中的所有值
for value in favorite_languages.values():
    print(value.title())

# 输出
'''
Python
C
Ruby
Python
'''
```

> 💡 **有时候，需要将一系列字典存储在列表中，或将列表作为值存储在字典中，这称为嵌套。**

**在列表中存储字典**

```python
# 嵌套
alien_0 = {'color': 'green', 'points': 5}
alien_1 = {'color': 'yellow', 'points': 10}
alien_2 = {'color': 'red', 'points': 15}

aliens = [alien_0, alien_1, alien_2] # 将字典存储到列表中

for alien in aliens: # 输出列表中的所有字典
     print(alien)
```

**在字典中存储列表**

```python
# 在字典中存储列表
favorite_languages = {
'jen': ['python', 'c'],
'sarah': ['c'],
'edward': ['ruby', 'go'],
'phil': ['python', 'vue'],
}

for name, language in favorite_languages.items():
    print("\\n" + name.title() + " is favorite languages1 are: ")

    for food in language:
        print('\\t The favorite language2 is : ' + food.title())

'''
Jen is favorite languages1 are: 
	 The favorite language2 is : Python
	 The favorite language2 is : C

Sarah is favorite languages1 are: 
	 The favorite language2 is : C

Edward is favorite languages1 are: 
	 The favorite language2 is : Ruby
	 The favorite language2 is : Go

Phil is favorite languages1 are: 
	 The favorite language2 is : Python
	 The favorite language2 is : Vue

进程已结束,退出代码0
'''
```

### 





