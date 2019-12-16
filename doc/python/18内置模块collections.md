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
# 如果key值没有,就会int() 返回0, 还可以使用lambda表达式,这样可以morning返回值; 
```

##  OrderedDict

* OrderedDict 旨在擅长重新排序操作,空间效率、迭代速度和更新操作的性能是次要的, OrderedDict 可以比 dict 更好地处理频繁的重新排序操作
* OrderedDict 排序测试不是按照key排序的,而是按照插入顺序排序的
* OrderedDict 类的 popitem(last=True), true为LIFO 后进先出 , false FIFO 先进先出
* OrderedDict 类有一个 move_to_end() 方法， `move_to_end(key, last=True) ` 可以有效地将元素移动到任一端,true末端, false 顶端
* Python 3.8之后， 有了 `__reversed__()` 方法。

```
from collections import OrderedDict

d = dict([('a', 1), ('b', 2), ('c', 3),('d', 4), ('e', 5), ('f', 6)])
print(d)

ordered_dict = OrderedDict(d)

ordered_dict['x'] = 11
ordered_dict['y'] = 22
print(ordered_dict) # 默认往后添加

# 更新一个dict,如有有key存在,就更新,并且则插入位置移动至末尾,key不存在就直接插入
class LastUpdateOrderDict(OrderedDict):

    def __setitem__(self,key,value):
        super().__setitem__(key,value)
        self.move_to_end(key)
    def get_item_LIFO(self):
        return self.popitem(True)
    def get_item_FIFO(self):
        return self.popitem(False)
myDict = LastUpdateOrderDict([('a', 1), ('b', 2), ('c', 3)])
myDict['x']=5
print(myDict)
# LastUpdateOrderDict([('a', 1), ('b', 2), ('c', 3), ('x', 5)])
myDict['b'] = 10
print(myDict)
#  LastUpdateOrderDict([('a', 1), ('c', 3), ('x', 5), ('b', 10)])

# LIFO
print(myDict.get_item_LIFO()) # ('b', 10)
print(myDict.get_item_LIFO()) # ('x',5)

# FIFO
print(myDict.get_item_FIFO())  # ('a', 1)

```

## ChainMap

* ChainMap可以把一组dict串起来并组成一个逻辑上的dict,ChainMap本身也是一个dict，但是查找的时候，会按照顺序在内部的dict依次查找, 但是更新的的时候,只更新第一个链
* 文档https://docs.python.org/zh-cn/3.8/library/collections.html#collections.ChainMap
* 应用场景 : 应用程序往往都需要传入参数，参数可以通过命令行传入，可以通过环境变量传入，还可以有默认参数。我们可以用ChainMap实现参数的优先级查找，即先查命令行参数，如果没有传入，再查环境变量，如果没有，就使用默认参数。

```
from collections import ChainMap
import os,argparse

# 构造缺省参数:
defaults = {
    'color': 'red',
    'user': 'guest'
}

# 构造命令行参数:
parser = argparse.ArgumentParser()
parser.add_argument('-u', '--user')
parser.add_argument('-c', '--color')
namespace = parser.parse_args()
command_line_args = { k: v for k, v in vars(namespace).items() if v }

# 组合成ChainMap:
combined = ChainMap(command_line_args, os.environ, defaults)
# 没有参数,打印默认值
print('color=%s' % combined['color'])
print('user=%s' % combined['user'])

# python hello.py -u tom
#color=red
#user=tom

```

## counter对象

* 计数器对象, dict的子类,计算元素出现的次数,分组统计的概念
```
from collections import Counter
# collections.Counter([iterable-or-mapping])
# 创建空
c = Counter()
# 字符串分组计数
c = Counter('gallahad')
print(c)  #  Counter({'a': 3, 'l': 2, 'g': 1, 'h': 1, 'd': 1})
c = Counter({'red': 4, 'blue': 2})
print(c)
c = Counter(cats=4, dogs=8)
print(c)


c = Counter(['red', 'blue', 'red', 'green', 'blue', 'blue'])
print(c)  #  Counter({'blue': 3, 'red': 2, 'green': 1})

# elements() # 按照首次出现的顺序排列
print(list(c.elements()))  # ['red', 'red', 'blue', 'blue', 'blue', 'green']

#设置一个计数为0不会从计数器中移去一个元素。使用 del 来删除它:
c['red']=0  
print(c)   # Counter({'blue': 3, 'green': 1, 'red': 0})
del c['red']
print(c)   # Counter({'blue': 3, 'green': 1})

```


