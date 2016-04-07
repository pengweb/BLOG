---
title: javascript--学习笔记(初级)
date: 2016-03-21 23:48:57
tags: [javascript,js]

---
&nbsp;

字符
charAt()-----获取指定位置的字符
split()-----分割字符串行程数组，肯定是以，分割， “”里边为空的时候每个字符都隔开用
substring()-----截取下标从哪里到哪里的中间元素，有两种一种是说他的长度是多少（脚标）
substr()-----从开始计数的总长度（长度）

indexOf-----获取某字符或字符串的出现的位置 是通过字符获得位置（可以设置起始位置）

Math.random()-----0-1之间随机排列
Math.round()-----四舍五入
Math.abs()-----绝对值

数组
concat()-----把两个不同数组合并成一个数组，用，隔开
join()-----把所有数组放入一个字符串中 中间用符号隔开 符号可以设置
pop()-----删除并返回最后一个元素
push()-----向最后一个位置添加一个数组
revrese()-----颠倒数组顺序
shift()-----删除第一个数组
slice()-----抽出一段位置内的数组
sort()-----数组进行排序
splice()-----删除一个元素并向数组添加一个新元素 相当于替换（这个没有例子不知道对不对）

setInterval()-----计时器
clearInterval()-----取消计时器
setTimeout()-----一般用来做计数器

History
back()-----浏览器历史后退一下
forward()-----前进一下
go()-----去指定的页面

Location
assign()-----当前页面打开新页面
reload()-----重新刷新一下当前页面
replace()-----当页刷新页面变到新页面 但是在本标签内完成 不触发新标签

Navigator
userAgent-----获得浏览器信息

getAttribute()-----获得某节点的属性值
setAttribute()-----设置某节点的属性值

nodeName-----节点名称
nodeValue-----节点值
nodeType-----节点类型

childNodes-----获得子节点
parentNode-----获得父节点
nextSibling-----获得兄弟节点之后
previousSibling-----获得兄弟节点之前

createElement-----创建一个节点元素
createTextNode-----创建一个节点文本
appendChild()-----创建一个末位的子节点
insertBefore()-----创建一个第一位的子节点 或者去指定一个节点之前的一个节点
removeChild()-----删除某个子节点
replaceChild()-----替换一个子节点

scrollHeight-----当前窗口的宽和高
offsetHeight-----当前区块高度

<hr />

&nbsp;

&nbsp;

<hr />

&nbsp;

&lt;script src=”xxx.js”&gt;&lt;/script&gt;

&nbsp;

所有的变量前都要加var

&nbsp;

var str = "abc\"def\"ghi"
用反斜杠来禁止解析双引号。

&nbsp;

确认：var  mychar=confirm（“你想去”）后边接if····else语句

提问：prompt   用法同上
<div>
<p align="left"><strong>语法:</strong></p>

<pre class="code"><strong>prompt(str1, str2);</strong></pre>
</div>
<p align="left"><strong>参数说明：</strong></p>

<div>
<pre class="code">str1: 要显示在消息对话框中的文本，不可修改
str2：文本框中的内容，可以修改</pre>
</div>
<strong>返回值:</strong>
<div>
<pre class="code">1. 点击确定按钮，文本框中的内容将作为函数返回值
2. 点击取消按钮，将返回<strong>null</strong></pre>
</div>
看看下面代码:
<div>
<pre lang="php">var myname=prompt("请输入你的姓名:","默认文本框的字例：小明");
if(myname!=null)
  {   alert("你好"+myname); }
else
  {  alert("你好 my friend.");  }
</pre>
</div>
打开新窗口：window.open

关闭窗口：window.close

innerHTML：语法：Object.innerHTML或者直接用+来插入

获取ID：语法：document.getElementById("")

改变css样式：语法Object.style.color=“red”

显示和隐藏：语法Object.style.display=“none”是隐藏    “block”是显示

改变控制类名   Object.className =要变更为的class名

取消设置：

function qxszdy(){

var qxsz =confirm("你想取消设置吗");

if（qxsz==true）{

var qxsz = document.getElementById("txt");

qxsz.removeAttribute("style");

}else{}

}

<hr />

&nbsp;
<pre class="best-text mb-10"></pre>
&nbsp;
<pre id="best-content-776042059" class="best-text mb-10"><span style="color: #ff0000;">&lt;表达式1&gt;?&lt;表达式2&gt;:&lt;表达式3&gt; </span></pre>
<pre id="best-content-776042059" class="best-text mb-10"><span style="color: #ff0000;">a=(b&gt;0)?b:-b; </span>
<span style="color: #ff0000;">当b&gt;0时，a=b；当b不大于0时，a=-b；这就是条件表达式。其实上面的意思就是把b的绝对值赋值给a。 </span>

</pre>
&nbsp;

操作符：

++是自加1的意思

--是自减1的意思

注意：

a++ ： 把（a++）作为一个整体表达式，a 的值虽然自增1，但是整个表达式的值是取 a自增 之前 的值；

++a : 也把（++a）作为一个整体表达式，a 的值也自增1，但是整个表达式的值是取 a 自增 之后 的值。

&nbsp;

+、-、*、/等

==、!=、&lt;、&gt;、&lt;=、&gt;=等

&amp;&amp;、||、！、等

注意：
<pre id="best-content-749697769" class="best-text mb-10">第一种情况：
a=3;
b=a++;
运行后
第一次b=3，以后a=4

第二种情况：
a=3;
b=++a;
运行后
b=4，a=4

100%7是100对7取余的意思结果是2

</pre>
=符号是赋值的意思

+除了有加的含义还有连接字符串用

&nbsp;
<pre>==用于一般比较，==在比较的时候可以转换数据类型。
</pre>
<pre>2. ===用于严格比较，===严格比较，只要类型不匹配就返回flase。
例子：“1”===1   false</pre>
运算顺序:

按照平时的乘除大于加减来算而且可以通过加减小括号来改变顺序

算术操作符 → 比较操作符 → 逻辑操作符 → "="赋值符号

&nbsp;

&nbsp;

<hr />

&nbsp;

数组：

创建数组语法：var myarray=new Array();

var myarr=new Array(8);  说明存储8个数据

数组赋值：

myarr[0]=1;

myarr[1]=2;

可以把上边简写：

var myarr=new Array(0,1)或者  //创建数组的同时赋值

var myarr=[0,1]                           //直接输入一个数组

&nbsp;

增加新成员直接添加myarr[2]=3;

注意：

1.创建的新数组是空数组，没有值，如输出，则显示undefined。
2.虽然创建数组时，指定了长度，但实际上数组都是变长的，也就是说即使指定了长度为8，仍然可以将元素存储在规定长度以外。

&nbsp;

获取数组长度；

语法：myarray.length；  可以直接获取长度myarray是变量可以随便改

可以修改长度，给他赋值   myarray.length=10;

例：
<pre class="code">var arr=[98,76,54,56,76]; // 包含5个数值的数组
document.write(arr.length); //显示数组的长度5</pre>
<pre class="code">arr[15]=34; //增加元素，使用索引为15,赋值为34 
alert(arr.length); //显示数组的长度16


</pre>
一级数组，我们看成一组盒子，每个盒子只能放一个内容。
<pre class="code">一维数组的表示: myarray[ ]</pre>
二维数组，我们看成一组盒子，不过每个盒子里还可以放多个盒子。
<pre class="code">二维数组的表示: myarray[ ][ ]</pre>
<strong>注意: </strong>二维数组的两个维度的索引值也是从0开始，两个维度的最后一个索引值为长度-1。

<strong>1. 二维数组的定义方法一</strong>
<pre class="code">var myarr=new Array();  //先声明一维 
for(var i=0;i&lt;2;i++){   //一维长度为2
   myarr[i]=new Array();  //在声明二维 
   for(var j=0;j&lt;3;j++){   //二维长度为3
   myarr[i][j]=i+j;   // 赋值，每个数组元素的值为i+j
   }
 }</pre>
<strong>注意: </strong>关于for 循环语句，请看第四章4-5 。

将上面二维数组，用表格的方式表示:

<a href="http://www.pengweb.net/wp-content/uploads/2015/02/537957a20001c24c03200210.jpg"><img class="attachment-medium" src="http://www.pengweb.net/wp-content/uploads/2015/02/537957a20001c24c03200210-300x197.jpg" alt="537957a20001c24c03200210" width="300" height="197" /></a>

2. <strong>二维数组的定义方法二</strong>

var Myarr = [[0 , 1 , 2 ],[1 , 2 , 3, ]]

重点：从外往里是一维--二维

<strong>3. 赋值</strong>

myarr[0][1]=5; //将5的值传入到数组中，覆盖原有值。

<strong>说明:</strong> myarr[0][1] ,0 表示表的行，1表示表的列。

<hr />

循环：

结束循环用break;  结束所有循环

continue：  跳过标有continue的语句

&nbsp;
<h2 id="J_CodeLang" class="code-head" data-lang="Javascript">多重判断（if..else嵌套语句）</h2>
<span style="color: #ff0000;">注意：一定是在else里再进行多重判断不能if里再加if，而是else里加if</span>
<div id="J_CodeDescr" class="code-description">
<div class="code-desc co">
<p align="left">要在多组语句中选择一组来执行，使用if..else嵌套语句。</p>
<p align="left"><strong>语法</strong><strong>:</strong></p>

<div>
<pre class="code"><strong>if(</strong>条件1<strong>)</strong>
{ 条件1成立时执行的代码}
<strong>else  if(</strong>条件2<strong>)</strong>
{ 条件2成立时执行的代码}
...
<strong>else  if(</strong>条件n<strong>)</strong>
{ 条件n成立时执行的代码}
<strong>else</strong>
{ 条件1、2至n不成立时执行的代码}</pre>
</div>
<p align="left">假设数学考试，小明考了86分，给他做个评价，60分以下的不及格，60(包含60分)-75分为良好，75(包含75分)-85分为很好，85(包含75分)-100优秀。</p>
<p align="left"><strong>代码表示如下</strong><strong>:</strong></p>
<p align="left"><a href="http://www.pengweb.net/wp-content/uploads/2015/02/541799000001aada05260280.jpg"><img class="attachment-medium" src="http://www.pengweb.net/wp-content/uploads/2015/02/541799000001aada05260280-300x160.jpg" alt="541799000001aada05260280" width="300" height="160" /></a></p>

<div>
<p align="left"><strong>结果:</strong></p>
<p align="left"><a href="http://www.pengweb.net/wp-content/uploads/2015/02/52d121a70001de7503470226.jpg"><img class="attachment-medium" src="http://www.pengweb.net/wp-content/uploads/2015/02/52d121a70001de7503470226-300x195.jpg" alt="52d121a70001de7503470226" width="300" height="195" /></a></p>

</div>
</div>
</div>
<h2 id="J_CodeLang" class="code-head" data-lang="Javascript">多种选择（Switch语句)</h2>
<div id="J_CodeDescr" class="code-description">
<div class="code-desc co">
<p align="left">当有很多种选项的时候，switch比if else使用更方便。</p>
<p align="left"><strong>语法:</strong></p>

<div>
<pre class="code"><strong>switch(</strong><strong>表达式)</strong>
{
<strong>case</strong><strong>值1:</strong>
  执行代码块 1
<strong>  break;</strong>
<strong>case</strong><strong>值2:</strong>
  执行代码块 2
  <strong>break;</strong>
<strong>...</strong>
<strong>case</strong><strong>值n:</strong>
  执行代码块 n
 <strong> break;</strong>
<span style="color: #ff0000;"><strong>default:                       如果上边都不对则运行这条</strong></span>
  与 case值1 、 case值2...case值n 不同时执行的代码
}</pre>
<p align="left">假设评价学生的考试成绩，10分满分制，我们按照每一分一个等级将成绩分等，并根据成绩的等级做出不同的评价。</p>

<div>
<p align="left"><strong>代码如下:</strong></p>
<p align="left"><a href="http://www.pengweb.net/wp-content/uploads/2015/02/52d1293c0001394705510767.jpg"><img class="attachment-medium" src="http://www.pengweb.net/wp-content/uploads/2015/02/52d1293c0001394705510767-216x300.jpg" alt="52d1293c0001394705510767" width="216" height="300" /></a></p>
<p align="left"><strong>执行结果:</strong></p>

<pre class="code"><strong>评语: 及格，加油!</strong></pre>
</div>
</div>
</div>
</div>
<h2 id="J_CodeLang" class="code-head" data-lang="Javascript">继续循环continue（可以用来做跳过某条操作）</h2>
<div id="J_CodeDescr" class="code-description">
<div class="code-desc co">
<p align="left">continue的作用是仅仅跳过本次循环，而整个循环体继续执行。</p>
<p align="left"><strong>语句结构：</strong></p>

<div>
<p class="code"><strong>for</strong>(初始条件;判断条件;循环后条件值更新) { if(特殊情况) { <strong>continue;</strong> } 循环代码 } 上面的循环中，当特殊情况发生的时候，本次循环将被跳过，而后续的循环则不会受到影响。好比输出10个数字，如果数字为5就不输出了。 do while结构的基本原理和while结构是基本相同的，但是它保证循环体至少被执行一次。因为它是先执行代码，后判断条件，如果条件为真，继续循环。</p>
<strong>函数调用：</strong>
<p class="code">function compare(x,y){
if(x&gt;y){
return x;
}
else if(x=y){
return x;
}else{
return y;
}
}</p>
x和y是变量是外界给的变量
compare(5,6)

&nbsp;
<h1><span style="color: #ff0000;">for循环和for in循环【for in 也可以进行<span style="color: #0000ff;">遍历</span>】</span></h1>
var x=[1,2,3,4]

for(y in x){

document.write(x[y]);

}

显示结果是1，2，3，4

这里的y并不是1，2，3，4

而是从0开始  位置
<h3><span style="color: #0000ff;"> 例题：</span><span style="color: #ff0000;">var obj = {a:1,b:2,c:3}现在想遍历这个JS对象中的 a,b,c</span></h3>
<pre id="best-content-360417656" class="best-text mb-10">&lt;script&gt;
var obj = {a:1,b:2,c:3}

for(var s in obj)
 alert(obj[s]);
&lt;/script&gt;</pre>

<hr />

<pre class="code"><a href="http://www.pengweb.net/wp-content/uploads/2015/02/53d1c6ed000151aa04190327.jpg"><img class="attachment-medium" src="http://www.pengweb.net/wp-content/uploads/2015/02/53d1c6ed000151aa04190327-300x234.jpg" alt="53d1c6ed000151aa04190327" width="300" height="234" />

月份和星期都是从0开始，调用的时候要+1

</a>
为了避免0-10在<span style="color: #ff0000;">显示的时候长短会变化</span>所以可以用到判断语句
var today=new Date();
var m=today.getMinutes();
m=checktime(m);
function checktime(){
if(i&lt;0){
i="0"+i;
return i;
}return i;
}

</pre>

<hr />
<p align="left"><strong>主要事件表:</strong></p>
<p align="left"><a href="http://img.mukewang.com/53e198540001b66404860353.jpg"><img src="http://img.mukewang.com/53e198540001b66404860353.jpg" alt="" /></a></p>

<pre class="code">关闭网页弹出：
window.onunload = onunload_message; 
 function onunload_message(){ 
 alert("您确定离开该网页吗？"); 
 } 


</pre>
<h2 id="J_CodeLang" class="code-head" data-lang="Javascript">鼠标经过事件（onmouseover）</h2>
<div id="J_CodeDescr" class="code-description">
<div class="code-desc co">

鼠标经过事件，当鼠标移到一个对象上时，该对象就触发onmouseover事件，并执行onmouseover事件调用的程序。

现实鼠标经过"确定"按钮时，触发onmouseover事件，调用函数info()，弹出消息框，代码如下:

&nbsp;

&nbsp;

注意：上边这个info（）也可以写成info(this);

那个函数里边可以有很多种变化，想插入文字什么的

function info(obj){

obj.innerHTML="哈哈哈哈"

或者改变背景颜色

obj.style.backgroun="#000"}

等等·····根据情况改变

还有在后边用到了

function haha(obj){

obj.onmouseover=function(){}

obj.onmouseout=function(){}

等等等事件情况

}

然后在js中或者for循环中直接运行haha（）

<strong>运行结果:</strong>

<a href="http://www.pengweb.net/wp-content/uploads/2015/02/53e196fd00017d8704870416.jpg"><img class="attachment-medium" src="http://www.pengweb.net/wp-content/uploads/2015/02/53e196fd00017d8704870416-300x256.jpg" alt="53e196fd00017d8704870416" width="300" height="256" /></a>

</div>
</div>

<hr />

<pre class="code">简单计算器：
&lt;script type="text/javascript"&gt;
function count(){
 var x,y,sh;
 x=parseInt(document.getElementById("srk1").value);
 y=parseInt(document.getElementById("srk2").value);
 z=document.getElementById("xx").value;
 switch(z){
 case "+":
 sh=x+y;
 break;
 case "-":
 sh=x-y;
 break;
 case "*":
 sh=x*y;
 break;
 default:
 sh=x/y;
 }
 document.getElementById("jgs").value=sh;
 }
&lt;/script&gt;

 &lt;input type="text" value="这里输入x" id="srk1" /&gt;
 &lt;select id="xx" multiple="multiple"&gt;
 &lt;option value="+"&gt;+&lt;/option&gt;;
 &lt;option value="-"&gt;-&lt;/option&gt;;
 &lt;option value="*"&gt;*&lt;/option&gt;;
 &lt;option value="/"&gt;/&lt;/option&gt;;
 &lt;/select&gt;
 &lt;input type="text" value="这里输入y" id="srk2" /&gt;
 &lt;input type="button" value="=" onclick="count()"/&gt;
 &lt;input type="text" value="这里输出结果sh" id="jgs" /&gt;

注意</pre>
<pre class="code">parseInt  这个用来命名是十进制
value  这里要善用这个语句取值

</pre>

<hr />

<pre class="code">对象：
Date/Array/String原理都是和数组是一样的 可以套用数组

Date：</pre>
<p align="left"><strong>访问方法语法：</strong>“&lt;日期对象&gt;.&lt;方法&gt;”</p>
<p align="left">Date对象中处理时间和日期的常用方法：</p>
<p align="left">::__IHACKLOG_REMOTE_IMAGE_AUTODOWN_BLOCK__::4</p>
<p align="left">注意：一定要先定义一下现在时间</p>
<p align="left">var mydate=new Date();</p>
<p align="left">后边可以进行其他处理</p>
<p align="left">获取年份mydate.getFullYear()</p>
<p align="left">星期用数组：</p>
<p align="left">先定义星期数组var datearr=["星期日"，"星期一"·······"星期六"]</p>
<p align="left">var mydate1=mydate.getDate();</p>
<p align="left">输出datearr[mydate1]</p>

<h2 id="J_CodeLang" class="code-head" data-lang="Javascript">String 字符串对象</h2>
定义字符串的方法就是直接赋值。比如：
<pre class="code">var mystr = "I love JavaScript!"</pre>
<p align="left"><strong>访问字符串对象的属性length:</strong></p>
stringObject.length; 返回该字符串的长度。
<div>
<pre class="code">var mystr="Hello World!";
var myl=mystr.<code>length</code>;

属性长度用length
都变大写用：toUpperCase()
都变小写：toLowerCase()


</pre>
<h2 id="J_CodeLang" data-lang="Javascript">返回指定位置的字符</h2>
<div id="J_CodeDescr">
<p align="left">charAt() 方法可返回指定位置的字符。返回的字符是长度为 1 的字符串。</p>
<p align="left">语法:</p>

<div>
<pre>stringObject.charAt(index)</pre>
<p align="left">注意：1.字符串中第一个字符的下标是 0。最后一个字符的下标为字符串长度减一（string.length-1）。</p>
<p align="left">2.如果参数 index 不在 0 与 string.length-1 之间，该方法将返回一个空字符串。</p>
<p align="left">如:在字符串 "I love JavaScript!" 中，返回位置2的字符：</p>

<div>
<pre>&lt;script type="text/javascript"&gt;
  var mystr="I love JavaScript!"
  document.write(mystr.charAt(2));
&lt;/script&gt;</pre>
<p align="left">注意：一个空格也算一个字符。</p>
<p align="left">以上代码的运行结果：</p>

<div>
<pre>l

</pre>
<h3 align="left"><span style="color: #ff0000;">indexOf() </span></h3>
<h3 align="left"><span style="color: #ff0000;">方法可返回某个指定的字符串值在字符串中首次出现的位置,输出值是0-length-1。</span></h3>
<p align="left">可以根据判断是否有这个字符串来判断是否含这个字符串</p>
<p align="left"><span style="color: #0000ff;">不存在返回-1；</span></p>
<p align="left">indexOf（“word”）  查这个字符串是否存在，是否&gt;0</p>
<p align="left"><strong>语法</strong></p>

<div>
<pre class="code">stringObject.indexOf(substring, startpos)


<strong><span style="color: #ff0000;">match:内容匹配</span></strong>
srt.match(“world”)
查world是否存在，如果存在就直接打印出来，如果不存在返回一个空null

</pre>
<h2 class="code-head" data-lang="Javascript"><span style="color: #ff0000;">replace  替换字符串</span></h2>
str.replace(“word”，“hahaha”)

将word替换成hahah
<h2 id="J_CodeLang" class="code-head" data-lang="Javascript">字符串分割split()</h2>
<div id="J_CodeDescr" class="code-description">
<div class="code-desc co">

<strong>知识讲解：</strong>

split() 方法将字符串分割为字符串数组，并返回此数组。
<h3><strong>语法：</strong></h3>
<div>
<pre class="code">stringObject.split(separator,limit)</pre>
<h3><strong>参数说明:</strong></h3>
<strong><a href="http://www.pengweb.net/wp-content/uploads/2015/02/532bee4800014c0404230108.jpg"><img class="attachment-medium" src="http://www.pengweb.net/wp-content/uploads/2015/02/532bee4800014c0404230108-300x77.jpg" alt="532bee4800014c0404230108" width="300" height="77" /></a></strong>

<strong>注意：</strong>如果把空字符串 ("") 用作 separator，那么 stringObject 中的每个字符之间都会被分割。

<strong>我们将按照不同的方式来分割字符串：</strong>

使用指定符号分割字符串，代码如下:
<div>
<pre class="code">var mystr = "www.imooc.com";
document.write(mystr.split(".")+"&lt;br&gt;");
document.write(mystr.split(".", 2)+"&lt;br&gt;");</pre>
<strong>运行结果:</strong>
<div>
<pre class="code">www,imooc,com
www,imooc</pre>
</div>
</div>
</div>
</div>
</div>
<pre class="code"></pre>
如果中间是空格，那（）里打空格就行，就把空格变成逗号了
<h2 id="J_CodeLang" class="code-head" data-lang="Javascript">提取字符串substring()</h2>
&nbsp;
<div id="J_CodeDescr" class="code-description">
<div class="code-desc co">substring() 方法用于提取字符串中介于两个指定下标之间的字符。 <strong>语法:</strong>
<pre class="code">stringObject.substring(starPos,stopPos)</pre>
<strong>参数说明:</strong>

<a href="http://www.pengweb.net/wp-content/uploads/2015/02/532bf1bb000151af04450082.jpg"><img class="attachment-medium" src="http://www.pengweb.net/wp-content/uploads/2015/02/532bf1bb000151af04450082-300x55.jpg" alt="532bf1bb000151af04450082" width="300" height="55" /></a>

<strong>注意：</strong>

1. 返回的内容是从 start开始(包含start位置的字符)到 stop-1 处的所有字符，其长度为 stop 减start。

2. 如果参数 start 与 stop 相等，那么该方法返回的就是一个空串（即长度为 0 的字符串）。

3. 如果 start 比 stop 大，那么该方法在提取子串之前会先交换这两个参数。

使用 substring() 从字符串中提取字符串，代码如下：
<div>
<pre class="code">&lt;script type="text/javascript"&gt;
  var mystr="I love JavaScript";
  document.write(mystr.substring(7));
  document.write(mystr.substring(2,6));
&lt;/script&gt;</pre>
<strong>运行结果</strong><strong>:</strong>
<pre class="code">JavaScript
love


</pre>
<h1>JS中substr和substring的用法和区别</h1>
&nbsp;

<strong>示例代码</strong>

var str = "I love JS!";// 有一个str字符串，如想获取JS子字符串，用两种方法如何实现。
str.substr(7, 2); // 获取子字符串。

str.substring(7, 9); // 获取子字符串。

<strong>结果:  JS</strong>

<strong>区别:第二参数，substr第二个参数是获取子字符串的长度，substring第二个参数是获取子字符串的结束位置</strong>

&nbsp;

&nbsp;
<h2 id="J_CodeLang" class="code-head" data-lang="Javascript">返回指定的字符串首次出现的位置</h2>
<div id="J_CodeDescr" class="code-description">
<div class="code-desc co">
<p align="left">indexOf() 方法可返回某个指定的字符串值在字符串中首次出现的位置。</p>
<p align="left"><strong>语法</strong></p>

<div>
<pre class="code">stringObject.indexOf(substring, startpos)</pre>
</div>
<p align="left"><strong>参数说明：</strong></p>
<p align="left"><a href="http://www.pengweb.net/wp-content/uploads/2015/02/53853d4200019feb04920149.jpg"><img class="attachment-medium" src="http://www.pengweb.net/wp-content/uploads/2015/02/53853d4200019feb04920149-300x91.jpg" alt="53853d4200019feb04920149" width="300" height="91" /></a>
<strong>说明：</strong></p>
<p align="left">1.该方法将从头到尾地检索字符串 stringObject，看它是否含有子串 substring。</p>
<p align="left">2.可选参数，从stringObject的startpos位置开始查找substring，如果没有此参数将从stringObject的开始位置查找。</p>
<p align="left">3.如果找到一个 substring，则返回 substring 的第一次出现的位置。stringObject 中的字符位置是从 0 开始的。</p>
<p align="left"><strong>注意：</strong>1.indexOf() 方法区分大小写。</p>
<p align="left">2.如果要检索的字符串值没有出现，则该方法返回 -1。</p>
<p align="left">例如: 对 "I love JavaScript!" 字符串内进行不同的检索：</p>

<div>
<pre class="code">&lt;script type="text/javascript"&gt;
  var str="I love JavaScript!"
  document.write(str.indexOf("I") + "&lt;br /&gt;");
  document.write(str.indexOf("v") + "&lt;br /&gt;");
  document.write(str.indexOf("v",8));
&lt;/script&gt;</pre>
以上代码的输出：
<div>
<pre class="code">0
4
9

注意：要熟练应用indexOf（）找到位置然后配合substr一起来选数组中的数字
记得用parseInt  来讲字符转换成十进制

</pre>
</div>
</div>
</div>
</div>
<h2 id="J_CodeLang" class="code-head" data-lang="Javascript">Math对象</h2>
<div id="J_CodeDescr" class="code-description">
<div class="code-desc co">

Math对象，提供对数据的数学计算。

使用 Math 的属性和方法，代码如下：
<h3></h3>
<div>
<pre class="code">&lt;script type="text/javascript"&gt;
  var mypi=Math.PI; 
  var myabs=Math.abs(-15);
  document.write(mypi);
  document.write(myabs);
&lt;/script&gt;</pre>
<strong>运行结果</strong><strong>:</strong>
<div>
<pre class="code">3.141592653589793
15</pre>
<strong>注意：</strong>Math 对象是一个固有的对象，无需创建它，直接把 Math 作为对象使用就可以调用其所有属性和方法。这是它与Date,String对象的区别。

Math 对象属性

<span lang="EN-US"><a href="http://www.pengweb.net/wp-content/uploads/2015/02/532fe7cf0001e7b505170269.jpg"><img class="attachment-medium" src="http://www.pengweb.net/wp-content/uploads/2015/02/532fe7cf0001e7b505170269-300x156.jpg" alt="532fe7cf0001e7b505170269" width="300" height="156" /></a></span>

Math 对象方法

<a href="http://www.pengweb.net/wp-content/uploads/2015/02/532fe841000174db05160622.jpg"><img class="attachment-medium" src="http://www.pengweb.net/wp-content/uploads/2015/02/532fe841000174db05160622-249x300.jpg" alt="532fe841000174db05160622" width="249" height="300" /></a>
<pre class="code">Math.random();</pre>
<strong>注意：</strong>返回一个大于或等于 0 但小于 1 的符号为正的数字值。

<strong>注意</strong><strong>:</strong>因为是随机数，所以每次运行结果不一样，但是0 ~ 1的数值。
<p align="left">获得0 ~ 10之间的随机数，代码如下:</p>

<div>
<pre class="code"><span style="color: #ff0000;">&lt;script type="text/javascript"&gt;
  document.write(Math.random()*10);
&lt;/script&gt;
<span style="color: #0000ff;">一般输出的不是整数都带小数，所以一般都是写成</span></span></pre>
<pre class="code"><span style="color: #ff0000;">&lt;script type="text/javascript"&gt;
  document.write(<span style="color: #0000ff;">parseInt</span>(Math.random()*10));
&lt;/script&gt;



<span style="color: #000000;">在比较大小的时候</span>
Math.min(1,2,3,4)
<span style="color: #000000;">可以直接在min后边输入</span></span></pre>
<h2 id="J_CodeLang" class="code-head" data-lang="Javascript">Array 数组对象</h2>
<p align="left"><strong>数组属性：</strong></p>
length 用法：&lt;数组对象&gt;.length；返回：数组的长度，即数组里有多少个元素。它等于数组里最后一个元素的下标加一。

<strong>数组方法：</strong>

<a href="http://www.pengweb.net/wp-content/uploads/2015/02/533295ab0001dead05190599.jpg"><img class="attachment-medium" src="http://www.pengweb.net/wp-content/uploads/2015/02/533295ab0001dead05190599-260x300.jpg" alt="533295ab0001dead05190599" width="260" height="300" /></a>

&nbsp;

concat() 方法用于连接两个或多个数组。此方法返回一个新数组，不改变原来的数组。

<strong>语法</strong>
<pre class="code">arrayObject.concat(array1,array2,...,arrayN)


</pre>
<h2 id="J_CodeLang" class="code-head" data-lang="Javascript">指定分隔符连接数组元素join()</h2>
<div id="J_CodeDescr" class="code-description">
<div class="code-desc co">

join()方法用于把数组中的所有元素放入一个字符串。元素是通过指定的分隔符进行分隔的。

<strong>语法：</strong>
<div>
<pre class="code">arrayObject.join(分隔符)</pre>
<p align="left"><strong>参数说明:</strong></p>
<a href="http://www.pengweb.net/wp-content/uploads/2015/02/533297ff0001516905150059.jpg"><img class="attachment-medium" src="http://www.pengweb.net/wp-content/uploads/2015/02/533297ff0001516905150059-300x34.jpg" alt="533297ff0001516905150059" width="300" height="34" /></a>

注意：返回一个字符串，该字符串把数组中的各个元素串起来，用&lt;分隔符&gt;置于元素与元素之间。这个方法不影响数组原本的内容。 我们使用join（）方法，将数组的所有元素放入一个字符串中，代码如下：
<div>
<pre class="code">&lt;script type="text/javascript"&gt;
  var myarr = new Array(3);
  myarr[0] = "I";
  myarr[1] = "love";
  myarr[2] = "JavaScript";
  document.write(myarr.join());
&lt;/script&gt;</pre>
<strong>运行结果：</strong>
<div>
<pre class="code">I,love,JavaScript


</pre>
<h2 id="J_CodeLang" class="code-head" data-lang="Javascript">颠倒数组元素顺序reverse()</h2>
<div id="J_CodeDescr" class="code-description">
<div class="code-desc co">
<p align="left">reverse() 方法用于颠倒数组中元素的顺序。</p>
<p align="left"><strong>语法：</strong></p>

<div>
<pre class="code">arrayObject.reverse()</pre>
</div>
<strong>注意：</strong>该方法会改变原来的数组，而不会创建新的数组。

定义数组myarr并赋值，然后颠倒其元素的顺序：
<div>
<pre class="code">&lt;script type="text/javascript"&gt;
  var myarr = new Array(3)
  myarr[0] = "1"
  myarr[1] = "2"
  myarr[2] = "3"
  document.write(myarr + "&lt;br /&gt;")
  document.write(my<code>arr.reverse()</code>)
&lt;/script&gt;</pre>
</div>
<strong>运行结果：</strong>
<div>
<pre class="code">1,2,3
3,2,1


记住：所有的end都只显示到end前一位就停止不用显示end位的数值



</pre>
<h2 id="J_CodeLang" class="code-head" data-lang="Javascript">数组排序sort()</h2>
<div id="J_CodeDescr" class="code-description">
<div class="code-desc co">
<p align="left"><strong>sort()</strong>方法使数组中的元素按照一定的顺序排列。</p>

<div>
<pre class="code">&lt;script type="text/javascript"&gt;
 <span style="color: #ff0000;"> function sortNum(a,b) {
  return a - b;
 //升序，如降序，把“a - b”该成“b - a”
}</span>
 var myarr = new Array("80","16","50","6","100","1");
  document.write(myarr + "&lt;br&gt;");
  document.write(myarr.sort(sortNum));
<span style="color: #ff0000;">//如果是document.write(myarr.sort()); 那么他默认是从小到大的顺序的，不用写一个函数的</span></pre>
<pre class="code">&lt;/script&gt;</pre>
</div>
<strong>运行结果：</strong>
<div>
<h3 class="code">80,16,50,6,100,1 1,6,16,50,80,100</h3>
<span style="color: #ff0000;"><strong>push</strong>是在数组最后一位再添加一个数组</span>
<span style="color: #ff0000;">x.push(“数组的值”)</span>

&nbsp;
<h2 id="J_CodeLang" class="code-head" data-lang="Javascript">选定元素slice()</h2>
<div id="J_CodeDescr" class="code-description">
<div class="code-desc co">

slice() 方法可从已有的数组中返回选定的元素。

<strong>语法</strong>
<div>
<pre class="code">arrayObject.slice(start,end)</pre>
<strong>参数说明：</strong>

<a href="http://www.pengweb.net/wp-content/uploads/2015/02/533299680001637b05160145.jpg"><img class="attachment-medium" src="http://www.pengweb.net/wp-content/uploads/2015/02/533299680001637b05160145-300x84.jpg" alt="533299680001637b05160145" width="300" height="84" /></a>

1.返回一个新的数组，包含从 start 到 end （不包括该元素）的 arrayObject 中的元素。

2. 该方法并不会修改数组，而是返回一个子数组。

<strong>注意：</strong>

1. 可使用负值从数组的尾部选取元素。

2.如果 end 未被规定，那么 slice() 方法会选取从 start 到数组结尾的所有元素。

3. String.slice() 与 Array.slice() 相似。

我们将创建一个新数组，然后从其中选取的元素，代码如下：
<div>
<pre class="code">&lt;script type="text/javascript"&gt;
  var myarr = new Array(1,2,3,4,5,6);
  document.write(myarr + "&lt;br&gt;");
  document.write(myarr.slice(2,4) + "&lt;br&gt;");
  document.write(myarr);
&lt;/script&gt;</pre>
</div>
<strong>运行结果：</strong>
<div>
<pre class="code">1,2,3,4,5,6
3,4          这上边是4  他是第4个向前看一位
1,2,3,4,5,6


注意：为什么那个老调不出来，是因为自己加了一句var newstar=new Array();  这句话的意思是加一个空数组，是空的，所以后边就没有数值了，所以除了最开始，其他地方不要加这个，不能要这句话，因为这个没有指定


<strong>Splice--删除某个元素替换成新元素，可以不替换</strong></pre>
<pre>&lt;script type="text/javascript"&gt;

var arr = new Array(6)
arr[0] = "George"
arr[1] = "John"
arr[2] = "Thomas"
arr[3] = "James"
arr[4] = "Adrew"
arr[5] = "Martin"

document.write(arr + "&lt;br /&gt;")
<code>arr.splice(2,3,"William")
</code>//删除角标为2的后3个元素（包括角标为2的元素），并且替换成William
document.write(arr)

&lt;/script&gt;</pre>
<pre class="code">
 例题：</pre>
<h2 id="J_CodeLang" class="code-head" data-lang="Javascript">编程练习</h2>
<div id="J_CodeDescr" class="code-description">
<div class="code-desc co">

某班的成绩出来了，现在老师要把班级的成绩打印出来。

<strong>效果图:</strong>
<pre class="code">2014年5月9日 星期六--班级总分为:81</pre>
<strong>格式要求：</strong>

1、显示打印的日期。 格式为类似“2014年03月21日 星期三” 的当前的时间。

2、计算出该班级的平均分（保留整数）。

<strong>同学成绩数据如下：</strong>

"小明:87; 小花:81; 小红:97; 小天:76;小张:74;小小:94;小西:90;小伍:76;小迪:64;小曼:76"

</div>
</div>
<pre class="code">&lt;!DOCTYPE HTML&gt;
&lt;html &gt;
&lt;head&gt;
&lt;meta http-equiv="Content-Type" content="text/html; charset=utf-8" /&gt;
&lt;title&gt;系好安全带,准备启航&lt;/title&gt;

&lt;script type="text/javascript"&gt;

 //通过javascript的日期对象来得到当前的日期，并输出。
var x=new Date();
var xingqi=x.getDay();
var xqsz=["星期日","星期一","星期二","星期三","星期四","星期五","星期六"]；
//这里定义一个星期的数组
document.write(x.getFullYear()+"年"+x.getMonth()+"月"+x.getDate()+xqsz[xingqi]);

 //成绩是一长窜的字符串不好处理，找规律后分割放到数组里更好操作哦
 var scoreStr = "小明:87;小花:81;小红:97;小天:76;小张:74;小小:94;小西:90;小伍:76;小迪:64;小曼:76";
 var newarr=scoreStr.split(";");
 
 //从数组中将成绩撮出来，然后求和取整，并输出。
 sum=0;        注意：一定要声明sum的值    这样的话才能有结果
 for(i=0;i&lt;newarr.length;i++){
 //sum+=parseInt(newarr[i].substring(3));
 var getnum=parseInt(newarr[i].substring(3));
//其实substring(3)是可以通过indexOf来获取的，只是获取这个3的值，以：为参考点来获取这个后一位的位置
 sum=sum+getnum;
 }
 
 jieguo=sum/newarr.length;
 document.write(jiegu);
&lt;/script&gt;
&lt;/head&gt;
&lt;body&gt;
&lt;/body&gt;
&lt;/html&gt;

</pre>

<hr />

<h2 id="J_CodeLang" class="code-head" data-lang="Javascript">window对象</h2>
<div id="J_CodeDescr" class="code-description">
<div class="code-desc co">

window对象是BOM的核心，window对象指当前的浏览器窗口。

<strong>window对象方法:</strong>

<strong><a href="http://www.pengweb.net/wp-content/uploads/2015/02/535483720001a54506670563.jpg"><img class="attachment-medium" src="http://www.pengweb.net/wp-content/uploads/2015/02/535483720001a54506670563-300x253.jpg" alt="535483720001a54506670563" width="300" height="253" /></a></strong>

&nbsp;

&nbsp;

function btnClick(){

<span style="color: #ff0000;">window.open("www.baidu.com","windowname","heigth=200,width=200,top=100,left=100,toolbar=no,menubar=no")</span>

}

<span style="color: #ff0000;">window.clock()    这个直接用，括号内不用加东西，执行这条语句就退出当前页</span>

<strong>注意:</strong>在JavaScript基础篇中，已讲解了部分属性，window对象重点讲解计时器。
<h2 id="J_CodeLang" class="code-head" data-lang="Javascript">计时器setInterval()</h2>
<div id="J_CodeDescr" class="code-description">
<div class="code-desc co">

在执行时,从载入页面后每隔指定的时间执行代码。

<strong>语法:</strong>
<pre class="code">setInterval(代码,交互时间);</pre>
<strong>参数说明：</strong>

1. 代码：要调用的函数或要执行的代码串。

2. 交互时间：周期性执行或调用表达式之间的时间间隔，以毫秒计（1s=1000ms）。

<strong>返回值:</strong>

一个可以传递给 clearInterval() 从而取消对"代码"的周期性执行的值。

<strong>调用函数格式(</strong>假设有一个clock()函数<strong>):</strong>
<pre class="code">setInterval("clock()",1000)
或
setInterval(clock,1000)

注意：一定要注意上边这个写法，要有引号，不要写错！！

学院是下边这么写：
<span style="color: #ff0000;">var x=setInterval(“ getTime()”,1000);</span>   学院是先写这个所要表现的结果
function getTime(){
var d=new Date();</pre>
<pre class="code">var t=d.toLocaleTimeString();</pre>
<pre class="code"><span style="color: #ff0000;">这句话的意思是将时间转换成字符串（）显示的是时分秒</span></pre>
<pre class="code">//var t=d.toLocaleDateString(); <span style="color: #ff0000;">这句话的意思是将时间转换成字符串（）显示的是年月日</span>
document.getElementById("t").innerHTML=t;
}

将字符串转换成时间对象的方法（参考）
function strToDate(str)
{
  var arys= new Array();
  arys=str.split('-');
  var newDate=new Date(arys[0],arys[1],arys[2]);  
  return newDate;
}</pre>
<h2 id="J_CodeLang" class="code-head" data-lang="Javascript">取消计时器clearInterval()</h2>
<div id="J_CodeDescr" class="code-description">
<div class="code-desc co">
<p align="left">clearInterval() 方法可取消由 setInterval() 设置的交互时间。</p>
<p align="left"><strong>语法：</strong></p>

<div>
<pre class="code">clearInterval(id_of_setInterval)</pre>
<strong>参数说明:</strong>
id_of_setInterval：由 setInterval() 返回的 ID 值。

每隔 100 毫秒调用 clock() 函数,并显示时间。当点击按钮时，停止时间,代码如下:
<pre class="code">&lt;!DOCTYPE HTML&gt;
&lt;html&gt;
&lt;head&gt;
&lt;meta http-equiv="Content-Type" content="text/html; charset=utf-8"&gt;
&lt;title&gt;计时器&lt;/title&gt;
&lt;script type="text/javascript"&gt;
   function clock(){
      var time=new Date();                     
      document.getElementById("clock").value = time;
   }
// 每隔100毫秒调用clock函数，并将返回值赋值给i
     var i=setInterval("clock()",100);
&lt;/script&gt;
&lt;/head&gt;
&lt;body&gt;
  &lt;form&gt;
    &lt;input type="text" id="clock" size="50"  /&gt;
    &lt;input type="button" value="Stop" onclick="clearInterval(i)"  /&gt;
  &lt;/form&gt;
&lt;/body&gt;
&lt;/html&gt;

注意调用的ID是给的一个变量的id
清楚是在html里直接调用的，js里不用定义


</pre>
<h2 id="J_CodeLang" class="code-head" data-lang="Javascript">计时器setTimeout()</h2>
<div id="J_CodeDescr" class="code-description">
<div class="code-desc co">
<p align="left">setTimeout()计时器，在载入后延迟指定时间后,去执行一次表达式,仅执行一次。</p>
<p align="left"><strong>语法:</strong></p>

<div>
<pre class="code">setTimeout(代码,延迟时间);</pre>
<strong>参数说明：</strong>

1. 要调用的函数或要执行的代码串。
2. 延时时间：在执行代码前需等待的时间，以毫秒为单位（1s=1000ms)。

当我们打开网页3秒后，在弹出一个提示框，<strong>代码如下:</strong>
<pre class="code">&lt;!DOCTYPE HTML&gt;
&lt;html&gt;
&lt;head&gt;
&lt;script type="text/javascript"&gt;
  setTimeout("alert('Hello!')", 3000 );
&lt;/script&gt;
&lt;/head&gt;
&lt;body&gt;
&lt;/body&gt;
&lt;/html&gt;</pre>
<p align="left">当按钮start被点击时，setTimeout()调用函数，在5秒后弹出一个提示框。</p>

<pre class="code">&lt;!DOCTYPE HTML&gt;
&lt;html&gt;
&lt;head&gt;
&lt;script type="text/javascript"&gt;
function tinfo(){
  var t=setTimeout("alert('Hello!')",5000);
 }
&lt;/script&gt;
&lt;/head&gt;
&lt;body&gt;
&lt;form&gt;
  &lt;input type="button" value="start" onClick="tinfo()"&gt;
&lt;/form&gt;
&lt;/body&gt;
&lt;/html&gt;</pre>
<p align="left">要创建一个运行于无穷循环中的计数器，我们需要编写一个函数来调用其自身。在下面的代码，当按钮被点击后，输入域便从0开始计数。</p>

<pre class="code">&lt;!DOCTYPE HTML&gt;
&lt;html&gt;
&lt;head&gt;
&lt;script type="text/javascript"&gt;
var num=0;
function numCount(){
 document.getElementById('txt').value=num;
 num=num+1;
 setTimeout("numCount()",1000);<span style="color: #ff0000;">这里这个是让他再返回去调用它本身numCount()</span>
 }</pre>
<pre class="code">setTimeout("numCount()",1000);     这里再加一句这个的目的是让这个程序运转起来，上边那个只是一个函数，但是还没有输入运行，所以通过这句话来运行！！！</pre>
<pre class="code"> &lt;/script&gt; &lt;/head&gt; &lt;body&gt; &lt;form&gt; &lt;input type="text" id="txt" /&gt; &lt;input type="button" value="Start" onClick="numCount()" /&gt; &lt;/form&gt; &lt;/body&gt; &lt;/html&gt;</pre>
&nbsp;
<p align="left">注意： 这个写法一定要加“”</p>

<pre class="code">setTimeout("numCount()",1000);</pre>
&nbsp;
<h2 id="J_CodeLang" class="code-head" data-lang="Javascript">编程练习</h2>
<div id="J_CodeDescr" class="code-description">
<div class="code-desc co">

制作一个跳转提示页面：

<strong>要求：</strong>

1. 如果打开该页面后，如果不做任何操作则5秒后自动跳转到一个新的地址，如慕课网主页。

2. 如果点击“返回”按钮则返回前一个页面。

<strong>效果:</strong>

<strong><a href="http://www.pengweb.net/wp-content/uploads/2015/02/537d6fed0001572608080402.jpg"><img class="attachment-medium" src="http://www.pengweb.net/wp-content/uploads/2015/02/537d6fed0001572608080402-300x149.jpg" alt="537d6fed0001572608080402" width="300" height="149" /></a></strong>

&lt;!DOCTYPE html&gt;
&lt;html&gt;
&lt;head&gt;
&lt;title&gt;浏览器对象&lt;/title&gt;
&lt;meta http-equiv="Content-Type" content="text/html; charset=utf-8"/&gt;
&lt;/head&gt;
&lt;body&gt;
&lt;!--先编写好网页布局--&gt;
&lt;a id="ti"&gt;&lt;/a&gt;秒后回到主页

<span style="color: #ff0000;">&lt;a href="javascript:history.back()"&gt;返回&lt;/a&gt;</span>

&lt;script type="text/javascript"&gt;
//var a=document.getElementById("ti");
var b=5;
function jishiqi(){
document.getElementById("ti").innerHTML=b;
b=b-1;
if(b==0){location.assign("www.baidu.com")
}
setTimeout("jishiqi()",1000)            <span style="color: #ff0000;">这里才是真正的调用自身而不是下边那个</span>
}setTimeout("jishiqi()")                      <span style="color: #ff0000;">这句话的目的只是调用jishiiqi（）这个函数，让这个函数运转起来</span>
//获取显示秒数的元素，通过定时器来更改秒数。

//通过window的location和history对象来控制网页的跳转。

&lt;/script&gt;
&lt;/body&gt;
&lt;/html&gt;

&nbsp;

如果用setInterval则可以按下边的写

&lt;script type="text/javascript"&gt;
//var a=document.getElementById("ti");
var b=5;
function jishiqi(){
document.getElementById("ti").innerHTML=b;
b=b-1;
if(b==0){location.assign("www.baidu.com")
}
}
setInterval("jishiqi()",1000)    <span style="color: #ff0000;">直接在这里调用上边的函数就行了，本来自身就是无限循环的</span>
//获取显示秒数的元素，通过定时器来更改秒数。

//通过window的location和history对象来控制网页的跳转。

&lt;/script&gt;

</div>
</div>
<h2 id="J_CodeLang" class="code-head" data-lang="Javascript">History 对象</h2>
<div id="J_CodeDescr" class="code-description">
<div class="code-desc co">

history对象记录了用户曾经浏览过的页面(URL)，并可以实现浏览器前进与后退相似导航的功能。

<strong>注意:从<strong>窗口</strong>被打开的那一刻开始记录，每个浏览器窗口、每个标签页乃至每个框架，都有自己的history对象与特定的window对象关联。</strong>

<strong>语法：</strong>
<pre class="code">window.history.[属性|方法]</pre>
<strong>注意：</strong>window可以省略。

<strong>History 对象属性</strong>

<a href="http://www.pengweb.net/wp-content/uploads/2015/02/53548c030001759e05840068.jpg"><img class="attachment-medium" src="http://www.pengweb.net/wp-content/uploads/2015/02/53548c030001759e05840068-300x35.jpg" alt="53548c030001759e05840068" width="300" height="35" /></a>

<strong>History 对象方法</strong>

<strong><a href="http://www.pengweb.net/wp-content/uploads/2015/02/53548c200001228206210123.jpg"><img class="attachment-medium" src="http://www.pengweb.net/wp-content/uploads/2015/02/53548c200001228206210123-300x59.jpg" alt="53548c200001228206210123" width="300" height="59" /></a></strong>

使用length属性，当前窗口的浏览历史总长度，<strong>代码如下：</strong>
<pre class="code">&lt;script type="text/javascript"&gt;
  var HL = window.history.length;
  document.write(HL);
&lt;/script&gt;</pre>
&nbsp;
<h2 id="J_CodeLang" class="code-head" data-lang="Javascript">Location对象</h2>
<div id="J_CodeDescr" class="code-description">
<div class="code-desc co">

location用于获取或设置窗体的URL，并且可以用于解析URL。

<strong>语法:</strong>
<pre class="code">location.[属性|方法]</pre>
<strong>location对象属性图示:</strong>

<a href="http://www.pengweb.net/wp-content/uploads/2015/02/53605c5a0001b26909900216.jpg"><img class="attachment-medium" src="http://www.pengweb.net/wp-content/uploads/2015/02/53605c5a0001b26909900216-300x65.jpg" alt="53605c5a0001b26909900216" width="300" height="65" /></a>

<strong>location 对象属性：</strong>

<strong><a href="http://www.pengweb.net/wp-content/uploads/2015/02/5354b1d00001c4ec06220271.jpg"><img class="attachment-medium" src="http://www.pengweb.net/wp-content/uploads/2015/02/5354b1d00001c4ec06220271-300x131.jpg" alt="5354b1d00001c4ec06220271" width="300" height="131" /></a></strong>

<strong>location 对象方法:</strong>

<strong><a href="http://www.pengweb.net/wp-content/uploads/2015/02/5354b1eb00016a2405170126.jpg"><img class="attachment-medium" src="http://www.pengweb.net/wp-content/uploads/2015/02/5354b1eb00016a2405170126-300x73.jpg" alt="5354b1eb00016a2405170126" width="300" height="73" /></a></strong>

&nbsp;
<h2 id="J_CodeLang" class="code-head" data-lang="Javascript">Navigator对象</h2>
<div id="J_CodeDescr" class="code-description">
<div class="code-desc co">

Navigator 对象包含有关浏览器的信息，通常用于检测浏览器与操作系统的版本。

<strong>对象属性:</strong>

<a href="http://www.pengweb.net/wp-content/uploads/2015/02/5354cff70001428b06880190.jpg"><img class="attachment-medium" src="http://www.pengweb.net/wp-content/uploads/2015/02/5354cff70001428b06880190-300x83.jpg" alt="5354cff70001428b06880190" width="300" height="83" /></a>

查看浏览器的名称和版本，<strong>代码如下:</strong>
<pre class="code">&lt;script type="text/javascript"&gt;
   var browser=navigator.appName;
   var b_version=navigator.appVersion;
   document.write("Browser name"+browser);
   document.write("&lt;br&gt;");
   document.write("Browser version"+b_version);
&lt;/script&gt;


</pre>
<h2 id="J_CodeLang" class="code-head" data-lang="Javascript">userAgent</h2>
<div id="J_CodeDescr" class="code-description">
<div class="code-desc co">

返回用户代理头的字符串表示(就是包括浏览器版本信息等的字符串)

<strong>语法</strong>
<pre class="code">navigator.userAgent</pre>
几种浏览的user_agent.，像360的兼容模式用的是IE、极速模式用的是chrom的内核。

<a href="http://www.pengweb.net/wp-content/uploads/2015/02/535a3a4a0001e03f06870189.jpg"><img class="attachment-medium" src="http://www.pengweb.net/wp-content/uploads/2015/02/535a3a4a0001e03f06870189-300x83.jpg" alt="535a3a4a0001e03f06870189" width="300" height="83" /></a>

使用userAgent判断使用的是什么浏览器(假设使用的是IE8浏览器),<strong>代码如下:</strong>
<pre class="code">function validB(){ 
  var u_agent = navigator.userAgent; 
  var B_name="Failed to identify the browser"; 
  if(u_agent.indexOf("Firefox")&gt;-1){  这个他运用了字符串查找的办法，找不到的时候用-1代替，所以这里是&gt;-1
      B_name="Firefox";          
  }else if(u_agent.indexOf("Chrome")&gt;-1){ 
      B_name="Chrome"; 
  }else if(u_agent.indexOf("MSIE")&gt;-1&amp;&amp;u_agent.indexOf("Trident")&gt;-1){ 
      B_name="IE(8-10)";  
  }
    document.write("B_name:"+B_name+"&lt;br&gt;");
    document.write("u_agent:"+u_agent+"&lt;br&gt;"); 
}</pre>
<strong>运行结果:</strong>

<a href="http://www.pengweb.net/wp-content/uploads/2015/02/535dea1e00017b0b06880265.jpg"><img class="attachment-medium" src="http://www.pengweb.net/wp-content/uploads/2015/02/535dea1e00017b0b06880265-300x116.jpg" alt="535dea1e00017b0b06880265" width="300" height="116" /></a>

</div>
</div>
</div>
</div>
</div>
</div>
</div>
</div>
&nbsp;
<h2 id="J_CodeLang" class="code-head" data-lang="Javascript">screen对象</h2>
<div id="J_CodeDescr" class="code-description">
<div class="code-desc co">

screen对象用于获取用户的屏幕信息。

<strong>语法：</strong>
<pre class="code">window.screen.属性</pre>
<strong>对象属性:</strong>

<strong><a href="http://www.pengweb.net/wp-content/uploads/2015/02/5354d2810001a47706210213.jpg"><img class="attachment-medium" src="http://www.pengweb.net/wp-content/uploads/2015/02/5354d2810001a47706210213-300x103.jpg" alt="5354d2810001a47706210213" width="300" height="103" /></a></strong>

&nbsp;

</div>
</div>
</div>
</div>
</div>
<pre class="code"> 综合例题：
&lt;div id="clock"&gt;5&lt;/div&gt;
 
 &lt;input type="button" value="haha" onClick="back1()"&gt;
 &lt;script type="text/javascript"&gt; 
 var num=50;
 function clock(){
 document.getElementById('clock').innerHTML=num;
 num=num-1;
 if(num&lt;0){
 location.assign("http://www.baidu.com")
 }else{setTimeout("clock()",1000);
 }
 }
 setTimeout("clock()",0);  以计数器为基础，先写出一个计数器，然后再计数器呢展开if不同情况来展示
 
 function back1(){
 window.history.back()
 }
 &lt;/script&gt; 

一个很聪明的写法：
&lt;a href="window.history.back()"&gt;返回&lt;/a&gt;

</pre>

<hr />

<h2 id="J_CodeLang" class="code-head" data-lang="Javascript">认识DOM</h2>
<div id="J_CodeDescr" class="code-description">
<div class="code-desc co">

文档对象模型DOM（Document Object Model）定义访问和处理HTML文档的标准方法。DOM 将HTML文档呈现为带有元素、属性和文本的树结构（节点树）。

<strong>先来看看下面代码:</strong>

<a href="http://www.pengweb.net/wp-content/uploads/2015/02/5375ca640001c67307860420.jpg"><img class="attachment-medium" src="http://www.pengweb.net/wp-content/uploads/2015/02/5375ca640001c67307860420-300x160.jpg" alt="5375ca640001c67307860420" width="300" height="160" /></a>
<p align="left"><strong>将HTML代码分解为DOM节点层次图:</strong></p>
<a href="http://www.pengweb.net/wp-content/uploads/2015/02/5375ca7e0001dd8d04830279.jpg"><img class="attachment-medium" src="http://www.pengweb.net/wp-content/uploads/2015/02/5375ca7e0001dd8d04830279-300x173.jpg" alt="5375ca7e0001dd8d04830279" width="300" height="173" /></a>

<strong>HTML</strong><strong>文档可以说由节点构成的集合，DOM节点有:</strong>

<strong>1. </strong><strong>元素节点：</strong>上图中&lt;html&gt;、&lt;body&gt;、&lt;p&gt;等都是元素节点，即标签。

<strong>2. </strong><strong>文本节点:</strong>向用户展示的内容，如&lt;li&gt;...&lt;/li&gt;中的JavaScript、DOM、CSS等文本。

<strong>3. </strong><strong>属性节点:</strong>元素属性，如&lt;a&gt;标签的链接属性href="http://www.imooc.com"。

<strong>节点属性:</strong>

<a href="http://www.pengweb.net/wp-content/uploads/2015/02/5375c953000117ee05240129.jpg"><img class="attachment-medium" src="http://www.pengweb.net/wp-content/uploads/2015/02/5375c953000117ee05240129-300x74.jpg" alt="5375c953000117ee05240129" width="300" height="74" /></a>

<strong>遍历节点树:</strong>

<a href="http://www.pengweb.net/wp-content/uploads/2015/02/53f17a6400017d2905230219.jpg"><img class="attachment-medium" src="http://www.pengweb.net/wp-content/uploads/2015/02/53f17a6400017d2905230219-300x126.jpg" alt="53f17a6400017d2905230219" width="300" height="126" /></a>

<b>以上图ul为例，它的父级节点body,它的子节点3个li,它的兄弟结点h2、P。</b>

<strong>DOM操作:</strong>

<a href="http://www.pengweb.net/wp-content/uploads/2015/02/538d29da000152db05360278.jpg"><img class="attachment-medium" src="http://www.pengweb.net/wp-content/uploads/2015/02/538d29da000152db05360278-300x156.jpg" alt="538d29da000152db05360278" width="300" height="156" /></a>

<strong>注意:</strong>前两个是document方法。

&nbsp;
<h2 id="J_CodeLang" class="code-head" data-lang="Javascript">区别getElementByID,getElementsByName,getElementsByTagName</h2>
<div id="J_CodeDescr" class="code-description">
<div class="code-desc co">

<b>以人来举例说明，人有能标识身份的身份证，有姓名，有类别(大人、小孩、老人)等。</b>

1. ID 是一个人的身份证号码，是唯一的。所以通过getElementById获取的是指定的一个人。

2. Name 是他的名字，可以重复。所以通过getElementsByName获取名字相同的人集合。

3. TagName可看似某类，getElementsByTagName获取相同类的人集合。如获取小孩这类人，getElementsByTagName("小孩")。

<strong>把上面的例子转换到HTML中，如下:</strong>
<pre class="code">&lt;input type="checkbox" name="hobby" id="hobby1"&gt;  音乐</pre>
input标签就像人的类别。

name属性就像人的姓名。

id属性就像人的身份证。

<strong>方法总结如下:</strong>

<a href="http://www.pengweb.net/wp-content/uploads/2015/02/5405263300018bcf05760129.jpg"><img class="attachment-medium" src="http://www.pengweb.net/wp-content/uploads/2015/02/5405263300018bcf05760129-300x67.jpg" alt="5405263300018bcf05760129" width="300" height="67" /></a>

<strong>注意：</strong>方法区分大小写

例子：

&lt;!DOCTYPE HTML&gt;
&lt;html&gt;
&lt;head&gt;
&lt;meta http-equiv="Content-Type" content="text/html; charset=gb2312"&gt;
&lt;title&gt;无标题文档&lt;/title&gt;
&lt;/head&gt;

&lt;body&gt;
&lt;form&gt;
请选择你爱好:&lt;br&gt;
&lt;input type="checkbox" name="hobby" id="hobby1"&gt;  音乐
&lt;input type="checkbox" name="hobby" id="hobby2"&gt;  登山
&lt;input type="checkbox" name="hobby" id="hobby3"&gt;  游泳
&lt;input type="checkbox" name="hobby" id="hobby4"&gt;  阅读
&lt;input type="checkbox" name="hobby" id="hobby5"&gt;  打球
&lt;input type="checkbox" name="hobby" id="hobby6"&gt;  跑步 &lt;br&gt;
&lt;input type="button" value = "全选" onclick = "checkall();"&gt;
&lt;input type="button" value = "全不选" onclick = "clearall();"&gt;
&lt;p&gt;请输入您要选择爱好的序号，序号为1-6:&lt;/p&gt;
&lt;input id="wb" name="wb" type="text" &gt;
&lt;input name="ok" type="button" value="确定" onclick = "checkone();"&gt;
&lt;/form&gt;
&lt;script type="text/javascript"&gt;
function checkall(){
var hobby = document.getElementsByTagName("input");
for(i = 0;i &lt; hobby.length;i++){
if(hobby[i].type == "checkbox")      注意：一定要记得通过.type来进行调取参数值
{
hobby[i].checked = true;
}
}
}
function clearall(){
var hobby = document.getElementsByName("hobby");
for(i = 0;i &lt; hobby.length;i++){
hobby[i].checked = false;
}
}

function checkone(){
var j=document.getElementById("wb").value;
var hobby = document.getElementById("hobby"+j);
hobby.checked = true;
}

&lt;/script&gt;
&lt;/body&gt;
&lt;/html&gt;
<h2 id="J_CodeLang" class="code-head" data-lang="Javascript">getAttribute()方法</h2>
<div id="J_CodeDescr" class="code-description">
<div class="code-desc co">

通过元素节点的属性名称获取属性的值。

<strong>语法：</strong>
<pre class="code">elementNode.getAttribute(name)</pre>
<strong>说明:</strong>

1. elementNode：使用getElementById()、getElementsByTagName()等方法，获取到的元素节点。

2. name：要想查询的元素节点的属性名字

看看下面的代码，获取h1标签的属性值：

<a href="http://www.pengweb.net/wp-content/uploads/2015/02/538d242700019ec809330432.jpg"><img class="attachment-medium" src="http://www.pengweb.net/wp-content/uploads/2015/02/538d242700019ec809330432-300x139.jpg" alt="538d242700019ec809330432" width="300" height="139" /></a>

<strong>运行结果:</strong>

h1标签的ID ：alink
h1标签的title ：getAttribute()获取标签的属值

注意：一定要先获取他的id之后再获取标签属性
<h2 id="J_CodeLang" class="code-head" data-lang="Javascript">setAttribute()方法</h2>
<div id="J_CodeDescr" class="code-description">
<div class="code-desc co">

setAttribute() 方法增加一个指定名称和值的新属性，或者把一个现有的属性设定为指定的值。

<strong>语法：</strong>
<pre class="code">elementNode.setAttribute(name,value)</pre>
<strong>说明：</strong>

1.name: 要设置的属性名。

2.value: 要设置的属性值。

<strong>注意：</strong>

1.把指定的属性设置为指定的值。如果不存在具有指定名称的属性，该方法将创建一个新属性。

2.类似于getAttribute()方法，setAttribute()方法只能通过元素节点对象调用的函数。

</div>
</div>
&nbsp;

例子：

&lt;!DOCTYPE HTML&gt;
&lt;html&gt;
&lt;head&gt;
&lt;meta http-equiv="Content-Type" content="text/html; charset=utf-8"&gt;
&lt;title&gt;无标题文档&lt;/title&gt;
&lt;/head&gt;
&lt;body&gt;
&lt;p id="intro"&gt;我的课程&lt;/p&gt;
&lt;ul&gt;
&lt;li title="JS"&gt;JavaScript&lt;/li&gt;
&lt;li title="JQ"&gt;JQuery&lt;/li&gt;
&lt;li title=""&gt;HTML/CSS&lt;/li&gt;
&lt;li title="JAVA"&gt;JAVA&lt;/li&gt;
&lt;li title=""&gt;PHP&lt;/li&gt;
&lt;/ul&gt;
&lt;h1&gt;以下为li列表title的值,当title为空时，新设置值为"WEB前端技术":&lt;/h1&gt;
&lt;script type="text/javascript"&gt;
var Lists=document.getElementsByTagName("li");
for (var i=0; i&lt;Lists.length;i++)
{
var text=Lists[i].getAttribute("title")
document.write(text +"&lt;br&gt;");
if(text=="")
{
Lists[i].setAttribute('title','WEB')
document.write(Lists[i].getAttribute("title")+"&lt;br&gt;");
}
}
&lt;/script&gt;
&lt;/body&gt;
&lt;/html&gt;
<h2 id="J_CodeLang" class="code-head" data-lang="Javascript">节点属性</h2>
<div id="J_CodeDescr" class="code-description">
<div class="code-desc co">

在文档对象模型 (DOM) 中，每个节点都是一个对象。DOM 节点有三个重要的属性 ：

1. nodeName : 节点的名称

2. nodeValue ：节点的值
<p id="content-313947931"><span style="color: #ff0000;">nodeValue指的是节点的值... value指的是元素节点中的value属性...</span></p>

<pre id="recommend-content-1414675176" class="recommend-text mb-10"><span style="color: #ff0000;">一般来说TEXT属性基本是文本框，文本域的值，value一般对应的是INPUT系列的值，nodevalue一般是节点的值，比如&lt;td&gt;hjkh&lt;/td&gt;获得的就是HJKH</span></pre>
3. nodeType ：节点的类型

直接用就行，例如：

document.write(list[i].nodeName+list[i].nodeValue+list[i].nodeType);

<strong>一、nodeName 属性: </strong>节点的名称，是只读的。

1. 元素节点的 nodeName 与标签名相同
2. 属性节点的 nodeName 是属性的名称
3. 文本节点的 nodeName 永远是 #text
4. 文档节点的 nodeName 永远是 #document

<strong>二、nodeValue 属性：</strong>节点的值

1. 元素节点的 nodeValue 是 undefined 或 null
2. 文本节点的 nodeValue 是文本自身
3. 属性节点的 nodeValue 是属性的值

<strong>三、nodeType 属性: </strong>节点的类型，是只读的。以下常用的几种结点类型:

<strong>元素类型    节点类型</strong>
元素          1
属性          2
文本          3
注释          8
文档          9
<h2 id="J_CodeLang" class="code-head" data-lang="Javascript">访问子结点childNodes</h2>
<div id="J_CodeDescr" class="code-description">
<div class="code-desc co">

访问选定元素节点下的所有子节点的列表，返回的值可以看作是一个数组，他具有length属性。

<strong>语法：</strong>
<pre class="code">elementNode.childNodes</pre>
<strong>注意：</strong>

如果选定的节点没有子节点，则该属性返回不包含节点的 NodeList。

<strong>我们来看看下面的代码:</strong>

<a href="http://www.pengweb.net/wp-content/uploads/2015/02/538405fa00010e6c05630357.jpg"><img class="attachment-medium" src="http://www.pengweb.net/wp-content/uploads/2015/02/538405fa00010e6c05630357-300x190.jpg" alt="538405fa00010e6c05630357" width="300" height="190" /></a>

<strong>运行结果:</strong>

<strong>IE:</strong>
<pre class="code">  UL子节点个数:3
  节点类型:1</pre>
<strong>其它浏览器:</strong>
<pre class="code">   UL子节点个数:7
   节点类型:3</pre>
<strong>注意:</strong>

1. IE全系列、firefox、chrome、opera、safari兼容问题

2. 节点之间的空白符，在firefox、chrome、opera、safari浏览器是文本节点，所以IE是3，其它浏览器是7，如下图所示:

<a href="http://www.pengweb.net/wp-content/uploads/2015/02/538d2b8a000163e303430127.jpg"><img class="attachment-medium" src="http://www.pengweb.net/wp-content/uploads/2015/02/538d2b8a000163e303430127-300x111.jpg" alt="538d2b8a000163e303430127" width="300" height="111" /></a>

<strong>如果把代码改成这样:</strong>

&lt;ul&gt;&lt;li&gt;javascript&lt;/li&gt;&lt;li&gt;jQuery&lt;/li&gt;&lt;li&gt;PHP&lt;/li&gt;&lt;/ul&gt;

<strong>运行结果:（IE和其它浏览器结果是一样的）</strong>
<pre class="code">UL子节点个数:3
  节点类型:1
例子：
&lt;body&gt;
&lt;div&gt;
 javascript 
 &lt;p&gt;javascript&lt;/p&gt;
 &lt;div&gt;jQuery&lt;/div&gt;
 &lt;h5&gt;PHP&lt;/h5&gt;
&lt;/div&gt;
&lt;script type="text/javascript"&gt;
 var node=document.getElementsByTagName("div")[0].childNodes
;               注意：这里记住了是第一个div的子节点，获取div一定要指定第几个div才行
 for(i=0;i&lt;node.length;i++){
 document.write(node[i].nodeType);
 }
 
 
&lt;/script&gt;
&lt;/body&gt;</pre>
<h2 id="J_CodeLang" class="code-head" data-lang="Javascript">访问子结点的第一和最后项</h2>
<div id="J_CodeDescr" class="code-description">
<div class="code-desc co">

一、<strong><code class="marker">firstChild </code></strong>属性返回‘childNodes’数组的第一个子节点。如果选定的节点没有子节点，则该属性返回 NULL。

<strong>语法：</strong>
<pre class="code">node.firstChild</pre>
<strong>说明：</strong>与elementNode.childNodes[0]是同样的效果。

二、<strong><code class="marker"> lastChild</code></strong> 属性返回‘childNodes’数组的最后一个子节点。如果选定的节点没有子节点，则该属性返回 NULL。

<strong>语法：</strong>
<pre class="code">node.lastChild</pre>
<strong>说明：</strong>与elementNode.childNodes[elementNode.childNodes.length-1]是同样的效果。

例子：

&lt;script type="text/javascript"&gt;
var x=document.getElementById("con");
document.write(x.firstChild.nodeName);
document.write(x.lastChild.nodeName);
&lt;/script&gt;
<h2 id="J_CodeLang" class="code-head" data-lang="Javascript">访问父节点parentNode</h2>
<div id="J_CodeDescr" class="code-description">
<div class="code-desc co">

获取指定节点的父节点

<strong>语法：</strong>
<pre class="code">elementNode.parentNode</pre>
<strong>注意:父节点只能有一个。</strong>

看看下面的例子,获取 P 节点的父节点，代码如下:
<pre class="code">&lt;div id="text"&gt;
  &lt;p id="con"&gt; parentNode 获取指点节点的父节点&lt;/p&gt;
&lt;/div&gt; 
&lt;script type="text/javascript"&gt;
  var mynode= document.getElementById("con");
  document.write(mynode.<strong>parentNode</strong>.nodeName);
&lt;/script&gt;</pre>
运行结果:
<pre class="code">parentNode 获取指点节点的父节点
DIV</pre>
<strong>访问祖节点:</strong>
<pre class="code">elementNode.parentNode.parentNode</pre>
看看下面的代码:
<pre class="code">&lt;div id="text"&gt;  
  &lt;p&gt;
    parentNode      
    &lt;span id="con"&gt; 获取指点节点的父节点&lt;/span&gt;
  &lt;/p&gt;
&lt;/div&gt; 
&lt;script type="text/javascript"&gt;
  var mynode= document.getElementById("con");
  document.write(mynode.<strong>parentNode.parentNode.</strong>nodeName);
&lt;/script&gt;</pre>
运行结果:
<pre class="code">parentNode获取指点节点的父节点
DIV
注意用：innerHTML来调出文本来
document.write(mylist.parentNode.parentNode.parentNode.lastChild.innerHTML);

</pre>
<h2 id="J_CodeLang" class="code-head" data-lang="Javascript">访问兄弟节点</h2>
<div id="J_CodeDescr" class="code-description">
<div class="code-desc co">

1. nextSibling 属性可返回某个节点之后紧跟的节点（处于同一树层级中）。

<strong>语法：</strong>
<pre class="code">nodeObject.nextSibling</pre>
<strong>说明：</strong>如果无此节点，则该属性返回 null。

2. previousSibling 属性可返回某个节点之前紧跟的节点（处于同一树层级中）。

<strong>语法：</strong>
<pre class="code">nodeObject.previousSibling</pre>
<strong>说明：</strong>如果无此节点，则该属性返回 null。

注意: 两个属性获取的是节点。Internet Explorer 会忽略节点间生成的空白文本节点（例如，换行符号），而其它浏览器不会忽略。

<strong>解决除ie外其他浏览器将空格当作一个文本文档识别问题的过滤方法:</strong>

判断节点nodeType是否为1, 如是为元素节点，跳过。

<a href="http://www.pengweb.net/wp-content/uploads/2015/02/5386e3c80001c25607010856.jpg"><img class="attachment-medium" src="http://www.pengweb.net/wp-content/uploads/2015/02/5386e3c80001c25607010856-246x300.jpg" alt="5386e3c80001c25607010856" width="246" height="300" /></a>

<strong>运行结果:</strong>
<pre class="code">LI = javascript
nextsibling: LI = jquery

</pre>
<h2 id="J_CodeLang" class="code-head" data-lang="Javascript">创建元素节点createElement</h2>
<div id="J_CodeDescr" class="code-description">
<div class="code-desc co">

createElement()方法可创建元素节点。此方法可返回一个 Element 对象。

<strong>语法：</strong>
<pre class="code">document.createElement(tagName)</pre>
<strong>参数:</strong>

tagName：字符串值，这个字符串用来指明创建元素的类型。

<strong>注意：</strong>要与appendChild() 或 insertBefore()方法联合使用，将元素显示在页面中。

我们来创建一个按钮，代码如下：
<pre class="code">&lt;script type="text/javascript"&gt;
   var body = document.body;   这句话是简写，最好不要这样写，这样只有IE认得。最好写成：
                                 var body=document.getElementsByTagName("body")
   var input = document.createElement("input");  
   input.type = "button";  
   input.value = "创建一个按钮";  
   body.appendChild(input);  
 &lt;/script&gt;</pre>
效果：在HTML文档中，创建一个按钮。

我们也可以使用setAttribute来设置属性，代码如下：
<pre class="code">&lt;script type="text/javascript"&gt;  
   var body= document.body;             
   var btn = document.createElement("input");  
   btn.setAttribute("type", "text");  
   btn.setAttribute("name", "q");  
   btn.setAttribute("value", "使用setAttribute");  
   btn.setAttribute("onclick", "javascript:alert('This is a text!');");       
   body.appendChild(btn);  
&lt;/script&gt;</pre>
效果：在HTML文档中，创建一个文本框，使用setAttribute设置属性值。 当点击这个文本框时，会弹出对话框“This is a text!”。

</div>
</div>
<pre class="code"></pre>
&nbsp;
<h2 id="J_CodeLang" class="code-head" data-lang="Javascript">创建文本节点createTextNode</h2>
&nbsp;
<div id="J_CodeDescr" class="code-description">
<div class="code-desc co">createTextNode() 方法创建新的文本节点，返回新创建的 Text 节点。 <strong>语法：</strong>
<pre class="code">document.createTextNode(data)</pre>
<strong>参数：</strong>

data : 字符串值，可规定此节点的文本。

我们来创建一个&lt;div&gt;元素并向其中添加一条消息，代码如下：

<a href="http://www.pengweb.net/wp-content/uploads/2015/02/53951c200001d32d07130554.jpg"><img class="attachment-medium" src="http://www.pengweb.net/wp-content/uploads/2015/02/53951c200001d32d07130554-300x233.jpg" alt="53951c200001d32d07130554" width="300" height="233" /></a>

<strong>运行结果:</strong>

<a href="http://www.pengweb.net/wp-content/uploads/2015/02/53951c720001996d04080225.jpg"><img class="attachment-medium" src="http://www.pengweb.net/wp-content/uploads/2015/02/53951c720001996d04080225-300x165.jpg" alt="53951c720001996d04080225" width="300" height="165" /></a>

&nbsp;

</div>
</div>
<h2 id="J_CodeLang" class="code-head" data-lang="Javascript">插入节点appendChild()</h2>
<div id="J_CodeDescr" class="code-description">
<div class="code-desc co">

在指定节点的【最后一个子节点】列表之后添加一个新的子节点。

<strong>语法:</strong>
<pre class="code">appendChild(newnode)</pre>
<strong>参数:</strong>

newnode：指定追加的节点。

我们来看看，div标签内创建一个新的 P 标签，代码如下:

<a href="http://www.pengweb.net/wp-content/uploads/2015/02/5398fd020001ad4905890193.jpg"><img class="attachment-medium" src="http://www.pengweb.net/wp-content/uploads/2015/02/5398fd020001ad4905890193-300x98.jpg" alt="5398fd020001ad4905890193" width="300" height="98" /></a>

<strong>运行结果:</strong>
<pre class="code">HTML
JavaScript
This is a new p

</pre>
<h2 id="J_CodeLang" class="code-head" data-lang="Javascript">插入节点insertBefore()</h2>
<div id="J_CodeDescr" class="code-description">
<div class="code-desc co">
<p align="left">insertBefore() 方法可在已有的子节点前插入一个新的子节点。</p>
<p align="left"><strong>语法:</strong></p>
<p align="left">insertBefore(newnode,node);</p>
<p align="left"><strong>参数:</strong></p>
<p align="left">newnode: 要插入的新节点。</p>
<p align="left">node: 指定此节点前插入节点。</p>
<p align="left">我们在来看看下面代码，在指定节点前插入节点。</p>
<p align="left"><a href="http://www.pengweb.net/wp-content/uploads/2015/02/5395318100010c6806960431.jpg"><img class="attachment-medium" src="http://www.pengweb.net/wp-content/uploads/2015/02/5395318100010c6806960431-300x186.jpg" alt="5395318100010c6806960431" width="300" height="186" /></a></p>
<p align="left"><strong>运行结果:</strong></p>

<div id="div1">
<pre class="code">This is a new p
JavaScript
HTML</pre>
</div>
<p align="left"><strong>注意:</strong> otest.insertBefore(newnode,node); 也可以改为:  otest.insertBefore(newnode,otest.childNodes[0]);</p>
<p align="left">注意上边那个改为里的otest.childNodes[0]  这个是可以指定节点的，在这个节点前增加的！！！</p>

<h2 id="J_CodeLang" class="code-head" data-lang="Javascript">删除节点removeChild()</h2>
<div id="J_CodeDescr" class="code-description">
<div class="code-desc co">

removeChild() 方法从子节点列表中删除某个节点。如删除成功，此方法可返回被删除的节点，如失败，则返回 NULL。

<strong>语法:</strong>
<pre class="code">nodeObject.removeChild(node)</pre>
<strong>参数:</strong>

node ：必需，指定需要删除的节点。

我们来看看下面代码，删除子点。

<a href="http://www.pengweb.net/wp-content/uploads/2015/02/5399744d000153a306060342.jpg"><img class="attachment-medium" src="http://www.pengweb.net/wp-content/uploads/2015/02/5399744d000153a306060342-300x169.jpg" alt="5399744d000153a306060342" width="300" height="169" /></a>

<strong>运行结果:</strong>
<pre class="code">HTML
删除节点的内容: javascript</pre>
<span style="color: #ff0000;"><strong>注意:</strong> 把删除的子节点赋值给 x，这个子节点不在DOM树中，但是还存在内存中，可通过 x 操作。</span>

<span style="color: #ff0000;">如果要完全删除对象，给 x 赋 null 值，代码如下:</span>

<a href="http://www.pengweb.net/wp-content/uploads/2015/02/539975a800017c8e04790082.jpg"><img class="attachment-medium" src="http://www.pengweb.net/wp-content/uploads/2015/02/539975a800017c8e04790082-300x51.jpg" alt="539975a800017c8e04790082" width="300" height="51" /></a>

&nbsp;
<h2 id="J_CodeLang" class="code-head" data-lang="Javascript">替换元素节点replaceChild()</h2>
<div id="J_CodeDescr" class="code-description">
<div class="code-desc co">

replaceChild 实现子节点(对象)的替换。返回被替换对象的引用。

<strong>语法：</strong>
<pre class="code">node.replaceChild (newnode,oldnew )</pre>
<strong>参数：</strong>

newnode : 必需，用于替换 oldnew 的对象。
oldnew : 必需，被 newnode 替换的对象。

我们来看看下面的代码:

<a href="http://www.pengweb.net/wp-content/uploads/2015/02/539557d70001c3ee07190429.jpg"><img class="attachment-medium" src="http://www.pengweb.net/wp-content/uploads/2015/02/539557d70001c3ee07190429-300x179.jpg" alt="539557d70001c3ee07190429" width="300" height="179" /></a>

效果: 将文档中的 Java 改为 JavaScript。

<span style="color: #ff0000;"><strong>注意: </strong></span>

<span style="color: #ff0000;">1. 当 oldnode 被替换时，所有与之相关的属性内容都将被移除。</span>

<span style="color: #ff0000;">2. newnode 必须先被建立。</span>

<span style="color: #ff0000;">3.要声明好newnode和oldnode这样才好处理后边</span>

<span style="color: #ff0000;">4.老节点的父节点中的子节点进行替换（新节点，老节点）</span>

<span style="color: #ff0000;">用公式表达就是：oldnode.parentNode.replaceChild(newnode,oldnode);</span>

&nbsp;
<h2 id="J_CodeLang" class="code-head" data-lang="Javascript">浏览器窗口可视区域大小</h2>
<div id="J_CodeDescr" class="code-description">
<div class="code-desc co">
<p align="left">获得浏览器窗口的尺寸【浏览器的视口，不包括工具栏和滚动条】的方法:</p>
<p align="left"><strong>一、对于IE9+、Chrome、Firefox、Opera 以及 Safari：</strong></p>
<p align="left">•  window.innerHeight - 浏览器窗口的内部高度</p>
<p align="left">•  window.innerWidth - 浏览器窗口的内部宽度</p>
<p align="left"><strong>二、对于 Internet Explorer 8、7、6、5：</strong></p>
<p align="left">•  document.documentElement.clientHeight表示HTML文档所在窗口的当前高度。</p>
<p align="left">•  document.documentElement.clientWidth表示HTML文档所在窗口的当前宽度。</p>
<p align="left">或者</p>
<p align="left">Document对象的body属性对应HTML文档的&lt;body&gt;标签</p>
<p align="left">•  document.body.clientHeight</p>
<p align="left">•  document.body.clientWidth</p>
<p align="left"><strong>在不同浏览器都实用的 JavaScript 方案：(用这个就行了)</strong></p>

<div>
<pre class="code">var w= document.documentElement.clientWidth
      || document.body.clientWidth;
var h= document.documentElement.clientHeight
      || document.body.clientHeight;

</pre>
<h2 id="J_CodeLang" class="code-head" data-lang="Javascript">网页尺寸scrollHeight</h2>
<div id="J_CodeDescr" class="code-description">
<div class="code-desc co">

scrollHeight和scrollWidth，获取网页【内容】高度和宽度(不包括滚动条)。

<strong>一、针对IE、Opera:</strong>
<p align="left">scrollHeight 是网页内容实际高度，可以小于 clientHeight。</p>
<p align="left"><strong>二、针对NS、FF:</strong></p>
<p align="left">scrollHeight 是网页内容高度，不过最小值是 clientHeight。也就是说网页内容实际高度小于 clientHeight 时，scrollHeight 返回 clientHeight 。</p>
<p align="left"><strong>三、浏览器兼容性（用这个就行了）</strong></p>

<div>
<pre class="code">var w=document.documentElement.scrollWidth
   || document.body.scrollWidth;
var h=document.documentElement.scrollHeight
   || document.body.scrollHeight;</pre>
<strong>注意:区分大小写</strong>

scrollHeight和scrollWidth还可获取Dom元素中内容实际占用的高度和宽度。
<h2 id="J_CodeLang" class="code-head" data-lang="Javascript">网页尺寸offsetHeight</h2>
<div id="J_CodeDescr" class="code-description">
<div class="code-desc co">

offsetHeight和offsetWidth，获取网页内容高度和宽度【包括滚动条等边线，会随窗口的显示大小改变】。
<p align="left"><strong>一、值</strong></p>
<p align="left">offsetHeight = clientHeight + 滚动条 + 边框。</p>
<p align="left"><strong>二、浏览器兼容性</strong></p>

<div>
<pre class="code">var w= document.documentElement.offsetWidth
    || document.body.offsetWidth;
var h= document.documentElement.offsetHeight
    || document.body.offsetHeight;

</pre>
<h2 id="J_CodeLang" class="code-head" data-lang="Javascript">网页卷去的距离与偏移量</h2>
<div id="J_CodeDescr" class="code-description">
<div class="code-desc co">

<strong>我们先来看看下面的图：</strong>

<a href="http://www.pengweb.net/wp-content/uploads/2015/02/5347b2b10001e1a307520686.jpg"><img class="attachment-medium" src="http://www.pengweb.net/wp-content/uploads/2015/02/5347b2b10001e1a307520686-300x274.jpg" alt="5347b2b10001e1a307520686" width="300" height="274" /></a>

<strong>scrollLeft:</strong>设置或获取位于给定对象左边界与窗口中目前可见内容的最左端之间的距离 ，即左边灰色的内容。

<strong>scrollTop:</strong>设置或获取位于对象最顶端与窗口中可见内容的最顶端之间的距离 ，即上边灰色的内容。

<strong>offsetLeft:</strong>获取指定对象相对于版面或由 offsetParent 属性指定的父坐标的计算左侧位置 。

<strong>offsetTop:</strong>获取指定对象相对于版面或由 offsetParent 属性指定的父坐标的计算顶端位置 。

<strong>注意:</strong>

<strong>1. 区分大小写</strong>

<strong>2. offsetParent：布局中设置postion属性(Relative、Absolute、fixed)的父容器，从最近的父节点开始，一层层向上找，直到HTML的body。</strong>

<a href="http://www.pengweb.net/wp-content/uploads/2015/02/54586e9b0001838b05000495.jpg"><img class="attachment-medium" src="http://www.pengweb.net/wp-content/uploads/2015/02/54586e9b0001838b05000495-300x297.jpg" alt="54586e9b0001838b05000495" width="300" height="297" /></a>

编程练习：
<h2 id="J_CodeLang" class="code-head" data-lang="Javascript">编程练习</h2>
<div id="J_CodeDescr" class="code-description">
<div class="code-desc co">

制作一个表格，显示班级的学生信息。

<strong>要求：</strong>

1. 鼠标移到不同行上时背景色改为色值为 #f2f2f2，移开鼠标时则恢复为原背景色 #fff

2. 点击添加按钮，能动态在最后添加一行

3. 点击删除按钮，则删除当前行

代码1：

&lt;!DOCTYPE html&gt;
&lt;html&gt;
&lt;head&gt;
&lt;title&gt; new document &lt;/title&gt;
&lt;meta http-equiv="Content-Type" content="text/html; charset=gbk"/&gt;
&lt;script type="text/javascript"&gt;

window.onload = function(){
var tr=document.getElementsByTagName("tr");
for(var i= 0;i&lt;tr.length;i++)
{
bgcChange(tr[i]);
}
// 鼠标移动改变背景,可以通过给每行绑定鼠标移上事件和鼠标移除事件来改变所在行背景色。
}
function bgcChange(obj)
{
obj.onmouseover=function(){                              <span style="color: #ff0000;">一个事件可以后边接一个函数-一定要是一个事件</span>
obj.style.backgroundColor="#f2f2f2";
}
obj.onmouseout=function(){
obj.style.backgroundColor="#fff";
}
}

// 编写一个函数，供添加按钮调用，动态在表格的最后一行添加子节点；
var num=2;
function add(){
num++;
var tr=document.createElement("tr");
var xh=document.createElement("td");
var xm=document.createElement("td");
xh.innerHTML="xh00"+num;
xm.innerHTML="第"+num+"学生";
var del=document.createElement("td");
del.innerHTML="&lt;a href='javascript:;' onclick='del(this)' &gt;删除&lt;/a&gt;";
var tab=document.getElementById("table");
tab.appendChild(tr);
tr.appendChild(xh);
tr.appendChild(xm);
tr.appendChild(del);
var tr = document.getElementsByTagName("tr");
for(var i= 0;i&lt;tr.length;i++)
{
bgcChange(tr[i]);
}
}

<span style="color: #ff0000;">下边红字是我自己写的，注意技巧和要点</span>

<span style="color: #ff0000;"> function add(){</span>
<span style="color: #ff0000;"> var a=document.getElementsByTagName("table")[0];       </span>

<span style="color: #0000ff;">***这里我用的不是ById 而是用的ByTagName()[];</span>

<span style="color: #0000ff;">因为如果是ByTagName()那肯定不是唯一的所以一定要指定后才能使用，所以加了[]</span>

&nbsp;

<span style="color: #ff0000;">var b=document.createElement("tr");</span>
<span style="color: #ff0000;"> b.innerHTML="&lt;td&gt;xh001&lt;/td&gt;&lt;td&gt;王小明&lt;/td&gt;&lt;td&gt;王小明&lt;/td&gt;"</span>

<span style="color: #0000ff;">***还有这里   innerHTML这个是本来就可以连html一起识别的，所以完全可以在这里写就可以了！！</span>
<span style="color: #ff0000;"> // var c=document.createElement("td");</span>
<span style="color: #ff0000;"> // var d=document.createElement("td");</span>
<span style="color: #ff0000;"> // var e=document.createElement("td");</span>
<span style="color: #ff0000;"> // c.innerHTML="第1个";</span>
<span style="color: #ff0000;"> // d.innerHTML="第2个"</span>
<span style="color: #ff0000;"> // e.innerHTML="第3个"</span>

<span style="color: #ff0000;"> // b.appendChild(c);</span>
<span style="color: #ff0000;"> // b.appendChild(d);</span>
<span style="color: #ff0000;"> // b.appendChild(e);</span>
<span style="color: #ff0000;"> a.appendChild(b);</span>
<span style="color: #ff0000;"> }</span>
// 创建删除函数
function del(obj)
{
var tr=obj.parentNode.parentNode;
tr.parentNode.removeChild(tr);
}

&lt;/script&gt;
&lt;/head&gt;
&lt;body&gt;
&lt;table border="1" width="50%" id="table"&gt;
&lt;tr&gt;
&lt;th&gt;学号&lt;/th&gt;
&lt;th&gt;姓名&lt;/th&gt;
&lt;th&gt;操作&lt;/th&gt;
&lt;/tr&gt;

&lt;tr&gt;
&lt;td&gt;xh001&lt;/td&gt;
&lt;td&gt;王小明&lt;/td&gt;
&lt;td&gt;&lt;a href="javascript:;" onclick="del(this);"&gt;删除&lt;/a&gt;&lt;/td&gt; &lt;!--在删除按钮上添加点击事件 --&gt;
&lt;/tr&gt;

&lt;tr&gt;
&lt;td&gt;xh002&lt;/td&gt;
&lt;td&gt;刘小芳&lt;/td&gt;
&lt;td&gt;<span style="color: #ff0000;">&lt;a href="javascript:;" onclick="del(this);"&gt;</span>删除&lt;/a&gt;&lt;/td&gt; &lt;!--在删除按钮上添加点击事件 --&gt;

上边这红字暂时这么记，href只是说他支持js但是具体还是要onclick来出发
&lt;/tr&gt;

&lt;/table&gt;
&lt;input type="button" value="添加一行" onclick="add()" /&gt; &lt;!--在添加按钮上添加点击事件 --&gt;
&lt;/body&gt;
&lt;/html&gt;

代码2：

&lt;!DOCTYPE html&gt;
&lt;html&gt;
&lt;head&gt;
&lt;title&gt; new document &lt;/title&gt;
&lt;meta http-equiv="Content-Type" content="text/html; charset=gbk"/&gt;
&lt;script type="text/javascript"&gt;

window.onload = function(){

// 鼠标移动改变背景,可以通过给每行绑定鼠标移上事件和鼠标移除事件来改变所在行背景色。
var str_tr=document.getElementsByTagName('tr');
for(var i=0;i&lt;str_tr.length;i++){
str_tr[i].setAttribute('onmouseover',document.all ? eval(function(){this.style.background="#f2f2f2"}) : 'javascript:this.style.background="#f2f2f2"');
str_tr[i].setAttribute('onmouseout',document.all?eval(function(){this.style.background="#fff"}):'javascript:this.style.background="#fff"');
}

}

// 编写一个函数，供添加按钮调用，动态在表格的最后一行添加子节点；
function addtr(){
var sNum=prompt('请输入学号','');
var sName=prompt('请输入姓名','');
if(sNum!=null&amp;&amp;sNum!=''&amp;&amp;sName!=null&amp;&amp;sName!=''){

var newtr=document.createElement('tr');
var newtrS=newtr.innerHTML='&lt;td&gt;'+sNum+'&lt;/td&gt;'+'&lt;td&gt;'+sName+'&lt;/td&gt;'+'&lt;td&gt;&lt;a href="javascript:;" onclick="del(this)"&gt;删除&lt;/a&gt;&lt;/td&gt;';
var oTC=document.getElementById("table").lastChild;
oTC.appendChild(newtr);

}else{alert('请重新输入');}
}

// 创建删除函数
<span style="color: #ff0000;">function del(obj){</span>
<span style="color: #ff0000;"> var oG=obj.parentNode.parentNode.parentNode;</span>
<span style="color: #ff0000;"> var oP=obj.parentNode.parentNode;</span>
<span style="color: #ff0000;"> oG.removeChild(oP);</span>

<span style="color: #0000ff;">这句最容易理解，值得推荐</span>
}
&lt;/script&gt;
&lt;/head&gt;
&lt;body&gt;
&lt;table border="1" width="50%" id="table"&gt;
&lt;tr&gt;
&lt;th&gt;学号&lt;/th&gt;
&lt;th&gt;姓名&lt;/th&gt;
&lt;th&gt;操作&lt;/th&gt;
&lt;/tr&gt;

&lt;tr&gt;
&lt;td&gt;xh001&lt;/td&gt;
&lt;td&gt;王小明&lt;/td&gt;
&lt;td&gt;&lt;a href="javascript:;" onclick="del(this)"&gt;删除&lt;/a&gt;&lt;/td&gt; &lt;!--在删除按钮上添加点击事件 --&gt;
&lt;/tr&gt;

&lt;tr&gt;
&lt;td&gt;xh002&lt;/td&gt;
&lt;td&gt;刘小芳&lt;/td&gt;
&lt;td&gt;&lt;a href="javascript:;" onclick="del(this)" &gt;删除&lt;/a&gt;&lt;/td&gt; &lt;!--在删除按钮上添加点击事件 --&gt;
&lt;/tr&gt;

&lt;/table&gt;
&lt;input type="button" value="添加一行" onclick="addtr()"/&gt; &lt;!--在添加按钮上添加点击事件 --&gt;
&lt;/body&gt;
&lt;/html&gt;

&nbsp;

方法3：（比较正规思维）

&lt;!DOCTYPE html&gt;
&lt;html&gt;
&lt;head&gt;
&lt;title&gt; new document &lt;/title&gt;
&lt;meta http-equiv="Content-Type" content="text/html; charset=utf-8"/&gt;
&lt;script type="text/javascript"&gt;
window.onload = function(){
var trs = document.getElementsByTagName('tr');
for(var i =0; i &lt; trs.length; i++){
trs[i].onmouseover = function(){
this.style.backgroundColor = "#f2f2f2";        <span style="color: #ff0000;">记得这里一定要用this 要不然不知道是谁</span>
}
trs[i].onmouseout = function(){
this.style.backgroundColor = "#fff";
}
}
}

function addTo(){
var table = document.getElementById('table').lastChild;

var tr = document.createElement('tr');

var td = document.createElement('td');
td.innerHTML="&lt;input type = 'text' /&gt;";
tr.appendChild(td);

td = document.createElement('td');
td.innerHTML="&lt;input type = 'text' /&gt;";
tr.appendChild(td);

td = document.createElement('td');
td.innerHTML='&lt;a href="#" onclick = "deleteItem(this);return false;" &gt;删除&lt;/a&gt;';
tr.appendChild(td);

table.appendChild(tr);
}

function deleteItem(obj){
var table = document.getElementById('table').lastChild;
var tr = obj.parentNode.parentNode;
table.removeChild(tr);

}
&lt;/script&gt;
&lt;/head&gt;
&lt;body&gt;
&lt;table border="1" width="50%" id="table"&gt;
&lt;tr&gt;
&lt;th&gt;学号&lt;/th&gt;
&lt;th&gt;姓名&lt;/th&gt;
&lt;th&gt;操作&lt;/th&gt;
&lt;/tr&gt;

&lt;tr&gt;
&lt;td&gt;xh001&lt;/td&gt;
&lt;td&gt;王小明&lt;/td&gt;
&lt;td&gt;&lt;a href="#" onclick = "deleteItem(this);return false;" &gt;删除&lt;/a&gt;&lt;/td&gt;
&lt;/tr&gt;

&lt;tr&gt;
&lt;td&gt;xh002&lt;/td&gt;
&lt;td&gt;刘小芳&lt;/td&gt;
&lt;td&gt;&lt;a href="javasript:;" onclick = "deleteItem(this);" &gt;删除&lt;/a&gt;&lt;/td&gt;
&lt;/tr&gt;
&lt;/table&gt;
&lt;input type="button" value="添加一行" onclick = "addTo();"/&gt;
&lt;/body&gt;
&lt;/html&gt;

<span style="color: #ff0000;">下边来说一个不在input里添加 onclick=什么的时间，但是要求他要有个id或其他name也许,用addEventListener来实现</span>

例如：

&lt;button id="btn"&gt;&lt;/button&gt;

&lt;script&gt;

document.getElementById(btn).addEventListener("click",function(){

alert("hello")

})

&lt;/script&gt;

<span style="color: #ff0000;">其中上边的click可以变幻成各种触发事件-----这个用处很大</span>

<span style="color: #ff0000;">然后后边那个函数，可以再进行改写一下，如下</span>

var x=document.getElementById("btn");

x.addEventListener("clock",hello())

function hello(){

alert("hello")

}

同样也可以移出事件

x.removeEventListener("clock",hello())

这样就不会显示hello了

&nbsp;

<span style="color: #ff0000;">DOM0事件处理</span>

&lt;button id="btn1"&gt;按钮&lt;/bottom&gt;

&lt;script&gt;

var btn1=document.getElementById("btn1")

btn1.onclick=function(){alert("hello")}   这个就是直接把一个函数赋值给这个事件

btn1.onclick=function(){alert("hello1")}    如果有这句的话结果只弹出hello1，只显示最后一个效果，所以改用DOM2事件

btn1.onclick=null;     清除事件 就没有事件了

&lt;/script&gt;

&nbsp;

DOM2事件：

就是上边的addevEntListener

例如

document.getElementById(btn).addEventListener("click",demo1（）)

document.getElementById(btn).addEventListener("click",demo2（）)

这里demo后边括号可以不加

function demo1(){

alert("hello1"）}

function demo2(){

alert("hello2"）}

上边这个会分别输出hello1，然后输出hello2

一样可以通过btn1.removeEventListener("click",demo2())

上边的兼容问题

ie是格式是attachEvent

和addEventListener是一样用法

通过判断语句来看是什么浏览器

var btn1=document.getElementById("btn1");

if(btn1.addEventListener){       假如这个浏览器支持这个语句则进行下边操作

btn1.addEventListener("clock",demo());

function demo(){

alert("hello")

}else  if（btn1.attachEvent）{     否则的话就是下边这句，让ie低版本运行

btn1.attachEvent("<span style="color: #ff0000;">onclock</span>",demo0())

function demo0{

alert("hello")}else{    <span style="color: #ff0000;">更低的时候就用DOM0事件就行了</span>

btn1.onclock=function(){alert("hello")}

}

}

&nbsp;

事件对象

type       应用  event.type

target      用法同上，获取事件的目标     下边例子是  buttom

stopPropagation():    阻止事件冒泡

preventDefault():    阻止事件默认行为

例子

document.getElementById(“btn”).addEventListener("colck",demo)

document.getElementById(“div”).addEventListener("colck",demo1)

<span style="color: #ff0000;">加了上边这句话后，按理说div是没有被点击的，只是点击了buttom产生的点击按钮</span>

<span style="color: #ff0000;">但是他会产生冒泡，div虽然没有被点击但是也被执行了，所以才用阻止冒泡的</span>

function demo(event){

alert(event.type)

event.stopPropagation();

<span style="color: #ff0000;">阻止事件冒泡要放在demo0里边，因为让他弹出后就执行这句话</span>

}

&nbsp;

function demo(event){

alert(“div”)}

<span style="color: #ff0000;">阻止事件行为：</span>

可以应用到阻止他弹出网页

&lt;a href="地址" id="aid"&gt;tiaozhuan&lt;/a&gt;

document.getElementById(“adi”).addEventListener("colck",demo2)

function demo2（event）{

event.preventDefault();  本来是应该跳转的，但是我用这句来阻止他跳转

}

&nbsp;
<h2 id="J_CodeLang" class="code-head" data-lang="Javascript">编程挑战</h2>
<div id="J_CodeDescr" class="code-description">
<div class="code-desc co">

现在利用之前我们学过的JavaScript知识，实现选项卡切换的效果。

<strong>效果图:</strong>

<img src="http://img.mukewang.com/53bd0e9e000163d203390200.jpg" alt="" />

<span style="color: #0000ff;">参考代码里：oLis[i].index = i;和oDivs[this.index].className = "";是什么意思？</span>

<span style="color: #0000ff;">第一句：给oLis中的所有元素设置一个索引值，便于查找</span>

<span style="color: #0000ff;">第二句：设置oDivs中的this.index元素中的className为空</span>
<h2><span style="color: #0000ff;">this.index就是你所点击li元素的索引所对应的div元素</span>
<span style="color: #ff0000;">当function被作为method调用时，this指向调用对象</span>。</h2>
</div>
</div>
</div>
</div>
</div>
</div>
</div>
</div>
</div>
</div>
</div>
</div>
</div>
</div>
</div>
</div>
</div>
</div>
</div>
</div>
</div>
</div>
</div>
</div>
</div>
</div>
</div>
</div>
</div>
</div>
</div>
</div>
</div>
</div>
</div>
</div>
</div>
</div>
</div>
</div>
</div>
</div>
</div>
</div>
</div>
</div>
</div>
</div>
</div>
</div>
</div>
</div>
</div>
</div>
</div>
</div>
</div>
</div>
</div>
</div>
</div>
</div>
</div>
</div>
</div>
</div>
</div>
</div>
</div>
</div>
</div>
</div>
</div>
</div>
</div>
</div>
</div>
</div>
<div class="codepen" data-height="729" data-theme-id="12905" data-slug-hash="NPLXqz" data-default-tab="js" data-user="duolew">
<pre><code>/**
 * Created by 鹏 on 2015/3/7.
 */

window.onload=function(){
        var gettab=document.getElementById("tab");
        var gettabul=gettab.getElementsByTagName("ul")[0];  //如果不通过gettab来找ul，那就要以全篇代码ul组成数组，太麻烦
        var gettabulli=gettabul.getElementsByTagName("li");
        var getdiv=gettab.getElementsByTagName("div");

            for (var i = 0; i &lt; gettabulli.length; i++) {    //不管三七二十一，先让他循环起来
                gettabulli[i].index=i;      //这句话我现在理解为，取出一个值，下边也保持一致使用这时候取出的值（索引目录）
                gettabulli[i].onmouseover=function(){    //上边取好值后，开始讨论取这个值时候li产生的现象
                    for(n=0;n&lt;gettabulli.length;n++) {   //其实这个就是格式化，让3个选项卡都变成一样的，之后再下边再设置被点击的那个！！
                        gettabulli[n].className = "";
                        getdiv[n].className = "hide";
                    }

                this.className="on";                       //取这个值得时候，就是鼠标在当前值上头，li的样式
                getdiv[this.index].className="txt";        //取这个值得时候，div的样式
                }
              }


}
</code></pre>
See the Pen <a href="http://codepen.io/duolew/pen/NPLXqz/">NPLXqz</a> by duolew (<a href="http://codepen.io/duolew">@duolew</a>) on <a href="http://codepen.io">CodePen</a>.

</div>
<script src="//assets.codepen.io/assets/embed/ei.js" async=""></script>