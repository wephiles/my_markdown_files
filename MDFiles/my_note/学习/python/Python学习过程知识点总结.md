<h1 style="text-align: center;font-size: 40px; font-family: '楷体';">
Python学习过程知识点总结
</h1>

# `pandas`模块

- df.head() 显示前 n 行数据

- df.tail() 显示后 n 行数据

- df.info() 显示数据的信息，包括列名、数据类型、缺失值等

- df.describe() 显示数据的基本统计信息，包括均值、方差、最大值、最小值等；

- df.shape 显示数据的行数和列数

- df\[column_name] 选择指定的列

- df.groupby(column_name) 按照指定列进行分组

- pd.merge(df1, df2, on=column_name) pandas 库中的 merge 函数用于合并两个 DataFrame 对象。它类似于 SQL 中的 JOIN 操作，可以根据一个或多个键将不同的数据集合并在一起。下面是 merge 函数的常用参数及其作用，以及如何使用这个函数的简单说明。:

    ```python
    left: 左侧的 DataFrame 对象。
    right: 右侧的 DataFrame 对象。
    
    how: 合并方式，可以是 'inner', 'outer', 'left', 'right' 中的一个。默认是 'inner'。
        'inner': 内连接，只保留两个 DataFrame 中都有的键。
        'outer': 外连接，保留两个 DataFrame 中的所有键，没有匹配的键将用 NaN 填充。
        'left': 左连接，保留左侧 DataFrame 的所有键，右侧没有匹配的键用 NaN 填充。
        'right': 右连接，保留右侧 DataFrame 的所有键，左侧没有匹配的键用 NaN 填充。
    
    on: 用于合并的列名。如果两个 DataFrame 中有相同的列名，可以直接使用这个参数。如果是多个列名，需要用列表形式传入。
    
    left_on: 左侧 DataFrame 中用于合并的列名。
    right_on: 右侧 DataFrame 中用于合并的列名。
    
    left_index: 如果为 True，则使用左侧 DataFrame 的索引作为合并键。
    right_index: 如果为 True，则使用右侧 DataFrame 的索引作为合并键。
    
    suffixes: 当列名冲突时，为每个 DataFrame 的列添加的后缀。默认是 ('_x', '_y')。
    copy: 如果为 True，则复制数据。默认是 True。
    indicator: 如果为 True，则在合并后的 DataFrame 中添加一个名为 '_merge' 的列，表示每行数据的来源。
    validate: 指定连接类型，如 'one_to_one', 'one_to_many', 'many_to_one', 'many_to_many'。默认是 None。
    ```

- df.describe() 计算基本统计信息，如均值、标准差、最小值、最大值等。

- df.mean() 计算每列的平均值。

- df.median() 计算每列的中位数。

- df.mode() 计算每列的众数。

- df.count() 计算每列非缺失值的数量。

- df.rename():在pandas中，rename()函数用于重命名DataFrame的列名或者索引。以下是一些常见的使用方式.在以下的例子中，inplace=True表示直接在原DataFrame上进行修改。如果你不希望修改原DataFrame，可以省略这个参数，rename()函数会返回一个新的DataFrame。

    - 参数：

        ```python
        mapper：字典或函数。这是一个可选参数，用于指定从旧标签到新标签的映射。如果是字典，可以为index或columns参数提供映射。如果是函数，那么它将应用于所有标签。  
        index：字典或函数。这是一个可选参数，用于指定从旧索引到新索引的映射。如果是字典，键是旧的索引，值是新的索引。如果是函数，那么它将应用于所有索引。  
        columns：字典或函数。这是一个可选参数，用于指定从旧列名到新列名的映射。如果是字典，键是旧的列名，值是新的列名。如果是函数，那么它将应用于所有列名。  
        axis：{0 或 'index', 1 或 'columns'}，默认为0。这是一个可选参数，用于指定要重命名的轴。如果axis=0或'index'，则重命名索引；如果axis=1或'columns'，则重命名列名。  
        copy：布尔值， 默认为True。这是一个可选参数，如果为True，那么即使新的索引与旧的索引相同，也会复制底层数据。如果为False，新的索引与旧的索引相同，底层数据不会被复制。  
        inplace：布尔值，默认为False。这是一个可选参数，如果为True，那么直接在原DataFrame上进行修改。如果为False，rename()函数会返回一个新的DataFrame，原DataFrame不会被修改。  
        level：int或level name，默认为None。这是一个可选参数，用于多级索引的情况，指定要重命名的级别。如果为None，则默认重命名所有级别。  
        errors：{'ignore', 'raise'}，默认为'raise'。这是一个可选参数，如果为'ignore'，则忽略无法重命名的错误；如果为'raise'，则如果存在无法重命名的错误，会引发错误
        ```

        ```python
        # 重命名列名：你可以通过传递一个字典到columns参数来重命名列名。字典的键是旧的列名，值是新的列名
        import pandas as pd
        
        # 创建一个DataFrame
        df = pd.DataFrame({
           'A': [1, 2, 3],
           'B': [4, 5, 6]
        })
        ```

        ```python
        # 重命名列名
        df.rename(columns={'A': 'a', 'B': 'b'}, inplace=True)
        
        ===============================================================================
        
        # 重命名索引：你可以通过传递一个字典到index参数来重命名索引。字典的键是旧的索引，值是新的索引
        import pandas as pd
        
        # 创建一个DataFrame
        df = pd.DataFrame({
           'A': [1, 2, 3],
           'B': [4, 5, 6]
        }, index=['x', 'y', 'z'])
        
        # 重命名索引
        df.rename(index={'x': 'X', 'y': 'Y', 'z': 'Z'}, inplace=True)
        ```

        ```python
        # 使用函数重命名：你也可以传递一个函数到columns或index参数，这个函数会被应用到每个列名或索引上。
        import pandas as pd
        
        # 创建一个DataFrame
        df = pd.DataFrame({
           'A': [1, 2, 3],
           'B': [4, 5, 6]
        })
        
        # 使用函数重命名列名
        df.rename(columns=str.lower, inplace=True)
        ```

# `pickle`模块



#`heapq`模块

`Python `的 `heapq` 是一个堆队列算法的实现，它提供了一些用于创建和操作堆的函数。堆是一种特殊的树状数据结构，其中每个父节点的值都小于或等于其子节点的值。在 `Python `中，`heapq` 模块通常用于实现优先队列。

以下是 `heapq` 模块的一些主要功能：

1. **`heapify()`**: 将一个列表转换为堆。它将任意列表转换为一个堆，使列表满足堆的性质。
2. **`heappush()`**: 添加一个元素到堆中。它将一个元素添加到堆的末尾，然后重新调整以维持堆的性质。
3. **`heappop()`**: 移除并返回堆中的最小元素。它从堆中移除并返回最小的元素，同时重新调整以维持堆的性质。
4. **`heappushpop()`**: 将一个元素添加到堆中并返回堆中当前的最小元素。如果添加的元素比当前的最小元素还小，则返回添加的元素。
5. **`heapreplace()`**: 将一个元素添加到堆中，并返回堆中移除的最小元素。这可以看作是 `heappop()` 后立即 `heappush()` 的操作。
6. **`merge()`**: 合并两个堆。它将两个已排序的输入列表合并为一个排序后的输出列表。
7. **`nlargest()`**: 从序列中找到最大的 `n` 个元素。它返回序列中最大的 `n` 个元素，以升序排列。
8. **`nsmallest()`**: 从序列中找到最小的 `n` 个元素。它返回序列中最小的 `n` 个元素，以升序排列。
9. **`len()`**: 返回堆中元素的数量。

这些功能使得 `heapq` 模块非常适合用于需要优先级队列的场景，如任务调度、事件驱动模拟等。由于堆的效率很高，`heapq` 操作通常具有对数时间复杂度，这使得它在处理大量数据时非常有效。

下面是一个简单的示例，展示如何使用 `heapq` 创建一个堆并进行操作：

```
import heapq

# 创建一个空堆
heap = []

# 添加元素到堆中
heapq.heappush(heap, 1)
heapq.heappush(heap, 5)
heapq.heappush(heap, 2)

# 移除并返回堆中的最小元素
print(heapq.heappop(heap))  # 输出 1

# 替换堆中的最小元素
print(heapq.heapreplace(heap, 3))  # 输出 2，并且将 3 添加到堆中

# 打印堆中的所有元素
print(heap)  # 输出 [3, 5]
```

这个示例展示了如何使用 `heapq` 模块的基本功能来创建一个堆，添加元素，移除最小元素，以及替换堆中的最小元素。

在Python中，`heapq`是一个提供堆队列算法实现的库。堆是一种特殊的树状数据结构，其中父节点的键值总是大于或等于其子节点的键值。这种性质使得堆可以用于实现优先队列，其中元素根据其键值进行排序。

`heapq`模块提供了一些函数来操作堆，包括：

1. `heapify(iterable)`: 将任何可迭代对象转换成堆。`iterable`中的元素将被重新排列，以形成一个堆。
2. `heappush(heap, item)`: 将一个新元素添加到堆中。
3. `heappop(heap)`: 移除并返回堆中的最小元素。
4. `heapreplace(heap, item)`: 移除并返回堆中的最小元素，然后添加新元素。
5. `heappushpop(heap, item)`: 如果新元素的键值小于堆中的最小元素，那么移除并返回堆中的最小元素，并添加新元素；否则，只添加新元素。
6. `heapsort(iterable)`: 对可迭代对象中的元素进行排序。
7. `merge(*iterables)`: 合并多个已排序的输入并产生一个迭代器，该迭代器生成的元素是所有输入中的最小元素。
8. `nlargest(n, iterable[, key])`: 返回数据集合中最大的n个元素。
9. `nsmallest(n, iterable[, key])`: 返回数据集合中最小的n个元素。

`heapq`模块的这些功能使得它非常适合用于那些需要根据优先级进行排序和检索的场景，例如任务调度、事件驱动模拟等。

下面是一个使用`heapq`模块实现最小堆的例子：

```
import heapq

# 创建一个空堆
h = []

# 添加一些元素
heapq.heappush(h, 1)
heapq.heappush(h, 3)
heapq.heappush(h, 5)

# 弹出并返回最小元素
print(heapq.heappop(h))  # 输出 1

# 再次弹出并返回最小元素
print(heapq.heappop(h))  # 输出 3
```

在这个例子中，`heapq.heappush`用于将元素添加到堆中，而`heapq.heappop`用于移除并返回堆中的最小元素。

# `queue`模块

Python 的 `queue` 模块提供了多种类型的队列实现，包括先进先出（FIFO）队列、LIFO（后进先出）队列，以及支持任务优先级的队列。以下是 `queue` 模块中一些常用类的简要介绍：

1. **`Queue`**: 标准的队列实现，使用FIFO原则，即先添加到队列中的元素将先被移除。
2. **`LifoQueue`**: 后进先出队列，类似于栈，使用LIFO原则。
3. **`PriorityQueue`**: 支持优先级的队列，元素会根据优先级被排序，优先级最高的元素最先被移除。
4. **`deque`**: 双端队列，允许在两端快速地添加（append）和移除（pop）元素。

使用 `queue` 模块的一个基本示例如下：

```
from queue import Queue

# 创建一个FIFO队列
q = Queue()

# 添加元素到队列
q.put('a')
q.put('b')
q.put('c')

# 从队列中移除并返回一个元素
first_item = q.get()

print(first_item)  # 输出: 'a'
```

为了使用 `queue` 模块，你需要先导入它。然后，你可以创建队列对象，并使用 `put()` 方法添加元素，使用 `get()` 方法移除并返回队列前端的元素。

如果你需要使用其他类型的队列，比如 `LifoQueue` 或 `PriorityQueue`，你只需创建相应类型的实例，并使用类似的 `put()` 和 `get()` 方法。

请注意，`queue` 模块的 `get` 方法会阻塞调用线程，直到队列中至少有一个元素，除非你指定了 `timeout` 参数。此外，`put` 方法也会阻塞，直到队列中有空间可以存放新元素，除非你指定了 `timeout` 参数。

#`sorted()` 

Python中的`sorted`函数用于对序列进行排序，并返回一个新的排序列表。`sorted`函数可以用于列表、元组以及任何可迭代对象。

### 基本用法

最基本的用法非常简单，只需将一个可迭代对象传递给`sorted`函数即可。

python

复制

```
my_list = [3, 1, 4, 1, 5, 9, 2, 6, 5]
sorted_list = sorted(my_list)
print(sorted_list)  # 输出：[1, 1, 2, 3, 4, 5, 5, 6, 9]
```

### 关键字参数

`sorted`函数接受两个关键字参数：

1. `key`: 用于指定一个函数，此函数将在每个元素比较前被调用。此函数将返回一个用于排序的值。
2. `reverse`: 设为`True`时，列表将被倒序排列。

#### 使用`key`参数

python

复制

```
# 使用key参数进行忽略大小写的排序
my_list = ['banana', 'Apple', 'cherry', 'Date']
sorted_list = sorted(my_list, key=str.lower)
print(sorted_list)  # 输出：['Apple', 'banana', 'cherry', 'Date']
```

#### 使用`reverse`参数

python

复制

```
# 使用reverse参数进行降序排序
my_list = [3, 1, 4, 1, 5, 9, 2, 6, 5]
sorted_list = sorted(my_list, reverse=True)
print(sorted_list)  # 输出：[9, 6, 5, 5, 4, 3, 2, 1, 1]
```

### 排序复杂对象

`sorted`函数也可以用于排序复杂对象，比如字典列表。

python

复制

```
# 根据字典中的键值对列表进行排序
my_list = [{'name': 'John', 'age': 35}, {'name': 'Doe', 'age': 25}, {'name': 'Jane', 'age': 40}]
sorted_list = sorted(my_list, key=lambda x: x['age'])
print(sorted_list)  
# 输出：[{'name': 'Doe', 'age': 25}, {'name': 'John', 'age': 35}, {'name': 'Jane', 'age': 40}]
```

### 使用`reverse`和`key`参数

你可以同时使用`reverse`和`key`参数。

python

复制

```
# 同时使用key和reverse参数
my_list = [{'name': 'John', 'age': 35}, {'name': 'Doe', 'age': 25}, {'name': 'Jane', 'age': 40}]
sorted_list = sorted(my_list, key=lambda x: x['age'], reverse=True)
print(sorted_list)  
# 输出：[{'name': 'Jane', 'age': 40}, {'name': 'John', 'age': 35}, {'name': 'Doe', 'age': 25}]
```

这样，你就可以根据不同的需求，使用`sorted`函数进行灵活的排序。

`sorted`函数使用`key`参数来指定一个函数，这个函数会在排序前对每个元素进行转换。排序时，`sorted`函数会使用转换后的值而不是原始元素进行比较。这种方式允许我们自定义排序逻辑，使得`sorted`函数能够适用于各种不同类型的数据和排序需求。

### `key`参数的处理过程

当`sorted`函数对可迭代对象进行排序时，它会按照以下步骤处理`key`参数：

1. 对可迭代对象中的每个元素，调用`key`函数。
2. 使用`key`函数返回的值作为排序的依据。
3. 根据这些值对元素进行排序。
4. 返回排序后的列表。

### 编写用于`sorted`的排序函数

编写用于`sorted`的排序函数通常很简单。这个函数应该接受一个元素作为参数，并返回一个用于排序的值。下面是一些例子：

#### 对字符串长度进行排序

python

复制

```
# 对字符串列表按照长度排序
my_list = ['banana', 'apple', 'cherry']
sorted_list = sorted(my_list, key=len)
print(sorted_list)  # 输出：['apple', 'banana', 'cherry']
```

#### 对复杂数据结构进行排序

python

复制

```
# 对字典列表按照多个键进行排序
my_list = [{'name': 'John', 'age': 35}, {'name': 'Doe', 'age': 25}, {'name': 'Jane', 'age': 40}]
# 先按年龄排序，年龄相同则按名字排序
sorted_list = sorted(my_list, key=lambda x: (x['age'], x['name']))
print(sorted_list)
# 输出：[{'name': 'Doe', 'age': 25}, {'name': 'John', 'age': 35}, {'name': 'Jane', 'age': 40}]
```

#### 使用自定义类进行排序

python

复制

```
# 定义一个类，并编写一个用于排序的key函数
class Student:
    def __init__(self, name, age, grade):
        self.name = name
        self.age = age
        self.grade = grade

    def __repr__(self):
        return f'{self.name}, {self.age}, {self.grade}'

# 创建学生列表
students = [Student('John', 20, 90), Student('Jane', 22, 85), Student('Doe', 20, 95)]

# 按照年龄排序
sorted_students_age = sorted(students, key=lambda student: student.age)
print(sorted_students_age)

# 按照成绩排序
sorted_students_grade = sorted(students, key=lambda student: student.grade)
print(sorted_students_grade)
```

在上面的例子中，我们定义了一个`Student`类，并为它编写了一个`__repr__`方法以便于打印。然后我们创建了学生列表，并使用`sorted`函数按照年龄和成绩对学生进行排序。

总结来说，编写用于`sorted`的排序函数就是定义一个能够提取排序依据的函数，然后将这个函数作为`key`参数传递给`sorted`函数。这样，`sorted`函数就能够根据我们提供的逻辑对数据进行排序。

# `inf`

在Python的math库中，`inf`表示无穷大。具体来说，`math.inf`表示一个大于所有可表示浮点数的值。当你需要表示一个理论上无限大的值时，可以使用`math.inf`。

例如，在数学中，当你想要表示一个函数的极限为无穷大时，或者在编程中，当你需要初始化一个变量，以便之后进行比较操作，并且这个变量应该表示一个无穷大的值时，`math.inf`就非常有用。

`math.inf`也有一些相关的属性和用法，比如：

- `math.isinf(x)`：如果x是`math.inf`或`-math.inf`，则返回`True`。
- `-math.inf`：表示负无穷大。
- `math.inf`与任何非零浮点数相乘或相除都会得到`math.inf`或`-math.inf`。
- `math.inf`与`math.inf`相除会得到`nan`（not a number，即非数）。

这里有一些简单的使用示例：

python

复制

```
import math

# 判断一个数是否为无穷大
print(math.isinf(math.inf))  # 输出: True

# 无穷大与有限数值的比较
print(1e308 < math.inf)  # 输出: True

# 负无穷大
print(-math.inf < 0)  # 输出: True

# 无穷大与无穷大相加
print(math.inf + math.inf)  # 输出: inf

# 无穷大与无穷大相乘
print(math.inf * math.inf)  # 输出: inf

# 无穷大除以无穷大
print(math.inf / math.inf)  # 输出: nan
```

在实际编程中，使用`math.inf`可以帮助简化代码，并且可以更好地处理边界条件。

# sys.maxsize

在Python中，`sys.maxsize` 是 `sys` 模块中的一个属性，它表示Python解释器所能支持的列表、集合、字典等数据结构所能容纳的最大元素数量。更准确地说，`sys.maxsize` 表示的是Python解释器所能支持的最大整数值，这个值依赖于平台和Python解释器的位数。

在32位系统中，`sys.maxsize` 通常被设置为 `2^31 - 1`，即 `2147483647`。在64位系统中，`sys.maxsize` 通常被设置为 `2^63 - 1`，即 `9223372036854775807`。

这个值经常被用于确定数据结构的容量限制，或者在需要根据系统最大值来设置算法某些参数时使用。例如，在实现排序算法或者进行大文件处理时，可能会根据 `sys.maxsize` 来决定是否需要采用特殊的处理方式来避免整数溢出的问题。

使用 `sys.maxsize` 的一个例子如下：

```
import sys

# 打印sys.maxsize的值
print(sys.maxsize)

# 根据sys.maxsize来确定一个合适的数组大小
array_size = min(sys.maxsize, 10000)  # 选取sys.maxsize和10000中较小的一个
```

在实际编程中，应该根据实际情况和需求来合理使用 `sys.maxsize`。

# 堆(heapq)

堆能够实现优先队列的原因是因为堆具有以下特性：

1. 堆是一个完全二叉树，通常是通过数组实现的。在堆中，父节点的值要么始终小于（最小堆），要么始终大于（最大堆）其子节点的值。
2. 在堆中，插入和删除的时间复杂度较低，插入的复杂度为 O(log n)，删除的复杂度也为 O(log n)，n 为堆中元素的个数。

这些特性使得堆非常适合实现优先队列。在优先队列中，元素被分配了一个优先级，并且当访问队列时，具有最高（或最低）优先级的元素首先被访问。

在Python中，可以使用 `heapq` 模块来实现堆，从而实现优先队列。这个模块提供了一些堆操作的函数，包括将元素推入堆（`heappush`）、从堆中弹出最小的元素（`heappop`）等。

以下是 `heapq` 模块的一些基本操作：

1. 创建一个空堆

```python
heap = []
```

1. 将元素推入堆

```python
import heapq
heapq.heappush(heap, 3)
heapq.heappush(heap, 1)
heapq.heappush(heap, 2)
# 现在 heap 的顺序是 [1, 3, 2]
```

1. 从堆中弹出最小的元素

```python
print(heapq.heappop(heap))  # 输出 1
# 现在 heap 的顺序是 [2, 3]
```

通过这种方式，堆实现了一个优先队列，可以方便地实现按优先级访问元素，使得具有最高（或最低）优先级的元素能够被优先访问。

在 Python 中，如果入堆的元素是多个元素组成的元组、列表或字典，出堆的顺序将按照以下规则进行比较：

1. 对于元组：Python 会按照元组中的元素从第一个开始进行依次比较，直到找到不相等的元素为止。例如，对于元组 (a, b, c)，Python 会首先比较 a，如果 a 相等，则比较 b，以此类推。
2. 对于字典：字典类型本身是不可比较的，因此无法直接将它们用于堆的比较。
3. 列表：和元组的判断方式是一样的。

因此，如果入堆的元素是多个元素组成的元组，则出堆的顺序将按照元组中的元素从左到右依次比较。

以下是一个使用元组入堆并出堆的示例：

```python
import heapq

heap = []
heapq.heappush(heap, (3, 'apple'))
heapq.heappush(heap, (1, 'banana'))
heapq.heappush(heap, (2, 'orange'))

while heap:
    print(heapq.heappop(heap))
```

运行上述代码会输出：

```
(1, 'banana')
(2, 'orange')
(3, 'apple')
```

在这个示例中，我们入堆的元素是元组，每个元组包含两个部分：一个数字和一个字符串。出堆的顺序是按照元组中的第一个元素（数字）进行比较的。
