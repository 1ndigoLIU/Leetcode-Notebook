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

### 数组切片slicing

正常输出index：

```python
nums = [0,1,2,3,4,5]
nums[:3] # [0, 1, 2] the first three elements of nums
nums[3:] # [3, 4, 5] everything from index 3 to the end
nums[1:3] # [1, 2] the sublist from index 1 through index 2

nums[:-2] # [0, 1, 2, 3] everything except the last two
nums[-2:] # [4, 5] the last two elements
```

当输入负数索引negative indexes：

切片里的负数索引表示从尾部反向进行 counting from the **end of the sequence** instead of from the beginning

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

st.add(5)
s.remove(5) # 按值删除；若不存在会抛 KeyError
s.discard(5) # 按值删除；若不存在什么也不做（更安全）
```

**集合 (set)** 查找：

- `set` 是基于 **哈希表（hash table）** 实现的。
- 每个元素会根据其 **哈希值 (`hash()`)** 计算出一个位置（槽位，slot），然后存储到哈希表里。

- `x in st` 会先计算 `hash(x)`，然后直接跳到对应槽位检查是否存在。
- 在没有严重哈希冲突的情况下，平均复杂度是 **O(1)**。
- 最坏情况是 **O(n)**（所有元素都哈希冲突），但哈希函数设计得比较好时很少发生。

### `dict()`字典 （hash表）

查找 / 插入 / 删除：平均时间复杂度 O(1)

```python
# initialize
count = {}

# frequency count of numbers 频次统计
count[num] = count.get(num, 0) + 1

# if num hasn’t appeared before, count[num] doesn’t exist yet — that will raise a KeyError
count[num] += 1
```

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

### `Counter`统计

`Counter` 是 Python 标准库 `collections` 模块里的一个类，常用来 **统计可迭代对象中元素出现的次数**，功能类似于一个字典，但针对计数做了优化。

#### 1. 基本用法

```python
from collections import Counter

data = ['a', 'b', 'c', 'a', 'b', 'a']
counter = Counter(data)
print(counter)  
# 输出: Counter({'a': 3, 'b': 2, 'c': 1})
```

它返回一个类似字典的对象，**键是元素，值是出现次数**。

#### 2. 统计字符串

```python
s = "mississippi"
c = Counter(s)
print(c)  
# Counter({'i': 4, 's': 4, 'p': 2, 'm': 1})
```

可以快速统计每个字符出现的频率。

---

#### 3. 常用方法

* **most\_common(n)**
  返回出现频率最高的 n 个元素：

  ```python
  c.most_common(2)
  # [('i', 4), ('s', 4)]
  ```

* **elements()**
  返回一个迭代器，将每个元素按出现次数重复：

  ```python
  list(c.elements())
  # ['m', 'i', 'i', 'i', 'i', 's', 's', 's', 's', 'p', 'p']
  ```

* **update()**
  可以用来增加计数：

  ```python
  c.update("pp")
  print(c)
  # Counter({'i': 4, 's': 4, 'p': 4, 'm': 1})
  ```

* **subtract()**
  减少计数：

  ```python
  c.subtract("is")
  print(c)
  # Counter({'s': 3, 'i': 3, 'p': 4, 'm': 1})
  ```

#### 4. 与数学运算结合

`Counter` 可以进行集合运算（交集、并集等），对计数有意义：

```python
a = Counter("apple")
b = Counter("pear")

print(a + b)   # 计数相加
# Counter({'p': 3, 'a': 2, 'l': 1, 'e': 2, 'r': 1})

print(a - b)   # 相减（负数会被去掉）
# Counter({'p': 1, 'l': 1})

print(a & b)   # 交集：取最小值
# Counter({'a': 1, 'p': 1, 'e': 1})

print(a | b)   # 并集：取最大值
# Counter({'p': 2, 'a': 1, 'l': 1, 'e': 1, 'r': 1})
```

#### 5. 应用场景

* 文本词频统计（自然语言处理）
* 数据去重和频率分析
* 找出最常见元素
* 简化需要手动写字典统计的逻辑



### random.randint

`random.randint(a, b)` 是 Python 内置模块 `random` 里的一个函数，用来**生成一个在指定范围内的随机整数**。

```python
import random

n = random.randint(a, b)
```

**参数 `a` 和 `b`**：两个整数，范围的左右端点，**包含端点**。

返回值：`a <= n <= b` 的随机整数。
