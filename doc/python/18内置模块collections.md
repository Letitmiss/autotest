# 内置模块collections
*  模块实现了特定目标的容器，以提供Python标准内建容器 dict , list , set , 和 tuple 的替代选择
   https://docs.python.org/zh-cn/3.8/library/collections.html
   

## namedtuple() 命名元组的工厂函数

### collections.namedtuple(typename, field_names, *, rename=False, defaults=None, module=None) 
* 返回一个新的元组子类，名为 typename 。这个新的子类用于创建类元组的对象，可以通过域名来获取属性值，同样也可以通过索引和迭代获取值。
 
 ```
from collections import namedtuple
Point = namedtuple('Point',['x','y'])
p = Point(11,22)
print(p.x + p.y) # 33
print(p)  # Point(x=11, y=22)
print(isinstance(p,tuple)) # true

#list赋值
p2=Point._make([11,22])
print(p2)
print(isinstance(p2,tuple))

#属性赋值
print(Point(x=10,y=20))
 
 ```
 * namedtuple是一个函数，它用来创建一个自定义的tuple对象，并且规定了tuple元素的个数，并可以用属性而不是索引来引用tuple的某个元素。

## deque 对象

### class collections.deque([iterable[, maxlen]])

* 返回一个新的双向队列对象，从左到右初始化(用方法 append()) ，从 iterable （迭代对象) 数据创建,如果 iterable 没有指定，新队列为空,
* Deque 支持线程安全，内存高效添加(append)和弹出(pop)，从两端都可以
* 如果 maxlen 没有指定或者是 None ，deques 可以增长到任意长度。否则，deque就限定到指定最大长度。一旦限定长度的deque满了，当新项加入时，同样数量的项就从另一端弹出。

```
from collections import namedtuple,deque


d = deque('abc')
print(d)
for x in d:
    print(x.upper())
# 左右添加
d.append('x')
d.appendleft('y')
print(d) #  deque(['y', 'a', 'b', 'c', 'x'])
# 出队列
print(d.pop()) # x 默认右边出,
print(d)  # deque已经变化 
print(d.popleft())  # y 左边出 

print(list(d)) #  ['a', 'b', 'c']

# 查看最左端的
print(d[0])  # a
# 查看最右端 
print(d[-1]) # c
# 翻转获得新的list 
print(list(reversed(d)))  # ['c', 'b', 'a']

if 'c' in d :
    print('ok')  # ok

d.extend('xyz') 
print(d) # # deque(['a', 'b', 'c', 'x', 'y', 'z'])

d.extendleft('qwe')
print(d)  #  deque(['e', 'w', 'q', 'a', 'b', 'c', 'x', 'y', 'z'])

d.append('nn')
d.appendleft('mm')
print(d)  # deque(['mm', 'e', 'w', 'q', 'a', 'b', 'c', 'x', 'y', 'z', 'nn'])
```

## defaultdict 
* `class collections.defaultdict([default_factory[, ...]])` 第一个参数 default_factory 提供了一个初始值,它默认为 None ,所有的其他参数都等同与 dict 构建器中的参数对待，包括关键词参数。
* 属性 `__missing__(key)` , 如果查询key失败,dict的 `__getitem__()被调用, getitem方法会调用__missing__(key)`,如果 default_factory 是 None ，它就返回一个 KeyError 并将 key 作为参数。如果 default_factory 不为 None ， 它就会会被调用，不带参数，为 key 提供一个默认值， 这个值和 key 作为一个对被插入到字典中，并返回。

```
from collections import namedtuple,deque,defaultdict

d = defaultdict(lambda: 0)
d['key']='abc'
print(d['key'])
# key不存在,默认值
print(d['ad'])
print(d)

s = [('yellow', 1), ('blue', 2), ('yellow', 3), ('blue', 4), ('red', 1)]

# list 作为 default_factory
d = defaultdict(list)
for k,v in s:
    d[k].append(v)

print(d)   # defaultdict(<class 'list'>, {'yellow': [1, 3], 'blue': [2, 4], 'red': [1]})
print(sorted(d.items())) # [('blue', [2, 4]), ('red', [1]), ('yellow', [1, 3])]
# 每个键第一次遇见时，它还没有在字典里面；所以条目自动创建，通过 default_factory 方法，并返回一个空的 list ,
# list.append() 操作添加值到这个新的列表里, 当下次调用的时候,正常取用操作

# 验证 key不存在事 返回一个空list
print(d['gray'])

# 设置int为 default_factory, 可以用来计数
s = 'mississippi'
d = defaultdict(int)
for k in s:
    d[k] += 1
print(sorted(d.items()))  # [('i', 4), ('m', 1), ('p', 2), ('s', 4)]

```

##  OrderedDict

