# 模块和面向对象-day08

概要：

- 模块
    - 自定义模块（已经讲了）
    - 内置模块
        - `shutil`
        - `re` 正则表达式
    - 第三方模块
        - `requests `模块
        - `bs4` 模块
- 面向对象: 面向对象(Object-Oriented Programming)，简称OOP,是一种编程范式，它使用“对象”来设计软件，这些对象包含了数据（属性）和可以操作这些数据的方法。面向对象的核心思想是将现实世界中的事物抽象成对象，通过对象之间的交互来实现软件功能。 面向对象编程具有以下几个基本特性：
    1. **封装（Encapsulation）**：封装是将对象的状态（属性）和行为（方法）结合在一起，并对外隐藏其内部实现细节的过程。通过使用访问修饰符（如public、private等）来控制对对象内部状态的访问，确保对象的完整性和安全性。
    2. **继承（Inheritance）**：继承是一种可以让一个类（子类或派生类）继承另一个类（父类或基类）属性和方法的机制。继承支持代码的重用，并能够建立类之间的层次关系，使得子类具有父类的所有特性，并且还可以添加或修改原有的行为。
    3. **多态（Polymorphism）**：多态是指允许使用子类的对象来替代父类的对象，从而在运行时确定具体调用哪个类的方法。多态性可以使得代码更加灵活和可扩展，同时也支持接口的实现，允许不同的对象对同一消息做出响应。

## 1 模块

### 1.1 自定义模块

- `py`文件或者文件夹
- `from `、`import`
- `sys.path`【运行的当前脚本的目录+系统内置模块的目录】
- 自己的模块名不要和内置模块名冲突。

#### 补充-主文件

主文件：就是程序的入口，只有执行这个主文件(`.py`文件)，程序才能运行起来.

```python
# 运行当前脚本时，__name__是python内部创建的一个变量 __name__ = "__main__"
# 如果当前的脚本是别人导入执行的，那么python会在这个脚本的内部创建__name__ = "module_name"
if __name__ == "__main__":  # 标志这个文件是主文件 
    ...
```

- 标志：含有`if __name__ == "__main__":`的为主文件
- 防止别人导入咱们的程序时执行程序。只有自己主动执行时才会执行程序。

### 1.2 内置模块

- `os`
- `random`
- `hashlib`
- `json`
- `time`
- `datetime`

#### 1.2.1 `shutil`模块

- 删除==**文件夹**==
  
    > [!IMPORTANT]
    >
    > 是删除**文件夹** 不是删除文件
    
    ```python
    import shutil
    
    shutil.rmtree("xx/xxx/xxxx")
    ```
    
- 拷贝文件夹
    ```python
    import shutil
    
    shutil.copytree("原文件夹", "目标文件夹路径")  # 没有文件夹会自动创建
    ```

    ```python
    import shutil
    shutil.copytree(r"D:/tree", r"D:/xx/xxx/xxxx")
    ```

- 拷贝文件
    ```python
    import shutil
    
    shutil.copy("源文件路径", "目标文件夹路径")
    ```

    ```python
    import shutil
    shutil.copytree(r"D:/tree/xxx.txt", r"D:/xx/xxx/xxxx")  # 如果不存在xxxx，那么创建一个较xxxx的文件（这个文件没有后缀）
    shutil.copytree(r"D:/tree/xxx.txt", r"D:/xx/xxx/xxxx/")  # 拷贝文件到文件夹 文件夹要是不存在会报错
    ```

- 重命名文件/文件夹
    ```python
    import shutil
    
    shutil.move("原来的文件名/文件夹名", "改变名字之后的文件名/文件夹名")  # 源文件不存在会报错 源文件夹不存在也会报错
    ```

- 压缩、解压缩
    ```python
    import shutil
    
    # 压缩
    # base_name: 压缩包文件名 format: 后缀名 root_dir: 要压缩到的文件夹路径
    shutil.make_archive(base_name="xx", format="zip", root_dir="xx/xxx/xxxx/")
    
    # 解压
    # filename: 压缩包文件名 extract_dir: 解压目录 format: 压缩的格式
    shutil.unpack(filename="xx.zip", extract_dir="xx/xxx/xxxx/", format="zip")
    ```

练习题：目录层级如下所示

```python
day01
	01 fullstack s7 day01 xxx.mp4
    02 fullstack s7 day01 xxx.mp4
    03 fullstack s7 day01 xxx.mp4
    04 fullstack s7 day01 xxx.mp4
    xxxx.md
```

寻找day01目录下的所有mp4为后缀的文件 重命名为

`04 fullstack s7 day01 xxx.mp4 -> 01 xxx.mp4`

```python
import os
import shutil

folder_path = r"D:\CSProjects\PycharmProjects\studyProject\wupeiqiStudyBilibili\day07\day01"

for name in os.listdir(folder_path):
    if name.rsplit(".", maxsplit=1)[-1] == "mp4":  # 参数“.”表示从右边(rsplit)分割 maxsplit=1表示分割右边第一个点
        new_name = name.replace("fullstack s7 day01 ", "")
        shutil.move(os.path.join(folder_path, name), os.path.join(folder_path, new_name))
```

#### 1.2.2 `re`模块

- 正则表达式？【与语言无关】
- `python`中的`re`模块

正则表达式是干什么的？

```python
text = """正则表达式，又称规则表达式，（Regular Expression，在代码中常简写为regex、regexp或RE），是一种文本模式，包括普通字符（例如，a到z之间的字母）和特殊字符（称为“元字符”），是计算机科学的一个概念。正则表达式是对字符串（包括普通字符和特殊字符）操作的一种逻辑公式，就是用事先定义好的一些特定字符以及这些特定字符的组合，组成一个“规则字符串”，这个“规则字符串”用来表达对字符串的一种过滤逻辑。正则表达式用来检索、替换那些符合某个模式（规则）的文本，通常被用来检索、替换那些符合某个模式（规则）的文本。正则表达式可以从一个基础字符串中根据一定的匹配模式替换文本中的字符串、验证表单、提取字符串等等，许多程序设计语言都支持利用正则表达式进行字符串操作。楼主:瑾瑜，电话 18866666666，邮箱: 12345679@163.com。求点赞求转发，求一键三连！！！"""

# 需求：将字符串中的邮箱提取出来 / 手机号
# 手机号特征： 1[3|5|8|9]\d{9}    ->  正则表达式规则
```

```python
import re

re_str = "1[3|5|8|9]\d{9}"


text = """正则表达式，又称规则表达式，（Regular Expression，在代码中常简写为regex、regexp或RE），是一种文本模式，
包括普通字符（例如，a到z之间的字母）和特殊字符（称为“元字符”），是计算机科学的一个概念。正则表达式是对字符串（包括普
通字符和特殊字符）操作的一种逻辑公式，就是用事先定义好的一些特定字符以及这些特定字符的组合，组成一个“规则字符串”，这
个“规则字符串”用来表达对字符串的一种过滤逻辑。正则表达式用来检索、替换那些符合某个模式（规则）的文本，通常被用来检索、
替换那些符合某个模式（规则）的文本。正则表达式可以从一个基础字符串中根据一定的匹配模式替换文本中的字符串、验证表单、提
取字符串等等，许多程序设计语言都支持利用正则表达式进行字符串操作。楼主:瑾瑜，电话 18866666666，邮箱: 12345679@163.com。
求点赞求转发，求一键三连！！！"""

phone_number = re.findall(re_str, text)

print(phone_number)  # 18866666666
```

提取邮箱

```python
\w+@\w+.\w+
```

##### 1.2.2.1 字符相关

- 固定文本
    ```
    import re
    
    text = "你好巴拉巴拉 biubiubiu computer science good morning longArc架构 计算机科学与技术 华为牛逼 打倒美帝国主义纸老虎 日本鬼子不得好死"
    
    data_list = re.findall("computer", text)  # ['computer']
    ```

- 匹配字符
    ```
    import re
    
    text = "你好巴拉巴拉 biubiubiu computer science good morning longArc架构 计算机科学与技术 华为牛逼 打倒美帝国主义纸老虎 日本鬼子不得好死 祝没有真心反对日本核污水拍害的日本人全都收到核辐射而死 hahaha 耶"
    
    data_list = re.findall("[abc]", text)  # 找 a b c 从前向后找
    # ['b', 'b', 'b', 'c', 'c', 'c', 'c', 'a', 'a', 'a']
    ```

    ```python
    import re
    
    text = "你好巴拉巴拉 biubiubiu computer science good morning longArc架构 计算机科学与技术 华为牛逼 打倒美帝国主义纸老虎 日本鬼子不得好死 祝没有真心反对日本核污水拍害的日本人全都收到核辐射而死 hahaha 耶"
    
    data_list = re.findall("h[abc]", text)  # 找 ha hb hc 从前向后找
    # ['ha', 'ha', 'ha']
    ```

- 字符范围 a-z 0-9
    ```python
    import re
    
    text = """你好巴拉巴拉 biubiubiu computer science good morning longArc架构 计算机科学与技术 华为牛逼 
    打倒美帝国主义纸老虎 日本鬼子不得好死 祝没有真心反对日本核污水拍害的日本人全都收到核辐射而死 hahaha 耶 2024年3月10日"""
    
    data_list = re.findall("[a-z]", text)  # 按照范围找
    """['b', 'i', 'u', 'b', 'i', 'u', 'b', 'i', 'u', 'c', 'o', 'm', 'p', 'u', 't', 'e', 'r', 's', 'c', 'i', 'e', 'n', 'c', 'e', 'g', 'o', 'o', 'd', 'm', 'o', 'r', 'n', 'i', 'n', 'g', 'l', 'o', 'n', 'g', 'r', 'c', 'h', 'a', 'h', 'a', 'h', 'a']"""
    ```

- `\d` -- 代表一个数字

    ```python
    import re
    
    text = """root-ad13main-c4ompu423416ter science-aad234main"""
    
    data_list = re.findall(r"\d", text)  # \d代表数字
    print(data_list)  # ['1', '3', '4', '4', '2', '3', '4', '1', '6', '2', '3', '4']
    ```

    ```python
    import re
    
    text = """root-ad13main-c4ompu423416ter science-aad234main"""
    
    data_list = re.findall(r"\d+", text)  # + 代表1个或者n个
    print(data_list)
    ```

    ```python
    import re
    
    text = """root-ad13main-c4ompu423416ter science-aad234main"""
    
    data_list = re.findall(r"\d*", text)  # * 代表0个或者n个
    print(data_list)
    ```

    ```python
    import re
    
    text = """root-ad13main-c4ompu423416ter science-aad234main"""
    
    data_list = re.findall(r"\d?", text)  # ? 代表0个或者1个  意思是只拿0个或1个(不管后面本来有多少个)
    ```

    ```python
    import re
    
    text = """root-ad13main-c4ompu423416ter science-aad234main"""
    
    data_list = re.findall(r"\d{2}", text)  # {n} 固定n个
    ```

    ```python
    import re
    
    text = """root-ad13main-c4ompu423416ter science-aad234main"""
    
    data_list = re.findall(r"\d{2,}", text)  # {n,} 固定n个,或者比n个更多
    ```

    ```python
    import re
    
    text = """root-ad13main-c4ompu423416ter science-aad234main"""
    
    data_list = re.findall(r"\d{2, 4}", text)  # {n, m} 固定n个到m个之间   :  n个 <= 个数 <= m个
    ```

- `\w` -- 字母 数字 下划线 (汉字)

    ```python
    import re
    
    text = """你好巴拉巴拉 biubiubiu computer science good morning longArc架构 计算机科学与技术 华为牛逼 
    打倒美帝国主义纸老虎 日本鬼子不得好死 祝没有真心反对日本核污水拍害的日本人全都收到核辐射而死 hahaha 耶 2024年3月10日"""
    
    data_list = re.findall("计算机\w+技术", text)  # 尽可能多的去匹配  -- 贪婪匹配 默认是贪婪的
    print(data_list)  # ['计算机科学与技术']
    ```

    

# 2 面向对象

## 1
