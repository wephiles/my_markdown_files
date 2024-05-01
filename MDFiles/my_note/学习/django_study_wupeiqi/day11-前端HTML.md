<h1 style="text-align: center;font-size: 40px; font-family: '楷体';">前端开发HTML-day11</h1>

概要：

```python
目的：开发一个平台(网站)
	- 前端开发:HTML、CSS、JavaScript
	- web框架: 接收请求并处理
	- MySQL数据库: 存储数据的地方 
    
快速上手
	基于Flask框架快速搭建一个网站
    
深入学习
	基于Django框架(主要)
```

# 1 快速开发网站

需要安装`flask`模块

```python
>>> pip install flask
```

```python
from flask import Flask

app = Flask(__name__)


# 创建了网址 /show/info 和函数 index 的映射关系
# 以后用户在浏览器访问 http://localhost:5000/show/info 时，会自动执行 index 函数
@app.route('/show/info')  # 注意最后面不带斜杠
def index():
    """

    Returns:

    """
    return "<h1>哈哈哈哈</h1>"


if __name__ == '__main__':
    app.run()
```

下面展示了`Flask`后台正在运行

![Clip_2024-05-01_18-08-07](./assets/Clip_2024-05-01_18-08-07.png)

下面展示了浏览器访问的结果：

![Clip_2024-05-01_18-09-26](./assets/Clip_2024-05-01_18-09-26.png)