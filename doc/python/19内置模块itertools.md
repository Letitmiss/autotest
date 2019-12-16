# itertools

* itertools模块提供的全部是处理迭代功能的函数，它们的返回值不是list，而是Iterator，只有用for循环迭代的时候才真正计算。
* 文档 https://docs.python.org/zh-cn/3.8/library/itertools.html


```
import itertools
# 无限迭代器,
#itertools.count(start=0, step=1)
count = itertools.count(1)
for n in count:
    print(n)

# itertools.cycle(iterable)
# 创建一个迭代器，返回 iterable 中所有元素并保存一个副本。当取完 iterable 中所有元素，返回副本中的所有元素。无限重复

cycle = itertools.cycle('ABCDEF')
for c in cycle:
    print(c)

#itertools.repeat(object[, times])
# repeat()负责把一个元素无限重复下去，不过如果提供第二个参数就可以限定重复次数：
ns = itertools.repeat('A', 3)
for n in ns:
    print(n)

# chain()
# chain()可以把一组迭代对象串联起来，形成一个更大的迭代器：
for c in itertools.chain('ABC', 'XYZ'):
    print(c)  # 'A' 'B' 'C' 'X' 'Y' 'Z'

# groupby()
# 把迭代器中相邻的重复元素挑出来放在一起
for key, group in itertools.groupby('AAABBBCCAAA'):
    print(key, list(group))
```
