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

## 小结

- 学习的标签
    ```html
    <h1></h1>
    <div></div>
    <span></span>
    <a></a>
    <img />
    ```

- 划分

    - 块级标签
        - `h`系列
        - `div`
    - 行内标签
        - `span`
        - `a`
        - `img`

- 嵌套

    ```html
    <div>
        <span>xxx</span>
        <img />
        <a></a>
    </div>
    ```

    ```html
    <h1>商品列表</h1>
        <a href="https://www.baidu.com" target="_blank"><img src="/static/a1.jpg" alt=""/></a>
        <a href="https://www.baidu.com" target="_blank"><img src="/static/a2.jpg" alt=""/></a>
        <a href="https://www.baidu.com"><img src="/static/a3.jpg" alt=""/></a>
        <a href="https://www.baidu.com"><img src="/static/a4.png" alt=""/></a>
    
    其中a标签中的target="_blank"，如果有这个属性，那么点击这个图片以后会新打开一个页面，在新打开的页面中显示链接的内容，原来的页面保持不变。
    ```

## 2.7 列表

无序列表

```html
<ul>
    <li>a</li>
    <li>b</li>
    <li>c</li>
</ul>
```

![Clip_2024-05-20_21-16-56](./assets/Clip_2024-05-20_21-16-56.png)

有序列表

```html
<ol>
    <li>a</li>
    <li>b</li>
    <li>c</li>
</ol>
```

![Clip_2024-05-20_21-16-48](./assets/Clip_2024-05-20_21-16-48.png)

## 2.8 表格

```html
<table border="1">  <!-- border属性设置边框 -->
    <thead>
    	<tr> <th>ID</th> <th>Name</th> <th>Age</th></tr>
    </thead>
    
    <tbody>
    	<tr> <td>10</td> <td>计算机</td> <td>18</td></tr>
        <tr> <td>10</td> <td>科学</td> <td>18</td></tr>
        <tr> <td>10</td> <td>技术</td> <td>18</td></tr>
        <tr> <td>10</td> <td>电脑</td> <td>18</td></tr>
        <tr> <td>10</td> <td>问题</td> <td>18</td></tr>
    </tbody>
</table>
```

未加边框:

![Clip_2024-05-20_21-21-53](./assets/Clip_2024-05-20_21-21-53.png)

加上边框:

![Clip_2024-05-20_21-24-37](./assets/Clip_2024-05-20_21-24-37.png)

## 案例

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>user list</title>
</head>
<body>
<table border="1">
    <thead>
    <tr>
        <th>ID</th>
        <th>Name</th>
        <th>Photo</th>
        <th>Email</th>
        <th>Operator</th>
    </tr>
    </thead>

    <tbody>
    <tr>
        <td>0</td>
        <td>computer</td>
        <td><img src="/static/a1.jpg" alt="" style="height: 50px"/></td>
        <td>123@163.com</td>
        <td>
            <a href="https://www.baidu.com">编辑</a>
            <a href="https://www.baidu.com">删除</a>
        </td>
    </tr>
    <tr>
        <td>1</td>
        <td>computer</td>
        <td><img src="/static/a1.jpg" alt="" style="height: 50px"/></td>
        <td>123@163.com</td>
        <td>
            <a href="https://www.baidu.com">编辑</a>
            <a href="https://www.baidu.com">删除</a>
        </td>
    </tr>
    <tr>
        <td>2</td>
        <td>computer</td>
        <td><img src="/static/a1.jpg" alt="" style="height: 50px"/></td>
        <td>123@163.com</td>
        <td>
            <a href="https://www.baidu.com">编辑</a>
            <a href="https://www.baidu.com">删除</a>
        </td>
    </tr>
    <tr>
        <td>3</td>
        <td>computer</td>
        <td><img src="/static/a1.jpg" alt="" style="height: 50px"/></td>
        <td>123@163.com</td>
        <td>
            <a href="https://www.baidu.com">编辑</a>
            <a href="https://www.baidu.com">删除</a>
        </td>
    </tr>
    <tr>
        <td>4</td>
        <td>computer</td>
        <td><img src="/static/a1.jpg" alt="" style="height: 50px"/></td>
        <td>123@163.com</td>
        <td>
            <a href="https://www.baidu.com">编辑</a>
            <a href="https://www.baidu.com">删除</a>
        </td>
    </tr>
    </tbody>
    
</table>
</body>
</html>
```



![Clip_2024-05-20_21-44-46](./assets/Clip_2024-05-20_21-44-46.png)

## 2.9 `input`系列 -- 行内标签

```html
<input type="text"/>
<input type="password"/>
<input type="file"/>

<!-- 两者的name属性相同->就是两者只能选一个 -->
<input type="radio" name="n1"/>男
<input type="radio" name="n1"/>女

<input type="checkbox"/>唱
<input type="checkbox"/>跳
<input type="checkbox"/>rap
<input type="checkbox"/>篮球
<input type="checkbox"/>dance
<input type="checkbox"/>sing
```

![Clip_2024-05-20_21-53-38](./assets/Clip_2024-05-20_21-53-38.png)

```html
<input type="button" value="这是Button里面显示的东西"/> <!-- 普通的按钮 -->
```

![Clip_2024-05-20_21-55-27](./assets/Clip_2024-05-20_21-55-27.png)

```html
<input type="submit" value="这是submit里面显示的东西"/> <!-- 提交表单 -->
```

![Clip_2024-05-20_21-57-14](./assets/Clip_2024-05-20_21-57-14.png)

## 2.10 下拉框 -- 行内标签

```html
<!-- 只能选一个 -->
<select>
    <option>北京</option>
    <option>上海</option>
    <option>广州</option>
</select>
```

![Clip_2024-05-20_21-59-18](./assets/Clip_2024-05-20_21-59-18.png)

```html
<!-- 能选择多个 选中其中一个 按住shift键，点击其他的就行 -->
<select multiple>
    <option>北京</option>
    <option>上海</option>
    <option>广州</option>
</select>
```

![Clip_2024-05-20_22-01-57](./assets/Clip_2024-05-20_22-01-57.png)

## 2.11 多行文本

```html
<textarea></textarea>
```

![Clip_2024-05-20_22-03-19](./assets/Clip_2024-05-20_22-03-19.png)

```html
<!-- 初始的大小为3行 可以理解为默认高度-->
<textarea rows="3"></textarea>
```

## 案例：用户注册

```python
@app.route("/user/register/")
def register():
    return render_template("register.html", name="JinYu")
```

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
</head>
<body>
<h1>用户注册</h1>
<div>
    用户名 : <input type="text"/>
</div>

<div>
    密 码 : <input type="password"/>
</div>

<div>
    性别 : <input type="radio" name="sex"> 男 <input type="radio" name="sex"> 女
</div>

<div>
    爱好:
    <input type="checkbox">篮球
    <input type="checkbox">足球
    <input type="checkbox">乒乓球
    <input type="checkbox">排球
</div>


<div>
    城市:
    <select name="city" id="city">
        <option>天水</option>
        <option>兰州</option>
        <option>西安</option>
        <option>北京</option>
        <option>天津</option>
    </select>
</div>

<div>
    熟悉的编程语言:
    <select name="language" id="language" multiple>
        <option>Python</option>
        <option>C</option>
        <option>C++</option>
        <option>Go</option>
        <option>java</option>
    </select>
</div>

<div>
    备注 : <textarea>...</textarea>
</div>

<div>
    <input type="button" value="提交">
    <input type="submit" value="submit">
</div>
</body>
</html>
```

![Clip_2024-05-22_21-19-12](./assets/Clip_2024-05-22_21-19-12.png)

## 总结

1. `flask`的工作流程：

![Clip_2024-05-22_21-22-17](./assets/Clip_2024-05-22_21-22-17.png)

2. 网络请求
    - 在浏览器的`URL`中写入一个地址并访问
        ```python
        浏览器会发送数据过去，本质上发送的是字符串
        "GET /explore http1.1\r\nhost: ...\r\n...\r\n\r\n"
        "POST /explore http1.1\r\nhost: ...\r\n...\r\n\r\n数据"
        ```

    - 浏览器向后端发送请求时

        - `get`请求【URL访问、表单提交】
            - 点击链接
            - 关键字搜索
            - `url`搜索
            - 向后台传入数据时，数据会拼接在`url`上
        - `post`请求【只能表单提交】
            - 提交数据 -- 表单
            - 数据不在`url`中体现，而是在请求体中。

## 案例：用户注册

新创建一个项目

新创建一个`flask`程序文件。 -- `get`请求

如果要将数据提交给后台 -- 就需要一个`form`标签将一些输入的数据包裹在里面。

`button`只是一个普通的按钮,而`submit`是专门和表单配合的.

```html
<h1>用户注册</h1>
<div>
    <form method="方法" action="提交的地址">
        用户名 : <input type="text"/>
        密 码 : <input type="password"/>
        <div>
            <input type="submit" value="submit">
        </div>
    </form>
</div>
```

```html
注意:如果要用get方法传递值到后端,那么需要首先用form将需要传递的标签全都包裹起来
并且form标签里面需要定义提交地址action和method方法,并且form标签里面唏嘘要有submit
另外,如果需要将传递的信息在url里面体现,那么需要在input标签里面加上name值
<h1>用户注册</h1>
<form method="get" action="/wephiles/index">
    <div>
        用户名 : <input type="text" name="name"/>
        密 码 : <input type="password" name="password"/>
    </div>
    <div>
        <input type="button" value="提交">
        <input type="submit" value="submit">
    </div>
</form>
```

```python
from flask import Flask, render_template

app = Flask(__name__)


@app.route("/register", methods=["GET"])
def register():
    return render_template("register.html")


if __name__ == '__main__':
    app.run()
```

浏览器显示效果:注意看`url`

![Clip_2024-05-22_21-52-52](./assets/Clip_2024-05-22_21-52-52.png)

注意:在form里面的标签有:input系列/textarea/select

**一定注意:必须要写name属性**

![Clip_2024-05-22_22-08-37](./assets/Clip_2024-05-22_22-08-37.png)

```python
from flask import Flask, render_template, request

app = Flask(__name__)


@app.route("/register", methods=["GET"])
def register():
    return render_template("register.html")


@app.route("/do/reg", methods=["GET"])
def do_register():
    # request接受通过get形式发送过来的数据
    print(request.args)

    return str(request.args)


@app.route("/post/reg", methods=["POST"])
def post_register():
    # request接受通过post形式发送过来的数据
    print(request.form)
    return str(request.form)


if __name__ == '__main__':
    app.run()
```

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
</head>
<body>
<h1>用户注册</h1>

<!--<form method="get" action="/do/reg">-->
<!--    <div>-->
<!--        用户名 : <input type="text" name="name"/>-->
<!--        密 码 : <input type="password" name="password"/>-->
<!--    </div>-->
<!--    <div>-->
<!--        <input type="button" value="提交">-->
<!--        <input type="submit" value="submit">-->
<!--    </div>-->
<!--</form>-->

<form method="post" action="/post/reg">
    <div>
        用户名 : <input type="text" name="name"/>
        密 码 : <input type="password" name="password"/>
    </div>
    <div>
        <input type="button" value="提交">
        <input type="submit" value="submit">
    </div>
</form>
<!--<div>-->
<!--    性别 : <input type="radio" name="sex"> 男 <input type="radio" name="sex"> 女-->
<!--</div>-->

<!--<div>-->
<!--    爱好:-->
<!--    <input type="checkbox">篮球-->
<!--    <input type="checkbox">足球-->
<!--    <input type="checkbox">乒乓球-->
<!--    <input type="checkbox">排球-->
<!--</div>-->


<!--<div>-->
<!--    城市:-->
<!--    <select name="city" id="city">-->
<!--        <option>天水</option>-->
<!--        <option>兰州</option>-->
<!--        <option>西安</option>-->
<!--        <option>北京</option>-->
<!--        <option>天津</option>-->
<!--    </select>-->
<!--</div>-->

<!--<div>-->
<!--    熟悉的编程语言:-->
<!--    <select name="language" id="language" multiple>-->
<!--        <option>Python</option>-->
<!--        <option>C</option>-->
<!--        <option>C++</option>-->
<!--        <option>Go</option>-->
<!--        <option>java</option>-->
<!--    </select>-->
<!--</div>-->

<!--<div>-->
<!--    备注 : <textarea>...</textarea>-->
<!--</div>-->

<!--<div>-->
<!--    <input type="button" value="提交">-->
<!--    <input type="submit" value="submit">-->
<!--</div>-->
</body>
</html>

```

完整版:

```python
from flask import Flask, render_template, request

app = Flask(__name__)


@app.route("/register", methods=["GET"])
def register():
    return render_template("register.html")


@app.route("/do/reg", methods=["GET"])
def do_register():
    # request接受通过get形式发送过来的数据
    print(request.args)

    return str(request.args)


@app.route("/post/reg", methods=["POST"])
def post_register():
    # request接受通过post形式发送过来的数据
    print(request.form.get("user"))
    print(request.form.get("password"))
    print(request.form.get("sex"))
    print(request.form.getlist("hobby"))
    print(request.form.get("city"))
    print(request.form.getlist("language"))
    print(request.form.get("more"))
    return str(request.form)


if __name__ == '__main__':
    app.run()
```

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
</head>
<body>
<h1>用户注册</h1>

<form method="post" action="/post/reg">
    <div>
        用户名 : <input type="text" name="name"/>
    </div>

    <div>
        密 码 : <input type="password" name="password"/>
    </div>

    <div>
        性别 : <input type="radio" name="sex" value="1"> 男 <input type="radio" name="sex" value="2"> 女
    </div>

    <div>
        爱好:
        <input type="checkbox" name="hobby" value="10">篮球
        <input type="checkbox" name="hobby" value="11">足球
        <input type="checkbox" name="hobby" value="12">乒乓球
        <input type="checkbox" name="hobby" value="13">排球
    </div>

    <div>
        城市:
        <select name="city">
            <option value="ts">天水</option>
            <option value="lz">兰州</option>
            <option value="xa">西安</option>
            <option value="bj">北京</option>
            <option value="tj">天津</option>
        </select>
    </div>

    <div>
        熟悉的编程语言:
        <select name="language" id="language" multiple>
            <option value="python">Python</option>
            <option value="c">C</option>
            <option value="cpp">C++</option>
            <option value="go">Go</option>
            <option value="java">java</option>
        </select>
    </div>

    <div>
        备注 :
        <textarea name="more">

    </textarea>
    </div>

    <div>
        <input type="submit" value="submit">
    </div>
</form>
</body>
</html>

```

改进`flask`后端文件和`html`文件:将两个分别处理的函数综合到一起,这样就可以根据请求方法的不同来进行不同的操作逻辑.

```python
from flask import Flask, render_template, request

app = Flask(__name__)


@app.route("/register", methods=["GET", "POST"])
def register():
    if request.method == 'GET':
        return render_template("register.html")
    else:
        # request接受通过post形式发送过来的数据
        print(request.form.get("user"))
        print(request.form.get("password"))
        print(request.form.get("sex"))
        print(request.form.getlist("hobby"))
        print(request.form.get("city"))
        print(request.form.getlist("language"))
        print(request.form.get("more"))
        return "<h1> 恭喜你,注册成功! </h1>"


@app.route("/do/reg", methods=["GET"])
def do_register():
    # request接受通过get形式发送过来的数据
    print(request.args)

    return str(request.args)


@app.route("/post/reg", methods=["POST"])
def post_register():
    # request接受通过post形式发送过来的数据
    print(request.form.get("user"))
    print(request.form.get("password"))
    print(request.form.get("sex"))
    print(request.form.getlist("hobby"))
    print(request.form.get("city"))
    print(request.form.getlist("language"))
    print(request.form.get("more"))
    return str(request.form)


if __name__ == '__main__':
    app.run()
```

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
</head>
<body>
<h1>用户注册</h1>

<form method="post" action="/register">
    <div>
        用户名 : <input type="text" name="user"/>
    </div>

    <div>
        密 码 : <input type="password" name="password"/>
    </div>

    <div>
        性别 : <input type="radio" name="sex" value="1"> 男 <input type="radio" name="sex" value="2"> 女
    </div>

    <div>
        爱好:
        <input type="checkbox" name="hobby" value="10">篮球
        <input type="checkbox" name="hobby" value="11">足球
        <input type="checkbox" name="hobby" value="12">乒乓球
        <input type="checkbox" name="hobby" value="13">排球
    </div>

    <div>
        城市:
        <select name="city">
            <option value="ts">天水</option>
            <option value="lz">兰州</option>
            <option value="xa">西安</option>
            <option value="bj">北京</option>
            <option value="tj">天津</option>
        </select>
    </div>

    <div>
        熟悉的编程语言:
        <select name="language" id="language" multiple>
            <option value="python">Python</option>
            <option value="c">C</option>
            <option value="cpp">C++</option>
            <option value="go">Go</option>
            <option value="java">java</option>
        </select>
    </div>

    <div>
        备注 :
        <textarea name="more">

    </textarea>
    </div>

    <div>
        <input type="submit" value="submit">
    </div>
</form>
</body>
</html>

```

## 案例:用户登录







