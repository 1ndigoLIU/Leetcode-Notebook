### `defaultdict`创建字典

`defaultdict` 是 `collections.defaultdict`，它继承自内置的 `dict`，但是可以指定一个 **工厂函数**，在访问不存在的键时，自动创建一个默认值，而不会抛出 `KeyError`。

```python
from collections import defaultdict

d = defaultdict(list)

d["a"].append(1)
d["a"].append(2)
d["b"].append(3)

print(d)
# 输出: defaultdict(<class 'list'>, {'a': [1, 2], 'b': [3]})
```

解释：

- `list` 是工厂函数（callable），当访问一个不存在的键时，就会自动执行 `list()` 来生成默认值（即空列表 `[]`）。
- 所以第一次访问 `d["a"]` 时，字典里没有 `"a"`，它会自动建立 `"a": []`，然后 `.append(1)` 就能直接用。



### `sorted(x)`

- `sorted()` 是 Python 内置函数，可以对 **可迭代对象**（列表、字符串、元组等）进行排序。
- 返回值是 **排序后的列表**。
- 对字符串调用时，会把字符串拆成单个字符，然后排序：

```python
sorted("cba")  
# ['a', 'b', 'c']
```



### `.join(...)`

- `join()` 是字符串方法，用来把一个 **可迭代对象里的字符串元素** 连接起来。
- 前面的 `''` 表示用 **空字符串** 作为分隔符。

```python
''.join(['a', 'b', 'c'])
# 'abc'
```



### `set`集合

`set()` 是 Python 内置函数，用于创建 **集合 (set)**。

特点：

- 元素 **唯一**（自动去重）
- 元素 **无序**（不保证顺序）

`set(list)` 会把参数列表转换成一个集合，去掉重复元素：

```python
nums = [1, 2, 2, 3]
st = set(nums)
print(st)  # {1, 2, 3}
```

**集合 (set)** 查找：

- `set` 是基于 **哈希表（hash table）** 实现的。
- 每个元素会根据其 **哈希值 (`hash()`)** 计算出一个位置（槽位，slot），然后存储到哈希表里。

- `x in st` 会先计算 `hash(x)`，然后直接跳到对应槽位检查是否存在。
- 在没有严重哈希冲突的情况下，平均复杂度是 **O(1)**。
- 最坏情况是 **O(n)**（所有元素都哈希冲突），但哈希函数设计得比较好时很少发生。



### `len()`获取长度

`len(obj)` 返回 **序列或容器中的元素个数**

常见对象：

- **列表 (list)**：`len([1, 2, 3]) → 3`
- **元组 (tuple)**：`len((1, 2)) → 2`
- **字符串 (str)**：`len("hello") → 5`
- **字典 (dict)**：`len({"a": 1, "b": 2}) → 2`  （统计键值对数量）
- **集合 (set/frozenset)**：`len({1, 2, 3}) → 3`
- **range**：`len(range(10)) → 10`
- **字节序列 (bytes/bytearray)**：`len(b"abc") → 3`

**时间复杂度**：O(1)
容器对象内部都维护了长度属性，无需遍历
