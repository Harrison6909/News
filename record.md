# 知识点记录

## LIST的方法


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