# Flask

轻型框架：只提供核心功能，自由灵活，高度定制。flask也被称为 “ microframework ” ，

重量级框架：提供丰富的功能和工具，能够支持各种操作，但灵活度不高。django为重量级框架

官方文档：

​				http://flask.pocoo.org/docs/0.12/      英文

​				http://docs.jinkan.org/docs/flask/     中文

flask依赖第三方库：

​				jinja2       模板引擎

​				werkzug  wsgi  工具集

​				Itsdangerous    基于django的签名模块

flask流行的原因：

​				有非常齐全的官方文档

​				有非常好的扩展机制和第三方扩展环境

​				社区活跃度非常高

​				微型框架的形式给开发者有了更大的选择空间

### BS/CS

BS：浏览器/服务器

CS：客户机/服务器

区别：

BS:用户固定，并且处于相同区域，拥有相同的操作系统；对客户的客户端要求比较高；每个客户端都必须安装和配置软件；每个用户都必须升级程序，可以采用自动升级。

CS：只需要浏览器和操作系统，与操作系统的型号没关系；客户端的要求较低，可以在任何地方进行操作，不需要装任何专门的软件，不必安装及维护

安全性：CS结构一般面向相对固定的用户群，程序更加注重流程，可以对权限进行多层次校验，提供了更安全的存取模式，对信息安全的控制能力很强。一般高度机密的信息系统采用C/S结构

### MVC/MTV

MVC：软件架构思想

​			M为模型，封装数据的交互操作；V是视图，实现数据呈现；C是控制器，接受用户的输入输出或请求，协调模型层和视图层之间的关系。使用MVC的作用是将M和V实现代码分离，从而使同一个程序可以使用不同的表达形式。C的存在是确保M和V的同步，一旦M改变，V应该同步更新实现模型层的复用

​			核心思想：解耦合

​			面向对象语言：高内聚，低耦合

##### 流程

​		用户输入---->通过控制器实现交互---->提交用户输入命令至业务模型---->进行逻辑判断，并调用数据库进行抓取---->根据业务逻辑选择不同的视图---->通过视图层将结果呈现给用户

MTV

​		MTV也叫做MVT，本质上和MVC没有区别

​		MTV中：

​		M：model---MVC中的M

​		T：template(模板)---MVC中的V

​		V：视图函数----MVC中的C

### flask基本使用

1. 虚拟环境的创建

   ```shell
   virtualenv flask1905 -p /usr/bin/python3
   source flask1905/bin/activate
   
   查看虚拟环境：
   pip freeze
   pip list
   
   虚拟环境迁移
   pip freeze > requirements.txt    迁出
   pip install -r requirements.txt  迁入
   ```

2. flask项目的创建

   ```python
   安装flask：pip install flask
   
   创建项目
   from flask import Flask
   app = Flask(__name__)
   
   @app.route('/')
   def hello():
       return 'hello'
   
   if __name__=="__main__":
       app.run
    
   启动服务器：python  文件名.py
   默认端口号：5000  只允许本机连接
   ```

3. 启动服务器默认参数修改

   ```python
   run中添加参数
   	debug：是否开启调试模式，开启后修改python代码自动重启，但如果修改静态文件不会自动重启
       host：主机ip
       port：端口号
       threaded：是否开启多线程
   ```

4. 命令行参数

   ```python
   安装：pip install flask-script        启动命令行参数
   
   初始化：
   	修改 文件.py为manager.py
       manager = Manager(app=app)
   	文件.run为manager.run()
   
   运行
   	python manager.py runserver -p  -h  -r
       -p:端口号
       -h:主机ip
       -r:重新加载(reload)  不需要重启服务器就可重新加载
       -d:调试模式
   ```

### 视图函数返回值

```python
1.可直接返回字符串
2.可直接返回网页
		return  render_template("test.html")
	导入css文件：<link rel="stulesheet" href="/static/css/hello.css">
```

### flask基础结构

```python
App
	templates:模板，默认和项目保持一致
    static:静态资源，默认和项目保持一致
    views
    models
    __init__
manager.py：执行主函数，与App同级，相当于把其他资源打包，只留一个主函数执行
```

### 蓝图

```python
蓝图
	1.宏观规划
    2.用来规划urls(路由)
    3.蓝图的基本使用：
    	pip install flask-blueprint
        初始化蓝图  blue = Blueprint('first',__name__)
        	-蓝图初始化只能放在视图层中，初始化蓝图后@app.route('/')改为@blue.route('/')
        调用蓝图进行路由注册  app.register_blueprint(blueprint=blue)
        	-路由注册放在主函数manager.py中
```

```python
manager.py:
    app = Flask(__name__)
    manager = Manager(app=app)
    app.register_blueprint(blueprint=blue)
    manager.run()
```

```python
views:
    blue=Blueprint('first',__name__)
    @blue.route('/')
    def hello():
        return '真好'
```

```python
__init__:
    def create_app():
        app = Flask(__name__)
        return app
```

### flask请求流程

```
1.请求到路由  app.route
2.视图函数
3.视图函数和models交互
4.模型返回数据给视图函数
5.视图函数渲染模板
6.模板返回给用户
```

### flask路由参数

带参数的请求

```python
@blue.route('/getstudent/<id>')
def getstudent():
    return id
```

```python
路由参数
<converter:var_name>
    converter:
        1.string:普通字符串类型，以'/'作为结束符
        2.path:也是字符串类型，但把'/'也作为字符，一次可接受多个参数
        3.int:整型
        4.float:浮点型
        5.uuid
        6.any:任意一个，格式:any(a,b):p,p只能在a,b中任选其一,否则会报错
```

### postman

```python
postman：模拟请求工具
请求方式：@blue.route('/',methods=[]) ---[]中可填写请求方式
		若不写methods，则默认为get、head、options
    	若指定了请求方式，则只能按[]中的几种请求方式访问，以其他方式访问会报错
```

### 反向解析

```python
获取请求资源路径
语法：url_for(蓝图名.方法名)
可避免硬指定，当用url_for指定后，程序中的url可随意改变，但运行过程不会因此受到改变
```

### request

```python
request是一个内置属性，不需要创建就可直接使用
    method:返回请求方法
    base_url:返回去掉参数后的url地址
    host_url:返回只有主机名+端口号的url地址
    url:返回完整的url地址
    remote_addr:返回请求的客户端地址
    files:文件上传
    headers:请求头
    path:路由中的路径

    request.args.get():获取get请求方式中的参数值
    request.form.get():获取post请求方式中的参数值

    cookie:请求中的cookie
session:与request类似，可直接使用
```

```python
@blue.route('/testRequest/')
def testRequest():
    # 获取的是请求方式/http方法
    print(request.method)
    # 去掉请求参数的路径
    print(request.base_url)
    # 主机的路径，不带请求资源路径
    print(request.host_url)
    # 完整路径
    print(request.url)
    # 客户端主机地址    反爬虫
    print(request.remote_addr)
    # 文件上传
    print(request.files)
    # 请求头
    print(request.headers)
    # 请求资源路径      购物车
    print(request.path)
    # 获取请求的cookies
    print(request.cookies)

    # http：//127.0.0.1：5000/testrequest/?name=zs
    # 获取name的值
    name = request.args.get('name')  # get请求获取
    print(name)

    name1 = request.form.get('name')  # post请求获取
    print(name1)
    return 'testRequest'
```

### response

```python
response即视图函数返回值
视图函数返回值主要分为两类
1.字符串
	直接返回字符串,通常只有一个参数返回,第二个返回值为状态码(可省略)
    	return '123',404
    render_template
    	渲染模板，将模板变为字符串，返回一个页面
        return  render_template('123.html')
2.response对象
	make_response
    	返回内容，状态码
        return make_response("<h1>123</h1>")
    redirect
    	重定向，通常和反向解析一起使用
        return redirect(url_for('first.abc'))
    Response
```

### 异常

```python
abort:抛出错误状态码，终止程序执行
    @blue.route('/test/')
    def test():
        abort(404)
        
捕获错误状态码:
    @blue.errorhandler(404)
    def test1(Exception):
        return '系统升级中....'
```

### 网页错误码

```python
200：成功
301：重定向
302：永久重定向
403：防跨站攻击   forbidden
404：路径错误
405：请求方式错误
500：服务器错误(业务逻辑错误)
```

### 端口号

```python
mysql：3306
mongodb：27017
oracle：1521
redis：6379

http：80
https：443

ftp：21
ssh：22
```



### 会话技术

```python
1.请求过程从request开始，到response结束
2.连接都是短连接
3.延长交互的生命周期
4.将关键数据记录下来
5.cookie是保存在浏览器/客户器的状态管理技术
6.session是服务器端的状态管理技术
```

cookie：

```python
1.客户端会话技术
2.所有数据都存储在客户端
3.以key-value键值对形式进行存储
4.服务器不做任何存储
5.特性:
    支持过期时间
    	max_age:以毫秒为单位
       	expries:记录日期
    根据域名进行cookie存储
    不能跨网站
    不能跨浏览器
    自动携带本网站的所有cookie
6.cookie是服务器操作客户端的数据
7.通过response进行操作
```

```python
cookie使用:
    需要先将response绑定一个response对象才能进行操作:
        response = redirect(url_for('first.abc'))
    设置cookie:
        response.set_cookie('name',name)
    获取cookie:
        name = request.cookies.get('name')
    删除cookie:
        response.delete_cookie('name')
```

```python
@blue.route('/tologin/')
def tologin():
    s = render_template('login.html')
    return s

@blue.route('/login/',methods=['post'])
def login():
    name = request.form.get('name')
    response = redirect(url_for('first.welcome'))
    response.set_cookie('name',name)
    return response

@blude.route('/welcome/')
def welcome():
    name = request.cookies.get('name')
    s = render_template('welcome.html')
    return s

@blue.route('/logout/')
def logout():
    response = redirect(url_for('first.welcome'))
    response.delete_cookie('name')
    return response
```



session:

```python
1.服务器会话技术
2.所有数据保存在服务器中
3.默认存在服务器中的内存中
4.存储形式采用键值对方式
```

```python
session使用:
    设置:session['name']=name
    获取:session.get('name')
    删除:
        resp.delete_cookie('session')
        session.pop('name')
```

```python

```

