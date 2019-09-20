# 数据库

### 层次模型 

优点: 

​	查询分类的效率⽐较⾼

缺点: 

​	没有导航结构，导致分类困难，数据不完整 

### 网状模型 

​	没有解决导航问题, 解决了数据完整性问题。 

### 关系模型 

现在的大多数数据库都为关系模型 

特点: 

​	每张表都是独⽴的, 没有导航结构 

​	表于表之间会建⽴公共字段, 也就将两张表之间建⽴了关系 

关系型数据库解决了数据的完整性, 也解决导航问题, 但是带来的是低效率. 

NOSQL(⾮关系型数据库): MongoDB, Redis 

### 列、行、字段的属性 

​	⼀行就是一条数据，⼀列就是⼀个字段, 也是表的⼀个属性 

​	字段的属性: 描述该列的功能

​	数据的冗余: 尽量避免相同数据的多次存储

### Linux数据库的开启和连接 

##### 开启数据库服务 

​	Ubuntu : service mysql start|stop|restart|reload|status 

​	Deepin : systemctl stop|start mysqld 

​	CentOS7 : systemctl stop|start mysqld 

​	CentOS6 : service mysqld start|stop|restart|reload|status 

##### 连接数据库 

​	语法: mysql -hloaclhost -uroot -p123456 -P9876 

​	-h : host(ip地址) localhost = 127.0.0.1 

​	-u : username(⽤户账户) 

​	-p : password(密码) 

​	-P : port(端⼝, 默认端⼝3306) 

##### 退出数据库 

​	exit 

​	quit 

​	\q 

​	ctrl + d 

### SQL语⾔

SQL 是⼀种特殊⽬的的编程语⾔，是⼀种数据库查询和程序设计语⾔，⽤于存取数据以及查询、更新和 

管理关系数据库系统；同时也是数据库脚本⽂件的扩展名。 

# 数据库的操作 

### 创建数据库 

create database if not exists \`数据库名` charset=字符编码(utf8mb4); 

注意：

​	数据库不允许创建相同名称的两个库，字符编码也不会默认指定utf8，

​	若想要用关键字作为库名，但又会报错，这时在库名左右加上``可有效避免冲突

### 查看数据库 

​	show databases;

### 选择数据库 

​	use  \`数据库名\`;

### 创建数据库 

​	create database  \`数据库名`;

###  修改数据库 

​	alter database \`数据库名` charset=字符集;

​	可给数据库添加默认编码

###  删除数据库 

​	drop  database   \`数据库名`;

# 表的操作 

表是数据库中真正存放数据的位置

在对表进行增删改时必须要先选择对应的库

### 表的创建 

create table [if not exists] \`表的名字`( 

 		id int  auto_increment primary key not null, 

 		account char(255)  , 

 		pwd varchar(65535) not null 

) engine=myisam charset=utf8mb4; 

charset若不指定，则默认使用库编码

engine若不指定，则默认使用innodb

### 查看所有的表 

​	必须先选择库

​	show tables; 

### 删除表 

​	drop table [if exists] `表名` 

### 显示建表结构 

​	desc(describe) \`表名`; 

### 修改表 

修改表的名称 

​		alter table \`原名\` rename \`修改的名字`; 

增加⼀个新的字段 

​		alter table \`表名\` add \`字段` 数据类型 属性; 

将某个字段添加在第⼀个位置

​		alter table \`表名\` add \`字段` 数据类型 属性 first; 

添加在某⼀个字段之后 

​		alter table \`表名\` add \`字段` 数据类型 属性 after 指定字段; 

修改字段的属性 

​		alter table \`表名\` modify \`字段名` 数据类型 属性; 

修改字段的名称 

​		alter table \`表名\` change \`原字段名\` \`新的字段名` 数据类型 属性; 

修改字段的位置 

​		alter table \`表名\` change \`原字段名\` \`新的字段名\` 数据类型 after \`指定字段`; 

修改表的引擎 

​		alter table \`表名` engine = innodb|myisam; 

移动表 到指定的数据库 

​		alter table \`表名` rename to 数据库名.表名; 

### 复制表 

把数据给复制过来了, 但是没有复制主键 ：

​		create table 表名 select * from 要被复制的表名 ; 

复制所有表结构, 但是不复制数据 ：

​		create table 表名 like 要被复制的表名 ; 

# CURD语句的基本使用

C:创建(create)    	U:更新(update)		R:读取(retrieve)		D:删除(delete)

### insert 插入

完整语句：insert into \`表名\`  (\`字段\`) values (\`值\`);

一次插入一行：insert into \`表名\` set  字段1=值，字段2=值;

按指定字段，一次插入多行：insert into \`表名\`  (\`字段\`)   values (\`值\`)  ,  (\`值\`);

指定全部字段，一次插入多行：insert into \`表名\`   values (\`值\`)  ,  (\`值\`);

### select 查询

通过*获取全部数据：select * from 表名;

通过指定字段获取数据：select  字段 from 表名;

通过指定字段加上条件查询：select 字段  from  表名 where  条件;

### update 更新

修改全表数据：update  表名  字段1=值，字段2=值;

使用条件判断修改数据：update  表名  字段1=值，字段2=值  where 条件;

### delete 删除

删除表中所有数据(逐行删除)：delete from 表名;

清空全表(一次性清空)：truncate 表名;

条件删除：delete  from  表名 where  条件;

# MySQL中的编码与数据类型

### 字符集

字符集在数据传输和保存数据的时候需要使用。

##### 常见字符集

ASCII：8位存储，最高位始终为0

LATIN1：在ASCII上做了扩展，启用了最高位，扩展了字符集的范围

GB2312：简体中文，一个字符占用两个字节

GBK：所有的中文字符，包括繁体，一个字符占用两个字节,最大字符串长度:65535/2-1

UTF8：国际通用编码，一个字符占用三个字节,最大字符串长度:65535/3-1

UTF8MB4：国际通用编码，一个字符占用四个字节,最大字符串长度:65535/4-1

##### 查看mysql系统支持的字符集

show  variables like  'character_%';

##### 修改当前的mysql系统的字符集编码

全部修改：set names gbk;

指定修改：set character_get_results = gbk;

修改的字符集只对当前操作有效，当重启数据库之后会重新回到默认状态

### 校对集

_ci:大小写不敏感

_cs:大小写敏感

_bin:采用二进制，大小写敏感

# mysql 的数据类型

### 整型

类型：tinyint   字节数：1   最小值：有符号(-128)，无符号(0)    最大值：有符号(127)，无符号(255)

类型：smallint 字节数：2 最小值：有符号(-32768)，无符号(0)最大值：有符号(32767)，无符号(65535)

类型：mediumint    字节数：3   

类型：int、integer   字节数：4   

类型：bigint              字节数：5   

##### 无符号类型

unsigned   ：无符号一定为非负数

##### 固定宽度

zerofill：类型定义时会固定宽度，zerofill将不足的部分用0补齐

### 浮点型

浮点数类型

类型：float      字节数：4

类型：double  字节数：8

定点数类型

类型：dec(m,d)、decimal(m,d)     字节数：m+2      有效取值由m和d决定

位类型

类型：bit(m)     字节数：1~8    最小数：bit(1)   最大数：bit(64)



定点数的使用方法：

m为支持的总长度，d为小数点后的位数，浮点型也可通过定长来固定长度

​			   float(m,d)

​				double(m,d)

​				decimal(m,d)

### 字符串类型

类型：char    				 字节数：M     M为0~255之间的整数

类型：varchar(M)          M为0~65535之间的整数，值的长度+1个字节

类型：tinyblob              允许长度0~255个字节，值的长度+1个字节

类型：blob                     允许长度0~65535个字节，值的长度+2个字节

类型：mediumblob      允许长度0~167772150个字节，值的长度+3个字节

类型：longblob             允许长度0~4294967295个字节，值的长度+4个字节

类型：tinytext               允许长度0~255个字节，值的长度+2个字节

类型：text                      允许长度0~65535个字节，值的长度+2个字节

类型：mediumtext       允许长度0~167772150个字节，值的长度+3个字节

类型：longtext              允许长度0~429497595个字节，值的长度+4个字节

类型：varbinary(M)      允许长度0~M个字节的变长字节字符串，值的长度+1个字节

类型：binary(M)            字节数：M   允许长度0~M个字节的定长字节字符串

##### char和varchar的区别

char：若固定字长大于输入的字符长度，则补空格，若小于输入的字符长度，则截掉超出的字符，再抛错

varchar：若固定字长大于输入的字符长度，留一位记录字长，不会额外补空格，若小于输入的字符长度，则截掉超出的字符，再抛错

### 枚举(enum)

格式：enum(‘选项‘)

优点：限制了可选值，节省空间，运行效率高

### 集合(set)

集合和枚举差不多，枚举相当于单选，而集合就相当于复选

set中最多可以有64个不同的成员。

### 时间类型

类型：date            字节数：4     最小值：1000-1-1                  最大值：9999-12-31

类型：datetime    字节数：8     最小值：1000-1-1  0:0:0        最大值：9999-12-31    23:59:59

类型：timestamp 字节数：4     最小值：19700101080001   最大值：2038的某个时刻

类型：time            字节数：3     最小值：-838:59:59               最大值：838:59:59

类型：year             字节数：1     最小值：1901                        最大值：2155

### 布尔值

bool类型：false(0)、true(1)

# 类的属性

### 插入值是否为空

null：可以为空

not null：不可为空

### 默认值

default  ’值‘

### 自动增长

auto_increment

自动增加的列，默认从1开始，常配合主键使用

### 主键

primary   key

主键不能为空，也不能重复，一张表中只能有一个主键

### 无重复

unique：唯一值，保证列当中的数据都不重复

### 备注

comment：字段说明，用来提示开发者相关的字段

# 注释

单行注释：--

多行注释：/*    */

----mysql独有：#

# 运算符

### 比较运算符

<>:不等于

between:存在于指定范围

in:存在于指定集合

is null:为null

is not null:不为null

like:通配符匹配，mysql中通配符为%

regexp/rlike：正则匹配

### 逻辑运算符

not/！：非

and/&&：与

or/||：或

xor：异或

# 数据库的查询

### select字段表达式

select即可以作查询，也可以作输出，可直接输出表达式的返回值

### from子句

语法：select 字段 from 表名

from后面跟着数据源，数据源可以写多个，也可以写查询出的结果

### where 子句

按指定条件过滤

语法：select  字段  from  表名  where   条件

where作条件查询，只返回结果为true的数据

##### 空值判断 

select  字段  from  表名  where   值 is null;

select  字段  from  表名  where    值 is not null;

##### 范围判断

select  字段  from  表名  where   值   between   值   and  值;

select  字段  from  表名  where   值   not   between   值   and  值;

### 分组查询group  by

按某一字段进行分组，将该字段相同内容的分为一组，分类统计为结果

如果有where的话要放在where后面

语法：select  字段  from  表名  where   条件    group  by   分组字段;

### having子句

having子句和where子句有很大的相似，但where子句后面不能跟聚合函数，而having后面可以跟聚合函数。

语法：select  字段  from  表名 having   条件;

having可以写在group  by的后面

### 字段排序order by 

order  by 的主要作用是排序，通常写在最后

语法：select  字段  from  表名  where   条件   order by  字段;

参数：

​			asc：降序，默认的，可不写

​			desc：升序

### 限制取出数量limit

语法：

​		select  字段  from  表名  limit  m;       从第1行开始取m行

​		select  字段  from  表名  limit  m，n;          从第m行开始取n行

​		select  字段  from  表名  limit  m   offset   n;    跳过前n行取m行数据

### 去重distinct

语法：select   distinct   字段   from    表名;

### dual 表

dual表是一个虚拟表，只是为了保证语句的完整性

语法：select   now()   from  dual;

# 函数

### 聚合函数

AVG()：							返回参数的平均值 

BIT_AND()： 				  按位返回AND 

BIT_OR()：                      按位返回OR 

BIT_XOR()：                    按位返回异或 

COUNT()：                      返回返回的⾏数 

COUNT(DISTINCT) ：    返回许多不同值的计数 

GROUP_CONCAT()：     返回连接的字符串 

JSON_ARRAYAGG()：     将结果集作为单个JSON数组返回 

JSON_OBJECTAGG()：    将结果集作为单个JSON对象返回 

MAX()：                           返回最⼤值 

MIN()：                            返回最⼩值 

STD()：                            返回样本的标准差 

STDDEV()：                     返回样本的标准差 

STDDEV_POP() ：           返回样本的标准差 

STDDEV_SAMP() ：        返回样本标准差 

SUM()：                           归还总和 

VAR_POP()：                   返回样本的标准差异 

VAR_SAMP()：                返回样本⽅差 

VARIANCE()：                 返回样本的标准差异

### 数值计算类函数

ABS(x)：               返回x的绝对值
CEIL(x)：              返回大于x的最大整数值
FLOOR(x)：         返回小于x的最大整数值
MOD(x，v)：      返回x/y的模
RAND()：             返回0到1内的随机值
ROUND(x.y)：     返回参数x的四舍五入的有y位小数的值
TRUNCATE(x,y)：返回数字x截断为y位小数的结果

### 日期计算类函数

CURDATE()：                                            返回当前日期
CURTIME()：                                             返回当前时间
NOW()：                                                    返回当前的8期和时间
UNIx_ TIMEST AMP(date)：                    返回日期date的UNIX时间截
FROM_ UNIXTIME：                                 返回UNIX时间截的日期值
WEEK(date)：                                           返回日期date为一年中的第几周
YEAR(date)：                                             返回日期date的年份
HOUR(time)：                                           返回time的小时值
MINUTE(time)：                                        返回time的分钟值
MONTHNAME(date)：                             返回date的月份名:
DATE_ FORMAT(date,fmt)：                    返回按字符串fmt格式化日期date值
DATE ADD(date,INTERVAL expr type)：返回一个日期或时间值加上一个时间间隔的时间值
DATEDIFF(expr,expr2)：                          返回起始时间expr和结束时间expr2之间的天数

### 字符串相关函数

CANCAT(2,2..n)：				连接51,52... Sn为一个字符串
INSERT(str,x,y,instr)：		将字符串str从第x位置开始，y个字符长的子串替换为字符串instr
LOWER(str)：					   将字符串str中所有字符变为小写
UPPER(str)：						将字符串str中所有字符变为大写
LEFT(str ,x)：						返回字符串str最左边的x个字符
RIGHT(str,x)：					  返回字符串str最右边的x个字符
LPAD(str,n ,pad)：			   用字符串pad对str 最左边进行填充，直到长度为n个字符长度
RPAD(str,n,pad)：			    用字符串pad对str最右边进行填充，直到长度为n个字符长度
LTRIM(str)：						  去掉字符串str左侧的空格
RTRIM(str)：						 去掉字符串str行尾的空格
REPEAT(str,x)：					返回str重复x次的结果
REPLACE(str,a,b)：			  用字符串b替换字符串str中所有出现的字符串a
STRCMP(s1,s2)：				 比较字符串s1和s2
TRIM(str)：						   去掉字符串行尾和行头的空格
SUBSTRING(str.x.,y)：		返回从字符串strx位置起y个字符长度的字串

### 其他函数

DATABASE()：			  返回当前数据库名
VERSION)：			     返回当前数据库版本
USER()：					  返回当前登录用户名
INET_ ATON(IP)：       返回IP地址的数字表示
INET_ NTOA(num)：  返回数字代表的IP地址
PASSWORD(str)：	   返回字符串str 的加密版本
MD5()：						返回字符串str 的MD5值

# 多表查询

### union联合查询

union用于合并两个或多个select语句的结果集

要求：两边select与的字段数必须一样，两边可以具有不同数据类型的字段

​			字段名默认按照左边的表来设置

用法：

​			select   字段   from    表1

​			union

​			select   字段   from    表2;

### 内连接inner join

使用inner  join时必须确保两个表中必须要有交集 

语法：

​			select   字段   from    表1   inner   join   表2   on   表1.字段=表2.字段;

或：

​			select   字段   from    表1   join   表2   on   表1.字段=表2.字段;

### 左连接left  join

left  join关键字从左表返回所有行，即使右表没有数据，也只是返回null

语法：

​			select   字段   from    表1   left   join   表2   on   表1.字段=表2.字段;

或：

​			select   字段   from    表1   left outer  join   表2   on   表1.字段=表2.字段;

### 右连接 right  join

right  join关键字从右表返回所有行，即使左表没有数据，也只是返回null

语法：

​			select   字段   from    表1   right   join   表2   on   表1.字段=表2.字段;

或：

​			select   字段   from    表1   right outer  join   表2   on   表1.字段=表2.字段;

### 子查询

查询语句中可以嵌套一个查询

语法：

语法：

​			select   字段   from    表1   where     值  in(select   值   from   表2);

# 数据库高级特性

### 权限管理

数据库的权限分为两个阶段：

1. 连接管理，限制用户连接mysql-server时使用的ip及密码

2. 操作检查，检查用户执行的指令是否被允许

##### 权限控制安全准则

1. 只授予能满足的最小权限

2. 限制用户登录的主机，防止外人登录

3. 禁止或删除没有密码的用户

4. 禁止用户使用弱密码

5. 定期清理无效的用户

##### 常用操作

1. 创建账户，授予权限

    8.0之前的版本：

   ​		crant  all   privileges on  \*.*   to  \`用户名\`  @  \`主机`  identified  by  "密码"  with  grant  option;

   ​		flush   privileges;         -----刷新使权限生效

   ​		all   privileges：授予全部权限，也可指定特定的权限

   ​		\*.*：允许操作的数据库和表

   ​		with  grant  privileges：允许该用户将自己拥有的权限授予别人

   8.0之后的版本：

   ​		create  user   \`用户名\`@\`主机名\`   identified  by  '密码';    ----创建账户

   ​		grant  all  on  \*.\*   to  \`用户名\`@\`主机名\`   with   grant  option;   ----授权

2. 修改密码

   alter   user  \`user\`@\`localhost\`  identified   with  mysql_native_password  by   "密码";

3. 查看权限

   show   grants;          ----查看当前用户的权限

   show   grants   for   \`用户名\`@\`主机\`;         -----查看用户的权限

4. 回收权限

   revoke   delete  on    \*.\*    from   \`用户名\`@\`主机\`

5. 删除用户

   use  mysql;

   select  host,user  from  user;

   drop  user  用户名@'%';

### 视图

视图是数据的特定子集，是从其他表里提取出的虚拟表

若其他表有修改，则视图中也会有所修改

视图操作只限查找，无法进行增删改

一般视图都是以v_为前缀，用来与正常表区分开

##### 创建视图

语法：create  view   视图名   as   查询语句

### 存储引擎

存储引擎就是如何存储数据，如何为数据建立索引和如何更新、查询数据等技术的实现方法。

#####  查看当前引擎

show  variables   like  ’￥storage_engine';

show  engines;

##### mysql 中常用的存储引擎

功能                  MYISAM          Memory            InnoDB           Archive
存储限制            256TB             RAM                   64TB                None
支持事务              No                   No                      Yes                    No
支持全文索引      Yes                   No                       No                    No
支持数索引          Yes                  Yes                       Yes                   No
支持哈希索引       No                  Yes                       No                    No
支持数据缓存       No                  N/A                      Yes                    No
支持外键               No                    No                     Yes                    No

通常数据库的存储引擎都是使用innodb

当存储数据过大时，会采用myisam

当需要存储一些虚拟表时，则会采用memory

##### 使用引擎

create   table   abc(

​		name   char(10)

)charset=utf8  engine=innodb;

### 索引

索引就是为特定的mysql字段进行一些特定的算法排序，索引可以大大的提高mysql的检索能力

![1567684713411](C:\Users\Ce\AppData\Roaming\Typora\typora-user-images\1567684713411.png)

mysql默认的索引数据结构为b tree

但使用索引时，索引也会占用一定的存储空间，而且会让写的操作变慢

#### 索引创建原则

1. 适合用于频繁查找的列
2. 适合经常用于条件判断的列
3. 适合经常用于排序的列
4. 不适合数据不多的列
5. 不适合很少查询的列

#### 创建索引

1. 建表时添加索引

   create  table  表(

   ​		id int not null,

   ​		username  varchar(20)  not  null,

   ​		index  索引名  (字段名(长度))

   )

2. 建表后添加索引

   create  index  \`索引名\`  on   表名(字段名(长度));

#### 删除索引

drop   index   \`索引名\`  on   表;

#### 唯一索引

1. 建表时添加唯一索引

   create  table  表(

   ​		id int not null,

   ​		username  varchar(20)  not  null,

   ​		unique  索引名  (字段名(长度))

   )

2. 建表后添加唯一索引

   create  unique  index  \`索引名\`  on   表名(字段名(长度));

#### 查看索引

show   index  from  表;

### 关系和外键

##### 关系

1. 一对一

   两张表中只有唯一的值相对应

2. 一对多

   A表中的一条数据可对应B表中的多条数据，但B表只能对应A表的一条数据

3. 多对多

   A表中的一条数据可对应B表中的多条数据，B表中的一条数据也可对应A表中的多条数据

##### 外键

外键是一种约束，他只是保证数据的一致性，对于系统性能而已并不能带来好处

###### 添加外键

为user和userinfo 建立关联的外键
				alter table userinfo add constraint fk_user_id foreign key(id) references  user(id);
建立用户与组的外键约束
				alter table user~ add gid int unsigned;
				alter table ~user~ add constraint 、fk_ group_ id~ foreign key(gid~ )  references group( id );
建立用户、商品、订单的外键约束
				alter table 、order~ add constraint 、fk_ user_ id foreign key(~uid~ )
				references user~( id~);
				alter table 、order~ add constraint、 fk_ prod_ id foreign key(~pid~ )
				references ~product~ ( id );

在对外键数据进行删除时，必须要先对子表数据进行删除，才能删除主表数据。

# 数据库事务及其他

### 事务

事务主要用于处理操作量大、复杂度高、并且关联性强的数据

事务就是完整的一套处理体系

##### 事务四大特性

1. 原子性

   事务只有全部完成和全部不完成两种状态，若执行过程中发生错误，则回滚至事务开始前的状态

2. 一致性

   事务开始和结束以后，数据库的完整性不会被破坏

3. 隔离性

   数据库允许多个并发事务同时对数据库进行读写和修改的能力，隔离性可以有效地防止高并发产生的数据错误

   事务隔离分为不同级别：

   ​		(1). 读取未提交

   ​		(2). 读提交

   ​		(3). 可重复读

   ​		(4). 串行化

4. 持久性

   事务处理结束后，对数据库的修改是永久的，即使系统故障也不会丢失

##### 语法与使用

开启事务：begin或start  transaction

提交事务：commit

回滚：rollback

创建保存点：savepoint  identifier

删除保存点：release  savepoint  identifier

把事务回滚到保存点：rollback  to  identifier

设置事务的隔离级别：set   transaction

​	innodb提供的隔离级别：read、uncommitted、read   committed、repeatable  read、serializable

### 锁

锁是计算机协助多个进程或线程并发访问某一资源的机制

锁可以保证数据并发访问的一致性、有效性

锁冲突也是影响数据库并发访问性能的一个重要因素

锁是mysql在服务器层和存储引擎层的并发控制

##### 分类

1. 行级锁

   锁定粒度最细，表示只对当前操作的行进行加锁

   行级锁只有innodb引擎支持

   特点：开销大，加锁慢，会出现死锁，锁定粒度最小，发生锁冲突的概率最低，并发度也最高

2. 表级锁

   锁定粒度最大，对整张表添加锁

   特点：开销小，加锁快，不会出现死锁，锁定粒度大，发生锁冲突的概率最高，并发度最低

3. 共享锁

   其他用户可以并发读取数据，但不能修改

4. 排他锁

   除了持有锁的用户外，其他用户都不能访问和查询

5. 乐观锁

6. 悲观锁

### 存储过程

存储过程是一种在数据库中存储复杂程序，以便外部程序调用的一种数据库对象

存储过程是为了完成特定功能的SQL语句集，经编译创建并保存在数据库中，用户可通过指定存储过程的名字并给定参数来调用执行

存储过程就是对SQL语句的代码封装和重用

1. 优点

   存储过程可封装并隐藏复杂的商业逻辑

   存储过程可以回传值，并可以接收参数

   存储过程可以用在数据检查，强制实行商业逻辑等。

2. 缺点

   存储过程，往往定制化于特定的数据库上，因为支持的语言不同，当切换系统时，需要重写

   存储过程的性能调校与撰写受限于各种数据库系统

##### 语法

1. 声明语句结束符，可以自定义：

   delimiter   $$
   或

   delimiter    //

2. 声明存储过程

   create  procedure  demp_in_parameter(IN  p_in  int)

3. 存储过程开始和结束符号

   begin  .........    end

4. 变量赋值

   set   @p_in=1

5. 变量定义

   declare  l_int  int  unsigned  default  4000000;

6. 创建mysql存储过程、存储函数

   create  procedure   存储过程名(参数)

7. 存储过程体

   create   function    存储过程名(参数)

##### 使用

1. 简单用法

   create   procedure  get_info()

   select  *  from  student;

   call  get_info();

2. 复杂用法

   delimiter  //

   create    procedure   foo(in  uid  int)

   begin

   select  * from  student   where  \`id\`=uid;

   end //

   delimiter;

   call   foo(3)

### python 操作

1. 安装:pip  install  pymysql

2. 语法

   import pymysql 

   db = pymysql.connect(

   ​								host='localhost', 

   ​								user='user', 

   ​								password='passwd', 

   ​								db='db', 

   ​								charset='utf8') 

   try: 

   ​		with db.cursor() as cursor: 

   ​				\# 插⼊ 

   ​				sql = "INSERT INTO \`users\` (\`email\`, \`password\`) VALUES (%s, %s)" 

   ​				cursor.execute(sql, (\'webmaster@python.org', 'very-secret')) 

   ​				\# 需要⼿动提交才会执⾏ 

   ​		db.commit() 

   ​		with db.cursor() as cursor: 

   ​				\# 读取记录 

   ​				sql = "SELECT \`id\`, \`password\` FROM \`users\` WHERE \`email\`=%s" 

   ​				cursor.execute(sql, ('webmaster@python.org',)) 

   ​				result = cursor.fetchone() 

   ​				print(result) 

   finally: 

   ​		db.close()

### 数据备份与恢复

1. 备份：mysqldump   -h   localhost  -u  root  -p123456  dbname > dbname.sql

2. 恢复：mysql   -h   localhost  -u  root   -p123456   dbname  <   ./dbname.sql