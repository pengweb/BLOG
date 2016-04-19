---
title: jquery--学习笔记
date: 2016-03-17 22:30:13
tags: [Javascript,jquery，笔记,note,js]

---
# 1.选择器
## 1.1基本选择器
``` js
$("#myELement")   //选择id值等于myElement的元素，id值不能重复在文档中只能有一个id值是myElement所以得到的是唯一的元素 
$("div")          //选择所有的div标签元素，返回div元素数组 
$(".myClass")     //选择使用myClass类的css的所有元素 
$("*")            // 选择文档中的所有的元素，可以运用多种的选择方式进行联合选择：例如$("#myELement,div,.myclass")
```
## 1.2层叠选择器
``` js
$("form input")      //选择所有的form元素中的input元素 
$("#main > *")       //选择id值为main的所有的子元素 
$("label + input")   //选择所有的label元素的下一个input元素节点，经测试选择器返回的是label标签后面直接跟一个input标签的所有input标签元素 
$("#prev ~ div")     //同胞选择器，该选择器返回的为id为prev的标签元素的所有的属于同一个父元素的div标签
```
## 1.3基本过滤选择器
``` js
$("tr:first")       //选择所有tr元素的第一个 
$("tr:last")        //选择所有tr元素的最后一个 
$("input:not(:checked) + spa   //过滤掉：checked的选择器的所有的input元素
$("tr:even")        //选择所有的tr元素的第0，2，4... ...个元素（注意：因为所选择的多个元素时为数组，所以序号是从0开始）
$("tr:odd")         //选择所有的tr元素的第1，3，5... ...个元素 
$("td:eq(2)")       //选择所有的td元素中序号为2的那个td元素 
$("td:gt(4)")       //选择td元素中序号大于4的所有td元素 
$("td:lt(4)")       //选择td元素中序号小于4的所有的td元素 
$(":header")        //选择h1、h2、h3之类的
$("div:animated")   //选择正在执行动画效果的元素
```
## 1.4内容过滤选择器
``` js
$("div:contains('John')")    //选择所有div中含有John文本的元素 
$("td:empty")                //选择所有的为空（也不包括文本节点）的td元素的数组 
$("div:has(p)")              //选择所有含有p标签的div元素 
$("td:parent")               //选择所有的以td为父节点的元素数组 
``` 
## 1.5可视化过滤选择器
$("div:hidden")      //选择所有的被hidden的div元素 
$("div:visible")     //选择所有的可视化的div元素 
## 1.6属性过滤选择器
``` js
$("div[id]")                     //选择所有含有id属性的div元素 
$("input[name='newsletter']")    //选择所有的name属性等于'newsletter'的input元素
$("input[name!='newsletter']")   //选择所有的name属性不等于'newsletter'的input元素
$("input[name^='news']")         //选择所有的name属性以'news'开头的input元素 
$("input[name$='news']")         //选择所有的name属性以'news'结尾的input元素 
$("input[name*='man']")          //选择所有的name属性包含'news'的input元素
$("input[id][name$='man']")      //可以使用多个属性进行联合选择，该选择器是得到所有的含有id属性并且那么属性以man结尾的元素
```
## 1.7子元素过滤选择器
``` js
$("ul li:nth-child(2)"),$("ul li:nth-child(odd)"),$("ul li:nth-child(3n + 1)")
$("div span:first-child")      //返回所有的div元素的第一个子节点的数组 
$("div span:last-child")       //返回所有的div元素的最后一个节点的数组 
$("div button:only-child")     //返回所有的div中只有唯一一个子节点的所有子节点的数组
```
## 1.8表单元素选择器
``` js
$(":input")        //选择所有的表单输入元素，包括input, textarea, select 和 button
$(":text")         //选择所有的text input元素 
$(":password")     //选择所有的password input元素 
$(":radio")        //选择所有的radio input元素 
$(":checkbox")     //选择所有的checkbox input元素 
$(":submit")       //选择所有的submit input元素 
$(":image")        //选择所有的image input元素 
$(":reset")        //选择所有的reset input元素 
$(":button")       //选择所有的button input元素 
$(":file")         //选择所有的file input元素 
$(":hidden")       //选择所有类型为hidden的input元素或表单的隐藏域	
```
## 1.9表单元素过滤选择器
``` js
$(":enabled")               	//选择所有的可操作的表单元素 
$(":disabled")              	//选择所有的不可操作的表单元素 
$(":checked")               	//选择所有的被checked的表单元素 
$("select option:selected") 	//选择所有的select 的子元素中被selected的元素
```
## 1.10应用实例
1.通过jquery的$()引用元素包括通过id、class、元素名以及元素的层级关系及dom或者xpath条件等方法，且返回的对象为jquery对象（集合对象），不能直接调用dom定义的方法。
2.只有jquery对象才能使用jquery定义的方法。注意dom对象和jquery对象是有区别的，调用方法时要注意操作的是dom对象还是jquery对象。
3.jQuery对象和DOM对象互换
（1）普通的dom对象可以通过$()转换成jquery对象。
``` js
$(document.getElementById("msg"))       //转化为jQuery对象
```
（2）如果jquery对象要转换为dom对象则必须取出其中的某一项，一般可通过索引取出。
``` js
$("#msg")[0]            //转化为DOM对象
$("div").eq(1)[0]
$("div").get()[1]
$("td")[5]
```
（3）eq()和get()的区别	
eq返回的是jquery对象，而 get(n)和索引返回的是dom元素对象。
*对于jquery对象只能使用jquery的方法，而dom对象只能使用dom的方法。*
	
# 2.DOM遍历
## 2.1筛选元素
``` js
.filter(selector)     //与selector匹配的元素
.filter(callback)     //callback中返回true的元素
.eq(index)            //从0开始计数的第index个选中元素
.first()              //选中元素中的第一个元素
.last()               //选中元素的最后一个元素
.slice(start[,end])   //从0开始计数的给定范围内的选中元素
.not(selector)        //与selector不匹配的元素
.has(selector)        //与selector匹配的的后代元素
```

## 2.2后代元素
``` js
.find(selector)        //与selector匹配的后代元素
.contents()            //子节点（包括文本节点）
.children([selector])  //子节点，可传入selector进行筛选
```

## 2.3同辈元素
``` js
.next([selector])                   //每个选中元素紧邻的下一个元素，可传入selector进行筛选
.nextAll([selector])                //每个选中元素后的所有同辈元素，可传入selector进行筛选
.nextUntil([selector],[filter])     //每个选中元素之后、直至但不包含第一个和selector匹配的元素，可传入filter进行筛选
.prev([selector])                   //每个选中元素紧邻的上一个元素，可传入selector进行筛选
.prevAll([selector])                //每个选中元素前的所有同辈元素，可传入selector进行筛选
.prevUntil([selector],[filter])     // 每个选中元素之前、直至但不包含第一个和selector匹配的元素，可传入filter进行筛选
.siblings([selector])               //所有同辈元素，可传入selector进行筛选
```

## 2.4祖先元素
``` js
.parent([selector])                  //每个选中元素的父元素，可传入selector进行筛选
.parents([selector])                 //每个选中元素的所有祖先元素，可传入selector进行筛选
.parentsUntil([selector],[filter])   //每个选中元素的所有祖先元素、直至但不包含第一个和selector匹配的元素，可传入filter进行筛选
.closest(selector)                   //与selector匹配的第一个元素，从元素自身开始沿DOM数向上搜索祖先元素
.offsetParent()                      //选中元素的第一个被定为的父元素(relative或absolute)
```

## 2.5集合操作
``` js
.add([selector])      //将与selector匹配的元素添加原对象集合中
.addBack()            //选中的元素加上JQuery内部栈中之前选中的元素
.end()                //内部JQuery栈中之前选中的元素
.map(callback)        //对每个选中调用回调函数callback之后的结果
.pushStack()          //指定的元素
```

## 2.6操作选中的元素
``` js
.is(selector)         //确定匹配的元素中是否有传入的与selector匹配的元素
.index()              //取得匹配元素相对其同辈元素的索引
.index(element)       //取得匹配元素中与指定元素对象的DOM节点的索引
$.contains(a,b)       //确定DOM节点a是否包含DOM节点b
.each(callback)       //迭代匹配元素，对每个元素执行callback
.length               //取得匹配元素的数量
.get()                //取得与匹配元素对应的DOM节点列表
.get(index)           //取得匹配元素中与指定索引对应的DOM节点
.toArray()            //取得与匹配元素对应的DOM节点列表
```

## 2.7应用实例
1.jquery集合遍历
``` js
$("p").each(function(i){this.style.color=["#f00","#0f0","#00f"][ i ]})
//为索引分别为0，1，2的p元素分别设定不同的字体颜色。

$("tr").each(function(i){this.style.backgroundColor=["#ccc","#fff"][i%2]})
//实现表格的隔行换色效果
```


# 3.事件绑定
## 3.1基本事件
``` js
.ready(handler)                         //DOM和CSS完全加载后之间handler
.on(type,[selector],[data],handler)     //绑定type事件，并指定事件处理程序handler;如果指定selector则执行事件委托
.on(events,[selector],[data])           //根据events对象的事件绑定多个事件处理程序
.off(type,[selector],handler)           //解除on给元素绑定的事件处理程序
.bind(type,[data],handler)              //绑定type事件，并指定事件处理程序handler
.one(type,[data],handler)               //绑定type事件，并指定事件处理程序handler,handler被调用后立即解除绑定
.unbind([type],[handler])               //解除bind给元素绑定的指定事件处理程序(不指定则解除所有指定)
.delegate(selector,type,[data],handler) //给与selector匹配的元素绑定type事件，并指定事件处理程序handler
.delegate(selector,handlers)            //给与selector匹配的元素绑定type事件，并指定事件处理程序handlers
.undelegate(selector,type,[handler])    //解除delegate给元素绑定的指定事件处理程序
```

## 3.2其它方法
``` js
.trigger(type,[data])           //触发元素上的事件并执行事件的默认操作
.triggerHandler(type,[data])    //触发元素上的事件，但不执行事件的默认操作
$.proxy(fn,context)             //创建一个新的在指定上下文中执行的函数。
```
## 3.3应用实例
1.遍历事件 
``` js
//为三个不同的p元素单击事件分别设定不同的处理
$("p").click(function(i){this.style.color=['#f00','#0f0′,'#00f'][ i ]})
```
2.模仿悬停事件 
hover(fn1,fn2)：一个模仿悬停事件的方法。当鼠标移动到一个匹配的元素上面时，会触发指定的第一个函数。当鼠标移出这个元素时，会触发指定的第二个函数。
3.删除绑定事件
``` js
$("p").unbind();//删除所有p元素上的所有事件
$("p").unbind("click")//删除所有p元素上的单击事件
``` 
4..trigger(eventtype): 在每一个匹配的元素上触发某类事件
``` js
$("p").trigger("click");//触发所有p元素的click事件
```

# 4.DOM完全操作
## 4.1样式和属性
``` js
.attr(key)           	//取得特性key的值
.attr(key，value)    	//设置特性key的值为value
.attr(key，fn)       	//将fn的返回值作为key的值
.attr(obj)           	//根据传入的键值对象参数设置特性的值
.removeAttr(key)     	//删除特性key的值
.prop(key)           	//取得属性key的值
.prop(key，value)    	//设置属性key的值为value
.prop(key，fn)       	//将fn的返回值作为key的值
.prop(obj)          	//根据传入的键值对象参数设置属性的值
.removeProp(key)     	//删除属性key的值
.addClass(class)     	//为匹配元素添加传入的类
.removeClass(class)  	//为匹配元素删除传入的类
.toggleClass(class)  	//对于匹配元素，如果存在类则删除，不存在则添加
.hasClass(class)     	//匹配元素中至少一个包含传入的类则返回true
.val()               	//获取第一个匹配元素的value属性值
.val(value)          	//设置每个匹配元素的value属性
```

## 4.2内容操作
``` js
.html()         //获取第一个匹配元素的HTML内容
.html(value)    //将每个匹配元素的HTML内容设置为value
.text()         //获取所有匹配元素的文本，以字符串返回
.text(value)    //将每个匹配元素的文本设置为value
```

## 4.3CSS和尺寸相关
``` js
.css(key)            //取得属性key的值
.css(key,value)      //设置key的值为value
.css(obj)            //根据传入的键值参数设置CSS的属性值
offset()             //返回第一个匹配元素相对于视口的坐标（单位是像素）
.position()          //返回第一个匹配元素相对.offsetParent()返回元素的坐标（单位是像素）
.scrollTop()         //返回第一个匹配元素的垂直滚动位置
.scrollTop(value)    //设置每个匹配元素的垂直滚动位置
.scrollLeft()        //返回第一个匹配元素的水平滚动位置
.scrollLeft(value)   //设置每个匹配元素的水平滚动位置
.height()            //返回第一个匹配元素的高度
.height(value)       //设置每个元素的高度
.width()             //返回第一个匹配元素的度
.width(value)        //设置每个元素的宽度
.innerHeight()       //返回第一个匹配元素的高度（包含内边距，不包含边框）
.innerWidth()        //返回第一个匹配元素的宽度（包含内边距，不包含边框）
.outerHeight([includeMargin])       //返回第一个匹配元素的高度（包含内边距和边框，bool为true，则包含外边距，反之不包含）
.outerWidth([includeMargin])        //返回第一个匹配元素宽度（包含内边距和边框，bool为true，则包含外边距，反之不包含）
```

## 4.4DOM插入
``` js
.append(content)          //在每个匹配元素内部的末尾插入content
.appendTo(selector)       //将匹配元素插入到与selector匹配的元素的内部的末尾
.prepend(content)         //在每个匹配元素内部的开头插入content
.prependTo(selector)      //将匹配元素插入到与selector匹配的元素的内部的开头
.after(content)           //在每个匹配元素外部的后面插入content
.insertAfter(selector)    //将匹配元素插入到与selector匹配的元素的外部的后面
.before(content)          //在每个匹配元素部的前面插入content
.insertBefore(selector)   //将匹配元素插入到与selector匹配的元素的外部的前面
.wrap(content)            //匹配的每个元素包含在content中
.wrapAll(content)         //匹配的每个元素作为一个整体包含在content中
.wrapInner(content)       //匹配的每个元素的内部内容包含在content中
.unwrap()                 //删除元素的父元素（反操作）
```

## 4.5替换、删除和复制
``` js
.replaceWith(content)    //将匹配的元素替换为content
.replaceAll(selector)    //将与selector匹配的元素替换为匹配的元素
.empty()                 //删除每个元素的子节点
.remove([selector])      //从DOM中删除节点，selector可以用于筛选
.detach([selector])      //从DOM中删除节点，selector可以用于筛选，并保留JQuery给元素添加的数据
.clone([withHandlers],[deepWithHandlers])   //返回匹配元素的副本，也可以复制事件处理程序
```

## 4.6数据
``` js
.data(key)             //获取第一个匹配元素的key键对应的数据
.data(key,value)       //设置每个元素关联的key对应的数据值为value
.removeData(key)       //删除每个元素与key键关联的数据
```

# 5.动画
## 5.1基础动画
``` js
.show()                         	//显示匹配元素
.show(speed,[callback])         	//通过高度、宽度和透明度动画显示匹配元素
.hide() 							//隐藏匹配元素
.hide(speed,[callback])         	//通过高度、宽度和透明度动画隐藏匹配元素
.toggle([speed],[callback])     	//显示或隐藏匹配元素
.slideDown([speed],[callback])  	//以滑入方式显示匹配元素
.slideUp([speed],[callback])    	//以滑出方式隐藏匹配元素
.slideToggle([speed],[callback])	//以滑动方式显示或隐藏匹配元素
.fadeIn([speed],[callback])     	//以淡入方式显示匹配元素
.fadeOut([speed],[callback])    	//以淡出方式隐藏匹配元素
.fadeToggle([speed],[callback]) 	//以淡入淡出方式显示或隐藏匹配元素
.fadeTo(speed,opacity,[callback])   //调整匹配元素的透明度
```
## 5.2自定义动画
``` js
.animate(attrs,[speed],[easing],[callback]) 	//针对指定的css属性自定义动画
.animate(attrs,options)                     	//.animate的底层接口，支持队列控制
```
## 5.3应用实例
1.切换隐藏显示元素 
``` js
$( "#foo" ).toggle( display );

//上边相当于
if ( display === true ) {
  $( "#foo" ).show();
} else if ( display === false ) {
  $( "#foo" ).hide();
}
```

# 6.队列操作
``` js
.queue([queueName])                //返回第一个匹配元素上的动画队列
.queue([queueName]，callback)      //在动画队列的最后添加回调函数
.queue([queueName]，newQueue)      //以新队列替换旧队列
.dequeue([queueName])              //执行动画队列的下一个动画
.clearQueue([queueName])           //清除所有未执行函数
.stop([clearQueue],[jumpToEnd])    //停止当前动画,启动排列动画（若有）
.finish([queueName])               //停止当前动画并将所有排列的动画理解提前到它们的目标值
.delay(duration,[queueName])       //延迟duration毫秒执行队列中的下一个动画
.promise([queueName],[target])     //在集合中所有排队的操作完成后返回一个待解决的承诺对象
```

# 7.Ajax方法
## 7.1发送请求
``` js
$.ajax([url],options)						//使用传入的options发送一次Ajax请求
.load(url,[data],[callback])				//向传入的url生成一次Ajax请求，然后将响应放在匹配的元素中
$.get(url,[data],[callback],[returnType])	//向传入的url发送一个get请求
$.getJSON(url,[data],[callback])			//向传入的url发送一个Ajax请求，将响应作为JSON数据结构解析
$.getScript(url,[callback])					//向传入的url发送一个Ajax请求，将响应作为Javascript解析
$.post(url,[data],[callback],[returnType])	//向传入的url发送一个post请求
```

## 7.2监视请求
``` js
.ajaxComplete(handler)	  //绑定Ajax请求完成后调用的处理程序
.ajaxError(handler)		  //绑定Ajax请求发生错误后调用的处理程序
.ajaxSend(handler)		  //绑定Ajax请求开始时调用的处理程序
.ajaxStart(handler)		  //绑定Ajax请求开始但没有其它Ajax请求时调用的处理程序
.ajaxStop(handler)		  //绑定Ajax请求结束但没有其它Ajax请求时调用的处理程序
.ajaxSuccess(handler)	  //绑定Ajax请求成功返回响应时调用的处理程序
```

## 7.3配置
``` js
$.ajaxSetup(options)					//为后续的Ajax请求设置选项
$.ajaxPrefilter([dataType],handler)		//在$.ajax()处理请求之前，修改每个请求的选项
$.ajaxTransport(transportFunction)		//为Ajax事务定义一个新的传输机制
```

## 7.4实用方法
``` js
.serialize()		  //将一组表单控件的值编码为一个查询字符串
.serializeArray()	  //将一组表单控件的值编码为一个JSON数据结构
$.param(obj)		  //将任意值的对象编码为一个查询字符串
$.globalEval(code)	  //在全局上下文中求值给定的Javascipt字符串
$.parseJSON(json)	  //将JSON对象转为JavaScript对象
$.parseXML(xml)		  //将XML字符串转为XML文档
$.parseHTML(html)	  //将HTML元素转为DOM元素
```
## 7.5应用实例
1.jsonp使用
``` js
jQuery(document).ready(function(){
	$.ajax({
		type: "get",
		url: "http://flightQuery.com/jsonp/flightResult.aspx?code=CA1998",
		dataType: "jsonp",
		jsonp: "callback",
		jsonpCallback:"jsonpCallback",
		success: function(json){
			alert('json:' + json);
		},
		error: function(){
			alert('fail');
		}
	});
});
```
2.jsonp原理
``` js
<script type="text/javascript" src="http://remoteserver.com/remote.js">
//remote.js 其实就一句话 localFunction({“result":"我是远程js带来的数据"});，在浏览器加载完成之后，远端loading过来的这个文件可以执行本地的JavaScript代码，里面可以携带数据，不过需要有一个函数名作为媒介
</script>
<script type="text/javascript">
var localFunction = function(data){
	alert('我是本地函数，可以被跨域的remote.js文件调用，远程js带来的数据是：'+ data.result)
};
</script>
```

# 8.延迟对象
## 8.1创建对象
``` js
$.Deferred([setupFunction])		//创建一个新的延迟对象
$.when(deferreds)				//在给定的延迟对象解决了之后返回一个待解决的承诺对象
```

## 8.2延迟对象的方法
``` js
.resolve([args])				//解决延迟对象并使用给定的参数调用完成回调函数
.resolveWith(context,[args])	//解决延迟对象并使用给定的参数调用完成回调函数,同时让关键字this引用回调函数中的context
.reject([args])					//拒绝延迟对象并使用给定的参数调用失败回调函数
.rejectWith(context,[args])		//拒绝延迟对象并使用给定的参数调用失败回调函数,同时让关键字this引用回调函数中的context
.notify([args])					//执行progress回调
.notifyWith(context,[args])		//执行progress回调,同时让关键字this引用回调函数中的context
.promise([target])				//返回与当前延迟对象的承诺对象
```

## 8.3承诺对象的方法
``` js
.done(callback)			//当对象被解决之后调用callback
.fail(callback)			//当对象被拒绝之后调用callback
.always(callback)		//当对象被拒绝或被解决之后调用callback
.then(doneCallbacks,failCallbacks)		//当对象被解决之后调用doneCallbacks,当对象被拒绝之后调用failCallbacks
.progress(callback)		//当对象每次接到进度通知后调用callback
.isRejected()			//如果对象被拒绝，返回true
.isResolved()			//如果对象被解决，返回true
.state()				//返回当前运行状态，"pending"、"rejected"和"resolved"
.pipe([doneFilter],[failFilter])	//返回新的承诺对象
```

## 8.4应用实例
1.转化成deferred对象
``` js
$.Deferred(wait)         //用这种方法可以转化成deferred对象
.done(function(){ alert(“哈哈，成功了！”); })
.fail(function(){ alert(“出错啦！”); })
.always( function() { alert(“已执行！”);} );
```
2.为多个操作指定回调函数，并按顺序执行
``` js
$.when($.ajax("test1.html"), $.ajax("test2.html"))
```
*更多参考：http://www.ruanyifeng.com/blog/2011/08/a_detailed_explanation_of_jquery_deferred_object.html*

# 9.其它方法
## 9.1JQuery对象的属性
``` js
$.support	//返回一个属性对象，表示浏览器是否支持各种特性和标准，不推荐用这个
```

## 9.2数组和对象
``` js
$.each(collection,callback)		//迭代集合，对每一项执行callback
$.extend(target,obj1,obj2,….)	//扩展target对象，返回到target中
$.grep(array,callback,[invert])	//使用callback筛选数组
$.makeArray(obj)				//将obj对象转换为数组
$.map(array,callback)			//迭代集合，对每一项执行callback，将返回的结果作为一个新数组返回
$.inArray(value,array)			//判断value是否在array中，不在返回-1
$.merge(array1,array2)			//合并数组array1和array2
$.unique(array)					//从数组中移除重复的DOM元素
```



## 9.3对象判断
``` js
$.isArray(obj)			//判断对象obj是否为数组
$.isEmptyObject(obj)	//判断对象obj是否为空的
$.isFunction(obj)		//判断对象obj是否为函数
$.isPlainObject(obj)	//判断对象obj是否是通过字面量或new Object()创建的
$.isNumber(obj)			//判断对象obj是否为数值
$.isWindow(obj)			//判断对象obj是否为浏览器窗口
$.isXMLDoc(obj)			//判断对象obj是否为XML节点
$.type(obj)				//判断对象obj的JavaScript类
```

## 9.4其他
``` js
$.trim(string)				//移除字符串的前后空白符
$.noConflict([removeAll])	//向其它库过渡$标识符
$.noop()					//什么也不做的函数
$.now()						//以秒为单位，返回当前时间
$.holdReay(hold)			//防止触发ready事件或释放当前的保留
```
## 9.5应用实例
1.扩展功能 
``` js
//为jquery扩展了min,max两个方法
$.extend({
	min:function(a, b){return a< b?a:b; },
	max:function(a, b){return a> b?a:b; }
});
//使用扩展的方法（通过"$.方法名"调用）
alert("a=10,b=20,max="+$.max(10,20)+",min="+$.min(10,20));

//合并数组
var settings= $.extend({}, obj1, obj2);
```
2.each迭代 
``` js
$.each( [0,1,2],function(i, n){ alert( “Item #”+ i+ “: ”+ n ); });
//等价于
var tempArr=[0,1,2];
for(var i=0;i<tempArr.length;i++){
	alert(”Item #”+i+”: “+tempArr[ i ]);
}
//也可以处理json数据，如
$.each( { name: “John”, lang: “JS” },function(i, n){ alert( “Name: ”+ i+ “, Value: ”
+ n ); });
//结果
Name:name, Value:John
Name:lang, Value:JS
```
3.map(array, fn)：数组映射。把一个数组中的项目(处理转换后)保存到到另一个新数组中，并返回生成的新数组。
``` js
var tempArr=$.map( [0,1,2],function(i){return i+ 4; });
//tempArr内容为：[4,5,6]
var tempArr=$.map( [0,1,2],function(i){return i> 0 ? i+ 1 :null; });
//tempArr内容为：[2,3] 
```
4.$.merge(arr1,arr2):合并两个数组并删除其中重复的项目。
``` js
$.merge( [0,1,2], [2,3,4] )   //返回[0,1,2,3,4]
```
5.$.trim(str)：删除字符串两端的空白字符。
``` js
$.trim(”   hello, how are you? “); //返回”hello,how are you? ”
```
6.解决自定义方法或其他类库与jQuery的冲突 
``` js
jQuery.noConflict();
// 开始使用jQuery
```

# 10.项目总结
### 10.1 避免cdn取不到文件
``` js
<script type="text/javascript">
	<script type="text/javascript" language="Javascript" src="http://ajax.aspnetcdn.com/ajax/jquery/jquery-1.4.1.min.js "></script> 
	<script type='text/javascript'>
	//<![CDATA[ if (typeof jQuery == 'undefined') { document.write(unescape("%3Cscript src='/Script/jquery-1.4.1.min.js' type='text/javascript' %3E%3C/script%3E")); }//]]> 
	</script>
</script>
```
### 10.2 设置随机数，避免缓存
``` js
data: $content+ new Date(),  
```
这里加 new Date()的作用是，设置随机数，避免缓存，重新加载

### 10.3 停止往下运行
``` js
return false; 
```
### 10.4 this调用
``` js
var this = $(this)
```
jquery的this是$(this)
### 10.5 先获取一个id再获取一个class要比直接获取class快
``` js
$("#id .item") 比 $(".item") 快
```
### 10.6 获取DOM的索引值i
``` js
//js写法
for(var i=0;i&lt;getSlide.length;i++) {
     getSlide[i].index=i;
     getSlide[i].onmousewheel=function(){
     alert("haha");
     console.log(this.index);
     }
}
//jQuery写法
for(var i=0;i&lt;getSlide.length;i++){
    $(".slide").eq(i).attr("index",i);
    $(".slide").eq(i).on("mousewheel",function(){
        console.log($(this).attr("index"));
    });
}
//jQuery优化写法
$(".slide").each(function(i){
    $(this).attr("index",i).on("click",function(){
        console.log($(this).attr("index"));
    })
})
//jQuery绑定方法
$('.slide').each(function(i){
    $(this).data('index',i);
}).on('click', function(){
    // 绑定事件的时候不需要each, jquery会做这一部分
    console.log($(this).data('index'));
})
```
### 10.7 深拷贝合并继承
``` js
$.extend( true,target， object1, object2 );
```
target是目标对象--接收新属性
1.如果只有一个target，就会将jquery视为目标对象，这个target就是jquery扩展的新功能
2.如果除了目标对象还有至少一个对象，那么就会将剩下所有的对象合并到目标对象target内.
*注：这种的是浅拷贝，相同属性的话，后边的属性会覆盖掉前边的属性*
3.保留target，合并到新对象上，可以通过空对象来实现
``` js
var object = $.extend({}, object1, object2);
```
4.加上参数true的话，就是深拷贝（递归合并）---同样也是复制到target对象内
*注：这种合并的话，如果相同方法内有相同的属性，后边的属性会覆盖掉前边的属性*
### 10.8 回到顶部
``` js
$('.top').click(function (e) {
  e.preventDefault();
  $('html, body').animate({scrollTop: 0}, 800);
});
```
### 10.9 图片预加载
``` js
for (var i = 0; i < arguments.length; i++) {
$('<img>').attr('src', arguments[i]);
}
$.preloadImages('img/hover-on.png', 'img/hover-off.png');
```
### 10.10 检查图片是否加载完毕
``` js
$('img').load(function(){
    console.log('图片全部加载完成')
})
```
### 10.11 自动修复损坏的图片
``` js
$('img').on('error', function () {
  $(this).prop('src', 'img/broken.png');
});
```
### 10.12 禁用input字段
``` js
$('input[type="submit"]').prop('disabled', true);
//当你想把 disabled 的值改为 false 时，仅需在该 input 上再运行一次 prop 方法。
$('input[type="submit"]').prop('disabled', false);
//或者
$('input[type="submit"]').removeAttr('disabled');
```
### 10.13 停止链接跳转--就是阻止默认事件
``` js
$('a.no-link').click(function (e) {
  e.preventDefault();
});
```
### 10.14 所有列相同高度
``` js
var $rows = $('.same-height-columns');
$rows.each(function () {
  $(this).find('.column').height($(this).height());
});
//方法二
$(document).ready(function() {
function equalHeight(group) {
    tallest = 0;
    group.each(function() {
        thisHeight = $(this).height();
        if(thisHeight > tallest) {
            tallest = thisHeight;
        }
    });
    group.height(tallest);
}
// how to use
$(document).ready(function() {
    equalHeight($(".left"));
    equalHeight($(".right"));
});
});
```
### 10.15 新标签页打开链接
``` js
$('a[href^="http"]').attr('target', '_blank');
$('a[href^="//"]').attr('target', '_blank');
$('a[href^="' + window.location.origin + '"]').attr('target', '_self');
```
### 10.16 通过文本内容找到元素
``` js
var search = $('#search').val();
$('div:not(:contains("' + search + '"))').hide();
```
### 10.17 焦点在标签页上切换触发事件，H5新API
``` js
$(document).on('visibilitychange', function (e) {
  if (e.target.visibilityState === "visible") {
    console.log('Tab is now in view!');
  } else if (e.target.visibilityState === "hidden") {
    console.log('Tab is now hidden!');
  }
});
```
### 10.18 Delegate()函数有什么作用？
``` js
//如果你有一个父元素，需要给其下的子元素添加事件，这时你可以使用delegate()了，代码如下：
$("ul").delegate("li", "click", function(){
    $(this).hide();
});
//当元素在当前页面中不可用时，可以使用delegate()
```
### 10.19 怎样用jQuery编码和解码URL？
encodeURIComponent(url) and decodeURIComponent(url)
### 10.20 禁止右键点击
``` js
$(document).ready(function(){
    $(document).bind("contextmenu",function(e){
        return false;
    });
});
```
### 10.21 移除单词
``` js
$(document).ready(function() {
   var el = $('#id');
   el.html(el.html().replace(/word/ig, ""));
});
```
### 10.22 验证是否在jquery对象集合中
``` js
$(document).ready(function() {
   if ($('#id').length) {
  // do something
  }
});
```
### 10.23 克隆对象
``` js
$(document).ready(function() {
   var cloned = $('#id').clone();
// how to use
<DIV id=id></DIV>

});
```
### 10.24 统计元素个数
``` js
$(document).ready(function() {
   $("p").size();
});
```
### 10.25 禁用jquery（动画）效果
``` js
$(document).ready(function() {
    jQuery.fx.off = true;
});
```
### 10.26 jquery框架
```js
(function(window, undefined) {
    var jQuery = function() {}
    // ...
    window.jQuery = window.$ = jQuery;
})(window);
```
### 10.27 遇到外部链接自动添加target=”blank”的属性
```js
var root = location.protocol + '//' + location.host;
$('a').not(':contains(root)').click(function(){
    this.target = "_blank";
});
```
### 10.28 在文本或密码输入时禁止空格键
```js
$('input.nospace').keydown(function(e) {
	if (e.keyCode == 32) {
		return false;
	}
});
```

