---
title: Ejs学习总结
date: 2016-03-21 22:34:58
tags: [ejs,javascript,js]

---
一、什么是EJS

EJS是一个JavaScript模板库，用来从JSON数据中生成HTML字符串。

二、为什么要使用EJS

与最初的JavaScript相比较，一些不太了解你的代码的人可以更容易地通过EJS模板代码看得懂你的代码。 让我们放松一下，一起来享受下令人激动的干净简洁的感觉。

总之可以让代码更加干净整洁，让人易懂。

可以看如下的例子：

这是用javascript实现的代码
<blockquote>
<div>
<div id="highlighter_950641" class="syntaxhighlighter  js">
<div class="toolbar"></div>
<div class="toolbar">var html = "&lt;h1&gt;"+data.title+"&lt;/h1&gt;"
html += "&lt;ul&gt;"
for(var i=0; i&lt;data.supplies.length; i++) {
html += "&lt;li&gt;&lt;a href='supplies/"+data.supplies\[i]+"'&gt;"
html += data.supplies\[i]+"&lt;/a&gt;&lt;/li&gt;"
}
html += "&lt;/ul&gt;"</div>
</div>
</div></blockquote>
<div class="toolbar"></div>
<div class="toolbar">最终要实现的效果如下：</div>
![](/images/143136_Wd2M_1540325.png)

但是上面的代码看起来很乱，虽然实现了功能，但是不容易让人弄懂。不仅代码丑陋，而且你的HTML结构完全在JavaScript代码中丢失。

下面学习EJS同样实现上面的功效，它的工作原理如下：
![](/images/143620_u3yx_1540325.png)

使用<a href="http://www.ijser.cn/?tag=ejs" target="_blank" rel="nofollow">EJS</a>来找回你的明确、维护性良好的HTML代码结构。

注:data是json对象，不能使json字符串。

在HTML中引入EJS,以使javascript能够使用它，引入EJS的语句如下：
<blockquote>&lt;script type="text/javascript" src="/js/ejs.js"&gt;&lt;/script&gt;</blockquote>
创建一个EJS模板,命名为cleaning.ejs文件，内容如下：
<blockquote>
<div>&lt;h1&gt;&lt;%=title %&gt;&lt;/h1&gt;
&lt;ul&gt;
&lt;% for(var i=0; i&lt;supplies.length; i++) { %&gt;
&lt;li&gt;
&lt;a href='supplies/&lt;%=supplies\[i] %&gt;'&gt;
&lt;%= supplies\[i] %&gt;
&lt;/a&gt;
&lt;/li&gt;
&lt;% } %&gt;
&lt;/ul&gt;</div></blockquote>
我的HTML文档如下，引入EJS,并更加我们的提供EJS模板创建EJS对象，然后调用EJS对象成员函数解析JSON对象到模板中。
<blockquote>
<div>&lt;html&gt;
&lt;head&gt;
&lt;script type="text/javascript" src="/js/ejs.js"&gt;&lt;/script&gt;
&lt;script type="text/javascript"&gt;function myfunction(){
var data='{"title":"cleaning","supplies":\["mop","broom","duster"]}'
var html = new EJS({url: '/js/tmpl/cleaning.ejs'}).render(JSON.parse(data));
//JSON.parse(data) 把JSON字符串解析为原生的javascript值。
alert(html);
document.getElementById("div1").innerHTML=html;
}
&lt;/script&gt;
&lt;/head&gt;
&lt;body&gt;
&lt;button onclick="myfunction()"&gt;点击&lt;/button&gt;
&lt;div id="div1"&gt;&lt;/div&gt;
&lt;/body&gt;
&lt;html&gt;</div></blockquote>
从上面这个例子我们可以看到EJS模板的基本用法。

三、下面介绍下EJS的语法和功能：

1、缓存功能，能够缓存已经解析好的html模版；

2、&lt;% code %&gt;用于执行其中javascript代码。
<blockquote>
<div>&lt;% alert('hello world') %&gt;</div></blockquote>
3、&lt;%= code %&gt;会对code进行html转义；
<blockquote>
<div>&lt;h1&gt;&lt;%=title %&gt;&lt;/h1&gt; 注：会把title里面存的值给显示出来在h1中。
&lt;p&gt;&lt;%= 'hello world' %&gt;&lt;/p&gt; 注：会把hello world显示在h1中。
&lt;h1&gt;&lt;%= '&lt;b&gt;hello world&lt;/b&gt;' %&gt;&lt;/h1&gt; 注：会把hello world变粗，然后显示在h1中。</div></blockquote>
4、&lt;%- code %&gt;将不会进行转义；，这一行代码不会执行，像是被注释了一样，然后显示原来的html。也不会影响整个页面的执行。
<blockquote>
<%-title %>asd         最后显示asd，及显示原网页
现在版本的 ejs <%-‘<b>hello world</b>’%>将输出解析后的html,也就是加粗了的 hello world
<%# 'hello world' %>asd   最后显示asd，及显示原网页</blockquote>
5、支持自定义标签，比如'&lt;%'可以使用'{{'，                  <span style="color: #3366ff;">然后'%&gt;'用'}}'代替</span>；
ejs 里，默认的闭合标记是 &lt;%  .. %&gt;，我们也可以定义自己的标签。例如：
``` js
app.set("view options",{ 
 "open":"{{", 
 "close":"}}"
});
```
6、提供一些辅助函数，用于模版中使用
1)、first，返回数组的第一个元素；
2)、last，返回数组的最后一个元素；
3)、capitalize，返回首字母大写的字符串；
4)、downcase，返回字符串的小写；
5)、upcase，返回字符串的大写；
6)、sort，排序（Object.create(obj).sort()？）；
7)、sort_by:'prop'，按照指定的prop属性进行升序排序；
8)、size，返回长度，即length属性，不一定非是数组才行；
9)、plus:n，加上n，将转化为Number进行运算；
10)、minus:n，减去n，将转化为Number进行运算；
11)、times:n，乘以n，将转化为Number进行运算；
12)、divided_by:n，除以n，将转化为Number进行运算；
13)、join:'val'，将数组用'val'最为分隔符，进行合并成一个字符串；
14)、truncate:n，截取前n个字符，超过长度时，将返回一个副本
15)、truncate_words:n，取得字符串中的前n个word，word以空格进行分割；
16)、replace:pattern,substitution，字符串替换，substitution不提供将删除匹配的子串；
17)、prepend:val，如果操作数为数组，则进行合并；为字符串则添加val在前面；
18)、append:val，如果操作数为数组，则进行合并；为字符串则添加val在后面；
19)、map:'prop'，返回对象数组中属性为prop的值组成的数组；
20)、reverse，翻转数组或字符串；
21)、get:'prop'，取得属性为'prop'的值；
22)、json，转化为json格式字符串

7、利用&lt;%- include filename %&gt;加载其他页面模版；

四、使用创建好的EJS模板

基于我们之前写的模拟生成一个EJS对象
<blockquote>
<div>new EJS({url: '/js/tmpl/cleaning.ejs'})</div></blockquote>
对象有下面两个成员函数

1、ejs.compile(str, options); 将返回内部解析好的Function函数
2、ejs.render(str, options); 返回经过解析的字符串

ejs的render函数有两个参数 第一个是字符串，第二个是可选的对象，和其他javascript模版一样需要渲染的数据也是包含在option对象中的。
<blockquote>
<div>ejs.render(str,option);
// 渲染字符串 str 一般是通过nodejs文件系统的readfile方法读取ejs.render(str,{
data : user_data // 需要渲染的数据});

</div></blockquote>
其中options的一些参数为：
1、cache：是否缓存解析后的模版，需要filename作为key；
2、filename：模版文件名；
3、scope：complile后的Function执行所在的上下文环境；
4、debug：标识是否是debeg状态，debug为true则会输出生成的Function内容；
5、compileDebug：标识是否是编译debug，为true则会生成解析过程中的跟踪信息，用于调试；
6、client，标识是否用于浏览器客户端运行，为true则返回解析后的可以单独运行的Function函数；
7、open，代码开头标记，默认为'&lt;%'；
8、close，代码结束标记，默认为'%&gt;'；
9、其他的一些用于解析模版时提供的变量。
在express中使用时，options参数将由response.render进行传入，其中包含了一些express中的设置，以及用户提供的变量值。

五、最后总结一下EJS的应用场所
1.用JavaScript创建HTML字符串 正如我们在新手教程中所讨论的，在JavaScript中拼字符串的缺点是可维护性不好。当你在JavaScript中将这些字符串拼到一起时，很难看出你正在写的HTML是什么\---|一个你页面展现的结构。而使用模板可以让你通过代码的空行和缩进来清楚地展现出你的HTML。
2.基于WebService的AJAX网站开发 EJS可以接收WebService异步传送过来的JSON格式的数据，将这种数据直接传入你的模板里，然后将结果插入到你的页面中。你所需要做的只是通过以下代码：
3.
<blockquote>new EJS({url: 'comments.ejs'}).update('element_id', '/comments.json')</blockquote>
4.程序换肤功能
如果你想给用户自制页面显示的功能，EJS提供了非常适合的机制。EJS的模板只在浏览器里执行，因此对你的服务器没有任何安全风险。你可以允许你的用户上传EJS模板以及其关联的样式表，从而实现定制你的网站页面的功能。
<h3>自己写的(cinema文件夹内)</h3>
<h5>index.html</h5>
``` js
<script>
    $.ajax({
        url:"index-json",
        success:function(data){
            console.log(data);
            //var data = JSON.parse(data);  因为ajax会自动将传过来的字符串转换成json对象，所以这里就需要自己再转换了   
            var html = new EJS({url: './cinema/client/page/ejs/index.ejs'}).render(data);
            console.log(html);
            document.getElementById("container").innerHTML = html;
        }
    })
</script>
</pre>
<h5>index.ejs</h5>
<pre>
<ul>
<% for(i=0;i<movies.length;i++){ %>
    <li>
        <span><%= movies\[i]._id %></span>
        <span><%= movies\[i].title %></span>
        <span><%= movies\[i].poster %></span>
    </li>
    <% } %>
</ul>
```

