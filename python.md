# Python 学习笔记



[TOC]

## 1. The zen of Python

> The Zen of Python, by Tim Peters
>
> 
>
> Beautiful is better than ugly.
>
> Explicit is better than implicit.
>
> Simple is better than complex.
>
> Complex is better than complicated.
>
> Flat is better than nested.
>
> Sparse is better than dense.
>
> Readability counts.
>
> Special cases aren't special enough to break the rules.
>
> Although practicality beats purity.
>
> Errors should never pass silently.
>
> Unless explicitly silenced.
>
> In the face of ambiguity, refuse the temptation to guess.
>
> There should be one-- and preferably only one --obvious way to do it.
>
> Although that way may not be obvious at first unless you're Dutch.
>
> Now is better than never.
>
> Although never is often better than *right* now.
>
> If the implementation is hard to explain, it's a bad idea.
>
> If the implementation is easy to explain, it may be a good idea.
>
> Namespaces are one honking great idea -- let's do more of those!

## 2. Python2与Python3的主要区别

- **关键字/函数**：Python2中，`print`、`exec`是关键字；Python3中是函数。
- **编码**：Python2默认编码为`ASCII`，Python3默认编码为`UTF-8`。
- **字符串**：Python3的字符串有`unicode`和`str`，两者无明显界限；Python3将两者严格区分，`str`类型表示字符串，由`Unicode`编码，`bytes`类型表示字节序列。
- **True、False**：在Python2中是全局变量，可赋值；在Python3中是关键字。
- **迭代器**：Python3的`range()`、`dict.keys()`、`dict.vaules()`返回值均为迭代器，Python3中的`range`等价于Python2中的`xrange`。Python2迭代器需实现`next()`方法，Python3为`__next__()`魔术方法。
- **nonlocal**：Python3新增关键字，声明某变量为非全局变量。
- **long**：Python3取消了`long`类型，统一为`int`。
- **比较运算符**：Python3中比较运算符（`<`、`<=`、`>`、`>=`）比较不同类型的变量会抛出`TypeError`。

## 3. Python标准库中有关字符串和文本的常用内容

- `fnmatch.fnmatch`：支持shell通配符的字符串匹配，大小写区取决操作系统。
- `fnmatch.fnmatchcase`：支持shell通配符的字符串匹配，区分大小写。
- `html.escape`：将字符串转换为html安全字符串。
- `html.unescape`：将html安全字符串转化为普通字符串。
- `ord`：获取字符的Unicode编号。
- `os.get_terminal_size`：获取终端字符宽度。
- `re.compile`：预编译正则。
- `re.findall`：找到所有匹配项。
- `re.finditer`：找到所有匹配项，返回生成器。
- `re.match`：找到第一个匹配项。
- `re.split`：字符串分割。
- `re.sub`：字符串替换；被替换文本支持函数。
- `re.DOTALL`：`re.compile`参数，用于使`.`支持匹配包括换行符的所有字符。
- `re.IGNORECASE`：re函数中加入`flags=re.IGNORECASE`以忽略大小写。
- `str.endwith`：字符串结尾文本匹配，比正则快，参数支持元组。、
- `str.join`：字符串拼接。
- `str.lstrip`：去除左侧空格（或其他字符）。
- `str.rstrip`：去除右侧空格（或其他字符）。
- `str.startwith`：字符串开头文本匹配，比正则快，参数支持元组。
- `str.strip`：去除两侧空格（或其他字符）。
- `str.translate`：字符替换。
- `textwarp.fill`：以指定宽度格式化字符串。

## 4. Python标准库中有关数字、日期和时间的常用内容

- `bin`：将整型转换为二进制字符串（带前缀，`format`不带前缀）。
- `datetime.datetime.now`：返回当前时间。
- `datetime.datetime.strftime`：将`datetime.datetime`对象转换为指定格式的字符串。
- `datetime.datetime.strptime`：将字符串转化为`datetime.datetime`对象，性能很差。
- `datetime.datetime().replace`：替换年月日时分秒。
- `datetime.timedelta`：创建`datetime.datetime`实例，常用语加减法。
- `decimal.Decimal`：精确小数计算。
- `hex`：将整型转换为十六进制字符串（带前缀，`format`不带前缀）。
- `random.choice`：从序列中随机选择一个元素。
- `random.sample`：从序列中随机选择n个元素。
- `random.shuffle`：将序列乱序。
- `round`：取整，保留小数位数，仅用于显示时建议使用字符串格式化。
- `oct`：将整型转换为八进制字符串（带前缀，`format`不带前缀）。

## 5. Python标准库中有关数据结构与算法的常用内容

- `collections.defaultdict`：初始化字典键值。
- `collections.deque`：返回先进后出队列。
- `namedtuple`：命名数组，不可变，效率高于字典。
- `collections.Counter`：将可哈希对象序列转换为一个统计对象出现数量的字典。
- `collections.Counter.most_common`：找出可哈希对象序列中出现次数最多的n个对象。
- `collections.OrderedDict`：有序字典（双倍内存开销）。
- `dict.items`：将字典转换为一个列表，每个元素是一个元组，第一个值为key，第二个值为value。
- `filter`：筛选数据，返回生成器。
- `heapq`：堆队列模块。
- `itertools.groupby`：对字典或对象实例根据特定字段分组。
- `operator.itemgetter`：代替lambda作为`min`、`max`、`sorted`指定key的方法（字典列表）。
- `operator.attrgetter`：代替lambda作为`min`、`max`、`sorted`指定key的方法（对象列表）。
- `slice`：切片；可对切片命名。
- `zip`：聚合多个可迭代对象，返回一个迭代器。

## 6. Python标准库中有关加密、安全的常用内容

- `ssl.RAND_bytes`：生成加密安全的随机字节序列。