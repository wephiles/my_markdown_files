- pandas模块
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

- pickle模块

    - pickle库是Python中用于序列化和反序列化Python对象结构的模块。"序列化"指的是将Python对象转换为字节流，以便可以将其存储到磁盘上或通过网络传输到远程位置。"反序列化"则是将这些字节流转换回原始Python对象。  这个库对于数据持久化和跨程序共享对象非常有用。例如，你可以使用pickle库将机器学习模型训练后的状态保存下来，然后在另一个程序中加载这个状态，以便进行预测。
        - pickle.dump(data, file_object)  使用pickle库将数据对象序列化为字节流
        - pickle.load(file_object)  使用pickle库将字节流反序列化为数据对象
        

- collections模块
  - collections是Python的一个内置模块，它实现了特殊的容器数据类型，提供了Python内置的数据类型（如dict，list，set，和tuple）的替代选择。
  - defaultdict是collections模块中的一个类。它继承自内置的dict类，其功能与dict类似，但是它有一个特性：如果你试图访问或修改defaultdict中不存在的键，它会首先为这个键生成一个默认值。这个默认值是在创建defaultdict对象时通过传递一个函数（或者是一个默认值）来指定的。这个特性使得defaultdict在处理不存在的键时更加方便，因为它可以自动为不存在的键提供一个默认值，而不需要我们手动检查键是否存在或者捕获KeyError异常

  ```python
  from collections import defaultdict
  
  # 创建一个defaultdict，指定默认值为int类型，即0
  d = defaultdict(int)
  
  # 访问不存在的键，返回默认值0
  print(d['key'])  # 输出：0
  
  # 修改不存在的键，首先生成默认值0，然后将其加1
  d['key'] += 1
  print(d['key'])  # 输出：1
  ```

- dict(python内置字典)
    - setdefault(key, 默认值) setdefault是Python字典（dict）的一个方法。它的作用是如果字典中包含有给定键，则返回该键对应的值，否则返回为该键设置的默认值。如果键在字典中不存在，该方法还会将默认值插入到字典中。等于字典中的get()方法

- operator模块
  - itemgetter() itemgetter是Python的operator模块中的一个函数。它的主要作用是创建一个可调用对象，该对象以一个或多个索引参数获取序列或映射中的项。这个函数通常用于需要自定义排序或数据提取的场景
  - itemgetter 是 Python 标准库 operator 模块中的一个函数，它用于创建一个从指定数据项获取值的函数。这个函数通常用于多维数据的索引，比如列表或元组，以及在排序操作中指定排序的依据。itemgetter 可以接收一个或多个参数，这些参数指定了要从数据项中获取的索引位置。
  - ！！！ itemgetter()定义了一个函数 ！！！
    ```python
    from operator import itemgetter
    
    # 创建一个包含元组的列表，每个元组代表一个记录
    records = [
        ('sandy', 34),
        ('jane', 26),
        ('jim', 38),
        ('kate', 29)
    ]
    
    # 使用 itemgetter 创建一个函数，该函数根据元组中的第二个元素（年龄）来获取值
    get_age = itemgetter(1)
    
    # 使用这个函数来获取记录中的年龄
    print(get_age(records[0]))  # 输出: 34
    
    # 在排序时，可以使用 itemgetter 来指定排序的依据
    # 例如，按照年龄升序排序
    sorted_records = sorted(records, key=itemgetter(1))
    print(sorted_records)  # 输出: [('sandy', 34), ('jane', 26), ('kate', 29), ('jim', 38)]
    
    # 也可以按照年龄降序排序
    sorted_records_desc = sorted(records, key=itemgetter(1, reverse=True))
    print(sorted_records_desc)  # 输出: [('jim', 38), ('sandy', 34), ('kate', 29), ('jane', 26)]
    ```

- yield关键字
    - yield 是 Python 中的一个关键字，它的主要作用是将一个普通的函数转变为一个生成器（generator）。生成器是一种特殊的迭代器，不需要我们自己去编写迭代器的 __iter__() 和 __next__() 方法，只需要使用 yield 关键字就可以实现。  当一个函数被调用时，它会执行函数体中的代码，直到遇到 return 语句或者函数体结束。而当一个生成器被调用时，每次遇到 yield 语句时，函数会暂停并保存当前所有的运行信息，返回 yield 的值，并在下一次调用 next() 方法（或 for 循环）时从当前位置继续运行。  这种特性使得生成器非常适合用于需要大量或无限的序列，而又不需要一次性生成并保存在内存中的场景，例如文件读取，网络数据传输等。
    - 有yield的函数则返回一个可迭代的生成器generator对象，你可以使用for循环或者调用next()方法，send()方法遍历这个产生的实例化生成器对象来提取结果。
    - 生成器函数返回一个生成器对象，针对生成器对象，python提供了两个主要方法，一个是next()一个是send()。
    - next() 第一次对生成器对象调用next()，相当于启动生成器，会从生成器函数的第一行代码开始执行，直到第一次执行完yield语句后，跳出生成器函数。之后调用next()，进入生成器函数后，会从yield语句的下一句语句开始执行，然后重新运行到yield语句，执行后，跳出生成器函数。后面再次调用next()，依此类推。即执行一次next()则调用一次生成器函数，直至抛出不可迭代的错误。
        - 程序开始执行以后，因为fun_yield中有yield关键字，所以函数并不会真的执行，而是先得到一个实例化的生成器对象;
        - 直到调用next()，fun_yield正式开始执行;
    - send() send()函数和next()函数其实很相似，唯一的区别在于send()函数可以传入值，而next()函数不能传值，第一次调用时不能使用send()发送一个非       None的值，否则会出错的，因为没有yield语句来接收这个值。

- numpy1.26.3对应的hyperopt可用版本为0.2.5(暂时未知是否还有其他的低于0.2.5版本的hyperopt是被支持)，高于0.2.5版本的hyperopt是不被支持的

- pandas3.0的新特性
    - FutureWarning: A value is trying to be set on a copy of a DataFrame or Series through chained assignment using an inplace method.
    The behavior will change in pandas 3.0. This inplace method will never work because the intermediate object on which we are setting values always behaves as a copy.
    For example, when doing 'df[col].method(value, inplace=True)', try using 'df.method({col: value}, inplace=True)' or df[col] = df[col].method(value) instead, to perform the operation inplace on the original object.

- imp库
    - imp库在Python中是一个用于动态导入Python模块的库。它提供了一些函数，可以在运行时动态地加载和重新加载Python模块。
    - 这对于在运行时改变程序行为非常有用。  以下是一些imp库的主要函数：
    - imp.reload(module): 重新加载一个已经加载的模块。这对于在不退出Python解释器的情况下测试模块的修改非常有用。
    - imp.load_source(name, pathname[, file]): 从源文件加载一个模块。
    - imp.load_module(name, file, pathname, description): 加载一个模块，不管它是从源代码、编译的字节码还是动态链接的库。
    - 需要注意的是，从Python 3.4开始，imp库已经被标记为过时，大部分功能已经被importlib库取代。

- random模块
    - random模块在Python中用于生成伪随机数。它提供了一系列的函数，可以用来生成各种类型的随机数据，包括整数、浮点数、随机选择、随机排列等。  以下是一些random模块的主要函数：
    - random.random(): 返回一个在[0.0, 1.0)范围内的随机浮点数。
    - random.uniform(a, b): 返回一个在[a, b]范围内的随机浮点数。
    - random.randint(a, b): 返回一个在[a, b]范围内的随机整数。
    - random.randrange(start, stop[, step]): 返回一个从start开始，到stop结束，步长为step的随机整数。
    - random.choice(seq): 从序列seq中随机选择一个元素。
    - random.shuffle(seq): 将序列seq中的元素随机排列，返回None。
    - random.sample(population, k): 从总体序列或集合中，随机获取k个独立的元素。
    - 需要注意的是，random模块生成的是伪随机数，也就是说，它们是由一个确定的算法生成的，只是看起来像是随机的。如果你需要更高级的随机数，例如在密码学或安全性要求较高的场景中，你应该使用secrets模块或者numpy.random模块。
    - random.seed()函数在Python的random模块中，用于初始化随机数生成器。如果你不调用random.seed()，Python会使用系统当前时间来作为种子值。  当你为random.seed()提供一个特定的值（称为种子值）时，它会产生一个确定的随机数序列。也就是说，使用相同的种子值，你每次运行程序时，random模块生成的随机数序列都是一样的。这在需要重现结果的情况下非常有用，例如在调试程序或者进行科学研究时。  如果你不提供种子值，或者调用random.seed()时不带任何参数，那么Python会使用系统当前时间（或者其他来源的随机数）作为种子值，这样每次运行程序时，生成的随机数序列都会不同。

- HR(Hit Ratio)
    - 命中率，HR强调的是模型推荐的准确性，即用户的需求项是否包含在模型的推荐项中。

- MRR(Mean Reciprocal Rank)
    -  平均倒数排名,强调的是用户的需求项在模型推荐列表中的位置，越靠前越佳。

- NDCG()
    - 归一化折损累计增益

    - pycharm文档字符串不自动补全参数和返回值：
        - 参考这个网址：https://m.jb51.net/article/237020.htm

- enumerate()
    - enumerate()函数在Python中是一个内置函数，它允许我们在遍历一个序列（例如列表、元组、字符串等）的同时，获取当前元素的索引。
    - 其中，iterable是一个可迭代对象，start是可选参数，用于指定索引的起始值，默认为0
    - numerate()函数会返回一个枚举对象，该对象生成由索引和对应元素组成的元组，可以通过for循环来遍历

- 已经卸载pyarrow-6.0.1 成功安装Pyarrow-15.0.0

- scipy模块
    - scipy 是一个用于数学、科学和工程的 Python 库。它包含了大量的模块，用于优化、线性代数、积分、插值、特殊函数、快速傅里叶变换、信号处理和图像处理、常微分方程求解和其他科学与工程中常用的任务。
    - scipy.sparse 被用于处理稀疏矩阵。稀疏矩阵是其大部分元素为零的矩阵，使用稀疏表示可以节省大量内存。scipy.sparse 提供了多种稀疏矩阵的存储格式，如 CSR (Compressed Sparse Row)、CSC (Compressed Sparse Column) 等，并提供了这些稀疏矩阵的基本操作函数，如矩阵乘法、求和等。
    - scipy模块的功能：
        - 优化：寻找函数的最小值或最大值，解决线性规划问题等。
        - 插值：估计落在已知值范围内的未知值。
        - 线性代数：解决线性方程，计算行列式，特征值和特征向量等
        - 积分：计算定积分和不定积分，解决微分方程等。
        - 信号处理：卷积，相关，傅立叶分析，滤波等。
        - 统计：概率分布，统计测试等。

- argpartition
    - argpartition 是 NumPy 库中的一个函数，它可以找到数组中第 k 小的元素，并按此元素将数组分为两部分。在返回的索引数组中，前 k 个元素是数组中最小的 k 个元素（无序），剩余的元素是数组中其余的元素（无序）。

- numpy库中
    - 在数组前面加个负号（-）就会把数组中所有元素全部变成与各自相对应的相反数。

- 建立用户协同矩阵：
  - 以下步骤建立用户协同矩阵（User Similarity Matrix）：
```
"""
  创建倒排索引（Inverted File Index）：

  首先，程序遍历用户和物品的交互数据，为每个物品创建一个用户集合。这个集合包含了所有喜欢该物品的用户。这样，对于每个物品，程序每个物品都有一个对应的用户列表，这就是倒排索引。
  初始化用户协同矩阵：
  
  创建一个空的字典user_sim_matrix，用于存储用户之间的相似度。这个字典的键是用户ID，值是另一个字典，用于记录与其他用户的相似度。
  计算用户对物品的交集：
  
  对于倒排索引中的每个物品，程序遍历喜欢该物品的所有用户。对于每一对用户（u和v），如果他们不是同一个用户，就计算他们的交集。交集是通过计算两个用户共同喜欢的物品数量得到的。
  计算相似度：
  
  对于每一对用户，程序使用以下公式计算相似度：
  user_sim_matrix.setdefault(u, defaultdict(int))  # 初始化用户u的相似度字典
  user_sim_matrix[u][v] += 1. / math.log(1 + len(item_user[item]))
  这里，len(item_user[item])是喜欢该物品的用户数量，math.log(1 + len(item_user[item]))是对用户数量取对数，用于平滑处理，避免用户数量为0时的除零错误。
  归一化相似度：
  
  在计算完所有物品的用户对相似度后，程序对每个用户对的相似度进行归一化。归一化的公式是：
  user_sim_matrix[u][v] = con_items_count / math.sqrt(N[u] * N[v])
  这里，con_items_count是两个用户共同喜欢的物品数量，N[u]和N[v]分别是两个用户的购买商品数。归一化是通过除以两个用户购买商品数的平方根来实现的，这样可以使得相似度值在0到1之间，并且用户购买商品越多，相似度越小。
  保存用户协同矩阵：
  
  最后，程序将计算好的用户协同矩阵保存到文件中，以便后续使用。
  通过这个过程，程序能够为每个用户生成一个与其他用户相似度的矩阵，这个矩阵可以用于后续的推荐算法，如基于用户的协同过滤（User-based Collaborative Filtering）。这种方法可以有效地减少在推荐时计算相似度的计算量，因为相似度矩阵是预先计算好的。
"""
```

- 在Python中，字符串前面的r，u，和f都是前缀，它们分别表示原始字符串，Unicode字符串和格式化字符串

    -   r：原始字符串。在原始字符串中，所有的字符都是直接按照字面的意思来使用，没有转义特殊或不能打印的字符。原始字符串除在字符串的第一个引号前加上字母r（可以大小写）以外，与普通字符串有着几乎完全相同的语法

    -   u：Unicode字符串。在Python 2中，u前缀用于表示Unicode字符串。但在Python 3中，所有的字符串都是Unicode字符串，所以u前缀不再需要。

    -   f：格式化字符串。在Python 3.6及以上版本，f前缀用于创建格式化字符串。在格式化字符串中，可以在字符串内部使用花括号 {} 包围的表达式，这些表达式会被其值替换。

    -   b：字节字符串。在Python中，b前缀用于表示字节字符串。字节字符串是由单个字节作为基本元素（8位或者256个可能的值）的字符串。SS

- 在Python中，`super()`函数和直接调用父类构造器（如`ClassName.__init__()`）都可以用来初始化继承的类的属性。它们的主要区别在于它们如何确定应该调用哪个父类的构造器，以及它们在多重继承情况下的行为。

    - `super().__init__()` 的使用方式
        `super()`函数在Python 3.x中用于调用父类的方法，特别是当涉及到多重继承时。它会自动遵循方法解析顺序（MRO），这是Python解释器用来确定继承链中方法调用顺序的机制。使用`super()`时，你不需要知道父类的确切名称，因为Python会自动找到正确的父类。

        ```python
        class Parent(object):
            def __init__(self, value):
                self.value = value
        
        class Child(Parent):
            def __init__(self, value, extra):
                super().__init__(value)  # 调用Parent类的构造器
                self.extra = extra
        
        # 使用Child类创建实例
        child_instance = Child(10, "extra value")
        ```

        在这个例子中，`Child`类的构造器首先调用了`Parent`类的构造器，传递了`value`参数。然后，它继续设置`Child`类特有的属性`extra`。

    - `ClassName.__init__()` 的使用方式
        直接调用父类构造器的方式在Python 2.x中更常见，但在Python 3.x中不推荐使用，因为它不遵循MRO。这种方式需要你明确指定父类的名称。

        ```python
        class Parent(object):
            def __init__(self, value):
                self.value = value
        
        class Child(Parent):
            def __init__(self, value, extra):
                Parent.__init__(self, value)  # 直接调用Parent类的构造器
                self.extra = extra
        
        # 使用Child类创建实例
        child_instance = Child(10, "extra value")
        ```

        在这个例子中，我们直接调用了`Parent`类的构造器，而不是使用`super()`。

    - 区别

        - **MRO遵循**：

            - `super().__init__()`遵循MRO，这意味着在多重继承的情况下，它会正确地调用父类的构造器。

            - `ClassName.__init__()`不遵循MRO，它直接调用你指定的类，这可能导致在复杂的继承结构中调用错误的构造器。

        - **代码清晰度**：

            - 使用`super()`时，代码更加清晰，因为它表明你正在调用当前类的直接父类的构造器。

            - 直接调用父类构造器可能使代码更难理解，尤其是在继承链很长或复杂的情况下。

        - **Python版本兼容性**：

            - 在Python 2.x中，`super()`和直接调用父类构造器都可以工作，但直接调用父类构造器更常见。

            - 在Python 3.x中，推荐使用`super()`，因为它与MRO的改进相一致。

        - **错误处理**：

            - 如果你错误地指定了父类的名称，直接调用父类构造器可能导致运行时错误。

            - 使用`super()`可以减少这种类型的错误，因为它会自动找到正确的父类。

    - 总结来说，`super().__init__()`是Python 3.x中推荐的方式，因为它遵循MRO，提供了更好的错误处理，并且使代码更加清晰。而`ClassName.__init__()`虽然在某些情况下仍然可以使用，但它的直接性可能导致在复杂的继承结构中出现错误。

- 在`Python`中，`rfind` 方法是字符串（`str` 类型）的一个内置方法，它用于在字符串中从右到左查找子字符串的位置。与 `find` 方法不同，`find` 是从左到右查找，而 `rfind` 是从右到左查找。如果子字符串在字符串中找到了，`rfind` 返回子字符串最后一次出现的索引位置；如果未找到，则返回 `-1`。

- Python sorted函数
    ![image-20240301142846085](.\assets\image-20240301142846085.png)

- `itemgetter` 函数是 Python 标准库 `operator` 模块中的一个函数，它用于从列表的元素中提取指定的子项，并返回一个函数，这个函数可以接受一个序列（如列表或元组）作为输入，并返回指定的子项。这个功能通常用于排序操作，尤其是当你需要根据列表中的特定元素进行排序时。

    `itemgetter` 可以接受一个或多个整数作为参数，这些整数代表了你想要提取的元素的索引位置。例如，如果你有一个包含元组的列表，你可以使用 `itemgetter` 来根据元组中的某个特定元素进行排序。

    这里有一个使用 `itemgetter` 进行排序的例子：

    ```
    复制from operator import itemgetter
    
    # 假设我们有一个包含元组的列表，每个元组代表一个人的名字和年龄
    people = [
        ('Alice', 30),
        ('Bob', 25),
        ('Charlie', 35),
        ('David', 28)
    ]
    
    # 使用 itemgetter 根据年龄排序
    sorted_people = sorted(people, key=itemgetter(1))
    
    print(sorted_people)  # 输出: [('Bob', 25), ('Alice', 30), ('David', 28), ('Charlie', 35)]
    ```

    在这个例子中，`itemgetter(1)` 创建了一个函数，这个函数接受一个元组并返回元组的第二个元素（索引为 1 的元素，即年龄）。然后，`sorted` 函数使用这个函数作为排序的关键字，从而根据每个人的年龄对列表进行排序。

    `itemgetter` 也可以接受多个索引，用于更复杂的排序需求，例如根据多个字段进行排序。这种情况下，`itemgetter` 会返回一个元组，其中包含所有指定的子项。


- 当然，让我们更详细地探讨 `itemgetter` 函数的用法和它在排序中的应用。

    `itemgetter` 函数是 `operator` 模块中的一个实用工具，它允许你通过指定索引来创建一个获取元素的函数。这个函数可以用于 `sorted` 函数的 `key` 参数，以便根据列表中元素的特定子项进行排序。这在处理复杂数据结构，如包含多个字段的记录或对象时特别有用。

    **基本用法**

    `itemgetter` 可以接收一个或多个整数参数，这些参数指定了要从序列中提取的元素的索引。例如：

    ```
    from operator import itemgetter
    
    # 创建一个根据索引1（第二个元素）获取元素的函数
    get_second_item = itemgetter(1)
    
    # 使用这个函数获取列表中每个元组的第二个元素
    result = [get_second_item(item) for item in [('a', 1), ('b', 2), ('c', 3)]]
    print(result)  # 输出: [1, 2, 3]
    ```

    **排序**

    在排序中，`itemgetter` 通常用于指定排序的依据。例如，如果你有一个包含多个字段的列表，你可能想要根据某个特定字段进行排序。这时，你可以使用 `itemgetter` 来实现这一点。

    ```
    from operator import itemgetter
    
    # 假设我们有一个包含姓名和年龄的列表
    people = [
        ('Alice', 30),
        ('Bob', 25),
        ('Charlie', 35),
        ('David', 28)
    ]
    
    # 使用 itemgetter 根据年龄（索引1）进行降序排序
    sorted_people = sorted(people, key=itemgetter(1), reverse=True)
    
    print(sorted_people)  # 输出: [('Charlie', 35), ('Alice', 30), ('David', 28), ('Bob', 25)]
    ```

    在这个例子中，`itemgetter(1)` 创建了一个函数，这个函数接受一个元组并返回元组的第二个元素（年龄）。然后，`sorted` 函数使用这个函数作为排序的关键字，并通过设置 `reverse=True` 来实现降序排序。

    **多字段排序**

    `itemgetter` 还可以接受多个索引，允许你根据多个字段进行排序。这在数据库查询或处理多维数据时非常有用。例如，你可能想要先按年龄升序排序，然后在年龄相同的情况下按姓名降序排序。

    ```
    from operator import itemgetter
    
    # 使用 itemgetter 根据年龄升序排序，年龄相同的情况下按姓名降序排序
    sorted_people = sorted(people, key=itemgetter(1, 0), reverse=[False, True])
    
    print(sorted_people)  # 输出: [('Bob', 25), ('Alice', 30), ('David', 28), ('Charlie', 35)]
    ```

    在这个例子中，`itemgetter(1, 0)` 创建了一个函数，它首先根据年龄（索引1）排序，然后根据姓名（索引0）排序。`reverse` 参数是一个列表，它为每个字段指定了排序的方向。在这个例子中，年龄的排序方向是升序（`False`），而姓名的排序方向是降序（`True`）。

    `itemgetter` 是一个非常灵活的工具，它可以帮助你在处理列表和元组时进行复杂的排序操作。通过合理使用 `itemgetter`，你可以轻松地根据一个或多个字段对数据进行排序。

- `map()` `Python`的`map()`函数是一个非常有用的工具，它可以对可迭代对象中的每个元素应用一个指定的函数，然后返回一个迭代器，其中包含了所有元素经过函数处理后的结果。 -- 参考 https://blog.csdn.net/wuShiJingZuo/article/details/135620145


    - 基本语法：
        ```python
        map(function, iterable, ...)
        ```
    
    - 在使用map()函数时，有一些注意事项需要牢记：
    
        - map()函数返回的是一个迭代器，如果需要立即获取结果，需要将其转换为列表或其他数据结构。
        - 传递给map()的函数可以是自定义函数，也可以是内置函数或匿名函数（lambda表达式）。
        - 如果传递给map()的可迭代对象的长度不一致，map()将在最短的可迭代对象耗尽后停止迭代。
        - 在Python 3中，map()函数的返回值已经不再是列表，而是迭代器。如果需要列表，必须显式地将其转换为列表。





