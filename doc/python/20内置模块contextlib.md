# contextlib

try...finally 的写法很繁琐,使用with更加方便 
```
with open('/path/to/file', 'r') as f:
    f.read()
```
并不是只有open()函数返回的fp对象才能使用with语句。实际上，任何对象，只要正确实现了上下文管理，就可以用于with语句,实现上下文管理是通过__enter__和__exit__这两个方法实现的,实现这两个方法就可以
```
class Query(object):

    def __init__(self, name):
        self.name = name

    def __enter__(self):
        print('Begin')
        return self
    def __exit__(self, exc_type, exc_val, exc_tb):
        if exc_type:
            print('Error')
        else:
            print('End')
    def query(self):
        print("query info about %s .. " % self.name)

with Query('Bob') as q:
    q.query()

# 
# Begin
# query info about Bob .. 
# End
```
* @contextmanager 编写__enter__和__exit__仍然很繁琐，因此Python的标准库contextlib提供了更简单的写法
这个decorator接受一个generator，用yield语句把with ... as var把变量输出出去，然后，with语句就可以正常地工作了

```
from contextlib import contextmanager

class Query(object):

    def __init__(self, name):
        self.name = name

    def query(self):
        print('Query info about %s...' % self.name)

@contextmanager
def create_query(name):
    print('Begin')
    q = Query(name)
    yield q
    print('End')

with create_query('Tom') as qq:
    qq.query()
```
*  某段代码之前后打印日志, 执行顺序yield之前, whith语句内部代码块,yield之后代码块
```
@contextmanager
def tag(name):
    print('method is start run ...')
    yield
    print('method is stop')


with tag("123"):
    print('hello')
    print('python')
```

