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

咱们的网站和别人的网站不一样：

- 我们的难看，别人的好看。浏览器可以识别很多标签和数据。

![Clip_2024-05-01_19-56-10](./assets/Clip_2024-05-01_19-56-10.png)

- `Flask`框架支持：将所有的这些字符串写到一个文件中去

    ```python
    from flask import Flask, render_template
    
    app = Flask(__name__)
    
    
    # 创建了网址 /show/info 和函数 index 的映射关系
    # 以后用户在浏览器访问 http://localhost:5000/show/info 时，会自动执行 index 函数
    @app.route('/show/info')  # 注意最后面不带斜杠
    def index():
        """
    
        Returns:
    
        """
        # 调用 render_template 函数，传入模板文件名和数据字典，Flask自动打开来这个文件 读取内容 返回渲染后的 HTML 代码
        # 这个文件默认回去当前项目目录下的templates文件夹中找
        return render_template('index.html', name='wephiles')
    
    
    if __name__ == '__main__':
        app.run()
        
        # 自定义主机和端口号
        # app.run(host="", port="")
    ```

    ```python
    # index.html
    
    <!DOCTYPE html>
    <html lang="en">
    <head>
        <meta charset="UTF-8">
        <title>xxx</title>
    </head>
    <body>
        <h1>哈哈哈哈</h1>
        <h1>嘻嘻嘻嘻</h1>
    </body>
    </html>
    ```

    运行结果：

    ![Clip_2024-05-01_20-04-27](./assets/Clip_2024-05-01_20-04-27.png)

# 2 标签

## 2.1 编码(`head`标签里边的)

我们给服务器发请求，服务器返回给我们的数据中有个`<meta charset="UTF-8">`，我们的浏览器拿到数据后，就要进行编码

```html
<meta charset="UTF-8">
```

## 2.2 `title` `head`标签里边的

```html
<title>这是title</title>
```

![Clip_2024-05-01_20-15-07](./assets/Clip_2024-05-01_20-15-07.png)

## 2.3 标题 - 块级标签

```html
<h1>一级标题</h1>
<h2>二级标题</h2>
<h3>三级标题</h3>
<h4>四级标题</h4>
<h5>五级标题</h5>
<h6>六级标题</h6>
```

![Clip_2024-05-01_20-18-17](./assets/Clip_2024-05-01_20-18-17.png)

## 2.4 `div` 和 `span`

```html
<div>
    内容
</div>

<span> QWERTY </span>
```

- `div` 一个人占一整行 块级标签

    ```html
    <div>abcd</div>
    <div>efgh</div>
    ```

- `span` 自己有多大就占多大 行内标签(内联标签)

    ```html
    <span>abcd</span>
    <span>efgh</span>
    ```

注意，这两个标签比较素 + `css`样式

## 2.5 超链接 -- 行内标签

```html
跳转到别人的网站
<a href="https://www.baidu.com"> 点击跳转 </a>

# 跳转到自己的网站其他的地址
<a href="/get/news"> 点击跳转 </a>
```

## 2.6 图片 -- 行内标签

```html
<img src="图片地址(本地或者网络上的照片)" />

- 网络上的照片
<img src="https://pic.3gbizhi.com/uploadmark/20220916/35c9f1a1e642ba133b0efc2b58b9ae02.png"/>

- 自己的图片
	- 在项目中新建一个叫static的目录，图片就放在里面
	- 在页面上引入图片的时候：需要在图片名前面加上/static/
<img src="/static/fdeed94fb2284bd4b76c1fb8f097c99c.jpg"/>
```

设置图片宽高：

```html
定义高度，会将图片按比例缩放
<img style="height: 100px" src="/static/fdeed94fb2284bd4b76c1fb8f097c99c.jpg"/>

定义宽度和高度
<img style="height: 100px;width: 100px" src="/static/fdeed94fb2284bd4b76c1fb8f097c99c.jpg"/>

设置比例
<img style="width: 40%" src="/static/fdeed94fb2284bd4b76c1fb8f097c99c.jpg"/>
```

```python
# todo: day11-1 2:00:00
```



2.7 

















