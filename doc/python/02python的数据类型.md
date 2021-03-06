# 基础数据类型

## 数字类型
* 整数    
  所有自然整数,有正负之分
* 浮点数   
  小数, 浮点数不是精确的
注意: python的数字没有位数的大小限制
* 复数     
* 文档    
  https://docs.python.org/zh-cn/3.8/library/stdtypes.html#typesnumeric
```
# 计算实例
print(2+2)
print(8/5)  #  1.6
print( (50 - 5*6) / 4) #  /运算返回浮点数5.0
# 取整(向下取整)
print(8 // 5)  #  1.6输出 1
print( -8 // 5) # -1.6 取整 -2
# 取余数
print(8%5)   # 输出3
## 乘方
print(3 ** 3)  # 3的3次方 27

```
## 字符串类型

字符串是以单引号'或双引号"括起来的任意文本，比如'abc'，"xyz"等等。请注意，''或""本身只是一种表示方式，不是字符串的一部分，因此，字符串'abc'只有a，b，c这3个字符。如果'本身也是一个字符，那就可以用""括起来，比如"I'm OK"包含的字符是I，'，m，空格，O，K这6个字符。    
字符串类型, 是不可变的变量

```
print(100)
print(100+200)
print(100-200)
print("I'm OK")
print('my name is "cong"')
```
* 字符串编码问题   
在文件开始, 设置UTF-8
```
#!/usr/bin/env python3
# -*- coding: utf-8 -*-
```
## 布尔数据类型

只有True和False ,注意这里首字母大写  
布尔值有 and or not 三种运算 ,这是逻辑基础
```
print(2 > 3)  # False
print(5 > 3)  # True
print( 2>3 and 5>3) # False

print(True)  #True
print(True+1)  # 2 True是1
print(False+1)  # 1 False是0
```

## 空值

None是特殊的空值,是特殊的变量

## 变量 

变量的概念基本上和初中代数的方程变量是一致的，只是在计算机程序中，变量不仅可以是数字，还可以是任意数据类型。
a = 'ABC' 的解释:
1. 在内存中创建了一个'ABC'的字符串；
2. 在内存中创建了一个名为a的变量，并把它指向'ABC'。
```
a = 'ABC'
b = a
a = 'XYZ'
print(b)  # 输出ABC, 变量之间赋值传递的引用变量
```
# 常量

一般固定不变量,变量名大写 


# 输出格式化

一个常见的问题是如何输出格式化的字符串。我们经常会输出类似'亲爱的xxx你好！你xx月的话费是xx，余额是xx'之类的字符串，而xxx的内容都是根据变量变化的，所以，需要一种简便的格式化字符串的方式, 在Python中，采用的格式化方式和C语言是一致的，用%实现

占位符	替换内容    
%d	   整数    
%f	   浮点数   
%s	  字符串   
%x	   十六进制整数    
```
name='mama'
print('Hello %s' %name)

print('Hello %s' %'world')

age=18
address='china'
print('Hello %s, age is  %d , address %s !' %(name,age,address))

name = 'abc'

print(f'hello {name}')

a=123.456
print('num is %.2f' %a)

#字符串乘以数字
b = 'qwer'
c = b*20
print(b*2)
print(c)
```

##  类型检查

* type 函数
```
a = 123
b = '123'
c = True
print(a)
print(b)

print(type(a))
print(type(b))
print(type(c))
```

