# 常用内置模块 datetime

python标准库文档 https://docs.python.org/zh-cn/3.8/library/index.html

## datetime

* 文档 https://docs.python.org/zh-cn/3.8/library/datetime.html#datetime.date 
* 获取当前日期
```
from datetime import datetime,timezone,timedelta,time
print(datetime.now())
print(datetime.utcnow())
print(datetime.now(timezone.utc))

print(datetime(2015, 4, 19, 12, 20).timestamp())

print(datetime(2015, 4, 19, 12, 20).isoformat())
print(datetime.now(timezone.utc).isoformat())
```
* str与datetime互相转换
```
# str转datetime
date1=datetime.strptime('2019-1-1 18:56:56', '%Y-%m-%d %H:%M:%S')
print(date1) # 2019-01-01 18:56:56
print(type(date1)) # <class 'datetime.datetime'>

# datetime转str
date2 = date1.strftime('%H:%M:%S %m %Y')
print(date2)  # 18:56:56 01 2019
print(type(date2)) # <class 'str'>
```

* 时区转换

```
from datetime import datetime,timezone,timedelta,time
# 获取当前UTC时间,并强制设置时区是UTC+0.00
now_date = datetime.utcnow().replace(tzinfo=timezone.utc)
print(now_date)
# 转换北京时间
print(now_date.astimezone(timezone(timedelta(hours=8))))
# 东京时间
print(now_date.astimezone(timezone(timedelta(hours=9))))
```

* 时间加减
```
# 时间加减
print(datetime.now())
print(datetime.now() + timedelta(hours=10))
print(datetime.now() - timedelta(days=1))
print(datetime.now() + timedelta(days=1,hours=5))
print(datetime.now().timetuple())
```
