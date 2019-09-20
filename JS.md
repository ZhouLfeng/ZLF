# JS

#### 数据类型

基本：字符型，数值型，布尔型，空类型，未定义型

复合：数组型，对象型，函数型

document.wirte：将打印内容输出到body中

文本对象:浏览器中的主体部分，document控制所有文本对象(标签)

窗口对象:浏览器头部信息

window.alert：弹出警告对话框，前面的window可省略

window.prompt：弹出对话框输入

console.log：打印警告对话框输出至控制台中

var 变量名：定义变量

console.info：将变量输出至控制台

三元表达式：  ？  ：

字符串进行除+以外的运算会生成一个NAN类型

NaN加上任何数值类型还是NaN，加上字符串会按字符串的+法计算

NaN == NaN结果为false

NaN判断布尔值为false

null判断布尔值为false    转换为整型为0

undefined判断为false   转换为整型为NaN

#### 转换类型

Number：转化为整型，有字母转化为NaN

String：转化为字符串

Boolean：转化为布尔值

ParseInt：强制转化为整型，100px-->100、100.123b-->100

ParsetFloat：强制转化为浮点型，100.123b-->100.123

== ：只检查值是否相等

===：全等于，检查值和类型是否都相等，JS中判断默认用全等于

！==：不全等于

typeof：数据类型查找

eval：对象还原，寻找已存在的对象

#### 调用类

调用类时前面要加new关键字

python：while循环可以加else

js：while循环不能加else

测量数组长度：length

var a = new Array();

console.log(a.length)

数组追加：push

删除数据：delete

### 延时器

setTimeout()——设定延时器

var timer = window.setTimeout(code,millisec)

clearTimeout()——清除延时器变量

window.clearTimeout(timer)

 <!DOCTYPE html>
<html>
	<head>
		<meta charset="utf-8">
		<title></title>
		<script type="text/javascript">
			var i=0;
			var timer=0;
			function start2(){
				var inputObj = document.getElementById("result");
				inputObj.value = "当前计时:"+i+"秒";
				i++;
				timer = window.setTimeout("start2()",1000);
				document.getElementById("start").disabled = true;
				document.getElementById("stop").disabled = false;
			}
			function stop2(){
				window.clearTimeout(timer);
				document.getElementById("start").disabled = false;
				document.getElementById("stop").disabled = true;
				i=0;
			}
		</script>
	</head>
	<body>
		<input type="botton" id="result" value="当前计时:0秒"><br />
		<input type="submit" id="start" value="开始" onClick="start2()">
		<input type="submit" id="stop" value="停止" onClick="stop2()" disabled>
	</body>
</html>

### 定时器

setInterval()--每隔指定的毫秒值，执行JS程序一次(周期性执行)。

var timer = window.setInterval(code,millisec)

code为JS函数或对象方法，millisec为毫秒值

返回值：返回定时器的变量id，是一个整型。用来被clearInterval() 清除。

clearInterval()——清除定时器变量

window.clearInterval(timer)

<!DOCTYPE html>
<html>
	<head>
		<meta charset="utf-8">
		<title></title>
		<script type="text/javascript">
			var timer;
			var i = 1;
			function open2(){
				window.clearInterval(timer);
				timer = window.setInterval("start2()",1000);
			}
			function start2(){
				var inputObj = document.getElementById("result");
				inputObj.value = "当前计时:"+i+"秒";
				i++;
			}
			function stop2(){
				window.clearInterval(timer);
			}
		</script>
	</head>
	<body>
		<input id='result' type="botton" value="当前计时:0秒"><br>
		<input type="submit" value="开始" onClick="open2()">
		<input type="submit" value="停止" onClick="stop2()">
	</body>
</html>

### String对象

length属性--动态获取字符串的长度。

var len = strObj.length



toLowerCase()和toUpperCase()

strObj.toLowerCase() 将字母转成全小写。

strObj.toUpperCase() 将字母转成全大写。



charAt(index)----返回字符串中指定下标处的一个字符。

strObj.charAt(index)

index是指字符的下标。strObj是原字符串。

返回值：字符型的数据。如果参数 index 不在 0 与 string.length 之间，该方法将返回一个空字符串。





indexOf()

在原始字符串，从左往右查找指定的字符串，如果找到，返回其下标值。如果没有找到，返回-1。



strObj.indexOf(substr)

substr就是要查找的子字符串。

只查找第一次出现的字符，第二个相同的不再查找。



lastIndexOf()

在原始字符串，从右往左查找指定的字符。只查找第一次出现的字符，第二个相同的不再查找。

strObj.lastIndexOf(substr)

返回值：如果找到返回对应的索引值，如果没有找到，返回-1。



substr()

从原始字符串，提取指定的子字符串。

strObj.substr(startIndex [ , length])

startIndex是要查找的子字符串的开始位置(索引号)。

length可选项。从startIndex处往后提取length个字符。如果length省略，则一直提取到结尾。



substring()

从原始字符串，提取指定的子字符串。

strObj.substring(startIndex [ , endIndex])

startIndex是要查找的子字符串的开始位置(索引号)。

endIndex可选项。从startIndex到endIndex处的所有字符。如果endIndex省略，则一直提取到结尾。

左闭右开



 split()——将字符串转成数组

将一个字符串切成若干段，将一个字符串分割成一个数组。

array strObj.split(separator)

separator是一个字符串的分割符，可以为空字符串。

返回一个数组。



### Array对象

length属性

动态获取数组的长度，也就是元素的总个数。

var len = arrObj.length

join()

将一个数组各元素，用指定的连接号，连成一个字符串。

string arrObj.join(separator)

separator代表元素之间的连接号。



添加和删除数组元素

 delete删除元素的值，而下标还在(长度不会减少)。

push从后面插入新的元素。

shift()删除第1个数组元素，数组长度减1。并返回删除元素的值。

 pop()删除最后1个数组元素，数组长度减1。并返回删除元素的值。



### **Math数学对象**

Math.PI：圆周率

Math.abs()绝对值。如：Math.abs(-9) = 9

ceil()向上取整(整数加1，舍去小数)。如：Math.ceil(9.23) = 10 、Math.ceil(9.98) = 10

floor()向下取整(舍去小数)。如：Math.floor(9.87) = 9

round()四舍五入。如：Math.round(9.8)=10  Math.round(9.4) = 9

pow()幂次数。如：Math.pow(2,4) = 16

sqrt()开方。如：Math.sqrt(9) = 3 

random()返回0-1之间的随机小数。Math.random() = 0.9026920931341323

toFixed(2) 属于数值对象，保留小数点后面的几位数




