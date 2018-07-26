---
layout:     post
title:      Python Foundation (syntax)
subtitle:   Python Foundation
date:       2018-07-26
author:     Allen
catalog: true
tags:
    - Python Foundation
---

## python概述
## 基础语法
## 项目实践
---


### 1. Python概述
- 一种面向对象的解释型计算机程序设计语言
- 具有丰富且强大的内置库和第三方库
- 语法简洁灵活
- 开源、跨平台

#### 应用场景：
- 数据分析
- 人工智能
- 网络爬虫
- 自动化运维
- Web 开发


### 2. python的基础语法


- 开发流程
1. ##### 创建以.py结尾的python文件
2. ##### 在python文件中输入打印'hello world'的代码（这里的标点可以是单引号或双引号，注意的是要求半角符号[英文输入法情况]，不是全角[中文输入法情况]）
3. ##### 运行编写完的python代码文件

- 使用Pycharm创建Python项目
- 如果做数据可视化测试也可以使用anaconda中的notebook

### 3. 注释
- ##### 使用注释的原因
希望通过自己的语言来描述一段代码的实现逻辑和功能，方便理解代码，易于维护

实例1：
```
#打印hello world
print('hello world')
```

##### 单行注释
以#开头，只注释一行，多行注释需要在需要注释的内容开头分别添加

(诀窍，把多行代码选中，ctrl+/ 可以直接多行注释#)

实例2：
```
##打印hello world
#习惯输入空格，不要让代码挨的太近，不便于观察
print ('hello world')
```

##### 多行注释
'''注释内容'''或者"""注释内容"""，可以对多行内容整体进行注释

实例3:
```
"""
注释内容
"""

'''
注释内容
'''

#以上两种方法都可以对多行进行注释
```

##### 注释的作用
描述一段代码的实现逻辑和功能，增强代码可读性，易于维护

##### 注意
注释在代码执行过程中不会被执行，注释数量没有限制

### 4. 变量
#### 4.1 变量的定义
在python中，变量指向各种类型值的名字，当用到这个类型的值时，直接使用变量即可，不需要再写具体的值

格式：变量名 = 数值/字符串

实例4：
```
a = 100
b = 200 
c = a + b
print(c)

m = 'hello'
n = 'world'
q = m + n 
print(q)
```
结果：
```
300

'hello world'

```
- 变量的类型不需要显示指定，python解释器会自动判断数据类型，可以把任意数据类型赋值给变量（意思就是说，不用指定变量的类型，python解释器会自动判断）
- 变量名称命名简介明了，见名知意（意思就是说取变量名的时候最好用英文来当，最好是有实际意义的，这样阅读代码的时候可以知道变量的含义，如果需要，可以加以注释)
- 使用type(变量)查看变量类型

实例5：
```
#打印个人信息
name = 'zhangsan'    #名字--字符串
high = 180           #身高--数值型
weight = 20.0          #体重--数值型

#输入数值并且输出类型
print(name)
print(type(name))
print(high)
print(type(high))
print(weight)
print(type(weight))
```
结果：

```
zhangsan
<class 'str'>
180
<class 'int'>
20.0
<class 'float'>

##更多的数据类型，见下图
```

### 5. input输入、print输出

#### 5.1 Input()用于在程序中执行过程中接收用户输入的内容，默认接收的输入内容为字符串类型。

实例6：
```
card_id = input("请输入卡号:")
pwd = input("请输入密码:")

print(card_id)
print(type(card_id))
print(pwd)
```
结果：
```
请输入卡号:123
请输入密码:123
123
<class 'str'>
123

```

#### 5.2 print()用于在程序执行过程中输入内容
- 直接输出内容
- 输出单个和多个变量
- 格式化输入
- 格式化输出应用示例:print('你输入的名字是：%s'%name) 或者print('你输入的名字是{}。'.format(name))

实例7:
```
name = input()
print('你输入的名字是：%s'%name)
print('你输入的名字是：{}。'.format(name))
```
结果：
```
zhangsan 
你输入的名字是：zhangsan 
你输入的名字是：zhangsan 。

#常用的格式符号见下图
```
#常用的格式化符号有 %d，%s，%f

实例8:
```
#多个变量同时输出
card_id = "234567"
pwd = 123
#\n是换行符
print("您输入的卡号是：%s，\n您输入的密码是：%d" %(card_id,pwd))

print('====分割线====')
print('您输入的卡号是：{},\n您输入的密码是：{}'.format(card_id,pwd))
```
结果：
```
您输入的卡号是：234567，
您输入的密码是：123
====分割线====
您输入的卡号是：234567,
您输入的密码是：123

```
实例9：
```
#格式化输出浮点数,并指定精度
height = 180.35234
print("您的身高是：%.2f cm" %height)
print('您的身高是：{:.2f} cm'.format(height))
```

结果：

```
您的身高是：180.35 cm
您的身高是：180.35 cm

```
实例10：
```
#格式化输出时，打印%，要使用%%表示是字符串而不是转换说明符
p = 99.99321
print("您战胜了全国%.2f%%的用户" %p)
print('您战胜了全国{:.2f}的用户'.format(p))
```
结果：
```
您战胜了全国99.99%的用户
您战胜了全国99.99的用户

```
实例11：
```
#print无换行输出
print("hello",end="")
print("python")
```
结果：

```
hellopython

```

实例12：
```
#输出换行符
print("中国\n北京")
#转义字符\
print("中国\\n北京")
```
结果：
```
中国
北京
中国\n北京
```

### 6. 类型转换
#### 不同的类型之间进行转换

实例13：

```
a = 123
print(a)
print(type(a))
print('将int类型转换成字符型：')
b = str(a)
print(b)
print(type(b))

print('将int类型装换成浮点型')
c = float(a)
print(c)
print(type(c))
```
结果：
```
123
<class 'int'>
将int类型转换成字符型：
123
<class 'str'>
将int类型装换成浮点型
123.0
<class 'float'>
```





实例14：
```
#eval(str)把字符串自动转换成合适的数据类型
a1= eval("123")
a2 = eval("3.14")
print(type(a1))
print(type(a2))
```
结果：
```
<class 'int'>
<class 'float'>

```

### 7. 标识符、命名规则、关键字
#### 7.1 标识符
- 在python程序开发过程中，自定义的一些符号、名称
- 由字母、数字、下划线（_）组成，不能以数字开头
- 标识符区分大小写

实例15：
```
#不能以数字开头
2student = 'zhangsan'
print(2student)
#报错语法错误
```
结果：
```
  File "<ipython-input-15-978c7772c00c>", line 2
    2student = 'zhangsan'
           ^
SyntaxError: invalid syntax
```

实例16：
```
#python解释器是可以区分大小写的
student_name = 'zhangsan'
Student_name = 'lisi'
print(student_name)
print(Student_name)
```
结果：
```
zhangsan
lisi
```

#### 7.2 命名规则
- 见名如意，如name
- 驼峰命名法，如类名(UserInfo)、异常名(ValueError)等
- 小写字符+下划线，如变量名(user_name)、函数名(get_name)
- 不能使用关键字

#### 7.3 关键字
- 在python内部具有特殊功能的标识符
- 通过keyword模块的kwlist函数查看

实例17：
```
import keyword
#打印py3的关键字，命名是不能使用的
print(keyword.kwlist)
```
结果：

```

['False', 'None', 'True', 'and', 'as', 'assert', 'break', 'class', 'continue', 'def', 'del', 'elif', 'else', 'except', 'finally', 'for', 'from', 'global', 'if', 'import', 'in', 'is', 'lambda', 'nonlocal', 'not', 'or', 'pass', 'raise', 'return', 'try', 'while', 'with', 'yield']

```


### 8. 项目--计算器

实例18：
```
num1 = input("请输入第一个数字：")
operator = input("请输入运算符：")
num2 = input("请输入第二个数字：")

num_1 = int(num1)
num_2 = int(num2)

if operator == "+":
    result = num_1 + num_2
    print("计算结果：{}".format(result))
elif operator == "%":
    result = num_1 % num_2
    print("计算结果：{}".format(result))
elif operator == "**":
    result = num_1 ** num_2
    print("计算结果：{}".format(result))
elif operator == "//":
    result = num_1 // num_2
    print("计算结果：{}".format(result))
else:
    print("正在开发..")
```
