# Tornado

### HTTP服务器

HTTP协议是建立在TCP协议之上的短连接协议，它利用了TCP协议的可靠性，用来传输超文本

##### 最简单的HTTP Server

```python
#!/usr/bin/env python
import socket
from settings import *

addr = ('127.0.0.1', 9000)
sock = socket.socket(socket.AF_INET, socket.SOCK_STREAM)
sock.setsockopt(socket.SOL_SOCKET, socket.SO_REUSEADDR, 1)  # 打开地址重用选项
sock.bind(addr)
sock.listen(100)


def get_url(request_str):
    first_line = request_str.strip().split("\n")[0]
    url = first_line.split(" ")[1]
    return url


while True:
    cli_sock, cli_addr = sock.accept()
    cli_request = cli_sock.recv(1024).decode('utf8')

    # 获取用户的url
    url = get_url(cli_request)

    if url == '/foo':
        response = html % '爱妃退下'
    elif url == '/bar':
        response = html % '提阿西代码'
    else:
        response = html % 'hello word'

    cli_sock.sendall(response.encode('utf8'))
    cli_sock.close()
```
### web框架概述

web框架就是对上述的最简单的HTTP server进行封装，在添加各种拓展功能

##### web服务器原理

web服务器包括三部分：数据库，后端程序和前端页面，数据库就是进行存取数据，而后端就是把数据库中提取出的数据进行加工提交个前端，最后前端稍加修饰显示在页面中。

##### 常见的web框架

Django：全能型框架，具有很多功能，插件和文档丰富，社区活跃，适合快速开发，但内部耦合比较紧

Flask：微型框架，极其灵活，便于二次开发和扩展，生态环境好，插件也同样丰富

Tornado：异步处理，事件驱动(epoll)，性能优异

### Tornado 入门

```python
import tornado.ioloop
import tornado.web
from settings import *    # 导入网页参数
from tornado.options import parse_command_line, define, options

define("host", default="0.0.0.0", help="主机地址", type=str)
define("port", default=8000, help="主机端口", type=int)


class MainHandler(tornado.web.RequestHandler):
    def get(self):
        name = self.get_argument("name")
        self.write("hello %s" % name)


class HtmlHandler(tornado.web.RequestHandler):
    def get(self):
        self.write(html)


class TestGetHandler(tornado.web.RequestHandler):
    def get(self):
        name = self.get_argument("name")
        self.write("%s" % name)


class TestPostHandler(tornado.web.RequestHandler):
    def get(self):
        html = (
            '<form action="/test/post" method="post">'
            '姓名:<input type="text" name="name">'
            '<br>'
            '城市:<input type="text" name="city">'
            '<input type="submit" value="提交">'
            '</form>'
        )
        self.write(html)

    def post(self):
        name = self.get_argument('name')
        city = self.get_argument('city')
        self.write('%s生活在%s' % (name, city))


def make_app():
    return tornado.web.Application([
        (r"/", MainHandler),
        (r"/foo", HtmlHandler),
        (r"/test/get", TestGetHandler),
        (r"/test/post", TestPostHandler),
    ])


if __name__ == "__main__":
    app = make_app()
    app.listen(options.port, options.host)

    loop = tornado.ioloop.IOLoop.current()
    loop.start()
```

#####  一般格式


```python
import tornado.ioloop
import tornado.web
from tornado.options import parse_command_line,define,options

define("host",default="0.0.0.0",help="主机地址",type=str)
define("port",default=8000,help="端口号,type=int")

class Handler(tornado.web.RequestHandler):
    def get(self):
        pass
    def post(self):
        pass

def make_app():
    return tornado.web.Application([
        (r"/",Handler),
    ])

if __name__=="__main__":
    app = make_app()
    app.listen(options.port,options.host)
    
    loop = tornado.ioloop,IOLoop.current()
    loop.start()
```
##### 获取参数

get方式可从url中获取参数值，而post方式则是从form表单中获取参数值

name = self.get_argument("name")

##### 写入数据至页面

self.write(html)

### 练习

1. 开发接口，并根据用户传入的id显示对应的用户信息，

2. 开发接口，并根据用户传入的数值修改用户数据

```python
import tornado.ioloop
import tornado.web
from tornado.options import parse_command_line, define, options
import pymysql

define("host", default="0.0.0.0", help="主机地址", type=str)
define("port", default=8000, help="主机端口", type=int)

db = pymysql.connect(host='localhost',
                     user='z',
                     password='123321',
                     db='exam',
                     charset='utf8')


class MysqlGetHandler(tornado.web.RequestHandler):
    def get(self):
        ID = self.get_argument("ID")
        with db.cursor() as cursor:
            # 读取记录
            cursor.execute('select * from student where id = %s', (ID,))
            result = cursor.fetchall()
            mes = result[0]
            t = ['id', 'name', 'sex', 'city', 'description', 'birthday', 'only_child']
            for i in range(len(mes)):
                self.write(t[i])
                self.write("：")
                self.write(str(mes[i]))
                self.write("<br>")


class MysqlPostHandler(tornado.web.RequestHandler):
    def get(self):
        html = (
            '<form action="/mysql/post" method="post">'
            'ID:<input type="text" name="id">'
            '<br>'
            '姓名:<input type="text" name="name">'
            '<br>'
            '性别:<input type="radio" name="sex" value="男">男'
            '<input type="radio" name="sex" value="女">女'
            '<br>'
            '城市:<input type="text" name="city">'
            '<br>'
            '概述:<input type="text" name="description">'
            '<br>'
            '生日:<input type="text" name="birthday">'
            '<br>'
            '是否为独生子女:<input type="radio" name="only_child" value=1>是'
            '<input type="radio" name="only_child" value=0>否'
            '<br>'
            '<input type="submit" value="提交">'
            '</form>'
        )
        self.write(html)

    def post(self):
        id = self.get_argument('id')
        name = self.get_argument('name')
        sex = self.get_argument('sex')
        city = self.get_argument('city')
        description = self.get_argument('description')
        birthday = self.get_argument('birthday')
        only_child = self.get_argument('only_child')
        # print(name, sex, city, description, birthday, only_child)
        with db.cursor() as cursor:
            # 修改数据
            cursor.execute(
                'update student set name=%s,sex=%s,city=%s,description=%s,birthday=%s,only_child=%s where id = %s',
                [name, sex, city, description, birthday, only_child, id])
        db.commit()


def make_app():
    return tornado.web.Application([
        (r"/mysql/get", MysqlGetHandler),
        (r"/mysql/post", MysqlPostHandler)
    ])


if __name__ == "__main__":
    app = make_app()
    app.listen(options.port, options.host)

    loop = tornado.ioloop.IOLoop.current()
    loop.start()

    db.close()
```

# 数据库与模板系统

### ORM：对象关系映射

ORM是把数据库中的内容通过关系映射到后端程序中，形成一个关系类，然后可以通过关系类来对数据库形成控制

简单而言，就是后端定义一个类对应数据库的各个字段，通过ORM实现双向控制

ORM优点：

​			数据模型定义在一个地方，方便维护和更新，也利于重用代码

​			ORM有现成的工具，很多功能都可以自动完成

​			迫使你使用MVC架构，ORM就是天然的Model，能够使代码更清晰

​			基于ORM的业务代码比较简单，代码量少，语义性好，容易理解

​			不必编写性能不佳的SQL

常用的ORM：Django-ORM，SQLAlchemy，Peewee等

### 示例

库：sqlalchemy

##### 导入库

```python
improt datetime    # 生成日期

from sqlalchemy import create_engine
from sqlalchemy.orm import sessionmaker
from sqlalchemy import Column,String,Integer,Float,Date
from sqlalchemy.ext.declarative import declarative_base
from sqlalchemy import or_, and_, all_, any_
```

##### 建立与数据库的连接

```python
engine = ecreate_engine("mysql+pymysql://z:123321@localhost:3306/exam")
Base = declarative_base(bind=engine)   # 创建模型的基础类
Session = sessionmaker(bind=engine)
```

##### 生成类

```python
class User(Base):
    __table__='student'
    id = Column(Integer,primary_key=True)
    name = Column(String(20),unique=True)
    birthday = Column(Date)
    money = Column(Float,default=0.0)
```

##### 创建表

```python
Base.metadata.create_all(checkfirst=True)
```

##### 定义一些对象

```python
bob = User(name='bob', birthday=datetime.date(1990, 3, 21), money=234)
tom = User(name='tom', birthday=datetime.date(1995, 9, 12))
lucy = User(name='lucy', birthday=datetime.date(1998, 5, 14), money=300)
jam = User(name='jam', birthday=datetime.date(1994, 3, 9), money=58)
```

##### 数据库操作

```python
session = Session()

# 增加数据
session.add_all([bob,tom,lucy,jam])
session.commit()

# 删除数据
session.delete(bob)
session.commit()

# 修改数据
tom.money = 100
session.commit()

# 查询数据
q = session.query(User)   # 定义表的查询对象

# 直接查询ID为3的数据
user = q.get(3)
print(user.id,user.name)

# 使用filter_by按条件查询，filter_by内部含多个条件时，默认按and方法
user = q.filter_by(User.id>2).one()
for u in user:
    print(u.id,u.name)

# 使用filter进行范围查询，并对结果进行排序
user = q.filter(or_(User.id>2,User.money>10)).group_by('birthday')
for u in user:
    print(u.id,u.name,u.money)

# 根据查询结果进行更新
users.update({'money':User.money-1},synchronize_session=False)
session.commit()

# 按数量取出数据
users = q.limit(3).offset(4)
for u in user:
    print(u.id,u.name,u.money)
    
# 计数
num = q,filter(User.money>200).count()
print(num)

# 检查是否存在
exists = q.filter_by(name = 'z').exists()
result = session.query(exists).scalar()
print(result)
```

### Tornado 的模板系统

模板系统是为了更加快速，更方便的生产大量的页面而设计的一套程序

借助模板，我们可以先写好页面大致的模样，然后往预留数据的位置插入数据即可

##### 模板系统目录结构

```py
|——main.py
|——statics
|	|_img
|		|_coder.jpg
|__templates
	|_index.html
```

##### 模板与静态文件的路径配置

定义app时，在Application中定义，可以是相对路径，也可以是绝对路径，通常为绝对路径

```python
def make_app():
    routes = [
        (r'/', GetHandler),
        (r'/post', PostHandler)
    ]
    base_dir = os.path.join(os.path.dirname(__file__), "templates")   # templates的绝对路径
    static_dir = os.path.join(os.path.dirname(__file__), 'statics')   # statics的绝对路径
    return tornado.web.Application(
        routes,
        template_path=base_dir,  # 模版路路径
        static_path=static_dir,  # 静态文文件路路径
        autoreload=True
    )

app = make_app()
```

##### 模板中的变量

在网页中，如果要留一个位置交给后端传递数据，格式为{{ 变量名 }}

```html
<!DOCTYPE html>
<html lang='en'>
    <head><meta charset='UTF-8'> 
    <title>Templates</title>
</head>
<body>
    <div>你好 {{ name }}，欢迎回来！</div>
    <div>猜⼀猜，3 x 2 等于⼏？</div>
    <div>我就不告诉你等于 {{ 3 * 2 }}</div>
</body>
</html>
```

python变量传递

```python
class MainHandler(tornado.web.RequestHandler):
    def get(self):
        name = 'Tom'
        say = "Hello, world"
        self.render('index.html', name=name, say=say)
```

##### 模板中的if·····else 结构

模板中的控制语句由{%  %}来进行声明

一般结构：

```html
{% if 条件 %}
	<div>·····</div>
{% elif 条件 %}
	<div>·····</div>
{% else %}
	<div></div>
{% end %}
```

##### 模板中的for循环

循环语句和控制

语句实现方式差不多，都是用{%  %}来声明

一般结构：

```html
{% for i in rang(10) %}
	<p>{{ i }}</p>
{% end %}
```

##### 静态文件

静态文件一般放于statics目录中，通常的静态文件有图片，js等

路径名需要以/static/开头，也就是定义的绝对地址--static_path

若插入img中的一张coder.jpg图片

```htm
<img src="/static/img/coder.jpg">
```

##### 模板的继承

通过模板的继承，能够实现页面的动态展示，也就是只改变页面的一部分内容

父模板文件名通常定义为"base.html"，子模版替换时也可使用父模板中的css样式

父模板--base.html：

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Seamile</title>
    <style>
        body{
            width:900px;
            margin:0 auto;
        }
        .content{
            float:left;
            width:700px;
        }
        .sidebar{
            float:left;
            width:200px;
        }
        tr{
            white-space: nowrap;
        }
        a{
            font-size:16px;
            color:#000;
            text-decoration:none;
        }
        span{
            margin:0px auto;
        }
    </style>
</head>
<body>
    <div class="navbar">
        <img src="/static/img/coder.jpg" style="width:50px;height:50px;">
        <a href="/">主页</a>
        <a href="/post"></a>
    </div>

    <hr style="margin-bottom:30px;"/>

    <div class="content">
        {% block container %}{% end %}
    </div>
</body>
</html>
```

子模版--mod.html：

```html
{% extends 'base.html' %}

{% block container %}
    <form action="/post" method="post">
            序号:<input type="text" name="id">
            <br>
            姓名:<input type="text" name="name">
            <br>
            性别:<input type="radio" name="sex" value="男">男
            <input type="radio" name="sex" value="女">女
            <br>
            城市:<input type="text" name="city">
            <br>
            概述:<input type="text" name="description">
            <br>
            生日:<input type="text" name="birthday">
            <br>
            独生:<input type="radio" name="only_child" value=1>是
            <input type="radio" name="only_child" value=0>否
            <br>
            <input type="submit" value="提交">
    </form>

{% end %}
```

子模版--search.html：

```html
{% extends 'base.html' %}

{% block container %}
    <form action="/" method="get" style="margin-bottom:30px;">
        <input type="text" name="s" placeholder="可按序号,姓名,性别及住址搜索">
        <input type="submit">
    </form>
    <div>
        <table border="1px" rules="all" width="100%">
            <tr>
                {% for i in menu %}
                    <td><strong>{{ i }}</strong></td>
                {% end %}
            </tr>
            {% for i in user %}
            <tr>
                {% for j in i %}
                <td style="width:100px">{{ j }}</td>
                {% end %}
            </tr>
            {% end %}
        </table>
    </div>
    <hr style="margin-top:50px"/>

    <span>修改数据入口：<a href="/post">...</a></span>

{% end %}
```

# 虚拟环境与Git

### MVC网站架构

MVC模式是一种软件架构模式，把软件系统分为三个基本部分：

​		模型(model)：程序需要操作的数据或信息

​		视图(view)：提供给用户的操作界面，是程序的外壳

​		控制器(Controller)：负责根据用户从视图层输入的指令，选取数据层中的数据，然后进行相应的操作，一般就是软件系统的主函数

MVC的特点：构建简单，层次清晰，代码可复用性好，模块之间耦合度低

```html
|——main.py
|——model.py
|——view.py
|——statics
|	|_img
|		|_coder.jpg
|__templates
	|_index.html
```

### 虚拟环境

当不同模块使用的环境不同时，为了避免和我们系统安装的环境发生冲突，我们就可以使用虚拟环境来安装不同的运行环境来调试程序

##### 创建虚拟环境

```python
cd ~/项目文件夹

# 创建虚拟环境
# 虚拟环境可以创建在任何位置，不过一般和项目文件放在一起
virtualenv env
```

##### 加载虚拟环境

```python
source env/bin/activate
或
source ~/项目文件夹/env/bin/activate
```

##### 环境导出

```python
touch requeirements.txt
pip freeze > requeirements.txt
```

##### 退出虚拟环境

```python
deactivate  # 当调试结束之后，可以退出当前虚拟环境
```

##### 其他人重新搭建环境时

```python
pip install -r requirements.txt
```



### 版本控制工具与Git

##### 版本控制工具的作用

1. 能够追踪全部代码的状态
2. 能够进行版本之间的差异对比
3. 能够进行版本回滚
4. 能够协助多个开发者进行代码合并

##### 常见的版本控制工具

CVS：基本退出

svn：中心化的版本控制工具，需要一台中心服务器，各个开发者的代码都需要提交至中心服务器，如果中心服务器发生故障，则存储内容将不可获取

git：分布式的版本控制工具，去除了中心服务器，每个开发者都可以自提交，也可和svn一样提交至公共服务器

hg：纯python开发的版本控制工具

Github：依托git而创建的一个平台，有独立的公司在运作

---所有文本类的文件都可以交由版本控制工具来管理

##### 起步

1. 配置自己的账号和邮箱

   ```python
   git config --global user.name '名字'
   git config --global user.email '邮箱'
   ```

2. 设置要忽略的文件

   ```python
   touch .gitignore
   echo 忽略的文件名 > .gitignor
   
   .gitignor文件中可以存需要忽略的文件名，或某一类文件的通配符,例：
   *.pyc
   *.log
   *.sqlite3
   .DS_Store
   .venv/
   .idea/
   __pycache__/
   ```

3. 仓库初始化,产生一个.git的目录，这个文件夹就是本地仓库

   ```python
   git init
   ```

4. 将当前文件夹下的所有内容添加至暂存区

   ```python
   git add ./
   ```

5. 将暂存区的内容取消暂存状态

   ```python
   git reset 文件名
   ```

6. 将暂存区的内容提交至本地仓库，并以“管理系统”来备注

   ```python
   git commit -m '管理系统'
   ```

7. 查看提交历史

   ```python
   git log --graph  # 显示分支结构
   ```

8. 查看当前分支状态

   ```python
   git status
   ```

9. 暂缓区和工作区进行差异比较

   ```python
   git diff filename
   ```

10. 将本地仓库推送至远程仓库

   ```python
   git push -u origin master
   ```

11. 在~/.ssh目录下生成一对公钥和密钥,将公钥内容复制至GitHub中，这样就可实现不需要验证

    ```python
    ssh-keygen
    ```

12. 将GitHub中的整个程序拷贝到本地文件

    ```python
    git clone 'github中生成的url地址'
    ```

13. 将远程仓库的更新拉取到本地

    ```python
    git pull
    ```


14. 创建分支

    ```shell
    git branch 分支名     # 创建分支
    git checkout 分支名   # 切换分支
    或
    git checkout -b 分支名   # 切换并创建分支
    ```

15. 合并分支

    ```shell
    git merge 分支名
    ```

16. 错误追究

    ```shell
    git blame
    ```

    f