<h1 style="text-align: center;font-size: 40px; font-family: '楷体';">Django - day16</h1>

[TOC]

主题：员工管理系统

# 1 新建一个`Django`项目

# 2 创建`app`

# 3 设计表结构

```python
from django.db import models


# Create your models here.

class Department(models.Model):
    """部门表"""
    # id = models.BigAutoField(verbose_name='ID', primary_key=True, )
    title = models.CharField(verbose_name="部门标题--verbose_name参数表示备注信息", max_length=20)


class UserInfo(models.Model):
    """员工表"""
    name = models.CharField(verbose_name="员工姓名", max_length=10)
    password = models.CharField(verbose_name="密码", max_length=64)
    age = models.IntegerField(verbose_name="年龄")

    # decimal_places=2小数点位数 max_digits=10最大长度
    salary = models.DecimalField(verbose_name="账户余额", decimal_places=2, max_digits=10, default=0)
    time = models.DateTimeField(verbose_name="入职时间")

    # 这个是django里面做的约束 和数据库无关 写性别的时候只能写1/2,1代表男 2代表女
    gender_choices = (
        (1, '男'),
        (2, '女'),
    )
    gender = models.SmallIntegerField(verbose_name="性别", choices=gender_choices)

    # 外键 所属部门 部门名称/部门ID？ -- 两者都有存
    # 根据范式，存ID（节省内存开销）
    # 但是特大企业根据企业要求，存名称，查询次数会很多 会去连表（连表操作会比较耗时），允许数据冗余
    # 对部门ID，要约束吗？ -- 需要约束(不能乱写)--只能是部门表中已经存在的ID

    # # 这样写没约束：
    # department_id = models.CharField(verbose_name='这是备注', max_length=20)

    # 你得这样写 to是与哪张表关联 to_field是与哪一列做关联
    # django自动 -写的是department，但是生成数据的时候 叫department_id

    # # 部门被删除了 -- 直接删除用户（级联删除）
    # department = models.ForeignKey(to=Department, to_field='id', on_delete=models.CASCADE)

    # 部门被删除了 -- 不删除用户但是置空
    department = models.ForeignKey(to=Department, to_field='id', on_delete=models.SET_NULL, null=True, blank=True)

```

# 4 在`MySQL`中生成表

```python
python manage.py makemigrations
python manage.py migrate
```

# 5 静态文件管理

# 6 部门管理

注意，后续有更优解，但是先体验一下原始的方式做。

## 6.1 部门列表、添加部门

```python
# views.py

from django.shortcuts import render, HttpResponse, redirect
from mysite import models as my_md


# Create your views here.


def user_list(request):
    return render(request, "user_list.html")


def create_department(request):
    if request.method == 'GET':
        return render(request, "create_department.html")
    title = request.POST.get('title')
    my_md.Department.objects.create(title=title)
    return redirect("/department/list/")


def depart_list(request):
    data_list = my_md.Department.objects.all()

    return render(request,
                  "depart_list.html",
                  {'data_list_obj': data_list})

```

```python
# urls.py

from django.contrib import admin
from django.urls import path
from mysite import views

urlpatterns = [
    # path("admin/", admin.site.urls),
    path("user/list/", views.user_list),
    path("department/list/", views.depart_list),
    path("create/department/", views.create_department),
]

```

```html
<!-- create_department.html -->
{% load static %}
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Create Department</title>
    <link rel="stylesheet" href="{% static '/plugins/bootstrap-3.4.1/css/bootstrap.min.css' %}"/>
    <link rel="stylesheet" href="{% static '/plugins/font-awesome-4.7.0/font-awesome-4.7.0/css/font-awesome.min.css' %}"/>
</head>
<body>
<div class="container">
    <div class="panel panel-default">
        <div class="panel-heading">
            <h3 class="panel-title">新建部门</h3>
        </div>
        <div class="panel-body">
            <form class="form-inline" method="post" action="#" style="margin-top: 10px;">
                <div class="form-group">
                    <label for="exampleInputName2">部门名称</label>
                    <input type="text" name="title" class="form-control" id="exampleInputName2" placeholder="input department title">
                </div>
                <button type="submit" class="btn btn-primary">确 定</button>
                {% csrf_token %}
            </form>
        </div>
    </div>
</div>

<script src="{% static '/js/jquery37/jquery-3.7.1.min.js' %}"></script>
<script src="{% static '/plugins/bootstrap-3.4.1/js/bootstrap.min.js' %}"></script>
</body>
</html>
```

```html
<!-- depart_list.html -->

{% load static %}
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Depart List</title>
    <link rel="stylesheet" href="{% static '/plugins/bootstrap-3.4.1/css/bootstrap.min.css' %}"/>
    <link rel="stylesheet" href="{% static '/plugins/font-awesome-4.7.0/font-awesome-4.7.0/css/font-awesome.min.css' %}"/>
    <style>
        .navbar {
            border-radius: 0;
        }
    </style>
</head>
<body>

<div class="navbar navbar-default">
    <div class="container">
        <!-- Brand and toggle get grouped for better mobile display -->
        <div class="navbar-header">
            <button type="button" class="navbar-toggle collapsed" data-toggle="collapse" data-target="#bs-example-navbar-collapse-1" aria-expanded="false">
                <span class="sr-only">Toggle navigation</span>
                <span class="icon-bar"></span>
                <span class="icon-bar"></span>
                <span class="icon-bar"></span>
            </button>
            <a class="navbar-brand" href="#">企业管理系统</a>
        </div>

        <!-- Collect the nav links, forms, and other content for toggling -->
        <div class="collapse navbar-collapse" id="bs-example-navbar-collapse-1">
            <ul class="nav navbar-nav">
                <li class="active"><a href="/department/list/">
                    部门管理
                    <span class="sr-only">(current)</span>
                </a>
                </li>
                <li><a href="/user/list/">人员管理</a></li>
                <li><a href="#">产品管理</a></li>
                <li><a href="#">订单管理</a></li>
                <li><a href="#">物流管理</a></li>
            </ul>

            <ul class="nav navbar-nav navbar-right">
                <li><a href="#">登录</a></li>
                <li class="dropdown">
                    <a href="#" class="dropdown-toggle" data-toggle="dropdown" role="button" aria-haspopup="true" aria-expanded="false">
                        瑾瑜 <span class="caret"></span></a>
                    <ul class="dropdown-menu">
                        <li><a href="#">个人资料</a></li>
                        <li><a href="#">我的信息</a></li>
                        <li><a href="#">系统设置</a></li>
                        <li role="separator" class="divider"></li>
                        <li><a href="#">注销登录</a></li>
                    </ul>
                </li>
            </ul>
        </div>
    </div>
</div>

<div class="container">
    <div>
        <div class="panel panel-default">
            <div class="panel-heading">
                <a class="btn btn-primary" href="/create/department/" target="_blank">新建部门</a>
            </div>
            <div class="panel-body">
                <table class="table table-hover table-bordered table-striped">
                    <thead>
                    <tr>
                        <th>ID</th>
                        <th>Title</th>
                        <th>Operate</th>
                    </tr>
                    </thead>

                    <tbody>
                    {% for item in data_list_obj %}
                        <tr>
                            <td>{{ item.id }}</td>
                            <td>{{ item.title }}</td>
                            <td>
                                <a>
                                    <button type="button" class="btn btn-primary btn-xs">编辑</button>
                                </a>
                                <a>
                                    <button type="button" class="btn btn-danger btn-xs">删除</button>
                                </a>
                            </td>
                        </tr>
                    {% endfor %}
                    </tbody>
                </table>
            </div>
        </div>
    </div>
</div>
<script src="{% static '/js/jquery37/jquery-3.7.1.min.js' %}"></script>
<script src="{% static '/plugins/bootstrap-3.4.1/js/bootstrap.min.js' %}"></script>
</body>
</html>

```

```html
<!-- user_list.html -->
{% load static %}
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Depart List</title>
    <link rel="stylesheet" href="{% static '/plugins/bootstrap-3.4.1/css/bootstrap.min.css' %}"/>
    <link rel="stylesheet" href="{% static '/plugins/font-awesome-4.7.0/font-awesome-4.7.0/css/font-awesome.min.css' %}"/>
    <style>
        .navbar {
            border-radius: 0;
        }
    </style>
</head>
<body>

<div class="navbar navbar-default">
    <div class="container">
        <!-- Brand and toggle get grouped for better mobile display -->
        <div class="navbar-header">
            <button type="button" class="navbar-toggle collapsed" data-toggle="collapse" data-target="#bs-example-navbar-collapse-1" aria-expanded="false">
                <span class="sr-only">Toggle navigation</span>
                <span class="icon-bar"></span>
                <span class="icon-bar"></span>
                <span class="icon-bar"></span>
            </button>
            <a class="navbar-brand" href="#">企业管理系统</a>
        </div>

        <!-- Collect the nav links, forms, and other content for toggling -->
        <div class="collapse navbar-collapse" id="bs-example-navbar-collapse-1">
            <ul class="nav navbar-nav">
                <li><a href="/department/list/">部门管理</a></li>
                <li class="active"><a href="/department/list/">
                    人员管理
                    <span class="sr-only">(current)</span>
                </a>
                </li>
                <li><a href="#">产品管理</a></li>
                <li><a href="#">订单管理</a></li>
                <li><a href="#">物流管理</a></li>
            </ul>

            <ul class="nav navbar-nav navbar-right">
                <li><a href="#">登录</a></li>
                <li class="dropdown">
                    <a href="#" class="dropdown-toggle" data-toggle="dropdown" role="button" aria-haspopup="true" aria-expanded="false">
                        瑾瑜 <span class="caret"></span></a>
                    <ul class="dropdown-menu">
                        <li><a href="#">个人资料</a></li>
                        <li><a href="#">我的信息</a></li>
                        <li><a href="#">系统设置</a></li>
                        <li role="separator" class="divider"></li>
                        <li><a href="#">注销登录</a></li>
                    </ul>
                </li>
            </ul>
        </div>
    </div>
</div>

<div class="container">
    <div>
        <div class="panel panel-default">
            <div class="panel-heading">
                <a class="btn btn-primary" href="#" target="_blank">新建用户</a>
            </div>
            <div class="panel-body">
                <table class="table table-hover table-bordered table-striped">
                    <thead>
                    <tr>
                        <th>ID</th>
                        <th>Title</th>
                        <th>Operate</th>
                        <th>Operate</th>
                        <th>Operate</th>
                        <th>Operate</th>
                        <th>Operate</th>
                        <th>Operate</th>
                    </tr>
                    </thead>

                    <tbody>
                    {% for item in data_list_obj %}
                        <tr>
                            <td>{{ item.id }}</td>
                            <td>{{ item.title }}</td>
                            <td>{{ item.title }}</td>
                            <td>{{ item.title }}</td>
                            <td>{{ item.title }}</td>
                            <td>{{ item.title }}</td>
                            <td>{{ item.title }}</td>
                            <td>{{ item.title }}</td>
                            <td>
                                <a>
                                    <button type="button" class="btn btn-primary btn-xs">编辑</button>
                                </a>
                                <a>
                                    <button type="button" class="btn btn-danger btn-xs">删除</button>
                                </a>
                            </td>
                        </tr>
                    {% endfor %}
                    </tbody>
                </table>
            </div>
        </div>
    </div>
</div>


<script src="{% static '/js/jquery37/jquery-3.7.1.min.js' %}"></script>
<script src="{% static '/plugins/bootstrap-3.4.1/js/bootstrap.min.js' %}"></script>
</body>
</html>
```

## 6.2 删除部门

```python
def delete_department(request):
    del_id = request.GET.get('nid')
    my_md.Department.objects.filter(id=del_id).delete()
    # return render(request, )
    return redirect('/department/list/')
```

```html
<a href="http://127.0.0.1:8000/delete/department/?nid={{ item.id }}">
    <button type="button" class="btn btn-danger btn-xs">删除</button>
</a>
```

## 6.3 编辑部门

```python
# views.py
def edit_department(request, nid):
    row_obj = my_md.Department.objects.filter(id=nid).first()
    title_department = row_obj.title

    return render(request, "edit_department.html", {"title": title_department})

# urls.py
from django.contrib import admin
from django.urls import path
from mysite import views

urlpatterns = [
    # path("admin/", admin.site.urls),
    path("user/list/", views.user_list),
    path("department/list/", views.depart_list),
    path("create/department/", views.create_department),
    path("delete/department/", views.delete_department),

    # 如果按照下面这样写 你在发送请求到这个地址的时候 必须传递这样的url:http://127.0.0.1:8000/edit/1/department/
    path("edit/<int:nid>/department/", views.edit_department),
]
```

```html
<!-- edit_department.html -->
{% load static %}
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Edit Department</title>
    <link rel="stylesheet" href="{% static '/plugins/bootstrap-3.4.1/css/bootstrap.min.css' %}"/>
    <link rel="stylesheet" href="{% static '/plugins/font-awesome-4.7.0/font-awesome-4.7.0/css/font-awesome.min.css' %}"/>
</head>
<body>
<div class="container">
    <div class="panel panel-default">
        <div class="panel-heading">
            <h3 class="panel-title">修改部门信息</h3>
        </div>
        <div class="panel-body">
            <form class="form-inline" method="post" action="#" style="margin-top: 10px;">
                <div class="form-group">
                    <label for="exampleInputName2">部门名称</label>
                    <input type="text" name="title" class="form-control" value="{{ title }}" id="exampleInputName2" placeholder="input department title">
                </div>
                <button type="submit" class="btn btn-primary">确 定</button>
                {% csrf_token %}
            </form>
        </div>
    </div>
</div>

<script src="{% static '/js/jquery37/jquery-3.7.1.min.js' %}"></script>
<script src="{% static '/plugins/bootstrap-3.4.1/js/bootstrap.min.js' %}"></script>
</body>
</html>
```

![Clip_2024-06-15_17-32-36](./assets/Clip_2024-06-15_17-32-36.png)

![Clip_2024-06-15_17-33-26](./assets/Clip_2024-06-15_17-33-26.png)

再完整一下：

```python
# views.py

def edit_department(request, nid):
    if request.method == 'GET':
        # 获取的是queryset对象列表 即使只有一个对象 也会返回列表
        row_obj = my_md.Department.objects.filter(id=nid).first()
        title_department = row_obj.title

        return render(request, "edit_department.html", {"title": title_department})
    title = request.POST.get('title')
    my_md.Department.objects.filter(id=nid).update(title=title)
    return redirect('/department/list/')
```

# 7 模板的继承

- 部门列表
- 添加部门
- 编辑部门

我们发现我们的每个页面都有一个一样的导航条 -- 重复的操作 -- 模板的继承 -- 重复的东西写到模板里面即可

在`templates`目录里面创建一个名为`layout`的模板`html`文件：

```html
{% load static %}
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
    <link rel="stylesheet" href="{% static '/plugins/bootstrap-3.4.1/css/bootstrap.min.css' %}"/>
    <link rel="stylesheet" href="{% static '/plugins/font-awesome-4.7.0/font-awesome-4.7.0/css/font-awesome.min.css' %}"/>
    <style>
        .navbar {
            border-radius: 0;
        }
    </style>
</head>
<body>

<div class="navbar navbar-default">
	...这里为了能够看清楚，把导航栏的细节全删了。  
</div>

<div class="container">
    注意看下面这条语句 把这行语句删了 如果要copy
    {% block content %}{% endblock %}
</div>
<script src="{% static '/js/jquery37/jquery-3.7.1.min.js' %}"></script>
<script src="{% static '/plugins/bootstrap-3.4.1/js/bootstrap.min.js' %}"></script>
</body>
</html>

```

其他`html`想要应用上述模板：

```html
{% extends 'layout.html' %}

{% block content %}
<h1>测试模板</h1>
{% endblock %}

```

![Clip_2024-06-17_21-18-46](./assets/Clip_2024-06-17_21-18-46.png)

## 7.1 定义模板

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
    <link rel="stylesheet" href="{% static '...bootstrap.min.css' %}"/>
    <style>
    	...
    </style>
    {% block css %}{% endblock %}
</head>
<body>
<h1>标题</h1>
    
{% block content %}{% endblock %}

<h1>底部</h1>

{% block js %}{% endblock %}
<script src="{% static '.../jquery-3.7.1.min.js' %}"></script>
    
</body>
</html>
```

## 7.2 继承模板

```html
{% extends '模板名.html' %}

{% block css %}{% endblock %}
<link rel="stylesheet" href="{% static '...css' %}"/>

{% block content %}
这里写你新加的内容
{% endblock %}

{% block js %}{% endblock %}
<script src="{% static '...js' %}"></script>
```

![Clip_2024-06-17_22-02-17](./assets/Clip_2024-06-17_22-02-17.png)

![Clip_2024-06-17_22-02-45](./assets/Clip_2024-06-17_22-02-45.png)

```python
def user_list(request):
    query_set = my_md.UserInfo.objects.all()
    print(query_set[0].id)  # 1
    print(query_set[0].get_gender_display())  # 男
    print(query_set[0].department_id)
    print(query_set[0].department)
    print(query_set[0].department.title)
    return render(request, "user_list.html", {'query_set': query_set})
```

```html
{% for item in query_set %}
    <tr>
        <td>{{ item.id }}</td>
        <td>{{ item.name }}</td>
        <td>{{ item.password }}</td>
        <td>{{ item.age }}</td>
        <td>{{ item.salary }}</td>
        <td>{{ item.time }}</td>
        <td>{{ item.get_gender_display }}</td>
        <td>{{ item.department.title }}</td>
        <td>
            <a>
                <button type="button" class="btn btn-primary btn-xs">编辑</button>
            </a>
            <a>
                <button type="button" class="btn btn-danger btn-xs">删除</button>
            </a>
        </td>
    </tr>
{% endfor %}
```

如果想要将时间改成字符串的形式：按照下面的方式写：

```html
{% for item in query_set %}
    <tr>
        ...
        <td>{{ item.time|date:"Y-m-d" }}</td>
        ...
    </tr>
{% endfor %}
```

![Clip_2024-06-17_22-10-11](./assets/Clip_2024-06-17_22-10-11.png)

# 8 新建用户

- 原始方法理思路：不会采用（本质） 比较麻烦
- `Django`组件
  - `Form`组件
  - `ModelForm`组件（最简便）

`16-2 1:46:23`



















































