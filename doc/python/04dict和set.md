# dict和set数据结构

## dict
Python内置了字典：dict的支持，dict全称dictionary，在其他语言中也称为map，使用键-值（key-value）存储，具有极快的查找速度。
* dict内部存放的顺序和key放入的顺序是没有关系的。
* 需要牢记的第一条就是dict的key必须是不可变对象,在Python中，字符串、整数等都是不可变的，因此，可以放心地作为key。而list是可变的，就不能作为key.
```
#key-value数据结构
d1={'tom':75,'Bob':80,'Lisa':90}
print(d1)

print(d1['tom']) #输出value 75

# key不能重复会覆盖
d1['tom']=80
print(d1['tom'])

# key 不存在会报错
#print(d1['name'])

#判断是否存在
print('tom' in d1)

# get取值
print(d1.get('Bob'))
# 不存在,制定默认值
print(d1.get('John',-1))

#增加
d1.update(c=66)
print(d1)

#删除key
d1.pop('c')
print(d1)

key='abc'
value='ABC'
d1[key]=value
print(d1)

key2=[1,2]
d1[key2]=['a','b']
print(d1)
# TypeError: unhashable type: 'list' 抛出异常
```
## 创建dict的方式

* 创建方式,有四种    
  class dict(**kwarg)    
  class dict(mapping, **kwarg)      
  class dict(iterable, **kwarg)   
```
a = dict(one=1, two=2, three=3)
b = {'one': 1, 'two': 2, 'three': 3}
c = dict(zip(['one', 'two', 'three'], [1, 2, 3]))
d = dict([('two', 2), ('one', 1), ('three', 3)])
e = dict({'three': 3, 'one': 1, 'two': 2})
a == b == c == d == e
```
## dict数据结构更多方法

* 官方文档 : https://docs.python.org/zh-cn/3.8/library/stdtypes.html?highlight=dict#mapping-types-dict
