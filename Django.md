# Django

### CS/BS

```python
B/S(browser/server):浏览器/服务器
C/S(client/server):客户端/服务器

主流：B/S结构
	B/S结构是web兴起的一种网络结构框架，web浏览器是客户端最主流的应用软件，这种模式统一了客户端，将系统功能实现的核心部分集中到服务器上，简化了系统的开发、维护和使用。
    
CS/BS的区别:
    硬件环境：c/s：用户固定，并且处于相同区域，要求拥有相同的操作系统；b/s：只要有操作系统和浏览器
    客户端要求：c/s：客户端的计算机电脑配置要求较高；b/s：客户端的计算机配置要求较低
    软件安装：c/s：每一个客户端都必须安装和配置软件；b/s：可以在任何地方进行操作，不用安装专门的软件
    升级和维护：c/s：每个客户端都要升级程序，可以采用自动升级；b/s：不必安装及维护
    安全性：c/s：一般面向相对固定的用户群，程序更加注意流程，它可以对权限进行多层次校验，提供了更安全的存取模式，对信息安全的控制能力很强。一般高度机密的信息系统采用C/S结构适宜
```

```python
CS/BS:
    客户端和服务器的交互模式
    	client：客户端
        browser：浏览器
        server：服务器
        	web后端框架
            	python:
                    django
                    flask
                    tornado
                java:
                    struts2/struts1
                    hibernate
                    spring
                    springmvc
                    mybatis
                    springboot
                    springclude
                php:
                    yii
                    ci
                    thinkphp
```

### MVC

```python
MVC:软件架构思想
    MVC：软件架构思想
    	M为模型，封装数据的交互操作；V是视图，实现数据呈现；C是控制器，接受用户的输入输出或请求，协调模型层和视图层之间的关系。使用MVC的作用是将M和V实现代码分离，从而使同一个程序可以使用不同的表达形式。C的存在是确保M和V的同步，一旦M改变，V应该同步更新实现模型层的复用
        核心思想：解耦合
        面向对象语言：高内聚，低耦合
	流程
    	用户输入---->通过控制器实现交互---->提交用户输入命令至业务模型---->进行逻辑判断，并调用数据库进行抓取---->根据业务逻辑选择不同的视图---->通过视图层将结果呈现给用户
        
    Model：模型，封装数据的交互操作
    View：视图，是用来将数据呈现给用户
    Controller：控制器，接受用户的输入输出，协调model和view的关系，并对数据进行操作、筛选
```

### MTV

```python
MTV
	MTV也叫做MVT，本质上和MVC没有区别
    MTV中：
    	M：model---MVC中的M
        T：template(模板)---MVC中的V
        V：视图函数----MVC中的C
        
        
浏览器<-->控制器(Controller)[urls.py、views.py]<-->模型(Model)[models.py]<--->数据库
											^
    										|
        									V
            								视图(View)[templates]
```

### Django

简介

```python
	Django是一个开源的web应用框架，最初用于管理劳伦斯出版集团下的一些以新闻内容为主的网站，即CMS(内容管理系统)软件。
	django是一个重量级框架，内置了很多的功能，满足了开发者的需求
    目前使用版本：1.11.7
    官网：http://www.djangoproject.com
```

虚拟环境

```python
创建虚拟环境
	virtualenv 虚拟环境名称
进入虚拟环境
	source 虚拟环境名称/bin/activate
退出虚拟环境
	deactivate
```

虚拟化技术

```python
1. 虚拟机
2. 虚拟容器
	Docker
    	支持很多种语言
3. 虚拟环境--迷你
	python专用
    将python依赖隔离
```

安装

```python
安装django==版本号:
    pip install django==1.11.7
    pip install django==1.11.7 -i 下载源

检查django是否安装
	pip freeze
    pip list
    进入python环境:
        import django
        django.get_version()
```

创建django项目

```python
django-admin startproject 项目名称
tree 查看项目结构

项目结构:
    项目名字
    	manage.py
        	管理整个项目的文件
        项目名称
        	__init__
           	settings
            	项目配置文件
                	ALLOWED_HOST=['*']   设置可访问的IP
                   	LANGUAGE_CODE='zh-hans'  设置中文
                    TIME_ZONE='Asia/Shanghai' 设置时区
            urls
            	根路由
                	url(p1,p2)   p1为正则匹配规则，p2为视图函数路径
            wsgi
            	用在以后项目部署
                服务器网关结构
                webserver gateway interface
```

```python
启动项目
	python manage.py runserver
    	默认运行端口在8000上
        设置主机、端口号
        1. python manage.py runserver
        2. python manage.py runserver 9000   设置9000端口
        3. python manage.py runserver 0.0.0.0:9000  设置主机为0.0.0.0 端口为9000
           可单独设置端口号，但不能单独设置主机，若需要设置主机，需要连端口号一起设置了
```

```python
创建一个应用
	python manage.py startapp App/django-admin startapp App
    App结构:
        __init__
        views
        	视图函数
            	视图函数参数为request，返回值为HttpResponse
        models
        	模型
        admin
        	后台管理
        apps
        	应用配置
        tests
        	单元测试
        migrations
        	__init__
            迁移目录
```

拆分路由器

```python
建立App包
	python manage.py startapp App
    
    创建urls
    	urlpatterns={
            url(r'^index/',views.index)
        }
   	创建views方法
    
    主路由引用
    	url(r'^app/',include('App.urls'))
        
    url访问：
    	127.0.0.1:8000/app/index
```

编写第一个请求

```python
编写一个路由：
	App中在urlpatterns中引用视图函数
		url(r'^index/',views.index)
    主路由引用
    	url(r'^app/',include('App.urls'))
编写视图函数
	1. 视图函数：函数传参是一个request，默认为request，返回值必须是一个HttpResponse
    	def index(request):
            # 返回字符串
            # return HttpResponse('123')
            # 返回标签
            return HttpResponse('<h1>123</h1>')
    2. 返回值
    	(1) HttpResponse:
            	可返回字符串或标记语言
                return HttpResponse('123')
            	return HttpResponse('<h1>123</h1>')
        (2) render:
            	App下创建一个templates，templates中存放网页文件
                render返回的也是一个HttpResponse类型
                格式:render(request,'页面文件')
                    当templates文件在app中，使用render返回页面文件时
                    需要在主项目文件下的settings中的INSTALLED_APPS中注册App
                    注册方式：
                    	INSTALLED_APPS==>'App'
                      或INSTALLED_APPS==>'App.apps.AppConfig'  有版本限制，在1.9之后才能使用
模板配置两种情况:
    1. 在App中的templates文件
    	需要在主项目文件夹下的settings文件中的INSTALLED_APPS下注册App
    2. 在项目文件夹下的templates文件
    	需要在主项目文件夹下的settings文件中的TEMPLATES中的DIRS添加templates路径
        路径为:
            os.path.join(BASE_DIR,'templates')
            
    开发中通常会将templates放在项目文件夹下，以为模板可以继承和复用
```

Django工作机制

```python
	1. 用python manage.py runserver启动服务器时就载入了在同一目录下的settings.py，该文件包含了项目的配置信息，其中最重要的就是ROOT_URLCONF，它告诉Django哪个python模块应该用作本站的URLConf，默认是urls.py
	2. 当访问url时，Django会根据ROOT_URLCONF的设置来装载URLConf
    3. 之后按顺序逐个匹配URLConf里的URLpatterns，如果找到就会调用相关联的视图函数，并把HttpRequest对象作为第一个参数，通常是request
    4。 最后视图函数返回一个HttpResponse对象
```

### 模板显示

```python
显示在模板中
	需现在网页中挖坑
    {{ var }}
    填坑：
    	通过字典来实现传递
        def test(request):
            context = {
                'name': 'zs',
                'age': 18
            }
            return render(request, 'test.html', context=context)
        模板的兼容性很强
        	不传入不会报错，传入数据过多会自动过滤
            在传入浏览器时，会调用html的解析器进行转换，将模板语言转换成html
            
        循环语句：
        	{% for i in range(5) %}
            	{{ i }}
            {% endfor %}
        选择语句:
            {% if 条件 %}
            	语句
            {% elif %}
            	语句
            {% else %}
            	语句
            {% endif %}
            
render底层实现,主要用在发送邮件，邮件的内容需要使用render方法来操控
	加载
    	index = loader.get_template('index.html')
        context = {
            'name':'zs'
        }
    渲染
    	result = index.render(context=context)
        return HttpResponse(result)
```

### 修改数据库

```python
首先在settings中DATABASES中进行设置
	'ENGINE':'django.db.backends.mysql'
    'NAME':'djangoday01'    数据库名字
    'USER':'z'              数据库用户名
    'PASSWORD':'123321'     数据库密码
    'HOST':'localhost'      主机号
    'PORT':3306             端口号，加不加”都可以
        
迁移驱动问题:
    1. mysqlclient:python2,3都可直接使用,但对mysql安装有要求，必须指定位置存在配置文件
    2. mysql-python:python2支持，python3不支持
    3. pymysql:会伪装成mysqlclient和mysql-python,python2,3都支持
        需要在主项目下的__init__文件中配置
        	import pymysql
            pymysql.install_as_mysqldb()
```

### DML

```python
数据操作
	1. 迁移
    	生成迁移:python manage.py makemigrations
        执行迁移:python manage.py migrate
    2. ORM
    	object relational mapping  对象关系映射
        将业务逻辑和sql进行一个解耦合
        通过models定义实现，数据库表的定义
    3. 模型定义
    	(1) 继承models.Model
        (2) 会自动添加主键列
        (3) 必须指定字符串类型属性的长度
        	class Animals(models.Model):
                name = models.CharField(max_length=32)
                age = models.IntergerField()
                
    添加数据:
        animal = Animal()
        animal.name='hen'
        animal.age = '1'
        animal.save()
    数据查询:
        Animal.objects.all()      查询所有
        Animal.objects.get(pk=2)  查询主键值为2的数据
    修改数据:
        基于查询
        animal = Animal.objects.get(pk=2)
        animal.name = 'chicken'
        animal.save()
    删除:
        基于查询
        animal = Animal.objects.get(pk=2)
        animal.delete()
```

### Django Shell

```python
使用：django终端，python manage.py shell
集成了django环境的python终端，可在里面调试程序
```

### 数据级联

```python
一对多模型:通过一个学生可以获取一个英语成绩，英语成绩对应多个学生
    class Score(models.Model):
        english = model.IntergerField()
        
    class Student(models.Model):
        name = models.CharField(max_length=32)
        eng = models.ForeignKey(Score)
主查从(一方获取多方)：
	score = Score.objects.get(pk=1)
    students = score.student_set.all()
    for student in students:
        print(student.name)
    return HttpResponse('查询成功')
从查主(多方获取一方):
    student = Student.objects.get(pk=1)
    score = Student.eng
    return HttpResponsse(score.english)
```

### 元信息

```python
指定表名和字段名
class meta:
    db_table = '名字'
    
字段名一般为下划线命名方式
表名一般为驼峰式
```

### 定义字段

```python
字段类型:
    CharField:字符型
    TextField:文本类型，一般4000字节以上使用
    IntegerField:整型类型
    FloatField:浮点型
    BooleanField:布尔类型，true和false
    DecimalField:十进制浮点型
        有两个参数:
            DecimalField.max_digits-----位数总数
			DecimalField.decimal_places-小数点后的数字位数
    NullBooleanrField:有三个值，分别为true，null，false
    AutoField:根据实际ID自动增长的IntergerField
    FileField:一个上传文件的字段
    ImageField:继承了filefield的所有属性和方法，但上传的必须是图片

字符约束:
    max_length:最长长度
    default:默认值
    unique:不允许重复
    index:创建索引
    primary_key:创建主键
    db_column:字段名称，若未指定，则使用属性的名称
```

### 模型过滤

```python
模型过滤即数据查询
django默认通过模型的objects对象实现模型数据查询
django默认有两种过滤器来进行查询:
    filter:返回符合条件的数据
    exclude:返回不符合条件的数据
链式调用:
    filter和exclude可以连续调用来达成链式调用
    students = Student.object.filter().exclude().filter()
```

### 创建对象的方式

```python
1. 调用后通过属性赋值
	person = Person()
	person.name = 'zs'
    person.save()
2. 直接实例化对象，传入属性创建
	person = Person(name='zs')
    person.save()
3. 使用model.objects.create创建
	person = Model.objects.create(name='zs')
4. 在模型类中创建类方法建立对象
	@classmethod
    def create(cls,name):
        return cls(naem = name)
    person = Person.create('zs')
```

### 查询集

```python
查询集表示从数据库获取的对象集合，查询集可以有多个过滤器
```

```python
过滤器:
    过滤器是一个函数，通过条件查询的结果集为过滤后的数据，条件查询的方法就叫过滤器
    查询经过过滤器筛选后还是新的查询集，查询集还可以继续过滤查询
    查询集:QuerySet
        all:查询所有
            模型.objects.all()
        filter:条件查询
            模型.objects.filter()
        exclude:查询不符合条件的结果
            模型.objects.exclude()
        order_by:排序，默认升序
            模型.objects.order_by('id')    升序
            模型.objects.order_by('-id')   降序
        values:返回为字典类型
            persons = Person.objects.order_by('id')
            persons.values()
        切片:
            限制查询集，用下标的方法进行限制
            	左闭右开区间
            	不支持负数
                相当于limit  offset
              	persons = Student.objects.all()[0:5]
                
懒查询/缓存集:
    懒查询:只有当我们需要迭代结果时，或调用属性时，系统才会真正的去查询数据
          优化了我们结果和查询
    缓存集:每个查询集都包含了一个缓存，能最小化对数据的访问
          在新建的查询集中，缓存首次为空，第一次对查询集求值，会产生数据缓存，django会将查询的数据放到缓存中，并返回查询结果，以后的查询都会先到缓存集中调用
            不会真正的去数据库中调用，优化了程序的执行速度
```

```python
获取单个对象:
    get:
        若获取的结果不存在，则会报异常   DoesNotExist
        若获取的结果有多个，也会报异常   MultipleObjectsReturned
        当使用get获取时，需要捕获异常来确保项目的完整性
    last:
        返回查询集中的最后一个对象
    first:
        获取查询集中的第一个对象
内置函数:
    count:
        返回当前查询集中的对象个数
    exists:
        判断当前查询集中是否有数据，有则返回true，没有放回false
```

```python
字段查询:
    对sql原生语句中where的实现
    作为filter，exclude，get的参数
    语法:属性名称__比较运算符=值
        Person.objects.filter(age__gt=18)
    条件
    	属性__操作符=临界
        常用
            gt:大于
            gte:大于等于
            lt:小于
            lte:小于等于
            in:包含
                
            exact:判断，大小写不敏感
            startswith:是否以xx开头
            endswith:是否以xx结尾
            contains:是否包含,大小写不敏感
            isnull,isnotnull:是否为空，是否不为空
            ignore:忽略大小写
```

```python
时间:
    models.DateTimeField(auto_now_add=True)   第一次注册的时间
    models.DateTimeField(auto_now=True)       最后一次修改时间
    注意:当获取month信息时，会出现时区问题，需要在主项目文件夹下的settings中的USE_TZ修改为flase
    获取单个时间值:
        order = Order.objects.filter(time__year=2019)
        order = Order.objects.filter(time__month=2)
```

```python
聚合函数(主函数、多行函数):
    AVG:平均数
    Count:计数
    Max:最大值
    Min:最小值
    Sum:求和
   	person = Person.objects.aggregate(Max('age'))
```

```python
跨关系查询:
    模型:
        class Grade(models.Model):
            g_name = models.CharField(max_length=32)
        class Student(models.Model):
            s_name = models.CharField(max_length=32)
            s_grade = models.ForeignKey(Grade)
    使用:
        主查从:
            隐性属性:
                grade = Grade.objects.filter(pk=1)[0]
                students = grade.student_set.all()
                for student in students:
                    print(student.s_name)
            跨关系:
                students = Student.object.filter(s_grade__g_name='001')
        从查主:
            显性属性:
                student = Student.objects.filter(pk=1)[0]
                grade = student.g_grade
                print(grade)
            跨关系:
                grade = Grade.object.filter(student__s_name='zs')[0]
                print(grade.g_name)
```

```python
F对象:常适用于表内属性的值的比较
    计算男生数比女生数多的教室
    classroom = Classroom.objects.filter(boy_num__gt=F(girl_num))
    计算女生数比男生数多加10人还要多
    classroom = Classroom.objects.filter(boy_num__lt=F(girl_num)-15)
```

```python
Q对象:长适用于逻辑运算，与或非
    与:&   或:|   非:~
      计算女生人数小于15并且男生人数大于10的教室
    	classroom = Classroom.objects.filter(Q(bot_num__gt=10)&Q(girl_num__lt=15))
      计算女生人数不小于10的教室
    	classroom = Classroom.objects.filter(~Q(girl_num__lt=10)
```

### Template概念

```python
模板:
    在django项目开发中，模板有助于快速开发，能有快速的呈现给用户
    模板的设计方式实现了MVT中VT的解耦，VT有种多对多哦的关系
    模板处理过程中分为两个步骤:
        加载
        渲染
    模板除了可以静态填充，还可以动态呈现数据
    Django使用的是django模板，flask使用的是jinja2模板
```

### 模板语法

```python
变量:
    视图函数通过context传递一个字典到模板中，模板通过{{ 字典的key值 }}接收
    遵守标识符规则
    若变量不存在，则插入空值
```

```python
点语法:
    视图函数可以在context中存放一个key对应一个对象，在模板中可以通过{{ key.对象属性 }}
    	或{{ key.对象方法 }}来调用对象中的属性或方法
        但调用对象方法时不能够传递参数，因为jango模板不支持()
        
    索引:jango中的点语法还支持下标形式，通过{{ key.下标值 }}来调用列表或集合中该下标的值
        
    字典:还可以在传入的字典中再添加一个key对应一个字典，之后在模板中通过
        	{{ context中的key.对应字典的key }}来调用对应字典中值
```

```python
标签:
    标签分为单标签和双标签，双标签为成对出现
    
    功能标签:
        循环语句:
            {% for i in rang(5) %}
            	语句1
                {% empty %}-----起判断作用，若语句1不显示数据，则执行语句2
                语句2
            {% endfor %}
            
            forloop--循环状态记录:
                {{ forloop.counter }}:从1开始计数，表示当前是第几次循环
                {{ forloop.counter0 }}:从0计数，表示当前是第几次循环
                {{ forloop.revcounter }}:forloop.counter的倒序
                {{ forloop.revcounter0 }}:forloop.counter0的倒序
                {{ forloop.first }}:第一次循环
                {{ forloop.last }}:最后一次循环
                    
        选择语句:
            {% if 条件 %}
            	语句
            {% elif %}
            	语句
            {% else %}
            	语句
            {% endif %}
         
       	注释:
            单行注释:
                {#   注释   #}
            多行注释:
                {% comment %}
                    注释
                {% endcomment %}
                    
        withratio--乘:
            {% widthratio 数 分母 分子 %}
                    
        整除:
            {% if num|divisibleby:2 %}  ---num/2  整除
                    
        ifequal:
            {% ifequal value value2 %}
                    语句
            {% endifequal %}
            相当于
            {% if value==value2 %}
                    语句
            {% endif %}
```

```python
过滤器--|:
    将前面的输入作为后面的输出
    add:
        {{ count|add 2 }}   ---count+2
        {{ count|add -1 }}  ---count-2
    upper:全大写
    lower:全小写
    safe:确认安全，可执行html语句进行渲染
    endautoescape:             ------当选择off开关时，和safe效果一致 
        {% autoescape off %}   ------on:语句原样输出，不进行渲染；off:信任语句，进行渲染
        	语句
        {% endautoescape %}
```

```python
结构标签:
    block----填充块
    	当一个页面已经对父页面进行了块填充，若再有一个页面对该页面进行块填充，默认是会覆盖之前填充的块，若不想进行覆盖，则需要在块中的加入  {{ block.super }}
        
    extends---继承
    	子页面可以继承父页面，对父页面中的块进行填充，提高了模块的复用率
        {% extends '页面' %}
        
    include---包含
    	若父模块想调用另一个子模块进行快填充，则可以调用 {% include '页面' %}
```

```python
加载静态资源:
    静态资源包括html,css,js,img,font
    
    在加载静态资源之前，需要在主项目文件下的settings中配置static的路径
    	STATICFILES_DIRS=[
            os.path.join(BASE_DIR,'static')
        ]
    
    静态资源路径:/static/css/xxx.css  --------硬编码形式，当文件夹路径改变，需更改
        
    动态资源路径:
        {% load static %}            ----在html文件开头先读取static文件夹的路径
        {% static 'css/xx.css' %}    ----动态添加css样式，当文件有位置改动时，只需在settings中修改路径，不需要到模板中修改 
     仅在模板中可继续{% load static %}操作，并且DEBUG模式必须为TRUE，若DEBUG=False则不会加载
```

### 常见请求状态码

```python
200 成功
301 永久重定向
302 重定向
403 防跨站攻击
404 路径错误
405 请求方式错误
500 业务逻辑错误
```

### view视图函数

##### 基本用法

```python
概念及基础用法:
    概念:
        MTV中的V(视图函数)，相当于MVC中的C，控制器接收用户的输入输出请求，协调模板模型，对数据进行处理，负责的模型和模板的数据进行交互
    视图类型返回值:
        1. json数据返回
        		前后端分离
            	return JsonResponse
        2. 以网页形式返回
        		HttpResponse   -直接返回字符串或标签
            	render		   -返回页面
                redirect	   -重定向
```

```python
url正则匹配规则:
    url的正则匹配是从上至下进行匹配，若匹配到了就不会向下匹配
    匹配的正则前面不需要加'\'
    
    正则前需要加r表示原样输出，不进行转义
    
    若url中的路由最后加了'/',表示精准匹配
    若url中的路由最后没有加'/'，就是模糊匹配，会按照正则的路由匹配规则进行匹配
```

```python
url接收参数:
    获取值的数量需和视图函数中接收的数量一致，除去request
    
    位置参数:会按照视图函数变量接收的顺序一一赋值
        url获取一个值:
            url(r'^index/(\d+)/',views.index)
            表示从路由中获取一个参数，在index视图函数中就必须给定一个变量来接收这个值
            index(request,num):
                pass
        若需要或许多个值，则需要使用多个()来进行获取,同样的，视图函数中也需要多个变量来进行接收
            url(r'^index/(\d+)/(\d+)/(\d+)',views.index)
            index(request,num1,num2,num3):
                pass
        url获取的值也可以设置长度:(\d{3})----设置长度为3
            
    关键字参数:根据(?<变量名>\d+)中的变量名找寻视图函数中接收变量的名字来进行赋值
    	url(r'^index/(?P<num1>\d+)/(?P<num2>\d+)/(?P<num3>\d+)',views.index)
        index(request,num1,num2,num3):
                pass
```

##### 内置函数

```python
locals():
    将视图函数中的局部变量用字典的形式进行打包
    key为变量名，value为值
    eg:
        index(request):
            num = 1
            num1 = 2
         	return render(request,'index.html',context=local())
        
       	返回的形式:{
            'num':1,
            'num1':2,
        }
```

##### 反向解析

```python
用处:获取请求的资源路径，避免硬编码，可以提高代码的扩展性和可维护性

配置:
    1. 根目录urls中:
        include中添加参数namespace
        url(r'^vie/',include('viewApp.urls',namespace='vie'))
    2. 子urls中:
        添加参数name
        url(r'^index/',views.index,name='index')
    3. 在模板中使用:
        <a href="{% url 'vie:index' %}">index</a>
        若存在位置参数:
            <a href="{% url 'vie:index' num1 num2 %}">index</a>
        若存在关键字参数:
            <a href="{% url 'vie:index' num1=num1 num2=num2 %}">index</a>
```

