# 知识点记录


## Pyton标准库的方法


### json库
**json 库是 Python 标准库，常用方法有`json.loads()`,`json.dumps()`和`json.JSONEncoder`**

>*json.loads* 用来将 JSON 格式字符串转换为 Python 对象。它的用法如下：
```python
import json
json_str = '{"name": "Alice", "age": 18}'
python_obj = json.loads(json_str)
print(python_obj)  # {'name': 'Alice', 'age': 18}
```
>在这个例子中，json_str 是一个包含 JSON 格式数据的字符串，然后我们调用 json.loads(json_str) 将它转换为 Python 对象 python_obj。转换后的对象是一个 Python 字典，它的内容和 JSON 对象一致。

>*json.dumps* 用来将Python对象转换为 JSON 格式字符串。

>*json.JSONEncoder* 是一个 json 库的类，用于将 Python 对象编码成 JSON 格式字符串。默认情况下，json 库使用 `json.JSONEncoder` 来对 Python 对象进行编码。

### `Decimal(str)`方法
Decimal 是 Python 标准库中的一个数据类型，用于高精度运算。它可以处理浮点数的各种精度问题，特别是在进行金融计算时非常实用。

在使用 Decimal 数据类型时，我们需要将数字使用字符串的形式传入，例如：
```python
from decimal import Decimal

x = Decimal('0.1')
y = Decimal('0.2')
z = x + y
print(z)  # 0.3
```
> Decimal类型可以用`.quantize(Decimal('0.00'))`的方法设置对象的小数位精度

### `.append(tpye)`方法
再列表 'list' 末尾添加'tpye'元素


### `' '.join(string_list)`

使用指定字符串`' '`连接可迭代对象（例如列表、元组或字符串）`string_list`，得到一个新的字符串


## Django模型的方法


### 定义一个Django模型
```python
from django.db import models

class Person(models.Model):
    first_name = models.CharField(max_length=30)
    last_name = models.CharField(max_length=30)
    age = models.IntegerField()
    birthdate = models.DateField()
```
上面的代码定义了一个 Person 模型，其中包含了四个字段：

* first_name：人的名字，使用 CharField 类型存储，最大长度为 30 个字符。
* last_name：人的姓氏，使用 CharField 类型存储，最大长度为 30 个字符。
* age：人的年龄，使用 IntegerField 类型存储。
* birthdate：人的出生日期，使用 DateField 类型存储。


### `.objects.all()`方法
`.objects.all()` 是 Django 模型（Model）中的一个 QuerySet 方法，用于获取模型对应的数据表中的所有记录。具体来说，它做了以下几件事情：
1. 获取模型对应的数据表名。
2. 构造一个 SQL 查询语句，查询数据表中的所有记录。
3. 执行 SQL 查询，获取所有记录的数据，并返回一个 QuerySet 对象，其中包含了所有记录的模型实例（即模型对象）。

例如一个有模型Person，那么`Person.objects.all()`将获取person中所有记录，并返回一个包含所有记录的QuerySet对象。
```python
obj = Person.objects.all()
```


### `.objects.filter()`方法
.filter() 是 Django ORM 中用于过滤查询结果集的方法。它返回一个 QuerySet 对象，可以继续链式调用其他方法来对查询结果进行进一步的筛选或排序。

.filter() 方法接受一个或多个关键字参数，每个参数都指定了一个查询条件，例如：
```python
# 查询所有姓张并且年龄在 18-30 岁之间的人
Person.objects.filter(last_name='张', age__range=(18, 30))
```
其中，关键字参数的格式为 field__filter_type=value，其中 field 表示要过滤的字段名，filter_type 表示要进行的过滤操作，value 表示要匹配的值。比较常用的 filter_type 和其含义如下：

* exact （默认值）：精确匹配；
* iexact：忽略大小写的匹配；
* contains：包含匹配；
* icontains：忽略大小写的包含匹配；
* in：在指定的列表中匹配；
* gt：大于；
* gte：大于等于；
* lt：小于；
* lte：小于等于。

### `get_redis_connection()`方法
`get_redis_connection()`是Django中用于获取Redis连接的方法，它返回一个Redis连接对象，通过这个对象可以对Redis数据进行操作。
在 Django 中使用 Redis 缓存时，需要在 settings.py 文件中进行 Redis 配置。在 Redis 配置完成后，get_redis_connection() 便可以根据在配置中设置的连接信息返回一个 Redis 连接对象，从而可以使用 Redis 缓存。

Django 中的 Redis 缓存还支持以下哈希类型相关操作：

* hget(key, field)：获取哈希 key 中指定 field 的值
* hset(key, field, value)：在哈希 key 中添加一个指定 field 和 value 的键值对。如果指定的 field 在哈希 key 中已经存在，则会更新它的值
* hdel(key, *fields)：删除哈希 key 中指定的一个或多个 fields
* hkeys(key)：获取哈希 key 中所有的字段名
* hlen(key)：获取哈希 key 中字段的数量
* hexists(key, field)：检查哈希 key 中是否存在指定的 field