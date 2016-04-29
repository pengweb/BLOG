---
title: javascript高性能--学习笔记
date: 2016-03-20 14:12:05
tags: [javascript,笔记,note,js]

---

`递归的两个算法和回溯理解不好，BigPipe`

# 1.加载和执行

### 解析：

1.每次遇到`script`标签，都会霸道的让页面等待脚本解析和执行。
2.浏览器在解析到`body`标签之前，是不会渲染页面的任何部分的。
3.file1.js和file2.js之间**存在一个延时**，这段时间是file1.js执行的过程，所以下载和执行是逐个的。
4.开始加载图片，只在乎有没有图片，不在乎清不清晰，可以先加载模糊小图
5.更多加载参考文献：https://github.com/ChenChenJoke/JokerWebFont/tree/master/Performance

### 优化：

1.将script标签放到body底部
2.减少script标签数量。（每个script标签初始下载时都会阻塞页面渲染，并且下载js后会有延时，减少数量最小化延时）
3.不要直接放在link标签后，防止阻塞页面去等待样式表下载
4.减少外链数，下载1个100kb文件比4个25kb文件快
5.无阻塞脚本。
方法一：defer/async属性
实际应用中，执行顺序不定，所以不推荐
```
<script src='file.js' defer></script>
```

方法二：动态插入
元素被添加到页面时开始下载，无论何时启动下载和执行，都**不会阻塞**页面其他进程，所以放到head内更为保险。
如果文件内只含有供其他脚本调用接口时，会有问题，因为它无法判断是否自执行，所以就无法判断是否下载完成和准备就绪，所以通过判断readyState状态来进行插入。
```
function loadScript(url,callback){
	var script = document.creatElement('script');
	if (script.readyState){
		script.onreadystatechange = function(){
			if(script.readyState == "loaded" || script.readyState == "complete"){
				script.onreadystatechange = null;  //重置事件，避免处理两次
				callback();
			}
		}
	}else{
		script.onload = function(){
			callback();
		}
	}
	script.src = url;
	document.getElementsByTagName("head")[0].appendChild(script);
}
//注：如果想顺序执行，进行嵌套就可以了
```
方法三：XMLHttpRequest 脚本注入
大型的WEB应用不会采用这种方法
无法从CND下载，跨域问题
方法四（推荐）：
用方法二的loadScript(),把他放到body的底部。
好处：1.不会阻塞页面。2.DOM结构已经创建完毕，做好交互准备。


# 2.数据存取

### 分析：
1.字面量和局部变量存取数据最快，访问数组元素和对象成员代价更高。
2.**\[\[scope]]**包含了一个函数被创建的作用域中对象的集合，这个集合被称为函数的作用域链。
3.函数作用域中，每个对象被称为一个可变对象，每个可变对象都是以‘键值对’的形式存在。
4.函数每次执行时对应的**执行环境**都是独一无二的，所以多次调用同一个函数，会导致创建多个执行环境，造成性能问题，执行完毕后，执行环境会被销毁。
5.执行中，每遇到一个变量，都会经历一次解析**查找同名标识符**过程，搜索过程从作用域链头部开始，也就是活动对象开始，向作用域链下一个对象搜索，直到最外层的全局变量。正式这个搜索过程影响了性能。标识符所在位置越深，读写速度越慢。**局部变量总是最快的，全局变量是最慢的**，全局变量在最末端。
6.如果名字相同的两个变量存在作用域中，最先找到的那个会**遮蔽**后边那个。
7.闭包频繁访问**跨作用域**的标识符时，每次访问都会带来性能损耗。
8.对象的一个成员引用了一个函数的时候，称为"方法"，如果是非函数，则成为"属性"。
9.使用in操作符，可以搜索实例也可以搜索原型。只搜索实例可通过hasOwnProperty()来判断。
10.对象在原型链中的位置**越深**，找到它也就越慢。
*注意：改变作用域链很危险，不推荐使用！可以改变作用域链的语法有with语句eval语句和try···catch语句(异常对象推入catch内，且在作用域首位)*

### 优化：
1.将全局变量的引用存储在一个局部变量中。
```
var doc = document
```
2.将对象的属性或者方法存储在一个局部变量中。
```
var current = element.className;
```

# 3.DOM编程

### 分析：
1.DOM和javascript想象为一个岛屿，之间用收费桥梁连接，每次经过都要交费，次数越多，费用越多，所以尽可能减少过桥的次数。
2.通过getElementsByTagName()获得的是一个类数组的集合，读取一个集合的length比读取数组的length要慢的多。（高性能P43）
3.浏览器下载页面后解析。**DOM数→渲染树（DOM节点如何显示）→绘制。进行DOM操作后：DOM树→重新构造渲染树（重排）→重绘**。改变背景色不会改变宽高，所以不用重排，只用重绘。**获取布局信息**导致列队刷新重新渲染（重排）。
4.浏览器通道有7条9条的，老ie只有2条 document.write会阻塞通道

### 优化：
1.避免在讯中中访问或者修改DOM元素，应该用局部变量存储修改中的内容，循环结束后一次写入(innerHTML),把运算尽量留在ES这一端。
2.使用数组来合并大量字符串，这样让innerHTML效率更高。
3.将DOM集合放入一个数组内，求length要比直接对集合求length快。
```
//只是展示方法，并不推荐使用，因为在声明len这个变量的时候就已经是优化4的方法了
function toArray(coll){
	 a = [];
	 len = coll.length;            //其实这一步就已经进行了缓存，完全没有必要向下进行了
	for(var i = 0; i<len; i++){
		a[i] = coll[i];  //拷贝
	}
	return a;
}
var coll = document.getElementsByTagName('div');
var ar = toArray(coll);
function loopCopiedArray(){
	for (var count = 0; count<arr.length; count++){
		//代码处理
	}
}
```
4.当遍历一个集合时，第一优化原则是把**集合存储在局部变量中**，并把**length缓存在循环外部**，然后使用**局部变量替代这些需要多次读取的元素**。
```
function collectionLocal(){
	var coll = document.getElementsByTagName('div');
	len = coll.length,
	name = '';
	for(var count = 0; count<len; count++){
		name = coll[count].nodeName;      //避免在for内操作DOM集合
	}
}
```
5.childNodes是个集合，所以循环中注意缓存length属性，IE中nextSibling比childNodes要快很多。
6.最新querySelectorAll要比使用js和DOM遍历快很多，且得到一个Nodelist集合。
```
var element = document.querySelectorAll('#menu a');   //获取id为menu下的所有a标签
```
7.尽量少使用offsetTop、scrollTop、clientTop等获取布局信息属性，他们会刷新渲染列队，进行重排操作。
8.可以直接修改cssText避免一个样式修改多个style。
9.离线操作DOM，减少重绘和重排次数方法步骤：1.使元素脱离文档流 2.对其应用多重改变 3.把元素带回文档流

方法一：display
```
var ul = document.getElementById('mylist');
ul.style.display = 'none';
appendDataToElement(ul,data);     //上边定义的一个操作函数的方法
ul.style.display = 'block';
```

方法二：虚拟DOM
```
var fragment = document.createDocumentFragment();
appendDataToElement(fragment,data);       //对fragement进行操作；
document.getElementById('mylist').appendChild(fragment);
```

方法三：克隆
```
var old = document.getElementById('mylist');
var clone = old.cloneNode(true);
appendDataToElement(clone,data);
old.parentNode.replaceChild(clone,old);
```

10.队列化修改
将需要进行重排的操作放在一起进行执行
```
bodystyle.color = 'red';         //不需要重排
bodystyle.color = 'whith';       //不需要重排
tmp = computed.backgroundImage;  //需要重排
tmp = computed.backgroundColor;  //需要重排
```

11.赋值给变量-减少获取布局信息的次数，进行缓存布局
```
var current = myElement.offsetLeft;
```
12.脱离文档流，避免页面大面积重排
**绝对定位**或者浮动等脱离文档流属性
13.大量元素使用：hover，会降低响应速度
14.事件委托（高级程序设计P402）
每绑定一个事件处理器都是有代价的，事件绑定通常发生在onload或DOMContentReady时，此时对于富交互应用来说都是一个拥堵时刻，浏览器需要跟踪每个事件处理器，即占用了更多的内存又占用了更多处理时间，所以通过事件委托只绑定到一个事件处理器上。
```
//阻止浏览器默认事件和取消冒泡
if(typeof e.preventDefault === 'function'){
	e.preventDefault();
	e.stopPropagation();
}
```

# 4.算法和流程控制


### 分析：
1.死循环或者长时间运行的循环严重影响用户体验。
2.for循环初始化中的var语句创建的是一个函数级的变量，而不是循环级。
3.for···in循环，可以枚举任何对象的属性名，包括实例属性和原型链上的属性，且不分顺序。且他的循环速度是最慢的，因为每次迭代都要搜索实例和原型。
4.关注两点：每次迭代的事务复杂度，迭代的次数。
5.迭代潜在问题：终止**条件不明确**导致函数长时间运行，使得用户进入假死状态。而且还会遇到**调用栈大小限制**。
6.潜在调用栈溢出问题的脚本不应该被发布上线。
7.递归两种模式：
模式一：函数调用自身
```
function recurse(){
	recurse();
}
```

模式二：隐伏模式（互相调用）
```
function first(){
	second();
}
function second(){
	first();
}
```

### 优化：
减少迭代工作量：
1.局部变量，减少对象成员及数组项的查找次数。节省25%，IE节省50%；
```
len = items.length
```
2.颠倒数组的顺序，提高循环性能。
原理：减少一次判断，运行速度提高50%；
```
for(var i = items.length; i--){    //当i=0的时候，就为false了，就停止运行
	process(items[i]);
}
```
减少迭代次数
3.达夫设备（迭代数超过1000时候，效率才会明显提升）
```
var i = items.length % 8;     		//循环余数次
while(i){
	process(items[i--]);
} 
i = Math.floor(itmes.length / 8);   //迭代倍数
while(i){          
	process(items[i--]);       		//8个循环同时进行
	process(items[i--]);
	process(items[i--]);
	process(items[i--]);
	process(items[i--]);
	process(items[i--]);
	process(items[i--]);
	process(items[i--]);
}
```
4.基于函数的迭代要比基本的for循环慢8倍。
函数迭代一般有：原生forEach(),jquery的each()等
5.if···else 最多判断4次，否则选择switch判断。
6.if最可能出现的情况放在首位判断。
7.if···else判断次数超过4次的时候，可以通过**嵌套**来**缩小范围**。
8.查找表：将集合存入数组，进行查表，适用于离散值太多的时候。
```
//完全抛弃循环语句
var results = [result0,result1,result2,result3,result4];   
return results[value]     //返回对应元素的值
```
**9.避免递归，改用迭代**
```
//合并排序
function mergeSort(items){
	if(items.length == 1){
		return items;
	}
	var work = [];
	for(var i=0, len=items.length; i<len; i++){
		work.push([items[i]]);
	}
	work.push([]);  //如果数组长度为奇数
	for(var lim=len; lim>1; lim=(lim+1)/2){
		for(var j=0,k=0; k<lim; j++, k+=2){
			work[j]=merge(work[k], work[k+1]);
		}
		work[j] = [];  //如果数组长度为奇数
	}
	return work[0];
}
```

**10.Memoization**
缓存，避免重复的计算
```
function memoize(fundamental,cache){
	cache = cache || {};
	var shell = function(arg){
		if(!cache.hasOwnProperty(arg)){
			cache[arg] = fundamental(arg);
		}
		return cache[arg];
	}
	return shell;
}
//缓存阶乘函数
var memfactorial = memoize(factorial,{'0':1,'1':1});   
//调用新函数
var fact6 = memfactorial(6); 
```

# 5.字符串和正则表达式

### 分析：
1.构建字符串的常用方法是：通过一个循环不断向字符串末尾添加内容，所以字符串构建是非常糟糕的。
2.IE8的连接原理是：创建一个新的空间，然后分别放进去，代替旧的字符串引用。
3.通过Array.prototype.join进行合并字符串比其他方法都慢！
4.赋值表达式中所有要连接的字符串都属于编译器常量，运行期花在连接过程的时间和内存可以减少到零，这种做法非常不错。
5.使用concat比普通的+和+=稍慢。
6.两个正则表达式匹配相同的文本并不意味着执行速度一样。
7.部分匹配比完全不匹配所用的时间要长。
8.正则工作原理：**编译→设置起始位置→匹配每个正则表达式字元→匹配成功或失败。**
9.正则尝试2变后都失败才确认失败。
10.回溯：像是在走岔路口，当遇到岔路的时候就先在每个路口做一个标记。如果走了死路，就可以照原路返回，直到遇见之前所做过的标记，标记着还未尝试过的道路。如果那条路也走不能，可以继续返回，找到下一个标记，如此重复，直到找到出路，或者直到完成所有没有尝试过的路。
11.回溯会产生昂贵的计算消耗（低效之源）
12.正则表达式慢的原因通常是匹配失败的过程慢，而不是匹配成功的过程慢。

### 优化：
1.合并字符串方法：
```
str =+ "one" + "two";          //对str进行扩充，性能最好，但是IE不太适合
str = str + "one" + "two";    //和上句效果相同
```
2.正则表达式赋值给一个变量。避免重复执行这一步。
3.回退取值
匹配第三个字母是x的字符串
解决办法:先找到x，然后再将起始位置回退两个字符。
4.匹配任意字符用\[\s\S]而不用.
5.尽量避免使用贪婪或者惰性词。贪婪量词*替换成惰性（非贪婪）量词*?
6.定义其实标志（^或$）,字符类（\[a-z]或类似\d的速记符）和单词边界（\b）
7.分支尽量放在最前面，还有能不用分支尽量不用分支
cat|bat   可以写成\[cb]at
8.尽量使用非捕获组（?:）
9.暴露必须的字元
优化前：/(^ab|^cd)/    优化后：/^(ab|cd)/ 
10.将复杂的表达式拆分成多个简单的片段
11.搜索字面字符串的时候，尽量使用属性方法来获取，避免正则
```
//检查是否分号结尾
endsWithSemicolon = /;$/.test(str);
endWithSemicolon = str.charAt(str.length -1) == ";";
```
12.去除首位空白，原生js方法trim()
方法一：使用两个表达式，这种方法最周全推荐使用
```
if(!String.prototype.trim){
	String.prototype.trim = function(){
		return this.replace(/^\s+/,"").replace(/\s+$/,"")
	}
}
```
其他方法请查阅：高性能Javascript P100
13.**避免回溯失控：使相邻的字元互斥，避免嵌套量词对同一字符串的相同部分多次匹配，通过重复利用预查的原子组去除不必要的回溯。**


# 6.快速响应的用户界面
分析;
1.用户执行javascript和更新用户界面的进程通常称为“浏览器UI线程”，执行顺序为队列形式，要么运行javascript要么执行UI更新。大多数浏览器在javascript运行时会停止把心任务加入UI线程的队列中，也就是说javascript任务必须尽快结束，避免对用户体验造成影响。
2.浏览器限制了javascript运行时间。限制分两种：调用栈大小限制和长时间运行脚本限制。
3.度量运行时间多长两种方法：总时间不应该超过100毫秒
第一种是记录自脚本开始以来知性的语句的数量。
第二种是记录脚本执行的总时间。
4.当脚本执行时，**UI不随用户交互而更新**。所以为了更快响应用户，就应该通过定时器的方法来新增加一条UI线程，进行异步执行。
![](/images/定时器.jpg)

5.创建一个定时器会造成UI线程暂停，如果它从一个任务切换到下一个任务。定时器代码会重置所有相关的浏览器限制，包括长时间运行脚本定时器，**调用栈也被重置为0**。
6.定时器不可用于测量实际时间，因为不一定在设定时间后加入队列，要等之前任务完成才加入队列。
7.定时器处理数组副作用：总时常增加。因为每一条处理完成后，UI线程会空闲出来，并且在下一条开始处理之前会有一段延迟。为了避免锁定浏览器，用定时器也是有必要的。
8.Web worker不占用UI线程，每个新的Worker都在自己的线程内运行代码。
9.每个Web work都有自己的全局运行环境，其功能只是js的一个子集。属性见（高性能P120）
10.通过postMessage()方法,实现网页代码和Worker的数据传入和传出。
11.Web Workers适用于那些处理纯数据，或者与浏览器UI无关的长时间运行的脚本。一般为：编码/解码大字符串，复杂数学运算（包括视频和图像处理），大数组排序等等任何超过100毫秒的任务。

### 优化：
1.把循环的工作分解到一系列定时器中。考虑：**处理过程是否必须同步。数据是否必须按顺序执行。**
```
setTimeout(function(){
	process(todo.shift());   //可以取到todo.shift()删除掉的值
	//tudo是一个数组，如果还有需要处理的元素，创建另一个定时器
	if(todo.length>0){
		setTimeout(arguments.callee,25)    //调用自身函数
	}
},25);
```
2.分割任务：把一个任务分解成一系列的子任务。每个独立的方法放到一个数组内，通过定时器分别执行。
3.跟踪代码执行时间
```
var star = +new Data();   //+的作用是转换成数字
process();
var stop = +new Data();
var time = stop-star;
```
4.定时器嵌套实现有序定时器。定时器序列，同一时间只有一个定时器存在，只有当这个定时器结束时才会新创建一个。这样**有序执行**，就不会造成同一时间多个定时器存在，造成性能问题了。由最外层向最内层执行。
5.创建一个独立的重复定时器，每次执行多个任务。
6.Web Workers用法（高级程序设计P699）
WebWorkerExample01.html
```
<script>
        (function(){
            var data = [23,4,7,9,2,14,6,651,87,41,7798,24],
            worker = new Worker("WebWorkerExample01.js");   //创建web worker线程             
            worker.onmessage = function(event){  //onmessage监听接收信息时间
                alert(event.data);   //data是从WebWorkerExample01.js传来的处理后数据
            };
            worker.postMessage(data);    //将数组的data传给WebWorkerExample01.js     
        })();
</script>
```
WebWorkerExample01.js
```
self.onmessage = function(event){
    var data = event.data;   //这个data应该是页面中已经从ajax或者数组自定义的data
    data.sort(function(a, b){
        return a - b;
    });
    self.postMessage(data);    //将处理好的data传回网页
};
```

# 7.Ajax

### 分析：
1.多种方法向服务器请求数据：XHR、script动态脚本注入，iframes，Coment(短轮询服务器接口来回关闭，长轮询时候服务器接口一直打开)，Multipart XHR, CORS，SSE，Web Sockets
2.GET请求的数据会被缓存起来，且GET只发送一个数据包，而一个POST请求，至少发送两个数据包，一个装载头信息，另一个装在POST正文，如果请求多次请用GET。POST更适合发送大量数据到服务器，因为不关心额外数据包的数量，另一个原因是对URL长度没有限制，GET是有长度限制的。
3.上边有介绍动态脚本注入的方法，缺点是注入失败也不会得到反馈，而且不能访问请求头信息，必须封装在一个function函数内，而且还不安全，但是速度却非常快。
4.Multipart XHR是通过给图片加上base64码（这个码就是js内容）来通过XHR进行请求的（因为图片文件是没有安全策略的，还有就是**可以同时传送多个图片，减少http请求次数**，实时执行操作，readyState==3）。缺点：不能被浏览器缓存，老版本IE不支持readyState为3的状态。
5.Ajax最大的瓶颈就是Http请求，因此减少其数量会对整个页面的性能有很大的影响。
6.图片信标：非常类似动态脚本注入，创建一个新image对象，并把src属性设置为服务器上脚本的URL。该URL包含了我们通过GET传回的键值对数据。服务器回传数据最快且最有效的方式。缺点：无法发送POST，而且URL长度有限制（高性能P133）
7.XML：XML及其冗长而且语法有些模糊。
8.XPath在解析XML文档时比getElementsByTagName快许多。未被广泛支持，且必须使用旧式DOM遍历方法编写降级的代码。
9.JSON可以通过eavl()来解析JSON字符串，但是不推荐用这个，因为在解析的时候会自动执行JSON内部的javascript代码。所以尽可能使用JSON.parse().
标准版
```
[{
    "id":1,
    "username":'zhp'
}]
```

简化版：
```
[{
    "i":1,
    "u":'zhp'
}]
```

数组版：文件最小，下载最快，解析速度快出30%
```
[[1,zhp]]
```
10.JSON-P动态注入JSON文件，注入的是源生的javascript，所以文件会增大，不过不用解析，所以文件增大造成的影响是微不足道的。文件大小和下载耗时与XHR比，基本相同，但是解析速度提升了10倍。
11.HTML是一种缓慢又臃肿的数据格式。服务器生成HTML速度更快，但是数据占用更多的空间，传给客户端的时候需要很多的带宽。还有就是通过JSON传送客户端，客户端通过javascript来生成HTML。这需要大量的字符串操作，而字符串操作也是javascript中最慢的部分。
12.自定义格式：用一些简单的分隔符将数据链接起来，然后通过split()方法将其转化成数组形式。
![](/images/QQ截图20160310141455.jpg)

13.MXHR能大幅提升性能的主要原因是通过监听readyState为3的状态，我们可以在一个较大的响应还没有完全接受之前把它分段处理，这使得我们可以实时处理响应片段。

### 优化：

1.最快的Ajax的请求就是没有请求，所以进行缓存数据，让其不进行缓存。有两种方式
方法一：在服务器端，设置HTTP头信息以确保你的响应会被浏览器缓存。（简单好维护，缓存内容可以跨页面和跨会话）
Ajax请求必须使用GET请求。
Expires头信息格式：
```
Expires: Mon, 28 Jul 2099 23:30:00 GMT   //设置一个遥远的时间点（不能超过1年），且日期是GMT时间
```
PHP服务器上设置：
```
$lifetime = 7*24*60*60;   //7天，按秒计算
header('Expires: ' . gmdate('D, d M Y H:i:s', time() + $lifetime) . 'GMT');
```
```
$lifetime = 7*365*24*60*60;   //10年，按秒计算
header('Expires: ' . gmdate('D, d M Y H:i:s', time() + $lifetime) . 'GMT');
```
方法二：在客户端，将获取到的信息存储到本地，从而避免再次请求。（最大化控制权，废止缓存内容并获取更新）
```
var localCache = {};
function xhrRequest(url,callback){
	//检查此URL的本地缓存
	if(localCache[url]){
		callback.success(localCache[url]);
		return;
	}
	//此URL对应的缓存没有找到，则发送请求
	var req = createXhrObject();
	req.onerror = function(){
		callback.error();
	}
	req.onreadystatechange = function(){
		if(req.readyState ==4){
			if(req.responseText === '' || req.status == '404'){
				callback.error();
				return;
			}
			//存储响应文本到本地缓存
			localCache[url] = req.responseText;
			callback.success(req.responseText);
		}
	}
	req.open('GET',url,true);
	req.send(null);
}
```
2.减少请求数，合并js和css


# 8.编程实践
1.避免双重求值：一段js代码中执行另一段js代码，会导致双重求值的性能消耗。四种方法可能出现这种现象：eval()、Function()构造函数、setTimeout()和setInterval().双重求值比直接包含的代码执行速度慢许多。
```
result = eval('num1 + num2')  //括号内的字符串会自动运行-双重求值
```
2.无论javascript代码如何优化，都不会比javascript引擎提供的原生方法更快，所以尽量使用原生内置方法，例如Math对象，尽量使用内置属性。
3.querySelector()和querySelectorAll()比jQuery获取速度快将近10%。

### 优化：

1.建议传入函数而不是字符串--避免双重求值
2.创建对象和数组时，使用直接量是最快的方法；
```
var myObj = {};
var myArr = [];
```
3.避免重复执行：
方法一：
添加和移除事件处理器。
```
function addHandler(target,eventType,handler){
	if(target.addEventListener){
		target.addEventListener(eventType,handler,false)
	}else{
		target.attachEvent("on"+eventType,handler);
	}
}
function removeHandler(target,eventType,handler){
	if(target.removeEventListener){
		target.removeEventListener(eventType,handler,false)
	}else{
		target.detachEvent("on"+eventType,handler);
	}
}
```
**方法二：**
延迟加载-第一次调用进行重写addHandler,第二次调用的就是重写后的addHandler了，引用函数特性！
缺点：要执行一次后，下一次的时候才能用新的.
```
function addHandler(target,eventType,handler){
	if(target.addEventListener){
		target.addEventListener(eventType,handler,false)
	}else{
		target.attachEvent("on"+eventType,handler);
	}
        addHandler(target,eventType,handler)    //只多了这句重写addHandler
}
function removeHandler(target,eventType,handler){
	if(target.removeEventListener){
		target.removeEventListener(eventType,handler,false)
	}else{
		target.detachEvent("on"+eventType,handler);
	}
        removeHandler(target,eventType,handler)    //只多了这句重写removeHandler
}
```
方法三：
条件预加载-通过三元运算符来一次性重置函数
```
var addHandler = document.body.addEventListener?
	function(target,eventType,handler){
		target.addEventListener(eventType,handler,false)
	}:
	function(target,eventType,handler){
		target.attachEvent(eventType,handler,false)
	};
var removeHandler = document.body.addEventListener?
	function(target,eventType,handler){
		target.removeEventListener(eventType,handler,false)
	}:
	function(target,eventType,handler){
		target.detachEvent(eventType,handler,false)
	};
```
3.位操作-通过转化为2进制（toString(2)），然后通过对0/1判断true或者false
速度比原始版本快50%
```
25.toString(2);//11001
3.toString(2);//11
25&3 //1  为真

if(i%2){ }   //一直在0/1之间切换，所以可以用来做切换判断
if(i&1){ }   //效果和上边相同 
```
4.文件复用：像html，css等的复用，换肤，reset，报错页面，播放器或音乐
5.模块复用：用js绘制header，footer 。 iframe一般都是嵌入广告，先把文件拿过来，再去请求，浪费资源
6.分级加载：重要的先加载，视频->广告->评论，所以这些最好通过异步来加载
7.按需加载：惰性加载-滑倒底部后进行加载	


# 9.BigPipe
重要的东西同步加载，不重要的东西异步加载–首屏重要可以先加载，然后再加载下边的
下载时间不会缩短，只是做到按需加载，通过异步，先加载重要的，其他的通过异步加载
参考文献：
http://www.cnblogs.com/mofish/archive/2011/11/03/2234858.html
原理：
占位符：一个空的div，留着用js通过异步插入内容
textarea：通过后端把要传入的数据打到前端textarea内，textarea不会解析源码，当调用的时候取出来，平时用display：none来隐藏

### 缺点：
1.连接数增多，如果dns不好，比如国外用户，每次链接成本都很高，那很不适合
2.爬虫只能爬到html，接口返回的内容是爬不到的，爬接口的话，如果ip不是本域的话，是没有cookie，就是没有session权限的，也是没法获取的。还有就是如果通过跨域的话，如果请求量过高的话，服务器会把爬虫禁止掉的，因为会爬缓存和数据库，对服务器压力很大，所以爬虫只能爬到有占位符的文档
3.因为都是异步的，所以通信顺序就很难把握，做加载队列，又很麻烦
4.通过后端渲染到textarea里，然后就不用重复去请求服务器，但是如果有三个模块用到一个url的时候，就需要用一些观察者模式的方法，或者hashMap

# 10.构建并部署高性能javascript应用

### 优化
1.合并多个javascript文件
2.javaScript文件压缩
3.javascript的HTTP压缩。web浏览器请求资源时，通常会发送一个Accept-Encoding HTTP头来告诉Web服务器它支持哪种编码转换类型。
Accept-Encoding可用的值包括gzip、compress、deflate、identity。服务器看到这个请求头会选择最适合的编码方法，并通过Content-Encoding HTTP头通知客户端它的决定。
4.Gzip最流行的编码格式，减少70%下载量，提升性能的**首选武器**。图片或者PDF文件不应该使用Gzip压缩，因为他们本身已经被压缩过了。（高性能P170）
5.缓存javascript文件。通过Expires HTTP响应头。日期不应超过1年。手机端会有缓存大小限制，最好不要超过15k，超过15k可以拆分多个文件进行缓存，但是这样的话HTTP连接数就会增加，所以也是视具体情况而定。
设置过期时间有两种方法：
第一种：在HTTP头部直接设置时间。P146
第二种：Apache web server有ExpiresDefault指令，也可以通过这种方法来设置时间。P172
6.HTML5的manifest file是一种更好的方法，不会有Expires的问题。
7.可以通过添加时间戳来更新缓存
8.内容发布到CDN上-但是如果国外访问,DNS查询成本太高，有可能会更慢.
9.keep-alive 正常http有三次握手，同一个域名或ip复用，沿用之前的路径
10.cache-static 当访问不到的时候，也要给静态页面，让能看到完整的页面
11.图片优化的6种方法：

1. 使用base64编码代替图片
场景：适用于图片大小小于2KB，页面上引用图片总数不多的情况 原理：将图片转换为base64编码字符串inline到页面或css中 优势：减少http的请求次数，并可以放到后台数据库中，只传输字符串，有较多的构建工具可以直接实现 劣势：这种方法仅限于图片总数较少，而且图片大小小于2KB的情况。否则图片字符串会变得很长很长

2. 合并图片sprite(雪碧图)
场景：任何用到页面图片的场景 原理：将多个页面上用到的背景图片合并成一个大的图片在页面中引用 优势：可以有效的较少请求个数，而且，而不影响开发体验，使用构建插件可以做到对开发者透明。适用于页面图片多且丰富的场景。 劣势：生成的图片体积较大，减少请求个数同时也增加了图片大小，不合理拆分将不利于并行加载

3. 使用css、svg、canvas或iconfont代替图片
css代替图片
场景：适用于移动端或较高级的浏览器，而且绘制的图案较为简单。 原理：css方式可以用来绘制相对简单的团来代替图片，一般使用before或者after伪元素来丰富图案的复杂度。 优势：具有实现简单，图片体积小的特点，可以实现简单的动态效果 劣势：也受限于css的兼容性特点，绘制复杂图案困难svg的描述和适用场景上文已说明。

canvas代替图片
场景：需要高性能的图片或动画 原理：适用html5的canvas元素绘制创建图片 优势：整个就是画2D图形时，页面渲染性能比较高，页面渲染性能受图形复杂度影响小，性能只受图形的分辨率的影响，画出来的图形可以直接保存为 .png 或者.jpg的图形，适合于画光栅图像或者不规则图形 劣势：没有dom操作，必须依赖定时器，文字渲染性能差，不能添加描述(title属性什么的)，兼容性限制

iconfont是一种web字体来代替图片的解决方案
场景：代替页面上色彩单一的图片 
优势：兼容性好，应用广，目前使用也很广泛 
劣势：但是由于字体的颜色设置单一，只能用于代替颜色单一的图片，对于色彩复杂的图片，iconfont处理起来比较困难

4. 响应式图片
场景：不同终端对同一个图片需求不一样，可以根据终端加载不同的图片来节省没必要的流量 原理：通过picture元素，picturefill或平台判断来为不同终端平台输出不同的图片 优势：减少没必要的图片加载，灵活控制，慢速用户加载小图片不至于加载失败，移动端没必要加载大尺寸图片等，可以通过不同方式兼容所有浏览器 劣势：无法避免图片的加载过程，图片本身没优化

5. 图片压缩
场景：在不得不加载图片的前提下，要进一步提升优化效果，只能通过有损或无损压缩来减少图片的大小。
原理：对图片进行无损、有损压缩，转为压缩后图片来实现 优势：减少图片加载流量，效果比较明显 劣势：服务器和浏览器压力增大，而且服务器需要额外的服务支持

6. 更好的图片格式
场景：之前说到webp、bpg、sharpP等新图片格式具有更好的压缩比，可以使用这类新型的图片来代替原始图片 原理：对图片格式转换，在画质可以接受的情况下达到更好的压缩比效果 优势：减少图片加载流量，效果比较明显 劣势：服务器和浏览器压力增大，而且服务器需要额外的服务支持，格式转换要考虑浏览器的兼容性

# 11.DNS寻址及IP解析
当输入一个IP地址进行访问一个网站时候，最好设置一个301跳转将这个地址跳转到域名下，然后再通过域名再分配一个离用户最近的服务器或者网路最好的机房，这样访问速度就会更快
301和302跳转的区别：301为永久性跳转，302为临时性跳转，对seo不利
每次客户登陆的时候，都会产生一个cookie，当链接服务器的时候，发送给服务器，被认为是一个合法用户
域名解析方法是从右向左的，先解析的是.这个.是公网，最最外层的域名，然后才是com
一般运营商都会有一个自己的网址地图Hash Map,所以一般不用加.最后
TCP是传输协议，倒数第四层，IP属于网络层的协议，进行寻址，倒数第三层

# 12.调试工具

## Chrome命令
1.查找文件或内容
```
Ctrl+P
```
2.在文档内查找
```
Ctrl+Shift+F
```
3.保存Console
```
在Console面板右边有一个Preserve log勾选上
```
4.格式化压缩过的代码
```
{} 点这个符号
```
5.选择下一个匹配项
```
Ctrl+D
```

## 方法：
1.通过new Date()测量脚本运行时间。
2.分析匿名函数的最佳办法：是给他们取个名字，使用指针指向对象的方法。
通过下边这种方法这个匿名函数在Chrome这种调试工具中就有名字了。
方法一：
```
myNode.onclick = function newName(){   //给这个匿名函数添加个名字newName
	myApp.loadData();
}
var onClick = function newName2(){    //给声明为变量onClick的匿名函数添加个名字newName2
	myApp.loadData();
}
```
方法二：（自己推测并未考证）
通过new Date()方法，让匿名函数自执行来求运行时间。
3.查看栈的信息
```
console.trace()
```
4.输出数组数据
```
console.table(arr)
```
5.测试函数运行时间--也可以测循环语句时间
```
console.time()
函数
console.timeEnd()
```
6.测试更复杂的函数且显示更详细的问题-配合Profiles查看。
将profileEnd()调用封装在setTimeout中,使得可以异步生成报告，而不阻塞脚本执行。
结果：显示每个函数所花的时间，调用的次数，占总开销的百分比，及其他更多数据。

```
console.profile()
函数
console.profileEnd()
```
7.Chrome网络面板
每个资源后面的色块条将加载过程分解为不同阶段（DNS查找、等待响应）
蓝色表示页面DOMContentLoad时间触发的时刻。红色表示window的load事件触发的时刻。
每个脚本都在等待前一个脚本下载完成后才发起下一个请求。
8.Profiles
1.Collect Javascript CPU Profile
查看javascript CPU使用情况
2.Take Heap Snapshot(一般查看这个)
查看栈堆对象及相关DOM节点内存分配
用法：运行start，然后执行事件，再点击左上角黑圆点图标进行快照比较
3.Record Heap Allocations
记录对象分配超时，隔离内存泄漏
**9.Timeline**
网络和HTML解析(蓝色)，JavaScript(黄色)，样式重计算和布局(紫色)以及绘画和合成(绿色)事件
参考文章：http://www.oschina.net/translate/performance-optimisation-with-timeline-profiles
10.更多Chrome使用技巧
参考文章：https://github.com/ChenChenJoke/JokerChrome

# 13.测试工具

1.YSlow工具   
```
http://yslow.org/
```

2.奇云测
```
http://ce.cloud.360.cn/
```

3.阿里测
```
http://www.alibench.com/
```

4.百度应用性能检测中心
```
http://developer.baidu.com/apm/
```

5.Web PageTest
```
http://www.webpagetest.org/
```

# 14.雅虎军规
1.\[内容]尽量减少HTTP请求数
2.\[服务器]使用CDN（Content Delivery Network）
3.\[服务器]添上Expires或者Cache-Control HTTP头
4.\[服务器]Gzip组件
5.\[css]把样式表放在顶部
6.\[js]把脚本放在底部
7.\[css]避免使用CSS表达式
8.\[js, css]把JavaScript和CSS放到外面
9.\[内容]减少DNS查找
10.\[js, css]压缩JavaScript和CSS
11.\[内容]避免重定向
12.\[js]去除重复脚本
13.\[服务器]配置ETags
14.\[内容]让Ajax可缓存
15.\[服务器]尽早清空缓冲区
16.\[服务器]对Ajax用GET请求
17.\[内容]延迟加载组件
18.\[内容]预加载组件
19.\[内容]减少DOM元素的数量
20.\[内容]跨域分离组件
21.\[内容]尽量少用iframe
22.\[内容]杜绝404
23.\[cookie]给Cookie减肥
24.\[cookie]把组件放在不含cookie的域下
25.\[js]尽量减少DOM访问
26.\[js]用智能的事件处理器
27.\[css]选择 舍弃@import
28.\[css]避免使用滤镜
29.\[图片]优化图片
30.\[图片]优化CSS Sprite
31.\[图片]不要用HTML缩放图片
32.\[图片]用小的可缓存的favicon.ico（P.S. 收藏夹图标）
33.\[移动端]保证所有组件都小于25K
34.\[移动端]把组件打包到一个复合文档里
35.\[服务器]避免图片src属性为空
翻译：http://www.tuicool.com/articles/J3uyaa
官网：https://developer.yahoo.com/performance/rules.html

**雅虎军规不适用的地方：**
视频网站，先加载视频，浏览器是默认后加载，如果视频网视频后出来就不太符合了
游戏的话，要让背景和声音先出来而不能让数字先出来
多域名拆分cdn，在国外不适用
![](/images/前端性能优化.png)
