# List

Python内置的一种数据类型是列表：list。list是一种有序的集合，可以随时添加和删除其中的元素。list中的元素可以是不同类型
增删改查
```
list1=[1,2,3,4,5]
print("list1: " , list1[3])

print(list1)
print(len(list1))

#最后一个
print(list1[-1])
print(list1[-2])

# 增加
list1.append("123")
print(list1)

list1.insert(2,"admin")
print(list1)

# 删除最后一个
list1.pop()
print(list1)
# 指定删除
list1.pop(3)
print(list1)
# 更新
list1[3]='3333'
print(list1)

list1[3]=['23',45, "abc"]
print(list1)

p3=['23',45, "abc","ABC"]
list1[3]=p3
print(list1)

```

## 列表生成器
```
# list内置函数
L1= list(range(1,11))
print(L1)

# 生成[1x1, 2x2, 3x3, ..., 10x10]list
# 1 循环
L2=[]
for x in range(1,11):# 生成[1x1, 2x2, 3x3, ..., 10x10]
    L2.append(x*x)
print(L2)

# 2 使用生成器,语法[语句] 非常简洁
L3 = [x*x for x in range(1,11)]
print(L3)

# 加入判断 生成偶数平方
L4 = [ x*x for x in range(1,11) if x % 2 == 0 ]
print(L4)

# A B C 与 X Y Z 的全排列
L5 = [m + n  for m in 'ABC'  for n in 'XYZ' ]
print(L5)
# ['AX', 'AY', 'AZ', 'BX', 'BY', 'BZ', 'CX', 'CY', 'CZ']

# 使用dict类型制作list
d = { 'a':'A','b':'B','c':'C'}
L6 =[ x+'='+ y for x,y in d.items()]
print(L6)

# 使用函数
L7 = ['Hello', 'World', 'IBM', 'Apple']
print([s.lower() for s in L7])

# 判断,是字母转小写,组成新的list
x = 'abc'
y = 123
# isinstance 函数
print(isinstance(x, str))
print(isinstance(y, str))

L8 = ['Hello', 'World', 18, 'Apple', None]
print([s.lower() for s in L8 if isinstance(s,str)])
```


