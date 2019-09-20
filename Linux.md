# Linux

Linux是基于unix之上的系统，是一种开源系统

### 发行版

ReaHat：最成功的商用Linux

CentOS：社区版的RedHat

Fedora：个人版的RedHat

Debian：纯粹的自由软件构件的发行版，拥有最大的开源软件库

Ubuntu：最受欢迎的Linux发行版，目前学习使用

Gentoo：一切从源码开始手动安装。性能最高最稳定

Arch：省去编译，也是手动安装

ElementaryOS：华丽、优雅的桌面发行版，易用性极佳

Deepin：国人制作的发行版

### 命令行

#### sudo

以超管的身份执行后面的指令，后面可搭配任何已存在的指令

#### Ubuntu下的apt命令

apt后面需要跟参数再加上文件名或数据

##### 书写规范

apt  参数   文件名或其他数据

##### 参数

search：搜索

show：查看详情

install：安装

remove：删除

autoremove：自动删除无效的软件包

update：更新软件源信息

upgrade：升级软件

#### CentOS下的yum命令

centos下的yum命令和Ubuntu中的apt命令大同小异

##### 参数

search：搜索(后面跟文件名或其他数据)

install  ：安装(后面跟文件名或其他数据)

update：更新(后面跟-y)

remove：卸载(后面跟文件名或其他数据)

#### Ubuntu中安装python

Ubuntu中是自带python的，但是默认为python2.7，所以就需要手动安装python3.7，命令为

​			sudo apt python3.7

#### Ubuntu中安装pycharm和VNC

pycharm可在终端执行sudo snap install pycharm-community --classic来进行安装

安装VNC需要到官网下载安装，因为VNC是可兼容的，直接安装即可

#### 软件包

Ubuntu中软件包后缀为 deb

CentOS中软件包后缀为 rpm

# shell

操作系统中最核心的是kernel，他直接与硬件打交道，处理很多底层的事情，一般禁用户直接访问，外部程序若想要调用内核功能需要使用系统调用接口。

shell是有个应用程序，它连接了用户和Linux内核，他作为了一个桥梁，变相的能够让用户来调用内核做事情。

shell一般分为用户界面(GUI)和命令行(CLI)

常见的GUI shell：Gnome，KDS，Xface

常见的CLI shell：sh，csh，bash，zsh

Linux中可以通过命令cat /etc/shells来查看安装的shell

### Bash快捷键

ctrl+f：前进一个字符

ctrl+b：后退一个字符

ctrl+a：回到行首

ctrl+e：回到行尾

ctrl+w：向左删除一个单词

ctrl+u：向左删除全部

ctrl+k：向右删除全部

ctrl+y：恢复上次删除的内容

ctrl+l：清屏

### 目录结构

##### 系统目录

/：系统根目录，通常不会存储文件

boot：启动目录

bin：系统二进制目录，存放普通用户的GNU命令

sbin：系统超级二进制目录，存放超管的GNU命令

usr：资源目录

​		--bin：用户二进制目录，存放用户级的GNU命令

​		--sbin：用户超级二进制目录，存放管理员级的GNU命令

​		--local

​				--bin

​				--sbin

opt：第三方开发程序

etc：系统配置文件目录

proc：对当前进程、运行状态记录的目录

root：管理员家目录

home：用户家目录

run：运行目录，存放系统运行时的数据

tmp：临时目录，可在该目录中创建和删除临时工作文件

var：可变目录，用于存放经常变化的文件，例如日志文件

系统中的目录结构采用树型结构，一个文件夹下包含了多个文件夹和文件

![1566980723151](C:\Users\Ce\AppData\Roaming\Typora\typora-user-images\1566980723151.png)

### 目录操作

绝对路径：/a/d/h    从根目录一直写到操作目录

相对路径：../   或 ./ 

../：上次目录

./：当前目录

#### 目录操作命令

pwd：显示当前目录的绝对路径

ls ./：显示当前目录的文件

ls -l ./：以列表形式显示文件，无单位显示

ls -lh ./：以列表形式显示文件，有单位显示

ls -A ./：显示隐藏文件

cd (绝对路径/相对路径)：跳转路径

cd -：回到上一次所在的路径，可实现双向跳转

mkdir  a： 创建一个名为a的文件夹

mkdir -p a/b/c：创建一个三层结构的文件夹，a中包含b，b中包含c

​                              还可在路径中加{文件名1,文件名2}，这样搭建出的文件1和2是在同一个文件夹下，不是层级结构

### 文件操作

#### 文件命令

cp  a  b/：将a文件复制到b目录下

mv  a  b：将a文件移动到b所在的目录并改名为b，而原来的b文件将被销毁

rm a：删除名为a的文件，如果要删除一个文件夹时需要添加-r参数

touch abc：在当前目录中创建一个名为abc的文件

ln -s a b：为a文件创建一个软链接

ln a b：为a文件创建一个硬链接

##### 重命名

mv a.txt b.txt    将a.txt重命名为b.txt

##### 复制(cp)、移动(mv)、删除(rm)的通用参数

-i：覆盖前会提示是否覆盖

-n：若目标文件已存在，则停止该操作

-f：若目标文件已存在，则强制操作，覆盖前无提示，和-i、-n对立

-r：对文件夹进行操作

##### 软链接和硬链接

软链接：

​	可以跨分区创建，记录文件的地址，软链接就是通过记录中的地址来实现调用，若通过软链接来修改文件数据，源文件也会发生改变。

硬链接：

​	只可在同分区中创建，相当于给源文件起了个别名，把文件中的内容复制了一份，若一个文件有多个硬链接，但这几个硬链接在内存中只占用一个文件的大小，相当于共享链接中的数据。通过硬链接修改文件数据，源文件的数据并不会被修改，但其余的指向该源文件的硬链接都会发生改变。

### 压缩模块

压缩模块中最常用的为两个：tar和zip

##### tar：

压缩：tar -czf  new_file.tgz  file    (将file用tar方式压缩并重命名为new_file.tgz)

解压：tar -xzf  new_file.tgz            (将new_file.tgz解压出来)

##### zip：

压缩：zip -r new_file.zip file           (将file用zip方式压缩并重命名为new_file.zip)

解压：unzip  new_file.zip                (将new_file.zip解压出来)

# 用户权限

Linux是一个多用户系统，一个系统可拥有多个用户，为了便于管理多个用户，所以产生了用户组

用户和用户组都只拥有唯一的名称和ID，用户的ID为UID，用户组的为GID

系统中拥有最高权限为root，而root的uid和gid都为0



#### passwd

用户名和uid的对应关系记录在 /etc/passwd 中

单行格式：root: x : ​0 : 0 : root : /root : /bin/bash

root：用户名

x：已作废，之前用于记录密码

0：uid

0：gid

root：注释

/root：家目录

/bin/bash：登录后所使用的shell

#### group

用户组和gid的对应关系记录在 /etc/group 中

单行格式：sudo : x : ​27 : z,tom,test,a

sudo：组名

x：已作废，之前用于记录组密码

27：组ID

z,tom,test,a：该组的成员



#### shadow

用户的密码信息记录在 /etc/shadow 中，保存的是加密后的密码

单行格式：z:$6$QmoXOftm$HoDkicy3N1Od2orRxBTo4gGJpLmtC1alqf6aK9ULUVhgZe3VCeVluZr4cFrGwhguwYl3aIfy3KrBh63MTU6YC1:18135:0:99999:7:::

z：用户名

$6$QmoXOftm$HoDkicy3N1Od2orRxBTo4gGJpLmtC1alqf6aK9ULUVhgZe3VCeVluZr4cFrGwhguwYl3aIfy3KrBh63MTU6YC1：加密后的密码

18135：最后一次修改密码的日期，从1970-1-1开始，按天记录

0：密码几日内不可修改

99999：密码有效天数

7：密码失效前的几天内提醒

​    ：密码失效的宽限天数

​    ：账号失效日期

​    ：保留字段，暂无用处

# 用户管理

### 添加用户

用法：useradd -mU -G 组名 用户名

参数

​		-G groups：新账户的附加组列表

​		-m：在/home目录创建家目录

​		-U：创建与用户同名的组

### 删除用户

用法：userdel -r 用户名

-r：删除主目录和邮件池

### 修改密码

用法：passwd 用户名

### 切换用户

1.su 用户名：只切换用户身份，但还处于当前目录中

2.su - 用户名：切换用户身份，并返回该用户名的家目录中

# 用户组管理

### 添加组

用法：groupadd -aG 组名

参数：

​		-d HOME_DIR：用户的新主目录

​		-g GROUP：强制使用GROUP为新主组

​		-G GROUPS：新的附加组列表GROUPS

​		-a GROUPS：将用户追加至-G中提到的附加组中，并不从其他组中删除此用户

​		-L：锁定用户账号

​		-m：将家目录内容移至新的位置（只能和-d一起使用）

​		-s SHELL：该用户账号的新登陆shell

​		-U：解锁用户账号



### 常用创建用户及用户组方法： 

--sudo useradd -mU -s /bin/bash test

--passwd test

# 查看登录的用户

who：查看谁正在登录

w：查看谁正在登录，并显示每个登录用户正在执行的任务

last：查看历史登陆记录

lastb：查看失败的登陆记录

lastlog：查看所有登陆过的用户最后一次登录的时间

# 文件权限

文件权限分为三种：r--读(read)，w--写(write)，x--执行(execute)

Linux系统中又规定了对于不同的操作对象有不同的权限，操作对象分为：

1.owner：文件拥有着

2.group：同组成员

3.other：其他

### 查看文件权限

ls-l：可查看文件的所有信息，包括权限信息

格式：-rwxr-xr--   1      bob     staff        9824      8      28     21:22     test.py
-rwxr-xr--为权限信息，分解如下：

-：若为d则表示为文件夹，-就表示是普通文件，s表示socket文件

rwx：文件拥有着所拥有的权限

r-x：同组人员所拥有的权限

r--：其他人员可进行的操作

### 权限修改

用法：chmod [] 文件或目录

##### 1。指定对象设置权限

[]中包含了具体的操作，为：

​			u/g/o/a      +/-/=      r/w/x

其中u/g/o/a表示操作对象，u--文件拥有着，g--同组，o--其他，a--所有，可同时对多个对象设置权限，可用‘，’分割，还可以用例如 ug 这样的形式同时进行操作

+（添加权限），-（减少权限），=（设定指定权限）

r/w/x为权限参数，可同时包含多个权限

##### 2.利用数字设置权限

权限信息是一个10位数的数据，第一位是计算机自动设置，剩余9位为权限设置，我们就可以将这9位看作3-3-3的数据，前3位为文件拥有者的权限，中间为同组，最后是其他，这是我们就可以用二进制来表示是否具有权限，例如100，表示-r--------，200为--w-------。

##### 修改文件拥有者

用法：chown 用户：组名  文件名

简便用法：

​	在修改后的文件拥有者中输入命令sudo chown -R \`id -u\`:\`id -g\` c 即可修改文件拥有着为自己

# 文本操作

echo xyz：打印xyz

echo xyz > a.txt：将xyz写入到a.txt中

echo xyz >> a.txt：将xyz追加写入到a.txt中

cat 文件名：查看文件内容

head -n N 文件名：查看文件的前N行

tail -n N 文件名：查看文件的后N行

less 文件名：快速阅览文件

​	快捷方式：

​			j：向下

​			k：向上

​			f：向下翻屏

​			b：向上翻屏

​			g：到全文开头

​			G：到全文结尾

​			q：退出

sort 文本或文件：将内容升序排序

​			-r：将内容降序排序

uniq：去重，只删除临近的重复数据，通常和sort一起使用

awk ‘{print $N}’：打印出相关列

wc：字符统计

​			-c：统计字符

​			-w：统计单词

​			-l：统计行

管道符 |：用于连接多个命令，将前面的输出作为后面的输入

文本过滤grep：

​		参数：

​			-i：忽略大小写

​			-I：忽略二进制文件

​			-r：递归查找目录

​			-n：打印行号

​			-c：只显示匹配到的个数

​			-l：只显示匹配到的文件列表

​			-o：只显示匹配到的单词

​			-v：忽略制定的字段

​			-E：通过正则表达式匹配

​			--include=‘*.py’：仅包含py文件

​			--exclude=‘*.js'：不包含js文件

# vim

vim有三种模式：命令，插入和底栏命令

进入vim后默认为命令模式，按i可进入插入模式，若想再进入命令模式需按ESC，

底栏命令进入按：即可，

### 命令模式

h, j, k, l 光标左、下、上、右移动

ctl + e：向下滚动

ctl + y：向上滚动

ctl + f：向下翻屏

ctl + b：向上翻屏

yy：复制整行

p：粘贴到下一行

P：粘贴到上一行

dd：删除整行

d3w：向前删除3个单词

7x：删除7个字符

u：撤销
ctl + r：重做
c3w：剪切3个单词
gg：跳至至文文件首首行行行
shift + g：跳至至文文件结尾
shift + h：跳至至屏幕首首行行行
shift + m：跳至至屏幕中间
shift + l：跳至至屏幕结尾
ctl + v：列列编辑
shift + v：选中整列列
shift + >：向右缩紧
shift + <：向左缩紧

### 底栏模式

10：跳转至文件的第10行

%s/abc/123/g：将文件中所有的abc替换为123

set nu：打开行号显示

set nonu：关闭行号显示

w：保存

q：退出

wq：保存并退出

##### vim配置文件

​		~/.vimrc

# 进程状态

常用的查看进程信息的命令有ps、top

### PS命令

ps：显示敲下命令后一瞬间的进程状态，如果直接敲ps不带参数的话显示的信息会很少

ps命令支持三种不同类型的命令行参数：

#### ps -ef

​	-e：指定显示所有运行在系统上的进程

​	-f：扩展了输出

数据显示：

​	z@z:~$ ps -ef 
​	UID        PID  PPID  C STIME TTY          TIME     CMD
​	root         1     0         0 16:21   ?        00:00:01   /sbin/init splash
​	root         2     0         0 16:21   ?        00:00:00   [kthreadd]
​	root         3     2         0 16:21   ?        00:00:00   [rcu_gp]
​	root         4     2         0 16:21   ?        00:00:00   [rcu_par_gp]
​	root         6     2         0 16:21   ?        00:00:00   [kworker/0:0H-kb]
​	root         8     2         0 16:21   ?        00:00:00   [mm_percpu_wq]
​	root         9     2         0 16:21   ?        00:00:00   [ksoftirqd/0]
​	root        10    2         0 16:21   ?        00:00:00   [rcu_sched]

参数解析：

UID：启动进程的用户

PID：进程ID

PPID：父进程的进程号（若该进程是由另一进程启动）

C：进程生命周期中的CPU利用率

STIME：进程启动时的系统时间

TTY：进程启动时的终端设备

TIME：进程总共占用CPU的时间

CMD：进程运行的命令

#### ps aux

​	a：显示和任意终端关联的所有进程

​	u：采用基于用户的格式显示

​	x：显示所有的进程，包括未分配任何终端的进程

数据显示：

 z@z:~$ ps aux
 USER       PID %CPU %MEM     VSZ         RSS   TTY      STAT   START   TIME     COMMAND
 root         1       0.0         0.2     159896   9124     ?           Ss     16:21     0:01     /sbin/init spla
 root         2       0.0         0.0        0              0         ?           S       16:21     0:00      [kthreadd]
 root         3       0.0         0.0        0              0         ?           I<      16:21    0:00      [rcu_gp]
 root         4       0.0         0.0         0             0         ?           I<       16:21    0:00     [rcu_par_gp]

参数解析：

USER：执行这个进程的用户

PID：进程ID

%CPU：CPU占用率

%MEM：内存占用率

VSZ：进程占用的虚拟内存的大小，以KB为单位

RSS：进程占用的物理内存的大小

TTY：进程启动时的终端设备

STAT：进程状态

START：进程启动时间

TIME：进程累计占用CPU的时间

COMMAND：启动进程的命令



##### STAT 

​	代表当前进程状态的双字符状态码

​	第一个字符表示进程状态

​				O：正在运行

​				S：正在休眠

​				R：可运行，正等待CPU响应

​				Z：僵化进程

​				T：停止

​	第二个字符表示进程状态细节部分

​				<：该进程运行于高优先级上

​				N：该进程运行于低优先级上

​				L：该进程由页面锁定在内存中

​				s：该进程有控制进程

​				l：该进程是多进程的

​				+：该进程运行在前台

### TOP命令

可持续的查看某些进程的状态

当进程太多时，可以通过-p参数指定查看的进制ID来进行监视

数据显示：

top - 17:42:53  up  1:20,   1 user,  load average: 0.20, 0.06, 0.01
任务:  223 total,    1 running,  185 sleeping,    0 stopped,    0 zombie
%Cpu(s):   1.5 us,   1.2 sy,   0.0 ni,  77.4 id,  19.9 wa,   0.0 hi,   0.0 si,   0.0 st
KiB Mem :  4037168 total,   1949408  free,  1216528 used,    871232 buff/cache
KiB Swap:   2097148 total,   2097148  free,               0 used.   2581956 avail Mem 

PID  USER      PR   NI      VIRT        RES        SHR          S      %CPU     %MEM     TIME+ COMMAND      

1330     z         20    0    411056    72064    39476       S         3.6            1.8           0:09.57 Xorg        
2146     z         20    0    823356    43608    33204       S         3.0             1.1       0:02.47 gnome-term+ 
1516     z         20    0   3471856  196284    94708      S         1.7             4.9      0:28.99 gnome-shell 
10       root      20    0        0               0               0          I          0.3             0.0      0:00.68 rcu_sched   
1460      z         20   0    126384      2164       1796       S         0.3             0.1      0:03.71 VBoxClient  
1721      z         20   0   1030068    62288     47892      S         0.3            1.5      0:03.08 nautilus-d+ 

##### 头信息：

1. 系统运行的整体状态：开机时长，登陆用户数，系统负载

   ​		系统负载：load average: 0.20, 0.06, 0.01

   ​		数据分别代表：一分钟负载，五分钟负载，十五分钟负载

   ​		负载值越高代表服务器压力越大

   ​		负载值不要超过CPU的核心数，若超过核心数，则代表CPU压力过大，很多进程在等待处理

   ​		若调用uptime命令，显示结果就和头信息一样，结果都为系统状态

2.进程情况：任务总数，运行中的进程数量，休眠进程数量，停止的进程数量和僵尸进程数量

3.CPU使用情况：

​		us：用户态占用（user）

​		sy：内核态占用（system）

​		id：空闲的CPU（idle）

4.内存占用情况：内存总量，空闲内存，使用的内存，缓冲区占用的内存

5.交换分区的占用：交换分区是一种将内存数据存入硬盘的技术，在内存不足时使用

##### 进程区

PID：进程ID

USER：进程所属用户的名称

PR：进程的优先级

NI：进程的谦让度值

VIRT：进程占用的虚拟内存总量

RES：进程占用的物理内存总量

SHR：进程和其他进程共享的内存总量

S：进程的状态

%CPU：进程使用CPU的时间比例

%MEM：进程所使用的内存占可用内存的比例

TIME+：自进程启动到目前为止的CPU时间总量

COMMAND：进程所对应的命令行名称，也就是启动的程序名

### HTOP命令

htop是一种比top还能直观感受进程的工具，不过htop不是系统默认的命令，需要额外安装

# 进程的管理

kill：杀死进程或给进程发送数据

​		-1(HUP)：平滑重启

​		-9(KILL)：强制杀死进程

​		-15(TERM)：正常终止进程（默认）

pkill(ProcessName)：按名字清理进程

killall(MatchedProcessName)：处理名字匹配的进程

# 其他状态

### 内存状态free

可以通过-m或-g参数调整显示的单位

### 硬盘状态

iostat：查看硬盘写入和读取的状态

df -lh：查看硬盘分区及每个分区的剩余空间

du -hs ./：查看当前目录占用的硬盘大小

### 网络状态

##### ifconfig

查看网卡状态，一般用来检查自身IP地址

##### netstat -natp

查看网络连接状态

​		-a：显示所有选项

​		-t：显示所有与TCP相关的选项

​		-u：显示所有与UDP相关的选项

​		-x：显示所有与UNIX域相关的套接字选项

​		-n：拒接显示别名，能显示数字的全部转换为数字显示

​		-p：显示建立相关连接的程序名

​		-l：显示所有状态为LISTEN的连接

​		-e：显示扩展信息，如链接所对应的用户

​		-c：间隔一段时间执行一次netstat命令

​		-s：显示统计信息，对每种类型进行汇总

##### ping

格式：ping -i 0.5 -c 100 xx.xx.xx.xx

​		-i：间隔

​		-c：数量

​		-q：安静模式，只打印结果

##### lsof

​		lsof -i:[PORT]：查看占用端口的程序

​		lsof -i tcp：查看所有TCP连接

​		lsof -u abc：查看用户abc打开的所有文件

​		lsof -p 123：查看pid为123的进程打开的所有文件

##### 路由追踪

traceroute [HOST]

##### DNS查询

​	dig[DOMAIN]

​	host[DOMAIN]

​	nslookup[DOMAIN]

### 时间和日期

##### date

​	查看日期与时间

##### cal

​	查看日历

​			--one：查看本月的日历

​			--three：查看最近三个月的日历

​			--year：查看全年的日历

### 下载

##### curl

​	执行HTTP访问，也可用来下载

##### wget

​	下载

##### scp

​	在服务器之间上传或下载，格式：scp root@x.x.x.x:/root/abc ./abc

# Shell编程与运维

### Shell脚本

Shell 脚本⼀般是以 .sh 结尾的⽂本⽂件, 当然, 也可以省略扩展名。 

脚本⽂件第⼀⾏通过注释的⽅式指明执⾏脚本的程序。 

  		常⻅⽅式有: 

​				\#!/bin/sh 

​				\#!/bin/bash 

​				\#!/usr/bin/env bash 

Python 脚本的第⼀句⼀般是 #!/usr/bin/env python 

在 Shell 脚本中, # 开头的⽂本是注释

### 脚本创建过程

1. 创建a.sh ⽂件 

2. 将下⾯⽂本写⼊ a.sh 中 

\#!/bin/bash 

echo "Hello" 

echo "I am `whoami`" 

echo "I love Linux" 

echo "The CPU in my PC has \`cat /proc/cpuinfo |grep -c processor\` cores" 

exit

3. 执⾏ chmod a+x cpu-count.sh 对脚本授予可执⾏权限 

4. 输⼊ ./a.sh 执⾏脚本 

5. 查看脚本的退出状态: echo $? 

退出状态为 零 表示正常, 状态码为 正整数 代表异常退出 

### 变量 

1. 定义 

   变量的定义与其他语⾔差距不⼤, 需要注意的是赋值前后没有空格。  

   a=12345 

   b=xyz 

2. 使⽤ 

   使⽤变量时, 变量名前⾯加上 $ 符 

   ​	echo "---$a---\n===$b===" 

   ​	printf "---$a---\n===$b===\n" 

3. 注意 引号 的差别 

   echo "---$a---\n===$b===" 

   echo '---$a---\n===$b===' 

4. 定义当前Shell下的全局变量 
   1. 定义: export ABC=9876543210123456789 
   2. 定义完后, 在终端⾥⽤ source 加载脚本: source ./test.sh 

5. 常⽤的系统环境变量 

   $PATH : 可执⾏⽂件⽬录 

   $PWD : 当前⽬录 

   $HOME : 家⽬录 

   $USER : 当前⽤户名 

   $UID : 当前⽤户的 uid 

### 选择语句**:** **if** 

分⽀控制语句完整格式为:

if command 

then 

​	commands 

elif command 

then

​	commands 

else 

​	commands 

fi 

1. if 语句检查判断的依据实际上是, 后⾯所跟的命令的状态码: 0 为 true, 其他值 为 false 

   if ls /xxx 

   then 

   echo 'exist xxx' 

   else 

   echo 'not exist xxx' 

   fi 

2. 条件测试命令: [ ... ] 

   [ 的后⾯和 ] 的前⾯必须有空格, 否则会报错

   ⽤法: 

   if [ condition ] 

   then 

    commands 

   fi 

3. 条件列表 

   ##### 数值⽐较

   n1 -eq n2 检查n1是否与n2相等 

   n1 -ge n2 检查n1是否⼤于或等于n2 

   n1 -gt n2 检查n1是否⼤于n2 

   n1 -le n2 检查n1是否⼩于或等于n2 

   n1 -lt n2 检查n1是否⼩于n2 

   n1 -ne n2 检查n1是否不等于n2 

   ##### 字符串⽐较

   str1 = str2 检查str1是否和str2相同 

   str1 != str2 检查str1是否和str2不同 

   str1 < str2 检查str1是否⽐str2⼩ 

   str1 > str2 检查str1是否⽐str2⼤ 

   -n str1 检查str1的⻓度是否⾮0 

   -z str1 检查str1的⻓度是否为0 

   ##### ⽂件⽐较

   -d fifile 检查fifile是否存在并是⼀个⽬录 

   -e fifile 检查fifile是否存在 

   -f fifile 检查fifile是否存在并是⼀个⽂件 

   -r fifile 检查fifile是否存在并可读 

   -w fifile 检查fifile是否存在并可写 

   -x fifile 检查fifile是否存在并可执⾏ 

   -s fifile 检查fifile是否存在并⾮空 

   -O fifile 检查fifile是否存在并属当前⽤户所有 

   -G fifile 检查fifile是否存在并且默认组与当前⽤户相同 

   fifile1 -nt fifile2 检查fifile1是否⽐fifile2新 

   fifile1 -ot fifile2 检查fifile1是否⽐fifile2旧 

### 循环语句**: for** 

Shell 中的循环结构有三种: for、while和until 

for 循环的基本格式: 

​	for 变量 in 序列

​	do

​			执行命令

​	done

seq START END 语句⽤来产⽣⼀个数字序列 

$[ NUM1 + NUM2 ] 语句⽤来进⾏基本的数学运算 

[[ ... ]] 语句⽤来更⽅便的进⾏⽐较判断 

C语⾔⻛格的 for 循环 :

​	for ((i=0; i<10; i++)) 

​	do 

​		echo "num is $i" 

​	done 

### 函数 

函数定义 

function foo() { 

echo "---------------------------" 

echo "Hello $1, nice to meet you!" 

echo "---------------------------" 

} 

foo seamile 

定义时 function 不是必须的，可以省略

调用时在终端或脚本中直接输⼊函数名即可，不需要⼩括号

传参也只需将参数加到函数名后⾯，以空格做间隔，像正常使⽤命令那样

bar() { 

​	echo "执⾏者是 $0" 

​	echo "参数数量是 $#" 

​	echo "全部的参数 $@" 

​	echo "全部的参数 $*" 

​	if [ -d $1 ]; then # 检查传⼊的第⼀个参数是否是⽂件夹 

​		for f in `ls $1` 

​		do 

​				echo $f 

​		done 

​	elif [ -f $1 ]

​	then 

​			echo 'This is a file: $1' # 单引号内的变量不会被识别 

​			echo "This is a file: $1" # 如果不是⽂件夹, 直接显示⽂件名 

​	else 

​			echo 'not valid' # 前⾯都不匹配显示默认语句 

​	fi 

}

### 获取用户输入

read -p "请输⼊⼀个数字：" num 

echo "您输⼊的是：$num"

### 作业

##### 往some.log中追加内容

#!/bin/bash

function foo() {
        echo 'The system is running...' >> "./some.log"
}

#####  压缩成backup.tgz

#!/bin/bash

function foo() {
        tar -czf backup.tgz $1
        echo '压缩完成'
}

foo

##### 使用md5验证两个文件是否相同

#!/bin/bash

function foo() {
        a=`md5sum $1 | awk '{print $1}'`
        b=`md5sum $2 | awk '{print $1}'`
        if [ $a == $b ]
        then
                echo '这两个文件相同'
        else
                echo '这两个文件不相同'
        fi
}

