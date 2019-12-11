# Iterator与Iterable

## iterable
* 具体应该叫做可迭代对象,他的特点其实就是我的序列的大小长度已经确定了(list,tuple,dict,string等)。他遵循可迭代的协议,可以被for循坏
* 通过 `isinstance(x, A_tuple)` 判断是不是iterable   
  含__iter__()方法
## iterator:
* 具体应该叫做迭代器的对象。他的特点就是他不知道要执行多少次，所以可以理解不知道有多少个元素，每调用一次__next__()方法，就会往下走一步，当然是用__next__()方法只能往下走，不会回退。是惰性的。这样我可以存很大很大的数据，即使是整个自然数，也可以很轻松的用迭代器来表示出来
  含__iter__()方法   
  含__next__()方法
* Python的Iterator对象表示的是一个数据流，Iterator对象可以被next()函数调用并不断返回下一个数据，直到没有数据时抛出StopIteration错误,Iterator的计算是惰性的，只有在需要返回下一个数据时它才会计算.
```
from collections.abc import Iterator
L1 = (x*x for x in range(10)) # 生成器generator对象
L2 = [x*x for x in range(10)] # 列表生成式
print(L1)
print(L2)
print(isinstance(L1,Iterator)) # True
print(isinstance(L1,Iterable)) # True

print(isinstance(L2,Iterator)) # False
print(isinstance(L2,Iterable)) # True

t = (1,2,3)
print(isinstance(t,Iterator)) # False
print(isinstance(t,Iterable)) # True

d = { 'name':'123','age': 10}
print(isinstance(d,Iterator)) # False
print(isinstance(d,Iterable)) # True

a = 'adcd'
print(isinstance(a,Iterator)) # False
print(isinstance(a,Iterable)) # True

```
*  生成器都是Iterator对象，但list、dict、str虽然是Iterable，却不是Iterator

## 关系
* iterator继承iterable, Iterable可以通过iter()转换获得一个迭代器Iterator
```
L3=[1,2,3,4]
#L3.__next__() 没有这个方法
# 转换
L3_iterator=iter(L3)
print(type(L3_iterator))
print(L3_iterator.__next__()) # 1
print(L3_iterator.__next__()) # 2
print(L3_iterator.__next__()) # 3 

# 循环的区别
L4=[1,2,3,4]
for x in L4:
    print("第一次print",x)
for x in L4:
    print("第二次print",x)

L4=[1,2,3,4]
L4_iterator=iter(L4);

for x in L4_iterator:
    print("第一次print iterator",x)
for x in L4_iterator:
    print("第二次print iterator ",x)
```



