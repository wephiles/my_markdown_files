<h1 style="text-align: center; font-size: 70px;">Python内存管理</h1> 

—— 基于C语言源码底层分析

详情参考：`https://pythonav.com/wiki/detail/6/88/`

引用计数器为主，标记清除和分代回收为辅 + 缓存机制

-   引用计数器
-   标记清除
-   分代回收
-   缓存机制
-   Python的C源码（3.8.2版本）

## 引用计数器

### 环状双向链表 `refchain`

```C
static PyObject refchain = {&refchain, &refchain};
```

在`Python`程序中，创建的任何一个对象都会加在这个双向链表中

```python
name = "xxx"
age = 18
hobby = ["xxxx", "xxxxx", "xxxxxx"]
```

创建的不同类型的对象，放到链表中的时候，内部存储的数据可能不一样。

相同点与不同点：

```python
# 每一个新创建的对象 内部创建一些数据 [上一个对象 下一个对象 类型 引用个数]
# 下面这条语句，不会创建两个字符串，而会让新创建的对象的指针指向name这个对象的指针所指的内存块 就需要引用个数
name = "xxxx"
new = name  

# [上一个对象 下一个对象 类型 引用个数 value]
age = 18

# 每一个新创建的对象 内部创建一些数据 [上一个对象 下一个对象 类型 引用个数 item=... 元素个数]
hobby = ["xxxx", "xxxxx", "xxxxxx"]
```

在C源码中，如何体现每个对象相同的东西      ——  `PyObject`结构体，封装了四个值

在C源码中，有多个元素组成的对象            ——  `PyObject`结构体，封装了四个值 + `* ob_size`

### 类型封装结构体

```python
data = 3.14
# 内部会创建：
"""
_ob_next  = refchain 中的下一个对象
_ob_prev  = refchain 中的上一个对象
ob_refcnt = 1
ob_type   = float
ob_fval   = 3.14
"""
```

```c
// 在C源码中：
typedef struct {
    PyObject_HEAD  // 公用的数据
    double ob_fval;  // 存的是3.14这个值
} PyFloatObject;
```

### 引用计数器

```python
v1 = 3.14
v2 = 999
v3 = (1, 2, 3)
```

当`Python`程序运行时，会根据数据类型的不同，找到其对应的结构体，根据结构体中的字段创建相关的数据，然后将对象添加到`refchain`双向链表中。

在源码中，有两个关键的结构体：

`PyObject`和`PyVarObject`

每个对象都有`ob_refcnt`，就是引用计数器。值默认为1，当有其他变量引用对象时，计数器值就会发生变化。

-   引用

```python
a = 123
b = a
```

-   去除引用

```python
a = 123
b = a
del b  # b 变量删除 b对应的对象引用计数器 - 1
del a  # a 变量删除 a对应的对象引用计数器 - 1

# 当引用计数器变为0的时候，意味着没有变量使用这个对象，这个对象就是垃圾了，需要回收
	# 1. 将对象从refchain链表中移除
	# 2. 将对象销毁，将内存归还给内存
```

#### BUG：循环引用 & 交叉感染

```python
v1 = [11, 22, 33]
v2 = [44, 55, 66]
v1.append(v2)  # v1的引用计数器变为2
v2.append(v1)  # v2的引用计数器变为2

del v1  # 引用计数器 - 1
del v2  # 引用计数器 - 1
```

这样的代码越来越多的话，内存中就会一直被消耗。电脑重启就可以恢复

## 标记清除

—— 为了解决引用计数器循环引用的不足而产生的

如何实现的：在Python的底层中，再维护一个链表，专门放可能存在循环引用的对象。 —— 列表、字典、元组、集合

在内部，`某种情况下，会扫描可能存在循环引用的链表的每个元素，也会扫描子元素，如果最后又找回来了，那么说明有循环引用，如果有，那么让双方的引用计数器各自都 - 1，如果是0，那么是垃圾，如果不是0，那么不做处理` 

`BUG`: 

-   什么时候扫描 
-   可能存在循环引用的链表的扫描的代价比较大
-   上面两个问题怎么解决呢？ —— 分代回收

## 分代回收

把可能存在循环引用的对象维护成三个链表，分别是0代，1代，和2代

-   0代： 0代中的对象个数达到700个，扫描一次
    -   如果是垃圾，自减1，如果不是垃圾，那么就升级，从0代升到1代
-   1代： 0代扫描10次，那么1代扫描一次
-   2代： 1代扫描10次，那么2代扫描一次

## 小结

在Python中，维护了一个`refchain`的双向环状链表，存储程序中创建的所有对象，每种类型的对象中都有一个`ob_refcnt`引用计数器的值，维护着引用的个数，引用个数加一、减一，当引用计数器变为0的时候，则会进行垃圾回收（对象销毁、`refchain`中删除）。

但是，在`Python`中对于那些可以由多个元素组成的对象可能会存在循环引用的问题，为解决这个问题，`Python`引用了标记清除和分代回收，在其内部，维护四个链表，分别是`refchain`，还有0（700个） 1（10次） 2（10次）三代链表，在源码内部，达到各自的阈值时，就会触发扫描链表进行标记清除的动作，有循环的话，那么引用计数器的值各自减一，

但是，上面虽说是这样，在`Python`内部可能有一个点是需要优化的 —— 缓存

## Python缓存

### 池（int类型）

为了避免重复地创建和销毁常见对象，维护**池**。

```python
# 启动解释器的时候，会创建-5 -4 ...... 257区域的值，Python认为这些值是常见的
# 下面在交互模式下才起作用！！！
v1 = 7  # Python中不会开辟内存，直接去池中获取
v2 = 9  # Python中不会开辟内存，直接去池中获取
# 创建了三个对象 插入到refchain链表中

v3 = 9  # Python中不会开辟内存，直接去池中获取

print(id(v2))
print(id(v3))
# 我们发现他是一样的

# 如果是下面这样，且在交互模式下：
v4 = 999
v5 = 666
v6 = 666
# 上面三个会创建三个不同的对象
```

### `free_list`（`float/list/tuple/dict`）

当一个对象的引用计数器为0的时候，按理说应该回收，但是在Python中不会回收，而是将对象添加到free_list中，当做缓存，以后再创建对象的时候不再重新开辟内存空间，而是直接使用这个`free_list`。

```python
v1 = 3.14    # 开辟内存，内部存储结构体中定义几个值并存储到refchain中

del v1       # 从refchain中摘除，不会销毁，将对象添加到free_list中，free_list会有一个个数限制。free_list缓冲满了才销毁

v9 = 999.99  # 不会重新开辟内存，去free_list中获取对象，对象内部数据初始化，再放到refchain中
```

总结：缓存机制：

-   `int`类型     ：`small_ints` 池 `范围：[-5, 257)`
-   `float`类型   ：`free_list `100个
-   `str`类型     ：维护`unicode_latin1[256]`链表，内部将所有的`ascii字符`缓存起来，以后使用时就不再反复创建。
-   `list`类型    ：`free_list `80个
-   `tuple`类型   ：维护一个free_list数组且数组容量20，数组中元素可以是链表且每个链表最多可以容纳2000个元组对象。
-   `dict`类型    ：`free_list `80个

## 源码分析

此处等有时间再写。



































