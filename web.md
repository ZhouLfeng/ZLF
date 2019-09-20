### HTML

\<b>\</b>：加粗

\<i>\</i>：斜体

\<u>\</u>：下划线

\<s>\</s>：删除线

\<sup>\</sup>：上标

\<sub>\</sub>：下标

\<font>\</font>：下划线

color：文本颜色

size：文字大小

face：字体样式

\<p>\</p>：段落

\<br />：换行标记

\<hr  属性=“属性值”  />：水平线标记

属性：

color(颜色)

size(线的粗细)

width(线的宽度)

aligh(对齐方式)

noshade(是否去除阴影)

\<pre>\</pre>：原样输出

\<h1>\</h1>---\<h6>\</h6>：标题标记

\<div>\</div>：块状元素，占一行

\<span>\</span>：行内元素，由内容决定宽度

常见块状元素：p,h1-h6,pre,div,table

常见行内元素：font,b,i,u,sup,sub,span

空格:&nbsp

<:&lt

\>:&gt

&:&amp

版权号:&copy

￥:&yen

*:&times

/:&divide

无序列表：ul>li

有序列表：ol>li

自定义列表：dl>dd+dt

滚动字幕：

语法：`<marquee 属性 = “属性值”>……</marquee>`
属性:

Direction：滚动的方向，取值：left、right、up、down
Width：宽度
Height：高度
bgColor：背景色
scrollAmount：滚动步长值。值越大滚动的越快。默认值为6px。
scrollDelay：延时时间，两步之间停留的时间，以毫秒为单位。1秒＝1000毫秒



插入图片

语法格式:`<img  属性 = “属性值” />`
常用属性:

```html
src：指图片的路径，该路径可以是相对地址，也可以是绝对地址。
width：图片的宽度。
height：图片的高度。
alt：图片说明。当图片不存在时，显示一个提示信息。
border：图片边框的粗细。
left或right：可以实现图文混排。
left或right的功能相当于CSS中的“浮动”效果。
```



超链接

语法格式：`<a  属性 = “属性值”>……</a>`
常用属性:

```
href：链接的地址。该地址可以是绝对路径，也可以是相对路径。
target：链接的目标文件在哪个窗口中来打开。
		_blank：弹出一个空白窗口来打开文件。
		_self：在当前窗口中来打开目标文件。
		_parent：在父窗口中来打开目标文件。(常用于框架网页中)
		_top：在最顶层窗口中来打开目标文件。(常用于框架网页中)
name：指定一个锚点名称。所谓“锚点”用于长网页当中。
```

绝对路径：以http://开头

本地绝对路径:以file:///开头

相对路径:同一文件夹下



跳跃锚点

\<a name="top">123\</a>

\<a href="#top">go back\</a>



meta设置;

```
<meta name="viewport" content="width=device-width,minimum-scale=1.0,maximum-scale=1.0,maximum-scale=1.0,user-scalable=0"/>
```

这个是针对移动端浏览器写的一些页面属性，
`name="viewport"` --这就是针对移动端浏览器，
`width=device-width`--告诉浏览器页面的宽度应该等于设备的宽度，
`initial-scale=1.0`--页面将是原本尺寸展示，
如果后面是`2.0`的话，--就是是将页面放大两倍，
`maximum-scale=1.0`,--最大放大至原先大小，
`user-scalable=0` --是禁止缩放！

表格标签
结构

```
<table>
	<caption>我是一个表格</caption>
	<tr>
		<th>内容</th>
		<th>内容</th>
		<th>内容</th>
	</tr>
	<tr>
		<td>内容</td>
		<td>内容</td>
		<td>内容</td>
	</tr>
</table>
```

音频标签

\<audio src="文件" controls>   \</audio>

视频标签

\<video src="文件" controls>   \</video>



表单

\<form name="login"  method="post" action="http://www.xxxx.com/path" style='border:1px solid black'>
	<span>用 户 名 : </span>\<input type="text" name="username"  value="" placeholder='请输入账号'/>
    \<br/>
	\<span>登录密码:\</span>\<input type="password" name="pwd"  value="" placeholder='请输入密码'/>
    \<br/>
	\<input type="submit" name="submit"   value="登录" disabled />
\</form>

name：表单名称。用来区分不同的表单，JS可以通过name的值，对表单进行前端的验证。
method：表单数据的发送方式，取值：get和post
action：指定表单数据的处理程序。一般是服务器端的脚本程序(PHP/Python)。如果为空，则提交给自己来处理。
enctype：表单数据的一个加密(编码)方式。enctype属性只能在 method = post 的表单中。
	application/x-www-form-urlencoded   所有字符都进行加密，这种方式不能上传附件
	multipart/form-data //只对附件进行加密码(编码)，不对普通字符进行编码，如果上传文件，必须使用该值。



get和post方法：post用于提交数据，get提交数据最多只有4KB



表单中的各元素
单行文本域：用户名、地址、电话、邮箱等
语法格式：`<input type = “text” 属性 = “属性值” />`
常用属性:

```
type：元素的类型。取值：text、password、radio、checkbox、button、submit、reset等。
name：表单元素的名称。可以包含a-z、A-Z、0-9、_这些符号，但不能以数字开头。
value：元素的值。
size：文本框的长度，以字符为单位。
maxlength：最多可以输入的字符数
readonly：只读属性。如：readonly = “readonly”
disabled：禁用属性。如：disabled = “disabled”
```

单行密码框
语法格式：`<input type = “password” 属性 = “属性值”  />`

单选按钮
语法格式：`<input  type = “radio” 属性 = “属性值” />`

复选框

语法格式：`<input  type = “checkbox” 属性 = “属性值” />`

下拉列表
`<select>`标记的属性  name：元素的名称。

`<option>`标记的属性

value：元素的值

selected：是否默认选中

文本区域
语法：`<textarea  属性 = “属性值”></textarea>`

隐藏域
描述：看不见的表单元素，可以用它来传递一些值，这些值又不想让客户看见。
语法：`<input  type = “hidden”  name = “”  value = “”  />`

上传文件域
语法格式：`<input  type = “file”  属性 = “属性值”  />`

表单中的各种按钮
提交按钮：提交表单。如：`<input  type = “submit”  value = “提交表单”  />`
重置按钮：重新填写。如：`<input  type = “reset”  value = “重新填写”  />`
图片按钮(不常用)：指定图片的路径，功能也是提交表单。如：`<input type="image" src="images/btn02.png" />`
普通按钮：不具备任何功能，一般要绑定JS程序，来实现各种功能。

### CSS

语法格式：

<style type="text/css">
	h1 {color:red;font-size:12px;}
</style>

选择器

通配符：*

标签选择器：用标签名来声明

类选择器：定义一个类来标识css样式，通过标签中引用类名来完成css样式的套用

id选择器：用#加id名来标识css样式，标签中引用id=“id名”来套用

组合选择器：同时给多个元素添加同一种样式，中间用，隔开

后代元素选择器：用空格隔开

子元素选择器：用>隔开



##### 后代元素

伪类选择器

全局的链接样式,所有的样式都会改变
	a:link{color:gray;text-decoration:none;}
	a:visited{color:green;text-decoration:underline;}
	a:hover{color:red;}
	a:active{color:yellow;}
局部的链接样式,只有对应的几个类才有样式
	a.a1:link{color:black;text-decoration:none;}
	a.a1:visited{color:gray;text-decoration:underline;}
	a.a1:hover{color:blue;}
	a.a2:link{color:red;text-decoration:none;}
	a.a2:visited{color:black;text-decoration:underline;}
	a.a2:hover{color:green;}

px、em及rem

px：像素，绝对值

em：相对于当前对象内文本的字体尺寸，根据父类的变化而变化

rem：相对于根的比较，默认大小为16px

##### 样式属性

列表样式

list-style：列表样式，指定样式的符号，none(无符号)

边框属性

border-left：左边框线。
格式：border-left: 粗细 线型 颜色;(px)即div{border-left:5px solid red;}	多个参数值之间用空格隔开。
线型：none(无线)、solid(实线)、dotted(点状线)、dashed(虚线)、double(双线)
颜色:十进制  十六  单词
border-right：右边框线。
border-top：上边框线。
border-bottom：下边框线。

内边距 padding  默认顺序为--上右下左

padding-left:左侧内边距

padding-right:右侧内边距

padding-top:上侧内边距

padding-bottom:下侧内边距

外边距 margin    默认顺序为--上右下左

margin-left:左侧外边距

margin-right:右侧外边距

margin-top:上侧外边距

margin-bottom:下侧外边距

背景属性

background-color：背景颜色

background-image：图片路径

background-repeat：控制图片的平铺方式

​			no-repeat：不平埔

​			repeat-x：水平方向平埔

​			repeat-y：垂直方向平埔

​			repeat：水平和垂直都平埔（默认）

background-position：背景图片的定位方式

​			格式：background-position：方向定位

​			定位的单词：left、center、right、top、bottom

浮动和清除

浮动：

格式：float：浮动属性   属性：left、right

浮动元素不占空间，层次高于没有浮动的普通元素

浮动的元素一定是块元素

清除：

格式：clear：清除浮动，取值：left、right、both(清除两者)

继承性和优先级

继承性：

多个外层元素的样式会包含到内层元素中

选择器优先级：

单个选择器优先级：行内样式>id选择器>类选择器>标签选择器>通配符

组合选择器的优先级：指向越精准，优先级越高

display属性：控制元素显示方式

取值：none(不显示)、block(块元素)、inline(行内元素)

overflow属性：内容溢出处理

取值：scroll(滚动条)、hidden(隐藏)、auto(自动)、visible(显示)

cursor光标类型：改变光标显示类型

取值：pointer(手形)、help(帮助)、text(文本)、wait(等待)等

定位属性：

1.position：定位属性   属性取值：static(静态)、fixed(固定)、relative(相对)、absolute(绝对)

2.定位坐标值，left、right、top、bottom——距离目标元素的距离

3.固定定位——position：fixed

固定定位是相对于浏览器窗口进行定位的，不再占用空间，层级高于普通元素，固定之后一定是块元素

4.相对定位——position：relative

相对定位是相对于原来的位置进行定位，层级高于普通元素

5.绝对定位——position：absolute

绝对定位是相对于上层定位元素来进行定位，层级高于普通元素

HTML引入css方法

嵌入式：`<style  type = “text/css”>……</style>`

外联式：`<link href = “css/public.css” type = “text/css” rel = “stylesheet” />`

行内式：直接给标记添加style属性

表格属性

`border-collapse`：合并表格边框线。取值：`collapse`(合并)

### 全局CSS设置

1、所有HTML标记都要清除内外边距

```
html,body,ul,li,a,img,p,h1,h2,h3,h4,input{margin:0;padding:0;}

*{margin:0px;padding:0px;}
```

2、去除有序列列或无序列表前面的符号

```
	ul,li,ol{list-style:none;}
```

