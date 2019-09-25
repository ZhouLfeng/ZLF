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
使用session需要在__init__方法中配置app.config['SESSION_KEY']='110'        # 密钥
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
session持久化问题
-django默认为session做了持久化，就是存储在数据库中
-fask默认并没有为session作持久化处理，需要修改session配置
flask-session可以实现session的数据持久化
通常使用redis来进行存储
缓存在磁盘上时，管理磁盘文件使用lru，最近最少使用原则
持久化位置设定：
				app.config['SESSION_TYPE'] = 'redis'
初始化session对象：
				Session(app=app)
    			session = Session()       session.init_app(app=app)
查看redis内容：
				redis -cli
    			keys *
        		get key
            	ttl session    查看session存活天数     flask默认31天，django默认14天
```

### Template

```python
MVC中的V，MTV中的T
主要用来作数据展示用
模板处理过程分为两个阶段：1.加载   2.渲染
jinjia2模板引擎：
	1.本质上是html
    2.支持特定的模板语法
    3.flask作者开发
    4.优点：
    		速度快，被广泛使用
        	HTML设计和后端python分离
            减少python的复杂度
            非常灵活，快速和安全
            提供了控制，继承等高级功能
```

```python
模板：
	1.静态页面，前后端分离
    2.模板语言动态生成html
    	{{ var }}:接收变量
        {% tar %}：结构标签
        			block:模板中为挖坑操作，子模板中可作填坑操作，不想被覆盖，需要添加{{ super() }}
    宏定义：
    	无参
    	{% macro  say() %}
        
        {% endmacro %}
        
         有参
        {% macro  say(name) %}
       	{{ name }}
        {% endmacro %}
        
        外文件调用
        {% macro  say(name) %}
       	{{ name }}
        {% endmacro %}
        
        {% from 'html文件' import x %}
        {% say('action') %}
        
        
循环控制：
		{% for i in range(10) %}
    			{{ loop.first }}第一个
        		{{ loop.last }}最后一个
            	{{ loop.index }}索引
        {% endfor %}
选择：
		{% if 条件 %}
    			语句
        {% elif  条件 %}
        		语句
        {% else %}
        		语句
        {% endif %}
过滤器：
		{{ var|xxx|yyy|zzz }}
    	没有数量限制
        lower:小写
        upper:大写
        trim:去左右空格
        reverse:反转
        striptags:渲染之前将值中的标签去掉
        safe:标签生效
```

### models

```python
1.数据交互的封装
2.flask默认并没有提供任何数据库操作的api
	flask可以自己选择数据库，用原生语句实现功能，但原生语句冗余太多，代码利用率低，条件复杂的语句很长，所以不会选择原生sql
SQLAlchemy、MongoEngine：
	将对象的操作转换为原生SQL
    优点：
    	易用性，可以有效减少重复sql
        性能损耗少
        设计灵活，可以轻松实现复杂查询
        移植性好
3.flask中并没有提供默认的ORM
	orm：对象关系映射
    通过操作对象，实现对数据的操作
```

```python
flask-sqlalchemy:
    安装：pip install flask-sqlalchemy
    创建sqlalchemy对象:
        1. db = SQLAlchemy(app = app)
        2. db = SQLAlchemy()   ----放在models模块中
           db.init_app(app=app)----放在__init__模块中
    __init__中配置sqlalchemy：
    	app.config['SQLALCHEMY_DATABASE_URI']=
        		'dialect+driver://username:password@host:prot/database'
        app.config['SQLALCHEMY_TRACK_MODIFICATIONS']=False
   	创建表示必须要创建主键并且给定字符长度
```

```python
使用:
    定义模型：继承sqlalchenmy对象中的model
    定义字段：字段名=db.Colum(字段类型)
    		一定要添加一个主键
    创建表：db.create_all()
    删除表：db.drop_all()
    修改表名：__tablename__=''   在models中修改
    数据操作:
        添加：db.session.add(对象)
        	 db.sesssion.commit    ----提交
       	查询：模型名.query.all()
```

### 项目拆分

```python
1. 4种不同的测试环境:
      开发环境(develop)
      测试环境(test)
      演示环境(show)
      线上环境(product)
2. 拆分项目
	  规划项目结构
    	manager.py
        	app的创建
            Manager(flask-script管理对象)
        App
          __init__:
                创建Flask对象(create_app)
                加载settings文件
                调用init_ext方法
                调用init_blue方法
          settings:
            	App运行的环境配置
                运行环境
          ext:
            	用来初始化第三方插件
                sqlalchemy对象初始化 数据库
                session初始化
          views:
            	蓝图
                创建
                注册到app上
          models:
            	定义模型
```

```python
__init__.py:
    from flask import Flask

	from App import settings
	from App.ext import init_ext


	def create_app(way):
        app = Flask(__name__)

        app.config.from_object(settings.env_name[way])

        init_ext(app)

        return app

```

```python
ext.py:
    from flask_migrate import Migrate
    from flask_session import Session

    from App.models import db


    def init_ext(app):
        app.config['SECRET_KEY'] = '110'

        app.config['SESSION_TYPE'] = 'redis'
        app.config['SESSION_KEY_PREFIX'] = 'PYTHON'
        Session(app=app)

        db.init_app(app=app)

        migrate = Migrate()
        migrate.init_app(app=app,db=db)
```

```python
models.py:
    from flask_sqlalchemy import SQLAlchemy

    db = SQLAlchemy()


    class User1(db.Model):
        id = db.Column(db.Integer, primary_key=True, autoincrement=True)
        name = db.Column(db.String(32))

    class Emp(db.Model):
        id = db.Column(db.Integer, primary_key=True, autoincrement=True)
        name = db.Column(db.String(32))
```

```python
settings.py:
    def get_database_uri(DATABASE):
        dialect = DATABASE.get('dialect')
        driver = DATABASE.get('driver')
        username = DATABASE.get('username')
        password = DATABASE.get('password')
        host = DATABASE.get('host')
        port = DATABASE.get('port')
        database = DATABASE.get('database')
        return '{}+{}://{}:{}@{}:{}/{}'.format(dialect, driver, username, password, host, port, database)


    class Config():
        Test = False
        Debug = False
        SQLALCHEMY_TRACK_MODIFICATIONS = False


    class developConfig(Config):
        Debug = True
        DATABASE = {
            'dialect': 'mysql',
            'driver': 'pymysql',
            'username': 'z',
            'password': '123321',
            'host': 'localhost',
            'port': '3306',
            'database': 'day04'
        }
        SQLALCHEMY_DATABASE_URI = get_database_uri(DATABASE)


    class testConfig(Config):
        Test = True
        DATABASE = {
            'dialect': 'mysql',
            'driver': 'pymysql',
            'username': 'z',
            'password': '123321',
            'host': 'localhost',
            'port': '3306',
            'database': 'day04'
        }
        SQLALCHEMY_DATABASE_URI = get_database_uri(DATABASE)


    class showConfig(Config):
        Debug = True
        DATABASE = {
            'dialect': 'mysql',
            'driver': 'pymysql',
            'username': 'z',
            'password': '123321',
            'host': 'localhost',
            'port': '3306',
            'database': 'day04'
        }
        SQLALCHEMY_DATABASE_URI = get_database_uri(DATABASE)


    class productConfig(Config):
        Debug = True
        DATABASE = {
            'dialect': 'mysql',
            'driver': 'pymysql',
            'username': 'z',
            'password': '123321',
            'host': 'localhost',
            'port': '3306',
            'database': 'day04'
        }
        SQLALCHEMY_DATABASE_URI = get_database_uri(DATABASE)


    env_name = {
        'develop': developConfig,
        'test': testConfig,
        'show': showConfig,
        'product': productConfig,
    }

```

```python
views.py:
    from flask import Blueprint
    from App.models import db
    blue = Blueprint('blue', __name__)

    @blue.route('/')
    def hello_world():
        return 'Hello World!'

    @blue.route('/addUser/')
    def addUser():
        db.create_all()
        return '创建成功'
```

```python
manager.py:
    from flask_migrate import MigrateCommand
    from flask_script import Manager
    from App import create_app
    from App.views import blue

    # way = input('选择模式(develop,test,show,product):')

    app = create_app(way='develop')

    manager = Manager(app=app)

    app.register_blueprint(blueprint=blue)

    manager.add_command('db',MigrateCommand)

    if __name__ == '__main__':
        manager.run()
```

### flask-migrate

```python
1. 安装：pip install flask-migrate
2. 初始化
   -创建migrate对象，将app和db初始化，代码放在ext中
    	migrate = Migrate()
    	migrate.init_app(app=app,db=db)
   -懒加载初始化
		在manager中添加command(MigrateCommand)
    		manager.add_command('db',MigrateCommand)
3. 终端命令代码
	python  manager.py  db  ~~~
    -init  第一次使用，初始化
    -migrate  生成迁移文件    可加'-message “名称”'备注
    		不能生成有两种情况：模型定义从未调用过；数据库已有模型记录
    -upgrade  升级
    -downgrade  降级
```

### DML

```python
DDL：数据定义语言
	针对表操作：create   alter  drop
DML：数据操纵语言
	针对数据操作：insert   delete   update
DQL：数据查询语言  select
TCL：事务    commit   rollback
```

```python
增:
    1. 添加一个对象
    	db.session.add()
        -a = person()
        -a.name = '1'
        -a.age='1'
        -db.session.add(a)
        -db.session.commit()
    2. 添加多个对象
    	db.session.add_all()
        -s = []
        -for i in range(5):
            -p = person()
            -p.name='小%d' % i
            -p.age='%d' % i
            -s.append(p)
        -db.session.add_all(s)
        -db.session.commit()

删:
    db.session.delete(对象)   基于查询

改:
    db.session.add(对象)    基于查询
```

```python
查:
    1. 获取单个数据
      -按主键值获取，获取不到不会报错
    	person=Person.query.get(3)
      -first
    	person=Person.query.first()
    2. 获取结果集
      -x.query.all()  获取所有
      -x.query.filter_by(条件)   按条件查询
      -x.query.filter(条件)      按条件查询
        	filter_by:只支持主键查找，直接用=进行等值查找
            filter:比filter_by功能强大，用==进行等值查找，可根据其他字段的值进行查找，不过需要加数据库类名前缀，即Person.name==1
```

```python
数据筛选:
    order_by:
        降序：person=Person.query.order_by('age')
        升序：person=Person.query.order_by(db.desc('age'))
   	limit:
        取出前几行数据
        person=Person.query.limit(2)
    offset:
        跳过前几行
        person=Person.query.offset(2)

    limit和offset可以不区分前后位置，因为offset优先级比limit高，不论位置怎样写，都是offset先执行
    order_by需要先调用执行，不然会报错
    
sql关键字优先级：select  from  where  group_by  having   order_by
```

```python
分页器pagination:
    原生代码：
    	page：页数     page_per：每页显示的数据量
        person = Person.query.limit(page_per).offset(page_per*(page-1))
    封装：
    	person = Person.query.paginate(page_num,page_per,False).items
```

### 分页器方法

```python
分页器：BaseQuery.pagination(page_num,page_per,False)
方法(Pagination):
		items------迭代(遍历数据)
        pages------总页数
        prev_num---上一页的页码
        has_prev---是否有上一页
        next_num---下一页的页码
        has_next---是否有下一页
        iter_pages-上一页与下一页之间的页码
```

### 数据定义

一对多：

```python
1. 字段类型
	Integer
    String
    Date
    Boolean
2. 约束
	primary_key:主键
    autoincrement:主键自增长
    unique:唯一
    default:默认值
    index:索引
	not null:不能为空
    ForeignKey:外键---约束级联数据
        		使用relationship实现级联数据获取
            	格式:relationship('表名',brckref='表名',lazy=True/False)
                    '表名':关联的表
                    backref:提供反查询，可通过子表查找父表
                    lazy:懒查询模式，只有在真正调用的时候才会对数据库进行调用
```

### 模型关系

```python
1. 模型定义
	 	class Parent(db.Model):
              id=db.Column(db.Integer,primary_key=True,autoincrement=True)
              name=db.Column(db.String(30),unique=True)
              children=db.relationship("Child",backref="parent",lazy=True)

          class Child(db.Model):
              id = db.Column(db.Integer, primary_key=True)
              name = db.Column(db.String(30), unique=True)
              parent_id = db.Column(db.Integer, db.ForeignKey('parent.id'))
                
2.应用
		添加：
    		p = Parent()
        	p.name = '张三
            c = Child()
            c.name = '赵四'
            c1 = Chile()
            c1.name = '王五'
            p.childen = [c,c1]
            
            db.session.add(p)
            db.session.commit()
        
        查：
        	主查从：
            	clist = Child.query.filter(Parend.id == 1)
            从查主：
            	p = Parent.query.filter(Child.id == 1)
```

一对一：

```python
一对一需要在relationship中设置uselist=False，其他和一对多操作一样
```

多对多：

```python
1. 模型定义
		  class User(db.Model):
              id = db.Column(db.Integer,primary_key=True,autoincrement=True)
              name = db.Column(db.String(32))
              age = db.Column(db.Integer,default=18)

          class Movie(db.Model):
              id = db.Column(db.Integer,primary_key=True,autoincrement=True)
              name = db.Column(db.String(32))

          class Collection(db.Model):
              id = db.Column(db.Integer,primary_key=True,autoincrement=True)
              u_id = db.Column(db.Integer,db.ForeignKey(User.id))
              m_id = db.Column(db.Integer,db.ForeignKey(Movie.id))
               
2.应用场景(购物车添加)
		@blue.route('/getcollection/')
        def getcollection():
            u_id = int(request.args.get('u_id'))
            m_id = int(request.args.get('m_id'))
            c = Collection.query.filter(Collection.u_id == u_id).filter_by(m_id = m_id)

            if c.count() > 0:
                print(c.first().u_id,c.first().m_id)
                # print(c)
                # print(type(c))
                # print('i am if')
                return '已经添加到了购物车中'
             else:
                c1 = Collection()
                c1.u_id = u_id
                c1.m_id = m_id
                db.session.add(c1)
                db.session.commit()
                return 'ok'
```

### flask-debugtoolbar

```python
安装：pip install flask-debugtoolbar
ext中初始化：
	app.debug = True
    debugtoolbar = DebugToolBarExtension()
    debugtoolbar.init_app(app=app)
```

### flask-bootstrap

```python
安装:pip install flask-bootstrap
ext中初始化:
    bootstrap(app=app)
继承bootstrap模板:{% extends 'bootstrap/base.html' %}
```

### 缓存flask-cache

```python
目的：减少数据库的IO操作，优化加载
实现方式，即cache存放位置:
    1. 数据库(新建表)
    2. 文件
    3. 内存
    4. 内存级数据库(redis)
    
实现流程:
    1. 从路由函数进入程序
    2. 路由函数到视图函数
    3. 视图函数去缓存中查找
    4. 缓存中找到，直接进行数据返回
    5. 若没找到，去数据库中查找
    6. 查找到之后，添加到缓存中
    7. 返回数据到页面
    
安装:pip install flask-cache
初始化:
    指定使用的缓存方案
    	cache = Cache(config={'CACHE_TYPE':'Redis'})
        cache.init_app(app=app)
使用:
    必须在路由下面添加@cache.cached(timeout=30)
    配置:cache = Cache(config={'CACHE_TYPE':'Redis'})
        cache = Cache(config={'CACHE_KEY_PREFIX':'py'})
用法:
    1. 装饰器：@cache.cached(timeout=30)
    2. 原生
    	cache.get() ----获取缓存中的值
        cache.set() ----设置缓存数据
```

### 钩子

```python
用法:
    添加视图函数
    	@blue.before_request
        添加完之后就可以实现面向切面编程(纵向编程)
        即在各个视图函数执行之前都会执行钩子函数
```

### 四大内置对象

```python
1. request:请求的所有信息
2. response:服务端会话技术的接口
3. config:当前项目的配置信息
    		在模板中也可以直接调用config
        	在py代码中需要调用current_app.config
4. g:全局变量(global)
    	可以将变量变为全局变量以供其他函数的使用
        使用方式:g.变量名
            例：
            @blue.route('/g/')
            def g():
                g.ip = 1
                return 'ok'

            @blue.route('/g1/')
            def g1():
                print(g.ip)
                return 'wa'
```

### 路径

```python
os模块:
    os.path.join----------------拼接路径
    os.path.abspath(__file__)---当前文件的绝对路径
    os.path.dirname()-----------当前文件的上一级文件夹的路径

项目文件路径:
    变量放在settings配置文件中
    BASE_DIR = os.path.dirname(os.path.dirname(os.path.abspath(__file__)))

若static文件夹在项目文件夹中，需配置static_folder:
	app = Flask(__name__,static_folder=os.path.join(settings.BASE_DIR,'static'))
    
若templates文件夹在项目文件中，需配置templates_folder:
    app = Flask(__naem__,templates_folder=os.path.join(settings.BASE_DIR,'templates'))
```

### 前后端分离

```python
整合网络和软件的一种架构模式(表现层状态转移)
	每个URI代表一类资源，是对数据库的操作(增删改查)
使用请求方式来作为动作标识(GET,POST,PUT,DELETE,PATCH)
使用json来进行数据传输
```

原生

```python
概念：判断不同的请求方式，实现请求方法
高内聚，低耦合

通过判断request.method == '请求方式' 来进行分层，完成不同的操作
```

### flask-restful

```python
对原生的前后端分离的架构模式进行的框架简化

安装：pip install flask-restful
初始化：
	urls-----在init中调用init_urls
    	api = Api()
        api.add_resource(Hello,'/hello/')
        def init_urls(app):
            api.init_app(app=app)
   	apis基本用法
    	继承来自Resource
        class Hello(Resource):
            # 实现请求的对应函数
			def get(self):
                data = {
                    'msg':'get',
                    'status':200
                }
                return data
            
            def post(self):
                data = {
                    'msg':'post',
                    'status':200
                }
                return data
```

### 定制输入输出

```python
定制输出：
	fields中的类型约束
			String
			Integer
			Nested
			List
			Nested
     @marshal_with基本使用
    		类型括号中添加约束
        		attribute=变量名----约束该变量
            	default=值---------设置默认值
      		例：
            	r1Fields={
                    'msg':fields.String(default = 'OK')
                }
            	 @marshal_with(r1Fields)
                 class Hello(Resource):
                 def get(self):
                    data = {
                        'msg':'get',
                        'status':200
                    }
                    return data
               
            若预定义结构比返回数据字段多，则会给默认值
            	Interger默认值：0
                String默认值：null
            若预定义结构比返回数据字段少，则自动过滤
            
            
定制输入
	使用：
    	parser = reqparse.RequestParser()
        parser.add_argument("c_name", type=str)
        parser.add_argument("id", type=int, required=True, help="id 是必须的")
		parse = parser.parse_args()
		cat_name = parse.get("c_name")
        id = parse.get("id")
        print(id)
        在对象中添加字段
			对字段添加约束
			default
			required
				必须的参数
			help
				id是必须的
			action
				action=append
					c_name=tom&c_name=zs
		继承
			copy
			可以对已有字段进行删除和更新
			继承解析
    - 在整个项目中，通用字段可以创建一个基parser
    - 复用已有的部分参数转换数据结构
			parse_c parser.copy()   parse_c.remove_argument('')
```

