# jQuery

jQuery声明:<script src="./jquery-1.8.3.js"></script>

$(function(){})：当网页加载完成时

### 基本选择器

#id：根据元素的id属性来获取元素

element：根据元素的名称获取元素

selector1,selector2：匹配所有满足条件的元素

.class：根据元素的class属性来获取元素

js对象显示出来是一个标签的样式

jquery单个对象显示出来 是init

jquery集合对象显示出来是 init,集合中存储的是js的单个对象,通过.get()方法获取标签

### 层级选择器

子元素
$("div>p").html('<h1>python</h1>')
后代
$("body p").html('<h1>python</h1>')
同级

+表示div后面的第一个a

$('div+a').html("<h1>python</h1>")

~表示div后面的所有a标签

$('div~a').html("<h1>python</h1>")

### 简单选择器

:not(selector)：匹配除指定选择器以外的其他元素

:first ：匹配第一个元素

:last ：匹配最后一个元素

:even：匹配所有偶数

:odd ：匹配所有奇数

:eq(index) ：匹配索引为index的元素（默认索引从0开始）

:gt(index)：匹配索引大于index的元素

:lt(index) ：匹配索引小于index的元素

### 内容选择器

:contains(text)：匹配内容包含指定文本的元素

:empty ：匹配内容为空的元素

:has(selector) ：匹配具有指定选择器的元素

:parent：匹配具有子元素的元素（内容不为空的元素）

### 可见性选择器

:hidden：带有隐藏属性的标签

show()：隐藏属性显示

:visible：带有显示属性的标签

hide()：显示属性隐藏

### 属性选择器

[属性名] ：匹配具有指定属性的元素

[属性名=value]：匹配属性值等于value的元素

[属性名!=value] ：匹配属性值不等于value*的元素

[属性名^=value] ：匹配属性值以value开始的元素

[属性名$=value] ：匹配属性值以value结尾的元素

[属性名\*=value] ：匹配属性值包含value的元素

[属性名N]：匹配包含多个属性的元素

### 子属性选择器

div>:first：匹配div标签下的第一个子属性

### 表单选择器

:input ：匹配所有表单元素

:text ：匹配所有文本框

:password：匹配所有密码框

:radio ：匹配所有单选按钮

:checkbox：匹配所有复选框

:submit ：匹配提交按钮

:reset：匹配重置按钮

:image：匹配图像域

:button：匹配按钮

:file：匹配文件域

:hidden：匹配隐藏表单

##### 添加样式

$(':input').css('background','yellow');

$(':not(:parent)').html("123");

$(":radio").attr('disabled',true);

### 表单属性选择器

:enabled ：匹配所有可用元素

:disabled ：匹配所有不可用元素

:checked ：匹配复选框单选框所有选中元素

:selected ：匹配下拉选框所有选中元素

##### 实例（双控制开关）

<!DOCTYPE html>
<html>
	<head>
		<meta charset="utf-8">
		<title></title>
		<script src="./jquery-1.8.3.js"></script>
		<script type="text/javascript">
			var res = true;
			$(function(){
				var inp1 = $('input[name=sign1]');
				var inp2 = $('input[name=sign2]');
				inp1.click(function(){
					$('input[value=关]').attr('disabled',res);
					res = !res;
					$('input[value=开]').attr('disabled',res);
					})
				inp2.click(function(){
					$('input[value=关]').attr('disabled',res);
					res = !res;
					$('input[value=开]').attr('disabled',res);
					})
					//jquery对象,get(0)以后会转变成DOM对象
					// inp.get(0).checked;
					// $('input[type=submit]').attr('disabled',false);
			});
		</script>
	</head>
	<body>
		<span>控制1：</span>
		<input type="checkbox" name="sign1">
		<br>
		<input type="submit" value="开" disabled>
		<input type="submit" value="关" disabled>
		<br>
		<span>控制2：</span>
		<input type="checkbox" name="sign2">
	</body>
</html>

# DOM对象和jQuery

jquery对象转变位dom对象
console.log($('span').get(0));

dom对象转变为jquery对象
var html_=document.getElementById('a');
console.log($(html_));

# jQuery中的属性

### attr属性

attr(name)：获取指定元素的属性

attr(key,value)：设置元素的属性

attr(object)：为元素同时设置多个属性，要求参数是一个json数据

attr(key,fn)：通过函数的返回值设置元素属性

removeAttr(name)：移除元素属性

### class属性

addClass(class)：为元素添加class属性

removeClass(class)：删除元素的class属性

toggleClass(class)：切换样式，若元素中已有class属性，则删除；若没有，则添加

hasClass(class)：判断元素是否含有class属性

### css方法

css(name)：获取元素的css属性

css(name,value)：设置元素的name为value,一个只能添加一个样式

css(object)：设置元素的css样式，可同时添加多个

### offset位置

offset()：获取元素的位置，位置信息为外边距

offset(coordinates)：设置元素的位置，用[]包裹设置边距

### 元素尺寸

width()：获取元素的宽度

width(value)：设置元素的宽度

height()：获取元素的高度

height(value)：设置元素的高度

### 文本域值

##### 双标签

$('标签').html()：获取标签中的任何内容，包括标签

$('标签').html(value)：替换标签中的内容

$('标签').text()：获取标签中的文本内容

$('标签').text(value)：替换标签中的文本内容

##### 单标签

$('标签').val()：获取标签中的value内容

$('标签').val(value)：替换标签中的value内容

# jQuery 中的事件

### 常用事件

=> click(fn)：点击时触发
-> blur(fn)：失去焦点时触发
-> change(fn)：状态改变时触发
-> keypress(fn)：键盘按下时触发
-> mousedown(fn)：鼠标按下时触发
-> mouseover(fn)：鼠标悬浮时触发
-> mouseout(fn)：鼠标离开时触发
-> scroll(fn)：滚动时触发
dblclick(fn)：双击时触发
focus(fn)：获得焦点时触发
keydown(fn)：键盘按下时触发
keyup(fn)：键盘弹起时触发
load(fn)：页面载入时触发，功能与ready类似
unload(fn)：页面关闭时触发
mouseup(fn)：鼠标弹起时触发
mousemove(fn)：鼠标移动时触发
resize(fn)：调整大小时触发
select(fn)：文本选中时触发
submit(fn)：表单提交时触发

### 事件切换

hover(over,out)：鼠标悬浮与鼠标离开事件

over：鼠标悬浮事件

out：鼠标离开事件 

# 事件编程

### 绑定事件

##### bind(type,[data],fn)

​	意：为元素绑定的事件处理程序

​	type：事件类型

​	[data]：可选参数，事件发生时传递的数据

​	fn：事件的处理程序

##### bing({type:fn,type:fn})

​	意：为元素绑定多个数据

##### one(type,[data],fn)

​	意：为元素绑定事件处理程序，但只执行一次

##### unbind([type])

​	意：移除事件，解绑

### 事件绑定中的this对象

this在哪个标签中就表示哪个标签，在$中表示document，如果在网页编辑器中输入this，就表示window

# 动画

### 基本动画

##### 显示

show()：将隐藏元素显示

show(speed,[callback])：以动画效果显示

speed：动画变换时间

[callback]：事件完成后所触发的回调函数，可不填

##### 隐藏

hide()：将显示元素隐藏

hide(speed,[callback])：以动画效果隐藏

##### 切换

toggle()：切换显示或隐藏

toggle(switch)：switch为true时显示，为false时隐藏

toggle(speed,[callback])：以动画效果切换显示或隐藏

speed：’slow‘(慢)，’normal‘(正常)，’fast‘(快速)

### 滑动效果

slideDown(speed,[callback])：以动画效果向下滑动显示

slideUp(speed,[callback])：以动画效果向上滑动隐藏

slideToggle(speed,[callback])：以动画效果滑动显示或隐藏

### 淡入淡出效果

fadeIn(speed,[callback])：以动画形式淡入(显示)

fadeOut(speed,[callback])：以动画形式淡出(隐藏)

fadeTo(speed,opacity,[callback])：设置元素透明度

opacity：透明度(0-1)--0全透明，1不透明

### 自定义动画

animate(params,[speed])：自定义动画效果

params：自定义动画

speed：动画持续时间

# 文档操作

### 元素内部插入dom元素

##### 后面插入

A.append(B)：将B插入到A的后面

A.appendTo(B)：将A插入到B的后面

##### 前面插入

A.prepend(B)：将B插入到A的前面

A.prependTo(B)：将A插入到B的前面

### 元素外部插入dom元素

##### 后面插入

A.after(B)：将B插入到A外面的后面

A.insertAfter(B)：将A插入到B外面的后面

##### 前面插入

A.before(B)：将B插入到A外面的前面

A.insertBefore(B)：将A插入到B外面的前面

### 删除操作

empty()：清空元素内容，留一个空标签

remove()：删除元素节点及内容，什么都不留

### 复制操作

clone()：克隆元素

clone(true)：克隆元素同时复制元素的事件

### 替换操作

##### 值替换

html()：替换标签中的内容

##### 节点(标签)替换

replaceWith()：直接把一整个标签替换成想要的内容

### 包裹操作

wrap()：对每个元素进行单独包裹

### 查找操作

eq(index)：通过元素的索引查找元素，index默认从0开始

filter(expr)：查找与给定元素匹配的元素，expr匹配条件

not(expr)：查找与给定元素不匹配的元素

children([expr])：查找所有子元素

find(expr)：查找所有后代元素

next([expr])：查找紧邻的下一个元素

**nextAll()**：查找紧邻的后面的所有元素

prev([expr])：查找紧邻的上一个元素

**prevAll()**：查找紧邻的前面的所有元素

parent([expr])：查找当前元素的父元素

siblings([expr])：查找所有同级兄弟节点（无论上下）

# each方法

遍历jquery对象

$(m).each(function(i,item){}

# ajax交互

基本格式：

​				$.ajax({
​					url:'demo.json',
​					type:'get',
​					dataType:'json',
​					success:function(m){}

m为交互返回的数据

常见参数：

url:请求的页面

type:http请求，通常为get或post

dataType:期待的返回值类型，常见为text，xml或json，默认为text

success:当ajax成功请求时返回数据后的回调操作

不常用：

ajax方法只有一个参数，要求是一个json对象

async：是否异步，默认其值为true 

cache ：是否缓存，默认其值为true ,get

complete ：当Ajax状态码为4时，所触发的回调函数

contentType：请求头信息，如果是post请求，默认是，

# VUE框架

格式：

var app = new Vue({

​		el:'#app',  // 绑定id

​		data:{

​				变量

​		}，

​		methods:{

​				函数集

​		}

})