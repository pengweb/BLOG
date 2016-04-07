---
title: jquery--学习笔记(初级)
date: 2016-03-21 23:52:46
tags: [jquery,js,javascript]

---
jQuery 的选择器可谓之强大无比，这里简单地总结一下常用的元素查找方法
<pre>
$("#myELement")    选择id值等于myElement的元素，id值不能重复在文档中只能有一个id值是myElement所以得到的是唯一的元素 

$("div")           选择所有的div标签元素，返回div元素数组 

$(".myClass")      选择使用myClass类的css的所有元素 

$("*")             选择文档中的所有的元素，可以运用多种的选择方式进行联合选择：例如$("#myELement,div,.myclass")

层叠选择器： 

$("form input")         选择所有的form元素中的input元素 

$("#main > *")          选择id值为main的所有的子元素 

$("label + input")     选择所有的label元素的下一个input元素节点，经测试选择器返回的是label标签后面直接跟一个input标签的所有input标签元素 

$("#prev ~ div")       同胞选择器，该选择器返回的为id为prev的标签元素的所有的属于同一个父元素的div标签

基本过滤选择器： 

$("tr:first")               选择所有tr元素的第一个 

$("tr:last")                选择所有tr元素的最后一个 

$("input:not(:checked) + span")  

过滤掉：checked的选择器的所有的input元素

$("tr:even")               选择所有的tr元素的第0，2，4... ...个元素（注意：因为所选择的多个元素时为数组，所以序号是从0开始）

$("tr:odd")                选择所有的tr元素的第1，3，5... ...个元素 

$("td:eq(2)")             选择所有的td元素中序号为2的那个td元素 

$("td:gt(4)")             选择td元素中序号大于4的所有td元素 

$("td:lt(4)")              选择td元素中序号小于4的所有的td元素 

$(":header")            选择h1、h2、h3之类的

$("div:animated")     选择正在执行动画效果的元素

内容过滤选择器：

$("div:contains('John')") 选择所有div中含有John文本的元素 

$("td:empty")           选择所有的为空（也不包括文本节点）的td元素的数组 

$("div:has(p)")        选择所有含有p标签的div元素 

$("td:parent")          选择所有的以td为父节点的元素数组 

可视化过滤选择器：

$("div:hidden")        选择所有的被hidden的div元素 

$("div:visible")        选择所有的可视化的div元素 

属性过滤选择器：

$("div[id]")              选择所有含有id属性的div元素 

$("input[name='newsletter']")    选择所有的name属性等于'newsletter'的input元素

$("input[name!='newsletter']") 选择所有的name属性不等于'newsletter'的input元素

$("input[name^='news']")         选择所有的name属性以'news'开头的input元素 

$("input[name$='news']")         选择所有的name属性以'news'结尾的input元素 

$("input[name*='man']")          选择所有的name属性包含'news'的input元素

$("input[id][name$='man']")    可以使用多个属性进行联合选择，该选择器是得到所有的含有id属性并且那么属性以man结尾的元素

子元素过滤选择器：

$("ul li:nth-child(2)"),$("ul li:nth-child(odd)"),$("ul li:nth-child(3n + 1)")

$("div span:first-child")          返回所有的div元素的第一个子节点的数组 

$("div span:last-child")           返回所有的div元素的最后一个节点的数组 

$("div button:only-child")       返回所有的div中只有唯一一个子节点的所有子节点的数组

表单元素选择器：

$(":input")                  选择所有的表单输入元素，包括input, textarea, select 和 button

$(":text")                     选择所有的text input元素 

$(":password")           选择所有的password input元素 

$(":radio")                   选择所有的radio input元素 

$(":checkbox")            选择所有的checkbox input元素 

$(":submit")               选择所有的submit input元素 

$(":image")                 选择所有的image input元素 

$(":reset")                   选择所有的reset input元素 

$(":button")                选择所有的button input元素 

$(":file")                     选择所有的file input元素 

$(":hidden")               选择所有类型为hidden的input元素或表单的隐藏域

表单元素过滤选择器：

$(":enabled")             选择所有的可操作的表单元素 

$(":disabled")            选择所有的不可操作的表单元素 

$(":checked")            选择所有的被checked的表单元素 

$("select option:selected") 选择所有的select 的子元素中被selected的元素

 

选取一个 name 为”S_03_22″的input text框的上一个td的text值

$(”input[@ name =S_03_22]“).parent().prev().text()

名字以”S_”开始，并且不是以”_R”结尾的

$(”input[@ name ^='S_']“).not(”[@ name $='_R']“)

一个名为 radio_01的radio所选的值

$(”input[@ name =radio_01][@checked]“).val();

 

 

$("A B") 查找A元素下面的所有子节点，包括非直接子节点

$("A>B") 查找A元素下面的直接子节点

$("A+B") 查找A元素后面的兄弟节点，包括非直接子节点

$("A~B") 查找A元素后面的兄弟节点，不包括非直接子节点

$("A B") 查找A元素下面的所有子节点，包括非直接子节点
</pre>
<h2 id="J_CodeLang" class="code-head" data-lang="Javascript">#id 选择器</h2>
在id号为“default”的元素中显示id号为“divtest”元素的内容
<blockquote>&lt;body&gt;
&lt;div id="divtest"&gt;div的内容&lt;/div&gt;
&lt;div id="default"&gt;&lt;/div&gt;
&lt;script type="text/javascript"&gt;
<span style="color: #ff0000;">$("#default").html($("#divtest").html());  // $("#id") 获取这个id      html和js中innerHTML用法一样</span>
&lt;/script&gt;
&lt;/body&gt;</blockquote>
<h2 id="J_CodeLang" class="code-head" data-lang="Javascript">element 选择器</h2>
<pre class="code"><a href="http://img.mukewang.com/5286ddff0001239802840097.jpg"><img src="http://img.mukewang.com/5286ddff0001239802840097.jpg" alt="" /></a>


</pre>
<h2 id="J_CodeLang" class="code-head" data-lang="Javascript">.class 选择器</h2>
<img src="http://img.mukewang.com/5286e9f00001a50d03680173.jpg" alt="" />

结果是红色的red  这个red是通过<span style="color: #ff0000;">attr()</span>来得到的class的名字，而不是他的样式

&nbsp;
<h2 id="J_CodeLang" class="code-head" data-lang="Javascript">* 选择器</h2>
如下图所示： 使用*选择器，获取div中的所有子元素并设置三个子元素显示相同的内容。

<a href="http://img.mukewang.com/5286f46a0001f6dc02890170.jpg"><img src="http://img.mukewang.com/5286f46a0001f6dc02890170.jpg" alt="" /></a>

在浏览器中显示的效果：

<a href="http://img.mukewang.com/5286f4a00001331904770207.jpg"><img src="http://img.mukewang.com/5286f4a00001331904770207.jpg" alt="" /></a>

由于三个元素都包含在&lt;div&gt;元素中，因此，它们都是&lt;div&gt;元素的子元素，那么，就可以使用<code class="marker">$(“div *”)</code>的方式获取&lt;div&gt;元素中的这三个子元素，并使用<code class="marker">html()</code>方法来设置它们显示的内容。

实践证明，由于使用*选择器获取的是全部元素，因此，有些浏览器将会比较缓慢，这个选择器也需要谨慎使用。

&nbsp;
<h2 id="J_CodeLang" class="code-head" data-lang="Javascript">sele1,sele2,seleN选择器</h2>
例如，通过选择器获取其中的任意两个元素，并将它们显示的内容设为相同，如图所示：

<a href="http://img.mukewang.com/528705b000012a1102890134.jpg"><img src="http://img.mukewang.com/528705b000012a1102890134.jpg" alt="" /></a>

在浏览器中显示的效果：

<a href="http://img.mukewang.com/528705c700010e6d04720207.jpg"><img src="http://img.mukewang.com/528705c700010e6d04720207.jpg" alt="" /></a>

&nbsp;
<h2 id="J_CodeLang" class="code-head" data-lang="Javascript">ance desc选择器</h2>
例如，使用层次选择器，获取&lt;div&gt;元素中的全部&lt;span&gt;元素，并设置它们显示的内容，在如下图所示：

<a href="http://img.mukewang.com/528b4ecd00013c1503510178.jpg"><img src="http://img.mukewang.com/528b4ecd00013c1503510178.jpg" alt="" /></a>

在浏览器中显示的效果：

<a href="http://img.mukewang.com/528b4ecd00013c1503510178.jpg"><img src="http://img.mukewang.com/528b4e830001eb5c04630235.jpg" alt="" /></a>

&nbsp;
<h2 id="J_CodeLang" class="code-head" data-lang="Javascript">parent &gt; child选择器</h2>
如图所示：

<a href="http://img.mukewang.com/5292bfdd0001504503650226.jpg"><img src="http://img.mukewang.com/5292bfdd0001504503650226.jpg" alt="" /></a>

在浏览器中显示的效果：

<a href="http://img.mukewang.com/5292c57e00014aeb03050274.jpg"><img src="http://img.mukewang.com/5292c57e00014aeb03050274.jpg" alt="" /></a>

从图中可以看出，使用<code class="marker">$("div&gt;span")</code>选择器代码，获取的是&lt;div&gt;“家庭中”全部“子辈”&lt;span&gt;元素，<span style="color: #ff0000;">不包括“孙辈”&lt;span&gt;元素和“家庭外”的&lt;span&gt;元素</span>。

&nbsp;
<h2 id="J_CodeLang" class="code-head" data-lang="Javascript">prev + next选择器</h2>
例如，使用<code class="marker">prev + next</code>选择器，获取&lt;p&gt;元素最近邻的下一个元素，如下图所示：

<a href="http://img.mukewang.com/5292e68c000191c204000224.jpg"><img src="http://img.mukewang.com/5292e68c000191c204000224.jpg" alt="" /></a>

在浏览器中显示的效果：

<a href="http://img.mukewang.com/5292ebe60001dc2b03350376.jpg"><img src="http://img.mukewang.com/5292ebe60001dc2b03350376.jpg" alt="" /></a>

&nbsp;

&nbsp;
<h2 id="J_CodeLang" class="code-head" data-lang="Javascript">prev ~ siblings选择器</h2>
<div id="J_CodeDescr" class="code-description">
<div class="code-desc co">

与上一节中介绍的<code class="marker">prev + next</code>层次选择器相同，<code class="marker">prev ~ siblings</code>选择器也是查找prev 元素之后的相邻元素，但前者只获取第一个相邻的元素，而后者则获取prev 元素后面全部相邻的元素，它的调用格式如下：

<code class="marker">$(“prev ~ siblings”)</code>

其中参数prev与siblings两者之间通过“~”符号形成一种层次相邻的关系，表明siblings选择器获取的元素都是prev元素之后的同辈元素。

例如，使用<code class="marker">prev ~ next</code>选择器，获取&lt;p&gt;元素后面相邻的全部元素，并设置它们在页面中显示的内容，如下图所示：

<a href="http://img.mukewang.com/5292fc460001105a03310216.jpg"><img src="http://img.mukewang.com/5292fc460001105a03310216.jpg" alt="" /></a>

在浏览器中显示的效果：

<a href="http://img.mukewang.com/5292fc690001e15d04200411.jpg"><img src="http://img.mukewang.com/5292fc690001e15d04200411.jpg" alt="" /></a>

可以看出，调用<code class="marker">$("p~span")</code>选择器代码，获取了&lt;p&gt;元素下面两个(全部)的&lt;span&gt;元素，该元素不包含&lt;p&gt;元素上面的元素和不属于同辈范围的元素。

&nbsp;

<hr />

<h2 id="J_CodeLang" class="code-head" data-lang="Javascript">:first过滤选择器（:last）</h2>
<div id="J_CodeDescr" class="code-description" style="font: 14px/21px 'Microsoft Yahei', 'Hiragino Sans GB', Helvetica, 'Helvetica Neue', 微软雅黑, Tahoma, Arial, sans-serif; margin: 0px; padding: 0px; color: #1f2426; text-transform: none; text-indent: 0px; letter-spacing: normal; word-spacing: 0px; white-space: normal; -ms-word-break: break-all; font-size-adjust: none; font-stretch: normal; -webkit-text-stroke-width: 0px;">
<div class="code-desc co">

本章我们介绍过滤选择器，该类型的选择器是根据某过滤规则进行元素的匹配，书写时以“：”号开头,通常用于查找集合元素中的某一位置的单个元素。

在jQuery中，如果想得到一组相同标签元素中的第1个元素该怎样做呢？

在下面的示例代码中你可能注意到我们会使用

<code class="marker" style="margin: 0px 5px; padding: 0px 6px; border-radius: 2px; border: 1px solid #cccccc; font-family: Monaco, Menlo, 'Ubuntu Mono', Consolas, source-code-pro, monospace; font-size: 13px; font-style: normal; font-weight: normal; display: inline; background-color: #eeeeee;"> $(“li:first”)</code>

<strong>注意：</strong>书写时以“：”号开头。

<a href="http://img.mukewang.com/52971f6d0001adb103830271.jpg"><img src="http://img.mukewang.com/52971f6d0001adb103830271.jpg" alt="" width="301" height="215" /></a>

<strong>运行结果：</strong>

<strong><a href="http://img.mukewang.com/52971f8500010d9f04790289.jpg"><img src="http://img.mukewang.com/52971f8500010d9f04790289.jpg" alt="" /></a></strong>

&nbsp;

使用<code class="marker" style="margin: 0px 5px; padding: 0px 6px; border-radius: 2px; border: 1px solid #cccccc; font-family: Monaco, Menlo, 'Ubuntu Mono', Consolas, source-code-pro, monospace; font-size: 13px; font-style: normal; font-weight: normal; display: inline; background-color: #eeeeee;">li:first</code>过滤选择器可以很方便地获取ul列表中的第一个li元素.

<code class="marker" style="margin: 0px 5px; padding: 0px 6px; border-radius: 2px; border: 1px solid #cccccc; font-family: Monaco, Menlo, 'Ubuntu Mono', Consolas, source-code-pro, monospace; font-size: 13px; font-style: normal; font-weight: normal; display: inline; background-color: #eeeeee;">:first</code>过滤选择器的功能是获取第一个元素，常常与其它选择器一起使用，获取指定的一组元素中的第一个元素。

</div>
</div>
&nbsp;
<h2 id="J_CodeLang" class="code-head" data-lang="Javascript">:eq(index)过滤选择器</h2>
<div id="J_CodeDescr" class="code-description" style="font: 14px/21px 'Microsoft Yahei', 'Hiragino Sans GB', Helvetica, 'Helvetica Neue', 微软雅黑, Tahoma, Arial, sans-serif; margin: 0px; padding: 0px; color: #1f2426; text-transform: none; text-indent: 0px; letter-spacing: normal; word-spacing: 0px; white-space: normal; -ms-word-break: break-all; font-size-adjust: none; font-stretch: normal; -webkit-text-stroke-width: 0px;">
<div class="code-desc co">
<p style="color: #1f2426;">如果想从一组标签元素数组中，灵活选择任意的一个标签元素，我们可以使用</p>
<p style="color: #1f2426;"><code class="marker" style="margin: 0px 5px; padding: 0px 6px; border-radius: 2px; border: 1px solid #cccccc; font-family: Monaco, Menlo, 'Ubuntu Mono', Consolas, source-code-pro, monospace; font-size: 13px; font-style: normal; font-weight: normal; display: inline; background-color: #eeeeee;">:eq(index)</code></p>
<p style="color: #1f2426;">其中参数index表示索引号（即：一个整数），它从0开始，如果index的值为3，表示选择的是第4个元素。例如：</p>
<p style="color: #1f2426;"><a href="http://img.mukewang.com/529c00d40001669503040210.jpg"><img src="http://img.mukewang.com/529c00d40001669503040210.jpg" alt="" /></a></p>
<p style="color: #1f2426;">在浏览器中显示的效果：</p>
<p style="color: #1f2426;"><a href="http://img.mukewang.com/529c00f90001098804890294.jpg"><img src="http://img.mukewang.com/529c00f90001098804890294.jpg" alt="" /></a></p>
<p style="color: #1f2426;">从图中可以看出，通过调用<code class="marker" style="margin: 0px 5px; padding: 0px 6px; border-radius: 2px; border: 1px solid #cccccc; font-family: Monaco, Menlo, 'Ubuntu Mono', Consolas, source-code-pro, monospace; font-size: 13px; font-style: normal; font-weight: normal; display: inline; background-color: #eeeeee;">$("li:eq(3)")</code>过滤选择器代码，获取了第4个&lt;li&gt;元素，并使用css()方法设置了该元素在页面中显示的文字样式。</p>

<h2 id="J_CodeLang" class="code-head" style="color: #1f2426;" data-lang="Javascript">:contains(text)过滤选择器(记得给text加单引号)</h2>
<div id="J_CodeDescr" class="code-description" style="font: 14px/21px 'Microsoft Yahei', 'Hiragino Sans GB', Helvetica, 'Helvetica Neue', 微软雅黑, Tahoma, Arial, sans-serif; margin: 0px; padding: 0px; color: #1f2426; text-transform: none; text-indent: 0px; letter-spacing: normal; word-spacing: 0px; white-space: normal; -ms-word-break: break-all; font-size-adjust: none; font-stretch: normal; -webkit-text-stroke-width: 0px;">
<div class="code-desc co">
<p style="color: #1f2426;">与上一节介绍的:eq(index)选择器按索引查找元素相比，有时候我们可能希望按照<strong>文本内容</strong>来查找一个或多个元素，那么使用<code class="marker" style="margin: 0px 5px; padding: 0px 6px; border-radius: 2px; border: 1px solid #cccccc; font-family: Monaco, Menlo, 'Ubuntu Mono', Consolas, source-code-pro, monospace; font-size: 13px; font-style: normal; font-weight: normal; display: inline; background-color: #eeeeee;">:contains(text)</code>选择器会更加方便， 它的功能是选择<strong>包含</strong>指定字符串的全部元素，它通常与其他元素结合使用，获取包含“text”字符串内容的全部元素对象。其中参数<code class="marker" style="margin: 0px 5px; padding: 0px 6px; border-radius: 2px; border: 1px solid #cccccc; font-family: Monaco, Menlo, 'Ubuntu Mono', Consolas, source-code-pro, monospace; font-size: 13px; font-style: normal; font-weight: normal; display: inline; background-color: #eeeeee;">text</code>表示页面中的文字。</p>
<p style="color: #1f2426;">例如:</p>
<p style="color: #1f2426;"><a href="http://img.mukewang.com/529c067b00014cad03480210.jpg"><img src="http://img.mukewang.com/529c067b00014cad03480210.jpg" alt="" /></a></p>
<p style="color: #1f2426;">在浏览器中显示的效果：</p>
<p style="color: #1f2426;"><a href="http://img.mukewang.com/529c069b0001879204890294.jpg"><img src="http://img.mukewang.com/529c069b0001879204890294.jpg" alt="" /></a></p>
<p style="color: #1f2426;">从图中可以看出，调用<code class="marker" style="margin: 0px 5px; padding: 0px 6px; border-radius: 2px; border: 1px solid #cccccc; font-family: Monaco, Menlo, 'Ubuntu Mono', Consolas, source-code-pro, monospace; font-size: 13px; font-style: normal; font-weight: normal; display: inline; background-color: #eeeeee;">li:contains('土豪')</code>代码，可以很方便地获取&lt;li&gt;中<strong>包含</strong>‘土豪’字符内容的全部元素，并且只要与选择的元素中或子元素中包含该字符内容，就可以被选中。</p>
<p style="color: #1f2426;">注意：<code class="marker" style="margin: 0px 5px; padding: 0px 6px; border-radius: 2px; border: 1px solid #cccccc; font-family: Monaco, Menlo, 'Ubuntu Mono', Consolas, source-code-pro, monospace; font-size: 13px; font-style: normal; font-weight: normal; display: inline; background-color: #eeeeee;">li:contains('土豪')</code><span class="Apple-converted-space"> </span>土豪为什么必须加单引号呢？因为它是一个字符串，而不是一个变量，所以不加单或双引号的话是会报错的。</p>

<h2 id="J_CodeLang" class="code-head" style="color: #1f2426;" data-lang="Javascript">:has(selector)过滤选择器（selector也要记得加单引号）</h2>
<div id="J_CodeDescr" class="code-description" style="font: 14px/21px 'Microsoft Yahei', 'Hiragino Sans GB', Helvetica, 'Helvetica Neue', 微软雅黑, Tahoma, Arial, sans-serif; margin: 0px; padding: 0px; color: #1f2426; text-transform: none; text-indent: 0px; letter-spacing: normal; word-spacing: 0px; white-space: normal; -ms-word-break: break-all; font-size-adjust: none; font-stretch: normal; -webkit-text-stroke-width: 0px;">
<div class="code-desc co">
<p style="color: #1f2426;">除了在上一小节介绍的使用包含的字符串内容过滤元素之外，还可以使用包含的元素名称来过滤，<code class="marker" style="margin: 0px 5px; padding: 0px 6px; border-radius: 2px; border: 1px solid #cccccc; font-family: Monaco, Menlo, 'Ubuntu Mono', Consolas, source-code-pro, monospace; font-size: 13px; font-style: normal; font-weight: normal; display: inline; background-color: #eeeeee;">:has(selector)</code>过滤选择器的功能是获取选择器中包含指定元素名称的全部元素，其中<code class="marker" style="margin: 0px 5px; padding: 0px 6px; border-radius: 2px; border: 1px solid #cccccc; font-family: Monaco, Menlo, 'Ubuntu Mono', Consolas, source-code-pro, monospace; font-size: 13px; font-style: normal; font-weight: normal; display: inline; background-color: #eeeeee;">selector</code>参数就是包含的元素名称，是被包含元素。</p>
<p style="color: #1f2426;">例如：获取指定包含某个元素名的全部&lt;li&gt;元素，并改变它们显示文字的颜色，如下图所示：</p>
<p style="color: #1f2426;"><a href="http://img.mukewang.com/529c1a8300017dd003040210.jpg"><img src="http://img.mukewang.com/529c1a8300017dd003040210.jpg" alt="" /></a></p>
<p style="color: #1f2426;">在浏览器中显示的效果：</p>
<p style="color: #1f2426;"><a href="http://img.mukewang.com/529c1aab00017a4d04890294.jpg"><img src="http://img.mukewang.com/529c1aab00017a4d04890294.jpg" alt="" /></a></p>
<p style="color: #1f2426;">可以看出，通过使用<code class="marker" style="margin: 0px 5px; padding: 0px 6px; border-radius: 2px; border: 1px solid #cccccc; font-family: Monaco, Menlo, 'Ubuntu Mono', Consolas, source-code-pro, monospace; font-size: 13px; font-style: normal; font-weight: normal; display: inline; background-color: #eeeeee;">$("li:has('p')")</code>选择器代码，获取了包含&lt;p&gt;元素的全部&lt;li&gt;元素，并通过css方法改变了这些元素在页面中显示的文字样式。</p>

<h2 id="J_CodeLang" class="code-head" style="color: #1f2426;" data-lang="Javascript">:hidden过滤选择器</h2>
<div id="J_CodeDescr" class="code-description" style="font: 14px/21px 'Microsoft Yahei', 'Hiragino Sans GB', Helvetica, 'Helvetica Neue', 微软雅黑, Tahoma, Arial, sans-serif; margin: 0px; padding: 0px; color: #1f2426; text-transform: none; text-indent: 0px; letter-spacing: normal; word-spacing: 0px; white-space: normal; -ms-word-break: break-all; font-size-adjust: none; font-stretch: normal; -webkit-text-stroke-width: 0px;">
<div class="code-desc co">
<p style="color: #1f2426;"><code class="marker" style="margin: 0px 5px; padding: 0px 6px; border-radius: 2px; border: 1px solid #cccccc; font-family: Monaco, Menlo, 'Ubuntu Mono', Consolas, source-code-pro, monospace; font-size: 13px; font-style: normal; font-weight: normal; display: inline; background-color: #eeeeee;">:hidden</code>过滤选择器的功能是获取全部不可见的元素，这些不可见的元素中包括type属性值为hidden的元素。</p>
<p style="color: #1f2426;">例如，调用<code class="marker" style="margin: 0px 5px; padding: 0px 6px; border-radius: 2px; border: 1px solid #cccccc; font-family: Monaco, Menlo, 'Ubuntu Mono', Consolas, source-code-pro, monospace; font-size: 13px; font-style: normal; font-weight: normal; display: inline; background-color: #eeeeee;">:hidden</code>选择器获取不可见的&lt;p&gt;元素，并将该元素的内容显示在&lt;div&gt;元素中，如下图所示：</p>
<p style="color: #1f2426;"><a href="http://img.mukewang.com/529c1c5a00011bc303620165.jpg"><img src="http://img.mukewang.com/529c1c5a00011bc303620165.jpg" alt="" /></a></p>
<p style="color: #1f2426;">在浏览器中显示的效果：</p>
<p style="color: #1f2426;"><a href="http://img.mukewang.com/529c1c760001eaf304890212.jpg"><img src="http://img.mukewang.com/529c1c760001eaf304890212.jpg" alt="" /></a></p>
<p style="color: #1f2426;">从图中可以看出，先调用<code class="marker" style="margin: 0px 5px; padding: 0px 6px; border-radius: 2px; border: 1px solid #cccccc; font-family: Monaco, Menlo, 'Ubuntu Mono', Consolas, source-code-pro, monospace; font-size: 13px; font-style: normal; font-weight: normal; display: inline; background-color: #eeeeee;">$("p:hidden")</code>代码获取隐藏的&lt;p&gt;元素，并调用该元素的html()方法获取该元素中的内容，最后将该内容显示在&lt;div&gt;元素中。</p>

<h2 id="J_CodeLang" class="code-head" style="color: #1f2426;" data-lang="Javascript">:visible过滤选择器</h2>
<div id="J_CodeDescr" class="code-description">
<div class="code-desc co">
<p style="color: #1f2426;">与上一节的<code class="marker">:hidden</code>过滤选择器相反，<code class="marker">:visible</code>过滤选择器获取的是全部可见的元素，也就是说，只要不将元素的display属性值设置为“none”，那么，都可以通过该选择器获取。</p>
<p style="color: #1f2426;">例如，使用<code class="marker">:visible</code>选择器获取可见的&lt;p&gt;元素，并将该元素的内容显示在&lt;div&gt;元素中，如下图所示：</p>
<p style="color: #1f2426;"><a href="http://img.mukewang.com/529c2106000192f303620159.jpg"><img src="http://img.mukewang.com/529c2106000192f303620159.jpg" alt="" /></a></p>
<p style="color: #1f2426;">在浏览器中显示的效果：</p>
<p style="color: #1f2426;"><a href="http://img.mukewang.com/529c212000016e8e04890193.jpg"><img src="http://img.mukewang.com/529c212000016e8e04890193.jpg" alt="" /></a></p>
<p style="color: #1f2426;">从图中可以看出，调用<code class="marker">$("p:visible")</code>选择器代码，获取那个可见的&lt;p&gt;元素，并调用<code class="marker">html()</code>方法获取该元素的内容，最后将该内容显示在&lt;div&gt;元素中。</p>

<h2 id="J_CodeLang" class="code-head" style="color: #1f2426;" data-lang="Javascript">[attribute=value]属性选择器</h2>
<div id="J_CodeDescr" class="code-description">
<div class="code-desc co">
<p style="color: #1f2426;">属性作为DOM元素的一个重要特征，也可以用于选择器中，从本节开始将介绍通过元素属性获取元素的选择器，<code class="marker">[attribute=value]</code>属性选择器的功能是获取与属性名和属性值完全相同的全部元素，其中[]是专用于属性选择器的括号符，参数attribute表示属性名称，value参数表示属性值。</p>
<p style="color: #1f2426;">例如，使用<code class="marker">[attribute=value]</code>属性选择器，获取指定属性名和对应值的全部&lt;li&gt;元素，并设置它们显示的文字颜色，如图所示：</p>
<p style="color: #1f2426;"><a href="http://img.mukewang.com/52bcf22e0001409b03620209.jpg"><img src="http://img.mukewang.com/52bcf22e0001409b03620209.jpg" alt="" /></a></p>
<p style="color: #1f2426;">在浏览器中显示的效果：</p>
<p style="color: #1f2426;"><a href="http://img.mukewang.com/52bcf2560001ad0d04890326.jpg"><img src="http://img.mukewang.com/52bcf2560001ad0d04890326.jpg" alt="" /></a></p>
<p style="color: #1f2426;">从图中可以看出，使用<code class="marker">$("li[title='我最爱']")</code>属性选择器代码，获取了2个&lt;li&gt;元素，并调用css()方法设置它们在页面中显示的文字颜色，另外，属性值中的‘’单引号可以不写，由于属性名与属性值是等号，因此，它们之间不是包含关系，而是完全相同。</p>

<h2 id="J_CodeLang" class="code-head" style="color: #1f2426;" data-lang="Javascript">[attribute!=value]属性选择器（和上边正好相反）</h2>
<h2 id="J_CodeLang" class="code-head" style="color: #1f2426;" data-lang="Javascript">[attribute*=value]属性选择器</h2>
<div id="J_CodeDescr" class="code-description" style="color: #1f2426;">
<div class="code-desc co">

介绍一个功能更为强大的属性选择器<code class="marker">[attribute*=value]</code>，它可以获取属性值中包含指定内容的全部元素，其中[]是专用于属性选择器的括号符，参数attribute表示属性名称，value参数表示对应的属性值。

例如，使用<code class="marker">[attribute*=value]</code>属性选择器，获取属性值中包含某一指定内容的全部&lt;li&gt;元素，并设置它们显示的文字颜色，如下图所示：

<a href="http://img.mukewang.com/529c27b600019c1b03500209.jpg"><img src="http://img.mukewang.com/529c27b600019c1b03500209.jpg" alt="" /></a>

在浏览器中显示的效果：

<a href="http://img.mukewang.com/529c27e4000154cc04890326.jpg"><img src="http://img.mukewang.com/529c27e4000154cc04890326.jpg" alt="" /></a>

从图中可以看出，使用<code class="marker">$("li[title*='最']")</code>属性选择器代码，获取了3个&lt;li&gt;元素，这些元素的title属性值中都包含了“最”字符，获取这些元素后并调用<code class="marker">css()</code>方法设置这些元素在页面中显示的文字颜色。

</div>
</div>
<h2 id="J_CodeLang" class="code-head" style="color: #1f2426;" data-lang="Javascript">:first-child子元素过滤选择器</h2>
<div id="J_CodeDescr" class="code-description" style="color: #1f2426;">
<div class="code-desc co">

通过上面章节的学习，我们知道使用<code class="marker">:first</code>过滤选择器可以获取指定父元素中的首个子元素，但该选择器返回的只有一个元素，并不是一个集合，而使用<code class="marker">:first-child</code>子元素过滤选择器则可以获取每个父元素中返回的首个子元素，它是一个集合，常用多个集合数据的选择处理。

如下图，如果想把页面中每个ul中的第一个li获取到，并改变其颜色。则可以使用

<code class="marker">: first-child</code>

<a href="http://img.mukewang.com/529c2a9000014a0e03500322.jpg"><img src="http://img.mukewang.com/529c2a9000014a0e03500322.jpg" alt="" /></a>

在浏览器中显示的效果：

<a href="http://img.mukewang.com/529c2ab600011b5804890326.jpg"><img src="http://img.mukewang.com/529c2ab600011b5804890326.jpg" alt="" /></a>

通过<code class="marker">$("li:first-child")</code>选择器代码，获取了两个&lt;ul&gt;父元素中的第一个&lt;li&gt;元素，并使用<code class="marker">css()</code>方法修改了它们在页面中显示的文字颜色。

&nbsp;
<h2 id="J_CodeLang" class="code-head" data-lang="Javascript">:last-child子元素过滤选择器（和上边正好相反）</h2>
</div>
</div>

<hr style="color: #1f2426;" />

<h2 class="code-head" style="color: #1f2426;" data-lang="Javascript">:input表单选择器(<span style="color: #ff0000;">:前有空格</span>)</h2>
<div id="J_CodeDescr" class="code-description">
<div class="code-desc co">
<p style="color: #1f2426;">如何获取表单全部元素？<code class="marker">:input</code>表单选择器可以实现，它的功能是返回<strong>全部的表单元素</strong>，不仅包括所有&lt;input&gt;标记的表单元素，而且还包括&lt;textarea&gt;、&lt;select&gt; 和 &lt;button&gt;标记的表单元素，因此，它选择的表单元素是最广的。</p>
<p style="color: #1f2426;">如下图所示，使用<code class="marker">:input</code>表单选择器获取表单元素，并向这些元素增加一个CSS样式类别，修改它们在页面中显示的边框颜色。</p>
<p style="color: #1f2426;"><img src="http://img.mukewang.com/52970dc4000102ab03820242.jpg" alt="" /></p>
<p style="color: #1f2426;">在浏览器中显示的效果：</p>
<p style="color: #1f2426;"><img src="http://img.mukewang.com/52970dd300016ac304760305.jpg" alt="" /></p>
<p style="color: #1f2426;">可以看出，通过调用$("#frmTest :input")表单选择器代码获取了表单中的全部元素，并使用addClass()方法修改它们在页面中显示的边框颜色。addClass()方法的功能是为元素添加指定的样式类别名称，它的更多使用将会在后续章节中进行详细介绍。</p>

<h2 id="J_CodeLang" class="code-head" style="color: #1f2426;" data-lang="Javascript">:text表单文本选择器(<span style="color: #ff0000;">:前有空格</span>)</h2>
<div id="J_CodeDescr" class="code-description">
<div class="code-desc co">
<p style="color: #1f2426;"><code class="marker">:text</code>表单文本选择器可以获取表单中全部<span style="color: #ff0000;">单行</span>的<span style="color: #0000ff;">文本输入框</span>元素，单行的文本输入框就像一个不换行的字条工具，使用非常广泛。</p>
<p style="color: #1f2426;">例如，在表单中添加多个元素，使用<code class="marker">:text</code>选择器获取单行的文本输入框元素，并修改字的边框颜色，如下图所示：</p>
<p style="color: #1f2426;"><img src="http://img.mukewang.com/5297107600011ddf04240201.jpg" alt="" /></p>
<p style="color: #1f2426;">在浏览器中显示的效果：</p>
<p style="color: #1f2426;"><img src="http://img.mukewang.com/52971086000125ea04440275.jpg" alt="" /></p>
<p style="color: #1f2426;">从图中可以看出，通过<code class="marker">:text</code>表单选择器只获取单行的文本输入框元素，对于&lt;textarea&gt;区域文本、按钮元素无效。</p>

<h2 class="code-head" style="color: #1f2426;" data-lang="Javascript">:password表单密码选择器(<span style="color: #ff0000;">:前有空格</span>)</h2>
<div id="J_CodeDescr" class="code-description">
<div class="code-desc co">
<p style="color: #1f2426;">如果想要获取密码输入文本框，可以使用<code class="marker">:password</code>选择器，它的功能是获取表单中全部的密码输入文本框元素。</p>
<p style="color: #1f2426;">例如，在表单中添加多个输入框元素，使用<code class="marker">:password</code>获取密码输入文本框元素，并修改它的边框颜色，如下图所示：</p>
<p style="color: #1f2426;"><img src="http://img.mukewang.com/529713cd000159b804810217.jpg" alt="" /></p>
<p style="color: #1f2426;">在浏览器中显示的效果：</p>
<p style="color: #1f2426;"><img src="http://img.mukewang.com/529713e50001b30004510309.jpg" alt="" /></p>
<p style="color: #1f2426;">从图中可以看出，在多个文本输入框中，使用:password选择器只能获取表单中的密码输入文本框，并使用addClass()方法改变它的边框颜色。</p>

<h2 class="code-head" style="color: #1f2426;" data-lang="Javascript">:radio单选按钮选择器(<span style="color: #ff0000;">:前有空格</span>)</h2>
<div id="J_CodeDescr" class="code-description">
<div class="code-desc co">
<p style="color: #1f2426;">表单中的单选按钮常用于多项数据中仅选择其一，而使用<code class="marker">:radio</code>选择器可轻松获取表单中的<strong>全部单选按钮</strong>元素。</p>
<p style="color: #1f2426;">例如，在表单中添加多种类型的表单元素，使用<code class="marker">:radio</code>选择器获取并隐藏这些元素中的全部单选按钮元素，如下图所示：</p>
<p style="color: #1f2426;"><img src="http://img.mukewang.com/529715580001099503830280.jpg" alt="" /></p>
<p style="color: #1f2426;"><code class="marker">hide()</code>方法的功能是隐藏指定的元素。</p>
<p style="color: #1f2426;">在浏览器中显示的效果：</p>
<p style="color: #1f2426;"><img src="http://img.mukewang.com/529715c60001ca0504500321.jpg" alt="" /></p>

<h2 class="code-head" style="color: #1f2426;" data-lang="Javascript">:checkbox复选框选择器(<span style="color: #ff0000;">:前有空格</span>)</h2>
<div id="J_CodeDescr" class="code-description">
<div class="code-desc co">
<p style="color: #1f2426;">表单中的复选框常用于多项数据的选择，使用<code class="marker">:checkbox</code>选择器可以快速定位并获取表单中的复选框元素。</p>
<p style="color: #1f2426;">例如，在表单中增加多个不同类型的元素，使用<code class="marker">:checkbox</code>选择器获取其中的全部复选框元素，并将它们全部设为选中状态，如下图所示：</p>
<p style="color: #1f2426;"><a href="http://img.mukewang.com/52971ac700017fbf03830322.jpg"><img src="http://img.mukewang.com/52971ac700017fbf03830322.jpg" alt="" /></a></p>
<p style="color: #1f2426;">在浏览器中显示的效果：</p>
<p style="color: #1f2426;"><a href="http://img.mukewang.com/52971afe0001750304500280.jpg"><img src="http://img.mukewang.com/52971afe0001750304500280.jpg" alt="" /></a></p>

<h2 id="J_CodeLang" class="code-head" style="color: #1f2426;" data-lang="Javascript">:submit提交按钮选择器</h2>
<h2 class="code-head" style="color: #1f2426;" data-lang="Javascript">（<span style="color: #0000ff;">注意这个和上边的都不同</span>）</h2>
<h2 style="color: #1f2426;"><span style="color: #ff6600;">父子元素之间需要空格； 属性之间不需要空格</span></h2>
<div id="J_CodeDescr" class="code-description">
<div class="code-desc co">
<p style="color: #1f2426;">通常情况下，一个表单中只允许有一个“type”属性值为“submit”的提交按钮，使用<code class="marker">:submit</code>选择器可获取表单中的这个<strong>提交按钮</strong>元素。</p>
<p style="color: #1f2426;">例如，在表单中添加多个不同类型的按钮，使用<code class="marker">:submit</code>选择器获取其中的提交按钮，并使用<code class="marker">attr()</code>方法修改按钮显示的文本内容，如下图所示：</p>
<p style="color: #1f2426;"><a href="http://img.mukewang.com/52b2584e000129a804330199.jpg"><img src="http://img.mukewang.com/52b2584e000129a804330199.jpg" alt="" /></a></p>
<p style="color: #1f2426;">在浏览器中显示的效果：</p>
<p style="color: #1f2426;"><a href="http://img.mukewang.com/52b258c60001e23604500280.jpg"><img src="http://img.mukewang.com/52b258c60001e23604500280.jpg" alt="" /></a></p>
<p style="color: #1f2426;">从图中可以看出，使用<code class="marker">:submit</code>选择器从三种类型按钮中获取了提交按钮，并使用<code class="marker">attr()</code>方法将该按钮显示的文字修改为“点我就提交了”。</p>

<h2 class="code-head" style="color: #1f2426;" data-lang="Javascript">:image图像域选择器(<span style="color: #ff0000;">:前有空格</span>)</h2>
<div id="J_CodeDescr" class="code-description">
<div class="code-desc co">
<p style="color: #1f2426;">当一个&lt;input&gt;元素的“type”属性值设为“image”时，该元素就是一个图像域，使用<code class="marker">:image</code>选择器可以快速获取该类全部元素。例如，在表单中添加两种类型的图像元素，使用<code class="marker">:image</code>选择器获取其中的一种图像元素，并改变该元素的边框样式，如下图所示：</p>
<p style="color: #1f2426;"><a href="http://img.mukewang.com/52b26da200016f8604270192.jpg"><img src="http://img.mukewang.com/52b26da200016f8604270192.jpg" alt="" /></a></p>
<p style="color: #1f2426;">在浏览器中显示的效果：</p>
<p style="color: #1f2426;"><a href="http://img.mukewang.com/52b26dbd0001659f04500342.jpg"><img src="http://img.mukewang.com/52b26dbd0001659f04500342.jpg" alt="" /></a></p>
<p style="color: #1f2426;">从图中可以看出，使用<code class="marker">:image</code>选择器只能获取&lt;input&gt;图像域，而不能获取&lt;img&gt;格式的图像元素。</p>

<h2 class="code-head" style="color: #1f2426;" data-lang="Javascript">:button表单按钮选择器(<span style="color: #ff0000;">:前有空格</span>)</h2>
<div id="J_CodeDescr" class="code-description">
<div class="code-desc co">
<p style="color: #1f2426;">表单中包含许多类型的按钮，而使用<code class="marker">:button</code>选择器能获取且只能获取“type”属性值为“button”的&lt;input&gt;和&lt;button&gt;这两类普通按钮元素。</p>
<p style="color: #1f2426;">例如，在表单中添加多种类型的按钮元素，使用<code class="marker">:button</code>选择器获取其中的普通按钮元素，并修改它们的边框色，如下图所示：</p>
<p style="color: #1f2426;"><a href="http://img.mukewang.com/52b286a50001862e04740207.jpg"><img src="http://img.mukewang.com/52b286a50001862e04740207.jpg" alt="" /></a></p>
<p style="color: #1f2426;">在浏览器中显示的效果：</p>
<p style="color: #1f2426;"><a href="http://img.mukewang.com/52b286e100017beb04530252.jpg"><img src="http://img.mukewang.com/52b286e100017beb04530252.jpg" alt="" /></a></p>
<p style="color: #1f2426;">从图中可以看出，使用<code class="marker">:button</code>选择器只能获取两种类型的普通按钮，且修改了它们的边框颜色，并未获取表单中的“提交按钮”。</p>

<h2 class="code-head" style="color: #1f2426;" data-lang="Javascript">:checked选中状态选择器(<span style="color: #ff0000;">:前有空格</span>)</h2>
<div id="J_CodeDescr" class="code-description">
<div class="code-desc co">
<p style="color: #1f2426;">有一些元素存在选中状态，如复选框、单选按钮元素，选中时“checked”属性值为“checked”，调用:checked可以获取处于选中状态的全部元素。</p>
<p style="color: #1f2426;">例如，在表单中添加多个复选框和单选按钮，其中有一些元素处于选中状态，使用<code class="marker">:checked</code><strong>获取</strong>并<strong>隐藏</strong>处于选中状态的元素，如下图所示：</p>
<p style="color: #1f2426;"><a href="http://img.mukewang.com/52b28b1500017db404530386.jpg"><img src="http://img.mukewang.com/52b28b1500017db404530386.jpg" alt="" /></a></p>
<p style="color: #1f2426;">在浏览器中显示的效果：</p>
<p style="color: #1f2426;"><a href="http://img.mukewang.com/52b28b3b00015c7f04500290.jpg"><img src="http://img.mukewang.com/52b28b3b00015c7f04500290.jpg" alt="" /></a></p>
<p style="color: #1f2426;">从图中可以看出，使用<code class="marker">:checked</code>选择器可以获取处于选中状态的元素，并调用<code class="marker">hide()</code>方法将它们进行隐藏。</p>
<p style="color: #1f2426;"><span style="color: #0000ff;">例子：设置被选中的不可用     $("#frmTest :checked").attr("disabled", true);</span></p>

<h2 class="code-head" style="color: #1f2426;" data-lang="Javascript">:selected选中状态选择器(<span style="color: #ff0000;">:前有空格</span>)</h2>
<div id="J_CodeDescr" class="code-description">
<div class="code-desc co">
<p style="color: #1f2426;">与<code class="marker">:checked</code>选择器相比，<code class="marker">:selected</code>选择器只能获取&lt;select&gt;下拉列表框中全部处于选中状态的&lt;option&gt;选项元素。</p>
<p style="color: #1f2426;">例如，在一个添加多个&lt;option&gt;选项的下拉列表框中，使用<code class="marker">:selected</code>选择器修改处于选中状态的内容值，如下图所示：</p>
<p style="color: #1f2426;"><a href="http://img.mukewang.com/52b28d15000198f404430262.jpg"><img src="http://img.mukewang.com/52b28d15000198f404430262.jpg" alt="" /></a></p>
<p style="color: #1f2426;">在浏览器中显示的效果：</p>
<p style="color: #1f2426;"><a href="http://img.mukewang.com/52b28d370001a09004570304.jpg"><img src="http://img.mukewang.com/52b28d370001a09004570304.jpg" alt="" /></a></p>
<p style="color: #1f2426;">从图中可以看出，使用<code class="marker">:selected</code>选择器获取处于选中状态的&lt;option&gt;元素，并调用<code class="marker">text()</code>方法修改这些选中状态元素显示的内容。<code class="marker">text()</code>方法的功能是获取或设置元素的文本内容，该方法在后续将有详细的介绍。</p>


<hr style="color: #1f2426;" />

<h2 id="J_CodeLang" class="code-head" style="color: #1f2426;" data-lang="Javascript">使用attr()方法控制元素的属性</h2>
<div id="J_CodeDescr" class="code-description">
<div class="code-desc co">
<p style="color: #1f2426;"><code class="marker">attr()</code>方法的作用是设置或者返回元素的属性，其中<code class="marker">attr(属性名)</code>格式是获取元素属性名的值，<code class="marker">attr(属性名，属性值)</code>格式则是设置元素属性名的值。</p>
<p style="color: #1f2426;">例如，使用<code class="marker">attr(属性名)</code>的格式获取页面中&lt;a&gt;元素的“href”属性值，并将该值的内容显示在&lt;span&gt;元素中，如下图所示：</p>
<p style="color: #1f2426;"><a href="http://img.mukewang.com/52bb8ca300011b7203780146.jpg"><img src="http://img.mukewang.com/52bb8ca300011b7203780146.jpg" alt="" /></a></p>
<p style="color: #1f2426;">在浏览器中显示的效果：</p>
<p style="color: #1f2426;"><a href="http://img.mukewang.com/52bb8cc20001a63c04570304.jpg"><img src="http://img.mukewang.com/52bb8cc20001a63c04570304.jpg" alt="" /></a></p>
<p style="color: #1f2426;">从图中可以看出，通过<code class="marker">attr()</code>方法可以方便地获取元素中指定属性名称的内容，并将获取的内容通过<code class="marker">html()</code>方法显示在页面中。</p>
<p style="color: #1f2426;"><span style="color: #ff0000;">attr也可以修改属性</span></p>
<p style="color: #1f2426;"><span style="color: #ff0000;">例如：</span></p>
<p style="color: #1f2426;"><span style="color: #ff0000;">$("#aid").attr("href","http://www.baidu.com")</span></p>
<p style="color: #1f2426;"><span style="color: #ff0000;">如果是多属性则可以写成</span></p>
<p style="color: #1f2426;"><span style="color: #ff0000;">$("#aid").attr("href"："http://www.baidu.com"，</span></p>
<p style="color: #1f2426;"><span style="color: #ff0000;">                        “title"：”hello"</span></p>
<p style="color: #1f2426;"><span style="color: #ff0000;">)</span></p>

<h2 id="J_CodeLang" class="code-head" style="color: #1f2426;" data-lang="Javascript">操作元素的内容</h2>
<div id="J_CodeDescr" class="code-description">
<div class="code-desc co">
<p style="color: #1f2426;">使用<code class="marker">html()</code>和<code class="marker">text()</code>方法操作元素的内容，当两个方法的参数为空时，表示获取该元素的内容，而如果方法中包含参数，则表示将参数值设置为元素内容。</p>
<p style="color: #1f2426;">例如，分别使用<code class="marker">html()</code>和<code class="marker">text()</code>方法获取一个元素的内pww，并将获取的内容显示在不同的&lt;div&gt;元素中，如下图所示：</p>
<p style="color: #1f2426;"><a href="http://img.mukewang.com/52bb90400001a1eb03640193.jpg"><img src="http://img.mukewang.com/52bb90400001a1eb03640193.jpg" alt="" /></a></p>
<p style="color: #1f2426;">在浏览器中显示的效果：</p>
<p style="color: #1f2426;"><a href="http://img.mukewang.com/52bb905f0001d02d04880262.jpg"><img src="http://img.mukewang.com/52bb905f0001d02d04880262.jpg" alt="" /></a></p>
<p style="color: #1f2426;"><span style="color: #ff0000;">从图中可以看出，<code class="marker">html()</code>方法可以<strong>获取元素的HTML内容</strong>，因此，原文中的格式代码也被一起获取，而<code class="marker">text()</code>方法只是<strong>获取元素中的文本内容</strong>，并不包含HTML格式代码，所以它显示的内容并没有变“歪”。</span></p>
<p style="color: #1f2426;"><span style="color: #ff0000;">其实还有.val用法也是一样的</span></p>
<p style="color: #1f2426;"><span style="color: #ff0000;">还有：</span></p>
<p style="color: #1f2426;"><span style="color: #ff0000;">$("#p5").text(function(i,ot){</span></p>
<p style="color: #1f2426;"><span style="color: #ff0000;">return "old:"+ot+"new:"i"</span></p>
<p style="color: #1f2426;"><span style="color: #ff0000;">})</span></p>
<p style="color: #1f2426;"><span style="color: #ff0000;">这个是ot是修改后的文字 i是修改前的文字</span></p>

<h2 id="J_CodeLang" class="code-head" style="color: #1f2426;" data-lang="Javascript">操作元素的样式css和addClass</h2>
<div id="J_CodeDescr" class="code-description">
<div class="code-desc co">
<p style="color: #1f2426;">通过<code class="marker">addClass()</code>和<code class="marker">css()</code>方法可以方便地操作元素中的样式，前者括号中的参数为增加元素的样式名称，后者直接将样式的属性内容写在括号中。</p>
<p style="color: #1f2426;">例如，使用<code class="marker">addClass()</code>方法，改变&lt;div&gt;元素的背景色和文字颜色，如下图所示：</p>
<p style="color: #1f2426;"><a href="http://img.mukewang.com/52bb94080001c89c03270369.jpg"><img src="http://img.mukewang.com/52bb94080001c89c03270369.jpg" alt="" /></a></p>
<p style="color: #1f2426;">在浏览器中显示的效果：</p>
<p style="color: #1f2426;"><a href="http://img.mukewang.com/52bb942a000109d204480252.jpg"><img src="http://img.mukewang.com/52bb942a000109d204480252.jpg" alt="" /></a></p>
<p style="color: #1f2426;">从图中可以看出，通过<code class="marker">addClass()</code>方法为&lt;div&gt;元素增加了两个样式名称，从而改变了&lt;div&gt;元素的背景和文字颜色，增加多个样式名称时，要用空格隔开。</p>
<p style="color: #1f2426;">css()方法和addClass方法用法类似，只是需要去设置具体样式了。具体用法同学们可以在下面的任务中自己尝试</p>
<p style="color: #1f2426;"> <span style="color: #0000ff;">先说下css</span></p>
<p style="color: #1f2426;"><span style="color: #0000ff;">单个修改</span></p>
<p style="color: #1f2426;"><span style="color: #0000ff;">$("div").css("width","100px")    </span></p>
<p style="color: #1f2426;"><span style="color: #0000ff;">多个修改</span></p>
<p style="color: #1f2426;"><span style="color: #0000ff;">$("div").css({         <span style="color: #ff0000;">记得加一个大括号</span></span></p>
<p style="color: #1f2426;"><span style="color: #0000ff;">width:"100px",     <span style="color: #ff0000;">中间是用逗号隔开</span></span></p>
<p style="color: #1f2426;"><span style="color: #0000ff;">height:"100px"</span></p>
<p style="color: #1f2426;"><span style="color: #0000ff;">})</span></p>
<p style="color: #1f2426;"><span style="color: #0000ff;">移除样式：</span></p>
<p style="color: #1f2426;"><span style="color: #0000ff;">$("div").click(function(){</span></p>
<p style="color: #1f2426;"><span style="color: #0000ff;">$(this).removeClass("类名")；   这是移除样式</span></p>
<p style="color: #1f2426;"><span style="color: #0000ff;">$(this).toggleClass("类名");    <span style="color: #ff0000;">通过点击事件来切换两种样式</span>，原来和括号内样式</span></p>
<p style="color: #1f2426;"><span style="color: #0000ff;">})</span></p>

<h2 id="J_CodeLang" class="code-head" style="color: #1f2426;" data-lang="Javascript">移除属性和样式</h2>
<div id="J_CodeDescr" class="code-description">
<div class="code-desc co">
<p style="color: #1f2426;">使用<code class="marker">removeAttr(name)</code>和<code class="marker">removeClass(class)</code>分别可以实现移除元素的属性和样式的功能，前者方法中参数表示移除属性名，后者方法中参数则表示移除的样式名</p>
<p style="color: #1f2426;">例如，使用<code class="marker">removeAttr()</code>方法移除&lt;a&gt;元素中的“href”属性，如下图所示：</p>
<p style="color: #1f2426;"><a href="http://img.mukewang.com/52bb960c0001f4c603770161.jpg"><img src="http://img.mukewang.com/52bb960c0001f4c603770161.jpg" alt="" /></a></p>
<p style="color: #1f2426;">在浏览器中显示的效果：</p>
<p style="color: #1f2426;"><a href="http://img.mukewang.com/52bb962a00017ec807170294.jpg"><img src="http://img.mukewang.com/52bb962a00017ec807170294.jpg" alt="" /></a></p>
<p style="color: #1f2426;">从图中可以看出，使用<code class="marker">removeAttr()</code>方法移除元素的“href”属性后，再次显示元素的“href”属性值时，则为空值，&lt;a&gt;元素中的文字也丢失可点击的效果。</p>

<h2 id="J_CodeLang" class="code-head" style="color: #1f2426;" data-lang="Javascript">使用append()方法向元素内追加内容，最后一个元素</h2>
<h2 class="code-head" style="color: #1f2426;" data-lang="Javascript">prepend（）是第一个元素追加</h2>
<p style="color: #1f2426;"><span style="color: #ff0000;">添加一共加上下边一共有4种</span></p>

<div id="J_CodeDescr" class="code-description">
<div class="code-desc co">
<p style="color: #1f2426;"><code class="marker">append(content)</code>方法的功能是向指定的元素中追加内容，被追加的content参数，可以是字符、HTML元素标记，还可以是一个返回字符串内容的函数。</p>
<p style="color: #1f2426;">例如，在页面的&lt;body&gt;元素中追加一个具有“id”、“title”属性和显示内容的&lt;div&gt;元素，如下图所示：</p>
<p style="color: #1f2426;"><a href="http://img.mukewang.com/52bb980d0001c85804680122.jpg"><img src="http://img.mukewang.com/52bb980d0001c85804680122.jpg" alt="" /></a></p>
<p style="color: #1f2426;">在浏览器中显示的效果：</p>
<p style="color: #1f2426;"><a href="http://img.mukewang.com/52bb9828000185b404530235.jpg"><img src="http://img.mukewang.com/52bb9828000185b404530235.jpg" alt="" /></a></p>
<p style="color: #1f2426;">从图中可以看出，由于使用<code class="marker">append()</code>方法在&lt;body&gt;元素中追加了一些HTML 元素标记，因此追加后，这些元素标记直接生成对应的元素和属性显示在页面中。</p>

<h2 id="J_CodeLang" class="code-head" style="color: #1f2426;" data-lang="Javascript">使用appendTo()方法向被选元素内插入内容(只是插入并非增加)</h2>
<div id="J_CodeDescr" class="code-description">
<div class="code-desc co">
<p style="color: #1f2426;"><code class="marker">appendTo()</code>方法也可以向指定的元素内插入内容，它的使用格式是：</p>
<p style="color: #1f2426;"><code class="marker"><strong>$(content).appendTo(selector)</strong></code></p>
<p style="color: #1f2426;">参数content表示需要插入的内容，参数selector表示被选的元素，即把content内容插入selector元素内，默认是在尾部。</p>
<p style="color: #1f2426;">例如，使用<code class="marker">appendTo()</code>方法，将&lt;div&gt;外的&lt;span&gt;元素插入&lt;div&gt;内，如下图所示：</p>
<p style="color: #1f2426;"><a href="http://img.mukewang.com/52bcd7850001d30303360171.jpg"><img src="http://img.mukewang.com/52bcd7850001d30303360171.jpg" alt="" /></a></p>
<p style="color: #1f2426;">在浏览器中显示的效果：</p>
<p style="color: #1f2426;"><a href="http://img.mukewang.com/52bcd7ad0001f82b04670275.jpg"><img src="http://img.mukewang.com/52bcd7ad0001f82b04670275.jpg" alt="" /></a></p>
<p style="color: #1f2426;">从图中可以看出，使用<code class="marker">appendTo()</code>方法将类别名为“red”的&lt;span&gt;元素插入到&lt;div&gt;元素的尾部，相当于追加的效果。</p>
<p style="color: #1f2426;"><span style="color: #ff0000;">下边是配合着使用</span></p>
<p style="color: #1f2426;"><span style="color: #ff0000;">&lt;script type="text/javascript"&gt;</span>
<span style="color: #ff0000;"> var $html = "&lt;span class='red'&gt;小青蛙&lt;/span&gt;"</span>
<span style="color: #ff0000;"> $("body").append($html);</span>
<span style="color: #ff0000;"> $(".red").appendTo("div");</span>
<span style="color: #ff0000;"> &lt;/script&gt;</span></p>

<h2 id="J_CodeLang" class="code-head" style="color: #1f2426;" data-lang="Javascript">使用before()和after()在元素前后插入内容</h2>
<div id="J_CodeDescr" class="code-description">
<div class="code-desc co">
<p style="color: #1f2426;">使用<code class="marker">before()</code>和<code class="marker">after()</code>方法可以在元素的前后插入内容，它们分别表示在整个元素的前面和后面插入指定的元素或内容，调用格式分别为：</p>
<p style="color: #1f2426;"><code class="marker"><strong>$(selector).before(content)</strong></code>和<code class="marker"><strong>$(selector).after(content)</strong></code></p>
<p style="color: #1f2426;">其中参数content表示插入的内容，该内容可以是元素或HTML字符串。</p>
<p style="color: #1f2426;">例如，调用<code class="marker">before()</code>方法在一个&lt;span&gt;元素插入另一个&lt;span&gt;元素，如下图所示：</p>
<p style="color: #1f2426;"><a href="http://img.mukewang.com/52bcd9cd0001645203820142.jpg"><img src="http://img.mukewang.com/52bcd9cd0001645203820142.jpg" alt="" /></a></p>
<p style="color: #1f2426;">在浏览器中显示的效果：</p>
<p style="color: #1f2426;"><a href="http://img.mukewang.com/52bcd9fd0001594d04670263.jpg"><img src="http://img.mukewang.com/52bcd9fd0001594d04670263.jpg" alt="" /></a></p>
<p style="color: #1f2426;">从图中可以看出，使用<code class="marker">before()</code>方法将<strong>HTML格式</strong>的内容插入到原有&lt;span&gt;元素内容之前，而并不仅是它的内部文本。</p>

<h2 id="J_CodeLang" class="code-head" style="color: #1f2426;" data-lang="Javascript">使用clone()方法复制元素</h2>
<div id="J_CodeDescr" class="code-description">
<div class="code-desc co">
<p style="color: #1f2426;">调用<code class="marker">clone()</code>方法可以生成一个被选元素的副本，即复制了一个被选元素，包含它的节点、文本和属性，它的调用格式为：</p>
<p style="color: #1f2426;"><code class="marker"><strong>$(selector).clone()</strong></code></p>
<p style="color: #1f2426;">其中参数selector可以是一个元素或HTML内容。</p>
<p style="color: #1f2426;">例如，使用<code class="marker">clone()</code>方法复制页面中的一个&lt;span&gt;元素，并将复制后的元素追加到页面的后面，如下图所示：</p>
<p style="color: #1f2426;"><a href="http://img.mukewang.com/52bb9da80001fede03660123.jpg"><img src="http://img.mukewang.com/52bb9da80001fede03660123.jpg" alt="" /></a></p>
<p style="color: #1f2426;">在浏览器中显示的效果：</p>
<p style="color: #1f2426;"><a href="http://img.mukewang.com/52bb9dce0001d15304670256.jpg"><img src="http://img.mukewang.com/52bb9dce0001d15304670256.jpg" alt="" /></a></p>
<p style="color: #1f2426;">从图中可以看出，使用<code class="marker">clone()</code>方法复制元素时，不仅复制了该元素的文本和节点，还将它的“title”属性也一起复制过来了。</p>

<h2 id="J_CodeLang" class="code-head" style="color: #1f2426;" data-lang="Javascript">替换内容</h2>
<div id="J_CodeDescr" class="code-description">
<div class="code-desc co">
<p style="color: #1f2426;"><code class="marker">replaceWith()</code>和<code class="marker">replaceAll()</code>方法都可以用于替换元素或元素中的内容，但它们调用时，内容和被替换元素所在的位置不同，分别为如下所示：</p>
<p style="color: #1f2426;"><code class="marker"><strong>$(selector).replaceWith(content)</strong></code>和<code class="marker"><strong>$(content).replaceAll(selector)</strong></code></p>
<p style="color: #1f2426;">参数selector为被替换的元素，content为替换的内容。</p>
<p style="color: #1f2426;">例如，调用<code class="marker">replaceWith()</code>方法将页面中&lt;span&gt;元素替换成一段HTML字符串，如下图所示：</p>
<p style="color: #1f2426;"><a href="http://img.mukewang.com/52bcdc2c0001b69c04750130.jpg"><img src="http://img.mukewang.com/52bcdc2c0001b69c04750130.jpg" alt="" /></a></p>
<p style="color: #1f2426;">在浏览器中显示的效果：</p>
<p style="color: #1f2426;"><a href="http://img.mukewang.com/52bcdc4f0001e25f04830237.jpg"><img src="http://img.mukewang.com/52bcdc4f0001e25f04830237.jpg" alt="" /></a></p>
<p style="color: #1f2426;">从图中可以看出，使用<code class="marker">replaceWith()</code>方法替换类别名为“green”的&lt;span&gt;元素，替换之后，旧元素完全由新替换的元素所取代。</p>
<p style="color: #1f2426;"><span style="color: #ff0000;">$(selector).replaceWith(content)和 $(content).replaceAll(selector) 得看仔细了 replaceWith （元素）里面被替换得（内容） replaceAll （内容）覆盖掉（元素）里面内容</span></p>
<p style="color: #1f2426;"><span style="color: #ff0000;"> &lt;script type="text/javascript"&gt;</span>
<span style="color: #ff0000;"> var $html = "&lt;span class='red' title='hi'&gt;我是土豪&lt;/span&gt;";</span>
<span style="color: #ff0000;"> $($html).replaceAll(".green");</span>
<span style="color: #ff0000;"> &lt;/script&gt;</span></p>

<h2 id="J_CodeLang" class="code-head" style="color: #1f2426;" data-lang="Javascript">使用wrap()和wrapInner()方法包裹元素和内容</h2>
<div id="J_CodeDescr" class="code-description">
<div class="code-desc co">
<p style="color: #1f2426;"><code class="marker">wrap()</code>和<code class="marker">wrapInner()</code>方法都可以进行元素的包裹，但前者用于包裹元素本身，后者则用于包裹元素中的内容，它们的调用格式分别为：</p>
<p style="color: #1f2426;"><code class="marker"><strong>$(selector).wrap(wrapper)</strong></code>和<code class="marker"><strong>$(selector).wrapInner(wrapper)</strong></code></p>
<p style="color: #1f2426;">参数selector为被包裹的元素，wrapper参数为包裹元素的格式。</p>
<p style="color: #1f2426;">例如，调用<code class="marker">wrap()</code>方法，将&lt;span&gt;用&lt;div&gt;元素包裹起来，如下图所示：</p>
<p style="color: #1f2426;"><a href="http://img.mukewang.com/52bcdea700016dbf03980120.jpg"><img src="http://img.mukewang.com/52bcdea700016dbf03980120.jpg" alt="" /></a></p>
<p style="color: #1f2426;">在浏览器中显示的效果：</p>
<p style="color: #1f2426;"><a href="http://img.mukewang.com/52bcdf080001301504830245.jpg"><img src="http://img.mukewang.com/52bcdf080001301504830245.jpg" alt="" /></a></p>
<p style="color: #1f2426;">从图中可以看出，红色区域的&lt;span&gt;元素被蓝色边框的&lt;div&gt;元素通过<code class="marker">wrap()</code>方法包裹起来。</p>

<h2 id="J_CodeLang" class="code-head" style="color: #1f2426;" data-lang="Javascript">使用each()方法遍历元素</h2>
<div id="J_CodeDescr" class="code-description">
<div class="code-desc co">
<p style="color: #1f2426;">使用<code class="marker">each()</code>方法可以遍历指定的元素集合，在遍历时，通过回调函数返回遍历元素的序列号，它的调用格式为：</p>
<p style="color: #1f2426;"><code class="marker"><strong>$(selector).each(function(index))</strong></code></p>
<p style="color: #1f2426;">参数function为遍历时的回调函数，index为遍历元素的序列号，它从0开始。</p>
<p style="color: #1f2426;">例如，遍历页面中的&lt;span&gt;元素，当元素的序列号为2时，添加名为“focus”的样式，如下图所示：</p>
<p style="color: #1f2426;"><a href="http://img.mukewang.com/52bba3720001175203180227.jpg"><img src="http://img.mukewang.com/52bba3720001175203180227.jpg" alt="" /></a></p>
<p style="color: #1f2426;">在浏览器中显示的效果：</p>
<p style="color: #1f2426;"><a href="http://img.mukewang.com/52bba38e00013f0a04830260.jpg"><img src="http://img.mukewang.com/52bba38e00013f0a04830260.jpg" alt="" /></a></p>
<p style="color: #1f2426;">从图中可以看出，在使用<code class="marker">each()</code>方法遍历&lt;span&gt;元素时，回调函数中的“index”参数为元素的序列号，它从0开始，当为2时，表示第3个&lt;span&gt;元素增加样式。</p>

<h3 style="color: #1f2426;"><strong><span style="color: #ff0000;">主要是记得index和this的用法</span></strong></h3>
<p style="color: #1f2426;">补充知识点：</p>
<p style="color: #1f2426;"><span style="color: #ff0000;">向下遍历：</span></p>
<p style="color: #1f2426;">children（）：只能向下遍历一层，（）内可以加参数也可以不加</p>
<p style="color: #1f2426;">find（）：想改变下边哪个就改变下边哪个，只有一级</p>
<p style="color: #1f2426;">$("#div1").children().css({border:"3px solid #000"})</p>
<p style="color: #1f2426;"><span style="color: #ff0000;">向上遍历：</span></p>
<p style="color: #1f2426;">parent（）：上一层改变，参数其实没有什么意义主要是$()的上一层</p>
<p style="color: #1f2426;">parents（）：上所有级都改变</p>
<p style="color: #1f2426;">parentUntil（）：区间内的改变，不包含参数层</p>
<p style="color: #1f2426;"><span style="color: #ff0000;">同级遍历（7种）：</span></p>
<p style="color: #1f2426;">sibings（）：修改同级所有元素，除了他自己</p>
<p style="color: #1f2426;">next（）：修改他的下一个元素</p>
<p style="color: #1f2426;">nextALL()：修改他下边所有元素</p>
<p style="color: #1f2426;">nextUntil（）：修改他下边区间的元素，不包含两边值元素</p>
<p style="color: #1f2426;">prev（）：向上一个元素</p>
<p style="color: #1f2426;">preAll（）：向上所有元素</p>
<p style="color: #1f2426;">preUntil（）：修改他上边区间的元素，不包含两边值元素</p>
<p style="color: #1f2426;"><span style="color: #ff0000;">遍历的过滤：其实这个已经被单拿出来讲过了，可以翻阅上边</span></p>
<p style="color: #1f2426;">first（）：</p>
<p style="color: #1f2426;">last（）：</p>
<p style="color: #1f2426;">eq（）：</p>
<p style="color: #1f2426;">filter（）：看是不是满足标准例如filter（”p“）要包含p元素才能执行，类似于：has</p>
<p style="color: #1f2426;">not（）：和上边相反，是不能包含的，可以在html里指定class，这里让他不包含</p>

<h2 id="J_CodeLang" class="code-head" style="color: #1f2426;" data-lang="Javascript">使用remove()和empty()方法删除元素</h2>
<div id="J_CodeDescr" class="code-description" style="color: #1f2426;">
<div class="code-desc co">

<code class="marker">remove()</code>方法删除所选元素本身和子元素，该方法可以通过添加过滤参数指定需要删除的某些元素，而<code class="marker">empty()</code>方法则只删除所选元素的子元素。

例如，调用<code class="marker">remove()</code>方法删除&lt;span&gt;元素中类别名为“red”的，如下图所示：

<a href="http://img.mukewang.com/52bceff500018e0702910171.jpg"><img src="http://img.mukewang.com/52bceff500018e0702910171.jpg" alt="" /></a>

在浏览器中显示的效果：

<a href="http://img.mukewang.com/52bcf01c00013b5004830297.jpg"><img src="http://img.mukewang.com/52bcf01c00013b5004830297.jpg" alt="" /></a>

从图中可以看出，使用<code class="marker">remove(".red")</code>方法只是把&lt;span&gt;元素中类别名为“red”的这部分元素给删除了。

</div>
</div>
<p style="color: #1f2426;">&lt;body&gt;
&lt;h3&gt;使用empty()方法删除元素&lt;/h3&gt;
&lt;span class="green"&gt;香蕉&lt;/span&gt;
&lt;span class="green"&gt;桃子&lt;/span&gt;
&lt;span class="green"&gt;葡萄&lt;/span&gt;
&lt;span class="green"&gt;荔枝&lt;/span&gt;</p>
<p style="color: #1f2426;">&lt;script type="text/javascript"&gt;
<span style="color: #ff0000;">// $("span").empty()；    括号内什么都不用加，就是删除所有里边的元素就是删除所有的文字</span>
<span style="color: #ff0000;"> $("span").remove("span:contains('香蕉')");   删除掉含香蕉的整段代码，灵活应用</span>
&lt;/script&gt;
&lt;/body&gt;</p>


<hr style="color: #1f2426;" />

<h2 id="J_CodeLang" class="code-head" style="color: #1f2426;" data-lang="Javascript">页面加载时触发ready()事件</h2>
<div id="J_CodeDescr" class="code-description">
<div class="code-desc co">
<p style="color: #1f2426;"><code class="marker">ready()</code>事件类似于<code class="marker">onLoad()</code>事件，但前者只要页面的DOM结构加载后便触发，而后者必须在页面全部元素加载成功才触发，<code class="marker">ready()</code>可以写多个，按顺序执行。此外，下列写法是相等的：</p>
<p style="color: #1f2426;"><span style="color: #0000ff;"><code class="marker"><strong>$(document).ready(function(){})</strong></code><strong>等价于</strong><code class="marker"><strong>$(function(){});</strong></code></span></p>
<p style="color: #1f2426;">例如，当触发页面的<code class="marker">ready()</code>事件时，在&lt;div&gt;元素中显示一句话。如下图所示：</p>
<p style="color: #1f2426;"><a href="http://img.mukewang.com/52d227fa000171db03160136.jpg"><img src="http://img.mukewang.com/52d227fa000171db03160136.jpg" alt="" /></a></p>
<p style="color: #1f2426;">在浏览器中显示的效果：</p>
<p style="color: #1f2426;"><a href="http://img.mukewang.com/52d2281c00017ada04670222.jpg"><img src="http://img.mukewang.com/52d2281c00017ada04670222.jpg" alt="" /></a></p>
<p style="color: #1f2426;">从图中可以看出，当页面的DOM框架完成加载后，便触发<code class="marker">ready()</code>事件，在该事件中，通过id号为“tip”的元素，调用<code class="marker">html()</code>方法在页面中显示一段字符。</p>
<p style="color: #1f2426;"><span style="color: #ff0000;">&lt;script type="text/javascript"&gt;</span>
<span style="color: #ff0000;"> $(document).ready(function(){ </span>
<span style="color: #ff0000;"> $("#btntest").bind("click", function () {         //这里的bind下边课程可能会教到，是一个固定的，作为事件专用词</span>
<span style="color: #ff0000;"> $("#tip").html("我被点击了！");</span>
<span style="color: #ff0000;"> });</span>
<span style="color: #ff0000;"> });</span>
<span style="color: #ff0000;"> &lt;/script&gt;</span></p>

<h2 id="J_CodeLang" class="code-head" style="color: #1f2426;" data-lang="Javascript">使用bind()方法绑定元素的事件</h2>
<div id="J_CodeDescr" class="code-description">
<div class="code-desc co">
<p style="color: #1f2426;"><code class="marker">bind()</code>方法绑定元素的事件非常方便，绑定前，需要知道被绑定的元素名，绑定的事件名称，事件中执行的函数内容就可以，它的绑定格式如下：</p>
<p style="color: #1f2426;"><code class="marker"><strong>$(selector).bind(event,[data] function)</strong></code></p>
<p style="color: #1f2426;">参数event为事件名称，多个事件名称用空格隔开，function为事件执行的函数。</p>
<p style="color: #1f2426;">例如，绑定按钮的单击事件，单击按钮时，该按钮变为不可用。如下图所示：</p>
<p style="color: #1f2426;"><a href="http://img.mukewang.com/52d22aeb0001ee2b04480177.jpg"><img src="http://img.mukewang.com/52d22aeb0001ee2b04480177.jpg" alt="" /></a></p>
<p style="color: #1f2426;">在浏览器中显示的效果：</p>
<p style="color: #1f2426;"><a href="http://img.mukewang.com/52d22b0d0001f03204790244.jpg"><img src="http://img.mukewang.com/52d22b0d0001f03204790244.jpg" alt="" /></a></p>
<p style="color: #1f2426;">可以看出，由于使用<code class="marker">bind()</code>方法，绑定了按钮的单击事件，在该事件中将按钮本身的“disabled”属性值设为“true”，表示不可用，当点击时触该事件。</p>

<h2 id="J_CodeLang" class="code-head" style="color: #1f2426;" data-lang="Javascript">使用hover()方法切换事件</h2>
<div id="J_CodeDescr" class="code-description">
<div class="code-desc co">
<p style="color: #1f2426;"><code class="marker">hover()</code>方法的功能是当鼠标移到所选元素上时，执行方法中的第一个函数，鼠标移出时，执行方法中的第二个函数，实现事件的切实效果，调用格式如下：</p>
<p style="color: #1f2426;"><code class="marker"><strong>$(selector).hover(over</strong><strong>，</strong><strong>out);</strong></code></p>
<p style="color: #1f2426;">over参数为移到所选元素上触发的函数，out参数为移出元素时触发的函数。</p>
<p style="color: #1f2426;">例如，当鼠标移到&lt;div&gt;元素上时，元素中的字体变成金黄色，如下图所示：</p>
<p style="color: #1f2426;"><a href="http://img.mukewang.com/52d22c9900013dbd03190241.jpg"><img src="http://img.mukewang.com/52d22c9900013dbd03190241.jpg" alt="" /></a></p>
<p style="color: #1f2426;">在浏览器中显示的效果：</p>
<p style="color: #1f2426;"><a href="http://img.mukewang.com/52d22cba0001163f04670262.jpg"><img src="http://img.mukewang.com/52d22cba0001163f04670262.jpg" alt="" /></a></p>
<p style="color: #1f2426;">从图中可以看出，使用<code class="marker">hover()</code>方法执行两个函数，当鼠标移在元素上时调用<code class="marker">addClass()</code>方法增加一个样式，移出时，调用<code class="marker">removeClass()</code>方法移除该样式。</p>

<h2 id="J_CodeLang" class="code-head" style="color: #1f2426;" data-lang="Javascript">使用toggle()方法绑定多个函数</h2>
<div id="J_CodeDescr" class="code-description">
<div class="code-desc co">
<p style="color: #1f2426;"><code class="marker">toggle()</code>方法可以在元素的click事件中绑定两个或两个以上的函数，同时，它还可以实现元素的隐藏与显示的切换，绑定多个函数的调用格式如下：</p>
<p style="color: #1f2426;"><code class="marker"><strong>$(selector).toggle(fun1(),fun2(),funN(),...)</strong></code></p>
<p style="color: #1f2426;">其中，fun1，fun2就是多个函数的名称</p>
<p style="color: #1f2426;">例如，使用<code class="marker">toggle()</code>方法，当每次点击&lt;div&gt;元素时，显示不同内容，如下图所示：</p>
<p style="color: #1f2426;"><a href="http://img.mukewang.com/52d22e3a0001c56d02980289.jpg"><img src="http://img.mukewang.com/52d22e3a0001c56d02980289.jpg" alt="" /></a></p>
<p style="color: #1f2426;">在浏览器中显示的效果：</p>
<p style="color: #1f2426;"><a href="http://img.mukewang.com/52d22e570001902a04670335.jpg"><img src="http://img.mukewang.com/52d22e570001902a04670335.jpg" alt="" /></a></p>
<p style="color: #1f2426;">从图中可以看出，每次点击&lt;div&gt;元素时，都依次执行<code class="marker">toggle()</code>方法绑定的函数，当执行到最后一个函数时，再次点击将又返回执行第一个函数。</p>
<p style="color: #1f2426;">注意：toggle()方法支持目前主流稳定的jQuery版本1.8.2，在1.9.0之后的版本是不支持的。</p>

<h2 id="J_CodeLang" class="code-head" style="color: #1f2426;" data-lang="Javascript">使用unbind()方法移除元素绑定的事件</h2>
<div id="J_CodeDescr" class="code-description">
<div class="code-desc co">
<p style="color: #1f2426;"><code class="marker">unbind()</code>方法可以移除元素已绑定的事件，它的调用格式如下：</p>
<p style="color: #1f2426;"><code class="marker"><strong>$(selector).unbind(event,fun)</strong></code></p>
<p style="color: #1f2426;">其中参数event表示需要移除的事件名称，多个事件名用空格隔开，fun参数为事件执行时调用的函数名称。</p>
<p style="color: #1f2426;">例如，点击按钮时，使用<code class="marker">unbind()</code>方法移除&lt;div&gt;元素中已绑定的“dblclick”事件，如下图所示：</p>
<p style="color: #1f2426;"><a href="http://img.mukewang.com/52d22feb0001c9ee04750306.jpg"><img src="http://img.mukewang.com/52d22feb0001c9ee04750306.jpg" alt="" /></a></p>
<p style="color: #1f2426;">在浏览器中显示的效果：</p>
<p style="color: #1f2426;"><a href="http://img.mukewang.com/52d2300c0001ecfe06650362.jpg"><img src="http://img.mukewang.com/52d2300c0001ecfe06650362.jpg" alt="" /></a></p>
<p style="color: #1f2426;">从图中可以看出，当使用<code class="marker">unbind()</code>方法移除已绑定的“dblclick”事件时，再次双击&lt;div&gt;元素，样式和文字都没有任何变化，表明移除事件成功。</p>
<p style="color: #1f2426;">如果没有规定参数，unbind() 方法会删除指定元素的所有事件处理程序</p>
<p style="color: #1f2426;">&lt;script type="text/javascript"&gt;
$(function () {
$("div").bind("click",
function () {
$(this).removeClass("backcolor").addClass("color");
}).bind("dblclick", function () {
$(this).removeClass("color").addClass("backcolor");
})
$("#btntest").bind("click", function () {
<span style="color: #ff0000;">$("div").unbind("click" "dblclick");            //用空格隔开，不是逗号</span>
<span style="color: #ff0000;"> $(this).attr("disabled", "true");                    //我觉得这句话没有用，多此一举，效果一样</span>
});
});
&lt;/script&gt;</p>

<h2 id="J_CodeLang" class="code-head" style="color: #1f2426;" data-lang="Javascript">使用one()方法绑定元素的一次性事件</h2>
<div id="J_CodeDescr" class="code-description">
<div class="code-desc co">
<p style="color: #1f2426;"><code class="marker">one()</code>方法可以绑定元素任何有效的事件，但这种方法绑定的事件只会触发一次，它的调用格式如下：</p>
<p style="color: #1f2426;"><code class="marker"><strong>$(selector).one(event,[data],fun)</strong></code></p>
<p style="color: #1f2426;">参数event为事件名称，data为触发事件时携带的数据，fun为触发该事件时执行的函数。</p>
<p style="color: #1f2426;">例如，使用one方法绑定&lt;div&gt;元素的单击事件，在事件执行的函数中，累计执行的次数，并将该次数显示在页面中，如下图所示：</p>
<p style="color: #1f2426;"><a href="http://img.mukewang.com/52d231bd000192fb04310219.jpg"><img src="http://img.mukewang.com/52d231bd000192fb04310219.jpg" alt="" /></a></p>
<p style="color: #1f2426;">在浏览器中显示的效果：</p>
<p style="color: #1f2426;"><a href="http://img.mukewang.com/52d231dd00011da004890293.jpg"><img src="http://img.mukewang.com/52d231dd00011da004890293.jpg" alt="" /></a></p>
<p style="color: #1f2426;">从图中可以看出，由于使用了<code class="marker">one()</code>方法绑定&lt;div&gt;元素的单击事件，因为事件函数只能执行一次，执行完成后，无论如何单击，都不再触发。</p>

<h2 id="J_CodeLang" class="code-head" style="color: #1f2426;" data-lang="Javascript">调用trigger()方法手动触发指定的事件<span style="color: #ff0000;">(好像就是什么都不动，就已经是触发事件了)</span></h2>
<div id="J_CodeDescr" class="code-description">
<div class="code-desc co">
<p style="color: #1f2426;"><code class="marker">trigger()</code>方法可以直接手动触发元素指定的事件，这些事件可以是元素自带事件，也可以是自定义的事件，总之，该事件必须能执行，它的调用格式为：</p>
<p style="color: #1f2426;"><code class="marker"><strong>$(selector).trigger(event)</strong></code></p>
<p style="color: #1f2426;">其中event参数为需要手动触发的事件名称。</p>
<p style="color: #1f2426;">例如，当页面加载时，手动触发文本输入框的“select”事件，使文本框的默认值处于全部被选中的状态，如下图所示：</p>
<p style="color: #1f2426;"><a href="http://img.mukewang.com/52d233a30001df8204290153.jpg"><img src="http://img.mukewang.com/52d233a30001df8204290153.jpg" alt="" /></a></p>
<p style="color: #1f2426;">在浏览器中显示的效果：</p>
<p style="color: #1f2426;"><a href="http://img.mukewang.com/52d233c50001587304890256.jpg"><img src="http://img.mukewang.com/52d233c50001587304890256.jpg" alt="" /></a></p>
<p style="color: #1f2426;">从图中可以看出，由于文本输入框调用<code class="marker">trigger()</code>方法触发了“select”事件，因此，当页面加载完成后，文本框中的默认值处于全部被选中的状态。</p>

<h2 id="J_CodeLang" class="code-head" style="color: #1f2426;" data-lang="Javascript">文本框的focus和blur事件</h2>
<div id="J_CodeDescr" class="code-description">
<div class="code-desc co">
<p style="color: #1f2426;">focus事件在元素获取焦点时触发，如点击文本框时，触发该事件；而blur事件则在元素丢失焦点时触发，如点击除文本框的任何元素，都会触发该事件。</p>
<p style="color: #1f2426;">例如，在触发文本框的“focus”事件时，&lt;div&gt;元素显示提示内容，如下图所示：</p>
<p style="color: #1f2426;"><a href="http://img.mukewang.com/52d235210001b6f203730194.jpg"><img src="http://img.mukewang.com/52d235210001b6f203730194.jpg" alt="" /></a></p>
<p style="color: #1f2426;">在浏览器中显示的效果：</p>
<p style="color: #1f2426;"><a href="http://img.mukewang.com/52d2353f00013ccf04890294.jpg"><img src="http://img.mukewang.com/52d2353f00013ccf04890294.jpg" alt="" /></a></p>
<p style="color: #1f2426;">从图中可以看出，当点击文本框时，触发文本框的“focus”事件，在该事件中，页面中的&lt;div&gt;元素显示提示信息。</p>

<h2 id="J_CodeLang" class="code-head" style="color: #1f2426;" data-lang="Javascript">下拉列表框的change事件</h2>
<div id="J_CodeDescr" class="code-description">
<div class="code-desc co">
<p style="color: #1f2426;">当一个元素的值发生变化时，将会触发<code class="marker">change</code>事件，例如在选择下拉列表框中的选项时，就会触<code class="marker">change</code>事件。</p>
<p style="color: #1f2426;">例如，当在页面选择下拉列表框中的选项时，将在&lt;div&gt;元素中显示所选择的选项内容，如下图所示：</p>
<p style="color: #1f2426;"><a href="http://img.mukewang.com/52d236cc00019b6d04420272.jpg"><img src="http://img.mukewang.com/52d236cc00019b6d04420272.jpg" alt="" /></a></p>
<p style="color: #1f2426;">在浏览器中显示的效果：</p>
<p style="color: #1f2426;"><a href="http://img.mukewang.com/52d236ea0001022a04890294.jpg"><img src="http://img.mukewang.com/52d236ea0001022a04890294.jpg" alt="" /></a></p>
<p style="color: #1f2426;">从图中可以看出，由于使用<code class="marker">bind()</code>方法绑定了下拉列表的“change”事件，因此，当选择列表中的选项时，在&lt;div&gt;元素中显示所选择的选项内容。</p>


<hr style="color: #1f2426;" />

<h2 id="J_CodeLang" class="code-head" style="color: #1f2426;" data-lang="Javascript">调用show()和hide()方法显示和隐藏元素</h2>
<div id="J_CodeDescr" class="code-description">
<div class="code-desc co">
<p style="color: #1f2426;"><code class="marker">show()</code>和<code class="marker">hide()</code>方法用于显示或隐藏页面中的元素，它的调用格式分别为：</p>
<p style="color: #1f2426;"><code class="marker"><strong>$(selector).hide(speed,[callback])</strong></code><strong>和</strong><code class="marker"><strong>$(selector).show(speed,[callback])</strong></code></p>
<p style="color: #1f2426;">参数speed设置隐藏或显示时的速度值，可为“slow”、“fast”或毫秒数值，可选项参数callback为隐藏或显示动作执行完成后调用的函数名。</p>
<p style="color: #1f2426;">例如，在页面中，通过点击“显示”和“隐藏”两个按钮来控制图片元素的显示或隐藏状态，如下图所示：</p>
<p style="color: #1f2426;"><a href="http://img.mukewang.com/52dc9f250001508d03860257.jpg"><img src="http://img.mukewang.com/52dc9f250001508d03860257.jpg" alt="" /></a></p>
<p style="color: #1f2426;">在浏览器中显示的效果：</p>
<p style="color: #1f2426;"><a href="http://img.mukewang.com/52dc9f450001e4a205620313.jpg"><img src="http://img.mukewang.com/52dc9f450001e4a205620313.jpg" alt="" /></a></p>
<p style="color: #1f2426;">从图中可以看出，点击“显示”按钮时，可以将图片元素显示在页面中，点击“隐藏”按钮时，则将图片元素隐藏起来。</p>
<p style="color: #1f2426;">例题：</p>
<p style="color: #1f2426;"><strong>我来试试，亲自通过点击“标题”显示或隐藏“标题”下的内容</strong></p>
<p style="color: #1f2426;">在下列代码的第25和28行中，调用<code class="marker">show()</code>或<code class="marker">hide()</code>方法显示或隐藏正文。</p>
<p style="color: #1f2426;"><a href="http://img.mukewang.com/52dc9f8300015bc405620313.jpg"><img src="http://img.mukewang.com/52dc9f8300015bc405620313.jpg" alt="" /></a></p>
<p style="color: #1f2426;">&lt;body&gt;
&lt;h3&gt;使用show()和hide()方法显示和隐藏元素&lt;/h3&gt;
&lt;div&gt;
&lt;h4&gt;我喜欢吃的水果&lt;/h4&gt;
&lt;ul&gt;
&lt;li&gt;苹果&lt;/li&gt;
&lt;li&gt;甘桔&lt;/li&gt;
&lt;li&gt;梨&lt;/li&gt;
&lt;/ul&gt;
&lt;input id="hidval" type="hidden" value="0"/&gt;
&lt;/div&gt;
&lt;script type="text/javascript"&gt;
$(function () {
$("h4").bind("click", function () {
if ($("#hidval").val() == 0) {
$("ul").show(1200);
$("#hidval").val(1);   <span style="color: #ff0000;"> //这里的1 和下边val的0其实没有什么意义，完全是为了创造判断条件，0的时候执行什么1的时候执行什么</span>
} else {
$("ul").hide(300)
$("#hidval").val(0);
}
});
});
&lt;/script&gt;
&lt;/body&gt;</p>

<h2 id="J_CodeLang" class="code-head" style="color: #1f2426;" data-lang="Javascript">动画效果的show()和hide()方法</h2>
<div id="J_CodeDescr" class="code-description">
<div class="code-desc co">
<p style="color: #1f2426;">在上一小节中，调用<code class="marker">show()</code>和<code class="marker">hide()</code>方法仅是实现的元素的显示和隐藏功能，如果在这些方法中增加“speed”参数可以实现动画效果的显示与隐藏，同时，如果添加了方法的回调函数，它将在显示或隐藏执行成功后被调用。</p>
<p style="color: #1f2426;">例如，以动画的方式显示或隐藏页面中的图片，同时，当显示或隐藏完成时，对应的按钮状态将变为不可用，如下图所示：</p>
<p style="color: #1f2426;"><a href="http://img.mukewang.com/52dca0cb00012c5604130354.jpg"><img src="http://img.mukewang.com/52dca0cb00012c5604130354.jpg" alt="" /></a></p>
<p style="color: #1f2426;">在浏览器中显示的效果：</p>
<p style="color: #1f2426;"><a href="http://img.mukewang.com/52dca1180001468205960341.jpg"><img src="http://img.mukewang.com/52dca1180001468205960341.jpg" alt="" /></a></p>
<p style="color: #1f2426;">从图中可以看出，当以动画方式显示或隐藏图片时，图片在显示或隐藏过程中，则以动画效果按“speed”参数设置数字执行，完成后，调用回调函数中的代码。</p>
<p style="color: #1f2426;">上边那个例子也可以改为下边这个：</p>
<p style="color: #1f2426;">&lt;script type="text/javascript"&gt;
$(function () {
$("h4").bind("click", function () {
if ($("#hidval").val() == 0) {
$("ul").show(600,function(){
$("#hidval").val(1);
})
} else {$("ul").hide(600,function(){
$("#hidval").val(0);
})
}
})
});
&lt;/script&gt;</p>

<h2 id="J_CodeLang" class="code-head" style="color: #1f2426;" data-lang="Javascript">调用toggle()方法实现动画切换效果</h2>
<div id="J_CodeDescr" class="code-description">
<div class="code-desc co">
<p style="color: #1f2426;">第一节我们学过实现元素的显示与隐藏需要使用<code class="marker">hide()</code>与<code class="marker">show()</code>，那么有没有更简便的方法来实现同样的动画效果呢？</p>
<p style="color: #1f2426;">调用<code class="marker">toggle()</code>方法就可以很容易做到，即如果元素处于显示状态，调用该方法则隐藏该元素，反之，则显示该元素，它的调用格式是：</p>
<p style="color: #1f2426;"><code class="marker"><strong>$(selector).toggle(speed,[callback])</strong></code></p>
<p style="color: #1f2426;">其中speed参数为动画效果时的速度值，可以为数字，单位为毫秒，也可是“fast”、“slow”字符，可选项参数callback为方法执行成功后回调的函数名称。</p>
<p style="color: #1f2426;">例如，调用<code class="marker">toggle()</code>方法以动画的效果显示和隐藏图片元素，如下图所示：</p>
<p style="color: #1f2426;"><a href="http://img.mukewang.com/52dca25300010e0405830241.jpg"><img src="http://img.mukewang.com/52dca25300010e0405830241.jpg" alt="" /></a></p>
<p style="color: #1f2426;">在浏览器中显示的效果：</p>
<p style="color: #1f2426;"><a href="http://img.mukewang.com/52dca2730001372d06240327.jpg"><img src="http://img.mukewang.com/52dca2730001372d06240327.jpg" alt="" /></a></p>
<p style="color: #1f2426;">从图中可以看出，当按钮显示内容为“隐藏”时，点击该按钮，将调用<code class="marker">toggle()</code>方法以动画的方式隐藏图片元素，隐藏成功后，按钮显示的内容变为“显示”。</p>

<h2 id="J_CodeLang" class="code-head" style="color: #1f2426;" data-lang="Javascript">使用slideUp()和slideDown()方法的滑动效果</h2>
<div id="J_CodeDescr" class="code-description">
<div class="code-desc co">
<p style="color: #1f2426;">可以使用<code class="marker">slideUp()</code>和<code class="marker">slideDown()</code>方法在页面中滑动元素，前者用于向上滑动元素，后者用于向下滑动元素，它们的调用方法分别为：</p>
<p style="color: #1f2426;"><code class="marker"><strong>$(selector).slideUp(speed,[callback])</strong></code><strong>和</strong><code class="marker"><strong>$(selector).slideDown(speed,[callback])</strong></code></p>
<p style="color: #1f2426;">其中speed参数为滑动时的速度，单位是毫秒，可选项参数callback为滑动成功后执行的回调函数名。</p>
<p style="color: #1f2426;"><strong>要注意的是：</strong><code class="marker">slideDown()</code>仅适用于<strong>被隐藏的元素；</strong><code class="marker">slideup()</code>则<strong>相反。</strong></p>
<p style="color: #1f2426;">例如，调用<code class="marker">slideUp()</code>和<code class="marker">slideDown()</code>方法实现页面中元素的向上和向下的滑动效果，如下图所示：</p>
<p style="color: #1f2426;"><a href="http://img.mukewang.com/52dcb1b20001c7d403880386.jpg"><img src="http://img.mukewang.com/52dcb1b20001c7d403880386.jpg" alt="" /></a></p>
<p style="color: #1f2426;">在浏览器中显示的效果：</p>
<p style="color: #1f2426;"><a href="http://img.mukewang.com/5366e34c0001eab206860385.jpg"><img src="http://img.mukewang.com/5366e34c0001eab206860385.jpg" alt="" /></a></p>
<p style="color: #1f2426;">从图中可以看出，根据按钮中显示的内容，分别调用<code class="marker">slideUp()</code>和<code class="marker">slideDown()</code>方法，实现图片元素向上和向下的滑动效果，当每个滑动效果完成时，再通过回调函数改变按钮中显示内容。</p>
<p style="color: #1f2426;">滑动与淡入淡出的区别：滑动改变元素的高度，淡入淡出改变元素的透明度。</p>

<h2 id="J_CodeLang" class="code-head" style="color: #1f2426;" data-lang="Javascript">使用slideToggle()方法实现图片“变脸”效果</h2>
<h2 class="code-head" style="color: #1f2426;" data-lang="Javascript">（<span style="color: #ff0000;">区别就是这个不用判断初始状态，而且可以实现上下移动和隐藏出现同时进行</span>）</h2>
<div id="J_CodeDescr" class="code-description">
<div class="code-desc co">
<p style="color: #1f2426;">使用<code class="marker">slideToggle()</code>方法可以切换<code class="marker">slideUp()</code>和<code class="marker">slideDown()</code>，即调用该方法时，如果元素已向上滑动，则元素自动向下滑动，反之，则元素自动向上滑动，格式为：</p>
<p style="color: #1f2426;"><code class="marker"><strong>$(selector).slideToggle(speed,[callback])</strong></code></p>
<p style="color: #1f2426;">其中speed参数为动画效果时的速度值，可以为数字，单位为毫秒，也可是“fast”、“slow”字符，可选项参数callback为方法执行成功后回调的函数名称。</p>
<p style="color: #1f2426;">例如，在页面中，使用<code class="marker">slideToggle()</code>方法实现图片“变脸”效果，如下图所示：</p>
<p style="color: #1f2426;"><a href="http://img.mukewang.com/52dcb5930001bd2603830402.jpg"><img src="http://img.mukewang.com/52dcb5930001bd2603830402.jpg" alt="" /></a></p>
<p style="color: #1f2426;">在浏览器中显示的效果：</p>
<p style="color: #1f2426;"><a href="http://img.mukewang.com/52dcb5b40001da9d05510364.jpg"><img src="http://img.mukewang.com/52dcb5b40001da9d05510364.jpg" alt="" /></a></p>
<p style="color: #1f2426;">从图中可以看出，当点击第一张图片时，向上滑动收起该图片，当收起完成时，触发回调函数，调用第二张图片的<code class="marker">slideToggle()</code>方法，向下滑动显示第二张图片。</p>
<p style="color: #1f2426;"><span style="color: #ff0000;">$spn.html() == "向下滑" ? $spn.html("向上滑") : $spn.html("向下滑");</span></p>

<h2 id="J_CodeLang" class="code-head" style="color: #1f2426;" data-lang="Javascript">使用fadeIn()与fadeOut()方法实现淡入淡出效果</h2>
<div id="J_CodeDescr" class="code-description">
<div class="code-desc co">
<p style="color: #1f2426;"><code class="marker">fadeIn()</code>和<code class="marker">fadeOut()</code>方法可以实现元素的淡入淡出效果，前者淡入隐藏的元素，后者可以淡出可见的元素，它们的调用格式分别为：</p>
<p style="color: #1f2426;"><code class="marker"><strong>$(selector).fadeIn(speed,[callback])</strong></code><strong>和</strong><code class="marker"><strong>$(selector).fadeOut(speed,[callback])</strong></code></p>
<p style="color: #1f2426;">其中参数speed为淡入淡出的速度，callback参数为完成后执行的回调函数名。</p>
<p style="color: #1f2426;">例如，分别在页面中以淡入淡出的动画效果显示图片元素，如下图所示：</p>
<p style="color: #1f2426;"><a href="http://img.mukewang.com/549a7819000117a103910414.jpg"><img src="http://img.mukewang.com/549a7819000117a103910414.jpg" alt="" width="353" height="375" /></a></p>
<p style="color: #1f2426;">在浏览器中显示的效果：</p>
<p style="color: #1f2426;"><a href="http://img.mukewang.com/549a782d0001eea505410456.jpg"><img src="http://img.mukewang.com/549a782d0001eea505410456.jpg" alt="" width="358" height="301" /></a></p>
<p style="color: #1f2426;">从图中可以看出，当点击“淡出”按钮时，调用<code class="marker">fadeOut()</code>方法以淡出效果隐藏图片，当点击“淡入”按钮时，调用<code class="marker">fadeIn()</code>方法以淡入效果显示图片。</p>

<h2 id="J_CodeLang" class="code-head" style="color: #1f2426;" data-lang="Javascript">使用fadeTo()方法设置淡入淡出效果的不透明度</h2>
<div id="J_CodeDescr" class="code-description">
<div class="code-desc co">
<p style="color: #1f2426;">调用<code class="marker">fadeTo()</code>方法，可以将所选择元素的不透明度以淡入淡出的效果调整为指定的值，该方法的调用格式为：</p>
<p style="color: #1f2426;"><code class="marker"><strong>$(selector).fadeTo(speed,opacity,[callback])</strong></code></p>
<p style="color: #1f2426;">其中speed参数为效果的速度，opacity参数为指定的不透明值，它的取值范围是0.0~1.0，可选项参数callback为效果完成后，回调的函数名。</p>
<p style="color: #1f2426;">例如，分别调用<code class="marker">fadeTo()</code>方法，设置三个图片元素的不透明度值，如下图所示：</p>
<p style="color: #1f2426;"><a href="http://img.mukewang.com/52dcc1f20001235d03890370.jpg"><img src="http://img.mukewang.com/52dcc1f20001235d03890370.jpg" alt="" /></a></p>
<p style="color: #1f2426;">在浏览器中显示的效果：</p>
<p style="color: #1f2426;"><a href="http://img.mukewang.com/52dcc22a000195fb05070349.jpg"><img src="http://img.mukewang.com/52dcc22a000195fb05070349.jpg" alt="" /></a></p>
<p style="color: #1f2426;">从图中可以看出，调用<code class="marker">fadeTo()</code>方法，分别改变“opacity”参数的值，以淡入淡出的动画效果设置图片元素的不透明度。</p>

<h2 id="J_CodeLang" class="code-head" style="color: #1f2426;" data-lang="Javascript">调用animate()方法制作简单的动画效果</h2>
<div id="J_CodeDescr" class="code-description">
<div class="code-desc co">
<p style="color: #1f2426;">调用<code class="marker">animate()</code>方法可以创建自定义动画效果，它的调用格式为：</p>
<p style="color: #1f2426;"><code class="marker"><strong>$(selector).animate({params},speed,[callback])</strong></code></p>
<p style="color: #1f2426;">其中，params参数为制作动画效果的CSS属性名与值，speed参数为动画的效果的速度，单位为毫秒，可选项callback参数为动画完成时执行的回调函数名。</p>
<p style="color: #1f2426;">例如，调用<code class="marker">animate()</code>方法以由小到大的动画效果显示图片，如下图所示：</p>
<p style="color: #1f2426;"><a href="http://img.mukewang.com/52dcc3b30001fd5803210256.jpg"><img src="http://img.mukewang.com/52dcc3b30001fd5803210256.jpg" alt="" /></a></p>
<p style="color: #1f2426;">在浏览器中显示的效果：</p>
<p style="color: #1f2426;"><a href="http://img.mukewang.com/52dcc3ce0001af6604460337.jpg"><img src="http://img.mukewang.com/52dcc3ce0001af6604460337.jpg" alt="" /></a></p>
<p style="color: #1f2426;">从图中可以看出，调用<code class="marker">animate()</code>方法，以渐渐放大的动画效果显示图片元素，当动画执行完成后，通过回调函数在页面的&lt;div&gt;元素中显示“执行完成!”的字样。</p>

<h2 id="J_CodeLang" class="code-head" style="color: #1f2426;" data-lang="Javascript">调用animate()方法制作移动位置的动画</h2>
<div id="J_CodeDescr" class="code-description">
<div class="code-desc co">
<p style="color: #1f2426;">调用<code class="marker">animate()</code>方法不仅可以制作简单渐渐变大的动画效果，而且还能制作移动位置的动画，在移动位置之前，必须将被移元素的“position”属性值设为“absolute”或“relative”，否则，该元素移动不了。</p>
<p style="color: #1f2426;">例如，调用<code class="marker">animate()</code>方法先将图片向右移动90px，然后，再将图片宽度与高度分别增加30px，如下图所示：</p>
<p style="color: #1f2426;"><a href="http://img.mukewang.com/52dcc4eb0001c08e03410291.jpg"><img src="http://img.mukewang.com/52dcc4eb0001c08e03410291.jpg" alt="" /></a></p>
<p style="color: #1f2426;">在浏览器中显示的效果：</p>
<p style="color: #1f2426;"><a href="http://img.mukewang.com/52dcc50b0001ba2205060337.jpg"><img src="http://img.mukewang.com/52dcc50b0001ba2205060337.jpg" alt="" /></a></p>
<p style="color: #1f2426;">从图中可以看出，图片先向右移动了“90px”，然后，移动成功后，再在原来的基础之上以动画的效果增大30px，增加成功后，显示“执行完成！”的字样。</p>

<h2 id="J_CodeLang" class="code-head" style="color: #1f2426;" data-lang="Javascript">调用stop()方法停止当前所有动画效果</h2>
<div id="J_CodeDescr" class="code-description">
<div class="code-desc co">
<p style="color: #1f2426;"><code class="marker">stop()</code>方法的功能是在动画完成之前，停止当前正在执行的动画效果，这些效果包括滑动、淡入淡出和自定义的动画，它的调用格式为：</p>
<p style="color: #1f2426;"><code class="marker"><strong>$(selector).stop([clearQueue],[goToEnd])</strong></code></p>
<p style="color: #1f2426;">其中，两个可选项参数clearQueue和goToEnd都是布尔类型值，前者表示是否停止正在执行的动画，后者表示是否完成正在执行的动画，默认为false。</p>
<p style="color: #1f2426;">例如，在页面中，当图片元素正在执行动画效果时，点击“停止”按钮，中止正在执行的动画效果，如下图所示：</p>
<p style="color: #1f2426;"><a href="http://img.mukewang.com/52dcc63f00019e3203870387.jpg"><img src="http://img.mukewang.com/52dcc63f00019e3203870387.jpg" alt="" /></a></p>
<p style="color: #1f2426;">在浏览器中显示的效果：</p>
<p style="color: #1f2426;"><a href="http://img.mukewang.com/52dcc65f0001ef9605300345.jpg"><img src="http://img.mukewang.com/52dcc65f0001ef9605300345.jpg" alt="" /></a></p>
<p style="color: #1f2426;">从图中可以看出，当页面中的图片正在执行动画效果向右移动时，由于点击了“停止”按钮，执行了图片元素的stop方法，因此，中止了正在执行的动画效果。</p>

<h2 id="J_CodeLang" class="code-head" style="color: #1f2426;" data-lang="Javascript">调用delay()方法延时执行动画效果</h2>
<div id="J_CodeDescr" class="code-description">
<div class="code-desc co">
<p style="color: #1f2426;"><code class="marker">delay()</code>方法的功能是设置一个延时值来推迟动画效果的执行，它的调用格式为：</p>
<p style="color: #1f2426;"><code class="marker"><strong>$(selector).delay(duration)</strong></code></p>
<p style="color: #1f2426;">其中参数duration为延时值，它的单位是毫秒，当超过延时值时，动画继续执行。</p>
<p style="color: #1f2426;">例如，当页面中图片动画正在执行时，点击“延时”按钮调用<code class="marker">delay()</code>方法推迟2000毫秒后继续执行，如下图所示：</p>
<p style="color: #1f2426;"><a href="http://img.mukewang.com/52dcc785000162dc03840385.jpg"><img src="http://img.mukewang.com/52dcc785000162dc03840385.jpg" alt="" /></a></p>
<p style="color: #1f2426;">在浏览器中显示的效果：</p>
<p style="color: #1f2426;"><a href="http://img.mukewang.com/52dcc7a100014fb806800406.jpg"><img src="http://img.mukewang.com/52dcc7a100014fb806800406.jpg" alt="" /></a></p>
<p style="color: #1f2426;">从图中可以看出，当图片动画正在执行时，点击“延时”按钮，调用<code class="marker">delay()</code>方法中止当前正在执行的图片动画效果，当超过设置的延时值时，动画效果继续执行。</p>


<hr style="color: #1f2426;" />

<h2 id="J_CodeLang" class="code-head" style="color: #1f2426;" data-lang="Javascript">使用load()方法异步请求数据</h2>
<div id="J_CodeDescr" class="code-description">
<div class="code-desc co">
<p style="color: #1f2426;">使用<code class="marker">load()</code>方法通过Ajax请求加载服务器中的数据，并把返回的数据放置到指定的元素中，它的调用格式为：</p>
<p style="color: #1f2426;"><code class="marker"><strong>load(url,[data],[callback])</strong></code></p>
<p style="color: #1f2426;">参数url为加载服务器地址，可选项data参数为请求时发送的数据，callback参数为数据请求成功后，执行的回调函数。</p>
<p style="color: #1f2426;">例如，点击“加载”按钮时，向服务器请求加载一个指定页面的内容，加载成功后，将数据内容显示在&lt;div&gt;元素中，并将加载按钮变为不可用。如下图所示：</p>
<p style="color: #1f2426;"><a href="http://img.mukewang.com/52dccb920001d2d505970337.jpg"><img src="http://img.mukewang.com/52dccb920001d2d505970337.jpg" alt="" /></a></p>
<p style="color: #1f2426;">在浏览器中显示的效果：</p>
<p style="color: #1f2426;"><a href="http://img.mukewang.com/52dccbaf0001c21507380393.jpg"><img src="http://img.mukewang.com/52dccbaf0001c21507380393.jpg" alt="" /></a></p>
<p style="color: #1f2426;">从图中可以看出，当点击“加载”按钮时，通过调用<code class="marker">load()</code>方法向服务器请求加载fruit.html文件中的内容，当加载成功后，先显示数据，并将按钮变为不可用。</p>

<h2 id="J_CodeLang" class="code-head" style="color: #1f2426;" data-lang="Javascript">使用getJSON()方法异步加载JSON格式数据</h2>
<div id="J_CodeDescr" class="code-description">
<div class="code-desc co">
<p style="color: #1f2426;">使用<code class="marker">getJSON()</code>方法可以通过Ajax异步请求的方式，获取服务器中的数组，并对获取的数据进行解析，显示在页面中，它的调用格式为：</p>
<p style="color: #1f2426;"><code class="marker"><strong>jQuery.getJSON(url,[data],[callback])</strong></code><strong>或</strong><code class="marker"><strong>$.getJSON(url,[data],[callback])</strong></code></p>
<p style="color: #1f2426;">其中，url参数为请求加载json格式文件的服务器地址，可选项data参数为请求时发送的数据，callback参数为数据请求成功后，执行的回调函数。</p>
<p style="color: #1f2426;">例如，点击页面中的“加载”按钮，调用<code class="marker">getJSON()</code>方法获取服务器中JSON格式文件中的数据，并遍历数据，将指定的字段名内容显示在页面中。如下图所示：</p>
<p style="color: #1f2426;"><a href="http://img.mukewang.com/52dcced70001f67806010370.jpg"><img src="http://img.mukewang.com/52dcced70001f67806010370.jpg" alt="" /></a></p>
<p style="color: #1f2426;">在浏览器中显示的效果：</p>
<p style="color: #1f2426;"><a href="http://img.mukewang.com/52dccefe0001c87005860341.jpg"><img src="http://img.mukewang.com/52dccefe0001c87005860341.jpg" alt="" /></a></p>
<p style="color: #1f2426;">从图中可以看出，当点击“加载”按钮时，通过<code class="marker">getJSON()</code>方法调用服务器中的sport.json文件，获取返回的data文件数据，并遍历该数据对象，以<code class="marker">data[“name”]</code>取出数据中指定的内容，显示在页面中。</p>
<p style="color: #1f2426;">例子：</p>
<p style="color: #1f2426;">（$function(){}）</p>

<h2 id="J_CodeLang" class="code-head" style="color: #1f2426;" data-lang="Javascript">使用getScript()方法异步加载并执行js文件</h2>
<div id="J_CodeDescr" class="code-description">
<div class="code-desc co">
<p style="color: #1f2426;">使用<code class="marker">getScript()</code>方法异步请求并执行服务器中的JavaScript格式的文件，它的调用格式如下所示：</p>
<p style="color: #1f2426;"><code class="marker">jQuery.getScript(url,[callback])</code>或<code class="marker">$.getScript(url,[callback])</code></p>
<p style="color: #1f2426;">参数url为服务器请求地址，可选项callback参数为请求成功后执行的回调函数。</p>
<p style="color: #1f2426;">例如，点击“加载”按钮，调用<code class="marker">getScript()</code>加载并执行服务器中指定名称的JavaScript格式的文件，并在页面中显示加载后的数据内容，如下图所示：</p>
<p style="color: #1f2426;"><a href="http://img.mukewang.com/52dcd433000151e606000305.jpg"><img src="http://img.mukewang.com/52dcd433000151e606000305.jpg" alt="" /></a></p>
<p style="color: #1f2426;">在浏览器中显示的效果：</p>
<p style="color: #1f2426;"><a href="http://img.mukewang.com/52dcd44e000145de06380392.jpg"><img src="http://img.mukewang.com/52dcd44e000145de06380392.jpg" alt="" /></a></p>
<p style="color: #1f2426;">从图中可以看出，当点击“加载”按钮调用<code class="marker">getScript()</code>方法加载服务器中的JavaScript格式文件后，自动执行文件代码，将数据内容显示在&lt;ul&gt;元素中。</p>

<h2 id="J_CodeLang" class="code-head" style="color: #1f2426;" data-lang="Javascript">使用get()方法以GET方式从服务器获取数据</h2>
<div id="J_CodeDescr" class="code-description">
<div class="code-desc co">
<p style="color: #1f2426;">使用<code class="marker">get()</code>方法时，采用GET方式向服务器请求数据，并通过方法中回调函数的参数返回请求的数据，它的调用格式如下：</p>
<p style="color: #1f2426;"><code class="marker">$.get(url,[callback])</code></p>
<p style="color: #1f2426;">参数url为服务器请求地址，可选项callback参数为请求成功后执行的回调函数。</p>
<p style="color: #1f2426;">例如，当点击“加载”按钮时，调用<code class="marker">get()</code>方法向服务器中的一个.php文件以GET方式请求数据，并将返回的数据内容显示在页面中，如下图所示：</p>
<p style="color: #1f2426;"><a href="http://img.mukewang.com/52dcd5b1000161ce05970338.jpg"><img src="http://img.mukewang.com/52dcd5b1000161ce05970338.jpg" alt="" /></a></p>
<p style="color: #1f2426;">在浏览器中显示的效果：</p>
<p style="color: #1f2426;"><a href="http://img.mukewang.com/52dcd5d900010aaf06440326.jpg"><img src="http://img.mukewang.com/52dcd5d900010aaf06440326.jpg" alt="" /></a></p>
<p style="color: #1f2426;">从图中可以看出，通过<code class="marker">$.get()</code>方法向服务器成功请求数据后，在回调函数中通过data参数传回请求的数据，并以data.name格式访问数据中各项的内容。</p>
<p style="color: #1f2426;"><span style="color: #ff0000;">例子：<span style="color: #0000ff;">post其实一模一样，就是把get改成post</span></span></p>
<p style="color: #1f2426;"><span style="color: #ff0000;">$(function(){</span></p>
<p style="color: #1f2426;"><span style="color: #ff0000;">$("#btn").on("click",function(){</span></p>
<p style="color: #1f2426;"><span style="color: #ff0000;">$.get("server.php",{name:$(#namevalue).val()},function(data){</span></p>
<p style="color: #1f2426;"><span style="color: #ff0000;">$("#result").text(data);  最后一个是设置他的返回参数，让显示出来前边的结果，</span></p>
<p style="color: #1f2426;"><span style="color: #ff0000;">就是先读取后显示</span></p>
<p style="color: #1f2426;"><span style="color: #ff0000;">})；</span></p>
<p style="color: #1f2426;"><span style="color: #ff0000;">});</span></p>
<p style="color: #1f2426;"><span style="color: #ff0000;">})；</span></p>
<p style="color: #1f2426;">如果出现错误了的话应该：</p>
<p style="color: #1f2426;"><span style="color: #ff0000;">$(function(){</span></p>
<p style="color: #1f2426;"><span style="color: #ff0000;">$("#btn").on("click",function(){</span></p>
<p style="color: #1f2426;"><span style="color: #ff0000;">$.get("server.php",{name:$(#namevalue).val()},function(data){</span></p>
<p style="color: #1f2426;"><span style="color: #ff0000;">$("#result").text(data);  </span></p>
<p style="color: #1f2426;"><span style="color: #ff0000;">})；</span></p>
<p style="color: #1f2426;">.error(function(){</p>
<p style="color: #1f2426;">$("#result").text("通讯有问题")</p>
<p style="color: #1f2426;">})</p>
<p style="color: #1f2426;"><span style="color: #ff0000;">});</span></p>
<p style="color: #1f2426;"><span style="color: #ff0000;">})；</span></p>
<p style="color: #1f2426;">因为有时候网络不好，显示慢，但是要提示已经正在操作了，应该像下边这样</p>
<p style="color: #1f2426;"><span style="color: #000000;">$(function(){</span></p>
<p style="color: #1f2426;"><span style="color: #000000;">$("#btn").on("click",function(){</span></p>
<p style="color: #1f2426;"><span style="color: #ff0000;">$("#result").text("请求数据中请稍后")     </span></p>
<p style="color: #1f2426;"><span style="color: #000000;">$.get("server.php",{name:$(#namevalue).val()},function(data){</span></p>
<p style="color: #1f2426;"><span style="color: #000000;">$("#result").text(data);  </span></p>
<p style="color: #1f2426;"><span style="color: #000000;">})；</span></p>
<p style="color: #1f2426;"><span style="color: #000000;">.error(function(){</span></p>
<p style="color: #1f2426;"><span style="color: #000000;">$("#result").text("通讯有问题")</span></p>
<p style="color: #1f2426;"><span style="color: #000000;">})</span></p>
<p style="color: #1f2426;"><span style="color: #000000;">});</span></p>
<p style="color: #1f2426;"><span style="color: #000000;">});</span></p>
<p style="color: #1f2426;"><span style="color: #ff0000;">下边是Ajax加载片段（一般用.load,他是加载一个html）</span></p>
<p style="color: #1f2426;">($function(){</p>
<p style="color: #1f2426;">$("body").text("wait.......");</p>
<p style="color: #1f2426;">$("body").load("box.htm",function(a,status,c){</p>
<p style="color: #1f2426;">console.log(status);</p>
<p style="color: #1f2426;">if(status=="error"){</p>
<p style="color: #1f2426;">$("body").text("判断碎片加载失败")；</p>
<p style="color: #1f2426;">}</p>
<p style="color: #1f2426;">})</p>
<p style="color: #1f2426;">$.getScript("HelloJS.js").complete（function（）{   （<span style="color: #ff0000;">这里也是加载碎片，但是他是js，所以用getScript，并且连着complete回掉，来执行HelloJs.JS内文件</span>）</p>
<p style="color: #1f2426;">sayHello（）；</p>
<p style="color: #1f2426;">}）</p>
<p style="color: #1f2426;">})</p>

<h2 id="J_CodeLang" class="code-head" style="color: #1f2426;" data-lang="Javascript">使用post()方法以POST方式从服务器发送数据</h2>
<div id="J_CodeDescr" class="code-description">
<div class="code-desc co">
<p style="color: #1f2426;">与<code class="marker">get()</code>方法相比，<code class="marker">post()</code>方法多用于以POST方式向服务器发送数据，服务器接收到数据之后，进行处理，并将处理结果返回页面，调用格式如下：</p>
<p style="color: #1f2426;"><code class="marker">$.post(url,[data],[callback])</code></p>
<p style="color: #1f2426;">参数url为服务器请求地址，可选项data为向服务器请求时发送的数据，可选项callback参数为请求成功后执行的回调函数。</p>
<p style="color: #1f2426;">例如，在输入框中录入一个数字，点击“检测”按钮，调用<code class="marker">post()</code>方法向服务器以POST方式发送请求，检测输入值的奇偶性，并显示在页面中，如下图所示：</p>
<p style="color: #1f2426;"><a href="http://img.mukewang.com/52dcd7430001e25004690464.jpg"><img src="http://img.mukewang.com/52dcd7430001e25004690464.jpg" alt="" /></a></p>
<p style="color: #1f2426;">在浏览器中显示的效果：</p>
<p style="color: #1f2426;"><a href="http://img.mukewang.com/52dcd77200010b4c05450336.jpg"><img src="http://img.mukewang.com/52dcd77200010b4c05450336.jpg" alt="" /></a></p>
<p style="color: #1f2426;">从图中可以看出，当点击“检测”按钮时，获取输入框中的值，并将该值使用<code class="marker">$.post()</code>方法一起发送给服务器，服务器接收该值后并进行处理，最后返回处理结果。</p>

<h2 id="J_CodeLang" class="code-head" style="color: #1f2426;" data-lang="Javascript">使用serialize()方法序列化表单元素值</h2>
<div id="J_CodeDescr" class="code-description">
<div class="code-desc co">
<p style="color: #1f2426;">使用<code class="marker">serialize()</code>方法可以将表单中有name属性的元素值进行序列化，生成标准URL编码文本字符串，直接可用于ajax请求，它的调用格式如下：</p>
<p style="color: #1f2426;"><code class="marker"><strong>$(selector).serialize()</strong></code></p>
<p style="color: #1f2426;">其中selector参数是一个或多个表单中的元素或表单元素本身。</p>
<p style="color: #1f2426;">例如，在表单中添加多个元素，点击“序列化”按钮后，调用<code class="marker">serialize()</code>方法，将表单元素序列化后的标准URL编码文本字符串显示在页面中，如下图所示：</p>
<p style="color: #1f2426;"><a href="http://img.mukewang.com/52dcd9470001b1e705400481.jpg"><img src="http://img.mukewang.com/52dcd9470001b1e705400481.jpg" alt="" /></a></p>
<p style="color: #1f2426;">在浏览器中显示的效果：</p>
<p style="color: #1f2426;"><a href="http://img.mukewang.com/52dcd9660001637f05610308.jpg"><img src="http://img.mukewang.com/52dcd9660001637f05610308.jpg" alt="" /></a></p>
<p style="color: #1f2426;">从图中可以看出，当点击“序列化”按钮后，调用表单元素本身的<code class="marker">serialize()</code>方法，将表单中元素全部序列化，生成标准URL编码，各元素间通过&amp;号相联。</p>

<h2 id="J_CodeLang" class="code-head" style="color: #1f2426;" data-lang="Javascript">使用ajax()方法加载服务器数据</h2>
<div id="J_CodeDescr" class="code-description">
<div class="code-desc co">
<p style="color: #1f2426;">使用<code class="marker">ajax()</code>方法是最底层、功能最强大的请求服务器数据的方法，它不仅可以获取服务器返回的数据，还能向服务器发送请求并传递数值，它的调用格式如下：</p>
<p style="color: #1f2426;"><code class="marker"><strong>jQuery.ajax([settings])</strong></code><strong>或</strong><code class="marker"><strong>$.ajax([settings])</strong></code></p>
<p style="color: #1f2426;">其中参数settings为发送ajax请求时的配置对象，在该对象中，url表示服务器请求的路径，data为请求时传递的数据，dataType为服务器返回的数据类型，success为请求成功的执行的回调函数，type为发送数据请求的方式，默认为get。</p>
<p style="color: #1f2426;">例如，点击页面中的“加载”按钮，调用<code class="marker">ajax()</code>方法向服务器请求加载一个txt文件，并将返回的文件中的内容显示在页面，如下图所示：</p>
<p style="color: #1f2426;"><a href="http://img.mukewang.com/52dcdb5000014e9804600419.jpg"><img src="http://img.mukewang.com/52dcdb5000014e9804600419.jpg" alt="" /></a></p>
<p style="color: #1f2426;">在浏览器中显示的效果：</p>
<p style="color: #1f2426;"><a href="http://img.mukewang.com/52dcdb6b00010eea05990345.jpg"><img src="http://img.mukewang.com/52dcdb6b00010eea05990345.jpg" alt="" /></a></p>
<p style="color: #1f2426;">从图中可以看出，当点击“加载”按钮时，调用<code class="marker">$.ajax()</code>方法请求服务器中txt文件，当请求成功时调用success回调函数，获取传回的数据，并显示在页面中。</p>

<h2 id="J_CodeLang" class="code-head" style="color: #1f2426;" data-lang="Javascript">使用ajaxSetup()方法设置全局Ajax默认选项</h2>
<div id="J_CodeDescr" class="code-description">
<div class="code-desc co">
<p style="color: #1f2426;">使用<code class="marker">ajaxSetup()</code>方法可以设置Ajax请求的一些全局性选项值，设置完成后，后面的Ajax请求将不需要再添加这些选项值，它的调用格式为：</p>
<p style="color: #1f2426;"><code class="marker"><strong>jQuery.ajaxSetup([options])</strong></code><strong>或</strong><code class="marker"><strong>$.ajaxSetup([options])</strong></code></p>
<p style="color: #1f2426;">可选项options参数为一个对象，通过该对象设置Ajax请求时的全局选项值。</p>
<p style="color: #1f2426;">例如，先调用<code class="marker">ajaxSetup()</code>方法设置全局的Ajax选项值，再点击两个按钮，分别使用<code class="marker">ajax()</code>方法请求不同的服务器数据，并将数据内容显示在页面，如下图所示：</p>
<p style="color: #1f2426;"><a href="http://img.mukewang.com/52dcdce60001de2604780449.jpg"><img src="http://img.mukewang.com/52dcdce60001de2604780449.jpg" alt="" /></a></p>
<p style="color: #1f2426;">在浏览器中显示的效果：</p>
<p style="color: #1f2426;"><a href="http://img.mukewang.com/52dcdd090001ccfd06390382.jpg"><img src="http://img.mukewang.com/52dcdd090001ccfd06390382.jpg" alt="" /></a></p>
<p style="color: #1f2426;">从图中可以看出，使用<code class="marker">ajaxSetup()</code>方法设置了Ajax请求时的一些全局性的配置选项后，在两次调用ajax请求服务器txt文件时，只需要设置url地址即可。</p>

<h2 id="J_CodeLang" class="code-head" style="color: #1f2426;" data-lang="Javascript">使用ajaxStart()和ajaxStop()方法</h2>
<div id="J_CodeDescr" class="code-description">
<div class="code-desc co">
<p style="color: #1f2426;"><code class="marker">ajaxStart()</code>和<code class="marker">ajaxStop()</code>方法是绑定Ajax事件。ajaxStart()方法用于在Ajax请求发出前触发函数，ajaxStop()方法用于在Ajax请求完成后触发函数。它们的调用格式为：</p>
<p style="color: #1f2426;"><code class="marker"><strong>$(selector).ajaxStart(function())</strong></code><strong>和</strong><code class="marker"><strong>$(selector).ajaxStop(function())</strong></code></p>
<p style="color: #1f2426;">其中，两个方法中括号都是绑定的函数，当发送Ajax请求前执行<code class="marker">ajaxStart()</code>方法绑定的函数，请求成功后，执行ajaxStop ()方法绑定的函数。</p>
<p style="color: #1f2426;">例如，在调用<code class="marker">ajax()</code>方法请求服务器数据前，使用动画显示正在加载中，当请求成功后，该动画自动隐藏，如下图所示：</p>
<p style="color: #1f2426;"><a href="http://img.mukewang.com/52dcfb3a0001746d06020435.jpg"><img src="http://img.mukewang.com/52dcfb3a0001746d06020435.jpg" alt="" /></a></p>
<p style="color: #1f2426;">在浏览器中显示的效果：</p>
<p style="color: #1f2426;"><a href="http://img.mukewang.com/52dcfb5500013ffa06500337.jpg"><img src="http://img.mukewang.com/52dcfb5500013ffa06500337.jpg" alt="" /></a></p>
<p style="color: #1f2426;">从图中可以看出，由于使用<code class="marker">ajaxStart()</code>和<code class="marker">ajaxStop()</code>方法绑定了动画元素，因此，在开始发送Ajax请求时，元素显示，请求完成时，动画元素自动隐藏。</p>
<p style="color: #1f2426;">注意：该方法在1.8.2下使用是正常的</p>


<hr style="color: #1f2426;" />

<h2 id="J_CodeLang" class="code-head" style="color: #1f2426;" data-lang="Javascript">表单验证插件——validate</h2>
<div id="J_CodeDescr" class="code-description">
<div class="code-desc co">
<p style="color: #1f2426;">该插件自带包含必填、数字、URL在内容的验证规则，即时显示异常信息，此外，还允许自定义验证规则，插件调用方法如下：</p>
<p style="color: #1f2426;"><code class="marker"><strong>$(form).validate({options})</strong></code></p>
<p style="color: #1f2426;">其中form参数表示表单元素名称，options参数表示调用方法时的配置对象，所有的验证规则和异常信息显示的位置都在该对象中进行设置。</p>
<p style="color: #1f2426;">例如，当点击表单中的“提交”按钮时，调用validate插件验证用户名输入是否符合规则，并将异常信息显示在页面中，如下图所示：</p>
<p style="color: #1f2426;"><a href="http://img.mukewang.com/52e474e70001b2cc04780576.jpg"><img src="http://img.mukewang.com/52e474e70001b2cc04780576.jpg" alt="" /></a></p>
<p style="color: #1f2426;">在浏览器中显示的效果：</p>
<p style="color: #1f2426;"><a href="http://img.mukewang.com/52e475000001603706010355.jpg"><img src="http://img.mukewang.com/52e475000001603706010355.jpg" alt="" /></a></p>
<p style="color: #1f2426;">从图中可以看出，在页面中导入了validate插件，当用户在输入框中录入用户名时，自动根据规则进入验证，并显示提示信息，验证成功后，表单才能提交。</p>

<h2 id="J_CodeLang" class="code-head" style="color: #1f2426;" data-lang="Javascript">表单插件——form</h2>
<div id="J_CodeDescr" class="code-description">
<div class="code-desc co">
<p style="color: #1f2426;">通过表单form插件，调用<code class="marker">ajaxForm()</code>方法，实现ajax方式向服务器提交表单数据，并通过方法中的options对象获取服务器返回数据，调用格式如下：</p>
<p style="color: #1f2426;"><code class="marker"><strong>$(form). ajaxForm ({options})</strong></code></p>
<p style="color: #1f2426;">其中form参数表示表单元素名称；options是一个配置对象，用于在发送ajax请求过程，设置发送时的数据和参数。</p>
<p style="color: #1f2426;">例如，在页面中点击“提交”按钮，调用form插件的
<code class="marker">ajaxForm()</code>方法向服务器发送录入的用户名和密码数据，服务器接收后返回并显示在页面中，如下图所示：</p>
<p style="color: #1f2426;"><a href="http://img.mukewang.com/52e4861d000143ad04720449.jpg"><img src="http://img.mukewang.com/52e4861d000143ad04720449.jpg" alt="" /></a></p>
<p style="color: #1f2426;">在浏览器中显示的效果：</p>
<p style="color: #1f2426;"><a href="http://img.mukewang.com/52e4863b0001b62e07360383.jpg"><img src="http://img.mukewang.com/52e4863b0001b62e07360383.jpg" alt="" /></a></p>
<p style="color: #1f2426;">从图中可以看出，当点击“提交”按钮时，调用form表单插件中的ajaxForm()方法向指定的服务器以ajax方式发送数据，服务器接收后返回并将数据显示。</p>

<h2 id="J_CodeLang" class="code-head" style="color: #1f2426;" data-lang="Javascript">图片灯箱插件——lightBox</h2>
<div id="J_CodeDescr" class="code-description">
<div class="code-desc co">
<p style="color: #1f2426;">该插件可以用圆角的方式展示选择中的图片，使用按钮查看上下张图片，在加载图片时自带进度条，还能以自动播放的方式浏览图片，调用格式如下：</p>
<p style="color: #1f2426;"><code class="marker"><strong>$(linkimage).lightBox({options})</strong></code></p>
<p style="color: #1f2426;">其中linkimage参数为包含图片的&lt;a&gt;元素名称，options为插件方法的配置对象。</p>
<p style="color: #1f2426;">例如，以列表的方式在页面中展示全部的图片，当用户单击其中某张图片时，通过引入的图片插件，采用“灯箱”的方式显示所选的图片，如下图所示：</p>
<p style="color: #1f2426;"><a href="http://img.mukewang.com/52e488760001d36c05070495.jpg"><img src="http://img.mukewang.com/52e488760001d36c05070495.jpg" alt="" /></a></p>
<p style="color: #1f2426;">在浏览器中显示的效果：</p>
<p style="color: #1f2426;"><a href="http://img.mukewang.com/52e4889600013b1107220457.jpg"><img src="http://img.mukewang.com/52e4889600013b1107220457.jpg" alt="" /></a></p>
<p style="color: #1f2426;">从图中可以看出，当用户点击“我的相册”中某一张图片时，则采用“灯箱”的方式显示选中图片，在显示图片时，还可以切换上下张和自动播放及关闭图片。</p>

<h2 id="J_CodeLang" class="code-head" style="color: #1f2426;" data-lang="Javascript">图片放大镜插件——jqzoom</h2>
<div id="J_CodeDescr" class="code-description">
<div class="code-desc co">
<p style="color: #1f2426;">在调用jqzoom图片放大镜插件时，需要准备一大一小两张一样的图片，在页面中显示小图片，当鼠标在小图片中移动时，调用该插件的<code class="marker">jqzoom()</code>方法，显示与小图片相同的大图片区域，从而实现放大镜的效果，调用格式如下：</p>
<p style="color: #1f2426;"><code class="marker"><strong>$(linkimage).jqzoom({options})</strong></code></p>
<p style="color: #1f2426;">其中linkimage参数为包含图片的&lt;a&gt;元素名称，options为插件方法的配置对象。</p>
<p style="color: #1f2426;">例如，在页面中，添加一个被&lt;a&gt;元素包含的图片元素，当在图片元素中移动鼠标时，在图片的右边，将显示放大后的所选区域效果，如下图所示：</p>
<p style="color: #1f2426;"><a href="http://img.mukewang.com/52e49c2500014a9b04630338.jpg"><img src="http://img.mukewang.com/52e49c2500014a9b04630338.jpg" alt="" /></a></p>
<p style="color: #1f2426;">在浏览器中显示的效果：</p>
<p style="color: #1f2426;"><a href="http://img.mukewang.com/52e49c43000157d205720384.jpg"><img src="http://img.mukewang.com/52e49c43000157d205720384.jpg" alt="" /></a></p>
<p style="color: #1f2426;">从图中可以看出，当在小图片中移动鼠标时，将调用放大镜插件的<code class="marker">jqzoom()</code>方法，在图片的右侧显示与小图片所选区域相同的放大区域，实现放大镜的效果。</p>

<h2 id="J_CodeLang" class="code-head" style="color: #1f2426;" data-lang="Javascript">cookie插件——cookie</h2>
<div id="J_CodeDescr" class="code-description">
<div class="code-desc co">
<p style="color: #1f2426;">使用cookie插件后，可以很方便地通过cookie对象保存、读取、删除用户的信息，还能通过cookie插件保存用户的浏览记录，它的调用格式为：</p>
<p style="color: #1f2426;"><strong>保存：</strong><code class="marker"><strong>$.cookie(key</strong><strong>，</strong><strong>value)</strong></code><strong>；读取：</strong><code class="marker"><strong>$.cookie(key)</strong></code><strong>，删除：</strong><code class="marker"><strong>$.cookie(key</strong><strong>，</strong><strong>null)</strong></code></p>
<p style="color: #1f2426;">其中参数key为保存cookie对象的名称，value为名称对应的cookie值。</p>
<p style="color: #1f2426;">例如，当点击“设置”按钮时，如果是“否保存用户名”的复选框为选中状态时，则使用cookie对象保存用户名，否则，删除保存的cookie用户名，如下图所示：</p>
<p style="color: #1f2426;"><a href="http://img.mukewang.com/52e49d8100016e2c06280481.jpg"><img src="http://img.mukewang.com/52e49d8100016e2c06280481.jpg" alt="" /></a></p>
<p style="color: #1f2426;">在浏览器中显示的效果：</p>
<p style="color: #1f2426;"><a href="http://img.mukewang.com/52e49db900011a7706060340.jpg"><img src="http://img.mukewang.com/52e49db900011a7706060340.jpg" alt="" /></a></p>
<p style="color: #1f2426;">从图中可以看出，由于在点击“设置”按钮时，选择了保存用户名，因此，输入框中的值被cookie保存，下次打开浏览器时，直接获取并显示保存的cookie值。</p>

<h2 id="J_CodeLang" class="code-head" style="color: #1f2426;" data-lang="Javascript">搜索插件——autocomplete</h2>
<div id="J_CodeDescr" class="code-description">
<div class="code-desc co">
<p style="color: #1f2426;">搜索插件的功能是通过插件的<code class="marker">autocomplete()</code>方法与文本框相绑定，当文本框输入字符时，绑定后的插件将返回与字符相近的字符串提示选择，调用格式如下：</p>
<p style="color: #1f2426;"><code class="marker"><strong>$(textbox).autocomplete(urlData,[options]);</strong></code></p>
<p style="color: #1f2426;">其中，textbox参数为文本框元素名称，urlData为插件返回的相近字符串数据，可选项参数options为调用插件方法时的配置对象。</p>
<p style="color: #1f2426;">例如，当用户在文本框输入内容时，调用搜索插件的<code class="marker">autocomplete()</code>方法返回与输入内容相匹配的字符串数据，显示在文本框下，提示选择，如下图所示：</p>
<p style="color: #1f2426;"><a href="http://img.mukewang.com/52e49eb90001024606410464.jpg"><img src="http://img.mukewang.com/52e49eb90001024606410464.jpg" alt="" /></a></p>
<p style="color: #1f2426;">在浏览器中显示的效果：</p>
<p style="color: #1f2426;"><a href="http://img.mukewang.com/52e49ed2000183f806300354.jpg"><img src="http://img.mukewang.com/52e49ed2000183f806300354.jpg" alt="" /></a></p>
<p style="color: #1f2426;">从图中可以看出，当文本框与搜索插件相绑定后，输入任意字符时，都将返回与之相匹配的字符串，提示用户选择，文本框在空白双击时，显示全部提示信息。</p>

<h2 id="J_CodeLang" class="code-head" style="color: #1f2426;" data-lang="Javascript">右键菜单插件——contextmenu</h2>
<div id="J_CodeDescr" class="code-description">
<div class="code-desc co">
<p style="color: #1f2426;">右键菜单插件可以绑定页面中的任意元素，绑定后，选中元素，点击右键，便通过该插件弹出一个快捷菜单，点击菜单各项名称执行相应操作，调用代码如下：</p>
<p style="color: #1f2426;"><code class="marker"><strong>$(selector).contextMenu(menuId,{options});</strong></code></p>
<p style="color: #1f2426;">Selector参数为绑定插件的元素，meunId为快捷菜单元素，options为配置对象。</p>
<p style="color: #1f2426;">例如，选中页面&lt;textarea&gt;元素，点击右键，弹出插件绑定的快捷菜单，点击菜单中的各个选项，便在页面中显示操作的对应名称。如下图所示：</p>
<p style="color: #1f2426;"><a href="http://img.mukewang.com/52e49fde0001919605370483.jpg"><img src="http://img.mukewang.com/52e49fde0001919605370483.jpg" alt="" /></a></p>
<p style="color: #1f2426;">在浏览器中显示的效果：</p>
<p style="color: #1f2426;"><a href="http://img.mukewang.com/52e49ff80001ed4f06910367.jpg"><img src="http://img.mukewang.com/52e49ff80001ed4f06910367.jpg" alt="" /></a></p>
<p style="color: #1f2426;">从图中可以看出，当文本框与右键菜单通过插件<code class="marker">contextmenu()</code>方法绑定后，选中文本框，点击右键时，弹出快捷菜单，点击“新建”选项时，显示操作对应内容。</p>

<h2 id="J_CodeLang" class="code-head" style="color: #1f2426;" data-lang="Javascript">自定义对象级插件——lifocuscolor插件</h2>
<div id="J_CodeDescr" class="code-description">
<div class="code-desc co">
<p style="color: #1f2426;">自定义的lifocuscolor插件可以在&lt;ul&gt;元素中，鼠标在表项&lt;li&gt;元素移动时，自定义其获取焦点时的背景色，即定义&lt;li&gt;元素选中时的背景色，调用格式为：</p>
<p style="color: #1f2426;"><code class="marker"><strong>$(Id).focusColor(color)</strong></code></p>
<p style="color: #1f2426;">其中，参数Id表示&lt;ul&gt;元素的Id号，color表示&lt;li&gt;元素选中时的背景色。</p>
<p style="color: #1f2426;">例如，在页面中，调用自定义的lifocuscolor插件，自定义&lt;li&gt;元素选中时的背景色，如下图所示：</p>
<p style="color: #1f2426;"><a href="http://img.mukewang.com/52e4a100000199ac04200306.jpg"><img src="http://img.mukewang.com/52e4a100000199ac04200306.jpg" alt="" /></a></p>
<p style="color: #1f2426;">在浏览器中显示的效果：</p>
<p style="color: #1f2426;"><a href="http://img.mukewang.com/52e4a11d0001669107090375.jpg"><img src="http://img.mukewang.com/52e4a11d0001669107090375.jpg" alt="" /></a></p>
<p style="color: #1f2426;">从图中可以看出，当&lt;ul&gt;元素调用<code class="marker">focusColor()</code>方法绑定自定义的插件之后，当鼠标在&lt;li&gt;元素间移动时，显示自定义的背景色。</p>

<h2 id="J_CodeLang" class="code-head" style="color: #1f2426;" data-lang="Javascript">自定义类级别插件—— twoaddresult</h2>
<div id="J_CodeDescr" class="code-description">
<div class="code-desc co">
<p style="color: #1f2426;">通过调用自定义插件twoaddresult中的不同方法，可以实现对两个数值进行相加和相减的运算，导入插件后，调用格式分别为：</p>
<p style="color: #1f2426;"><code class="marker"><strong>$.addNum(p1,p2) </strong></code><strong>和</strong><code class="marker"><strong> $.subNum(p1,p2)</strong></code></p>
<p style="color: #1f2426;">上述调用格式分别为计算两数值相加和相减的结果，p1和p2为任意数值。</p>
<p style="color: #1f2426;">例如，在页面的两个文本框中输入任意数值，点击“计算”按钮调用自定义插件中<code class="marker">$.addNum()</code>方法，计算两数值的和并将结果显示在另一文本框中，如下图所示：</p>
<p style="color: #1f2426;"><a href="http://img.mukewang.com/52e4a2230001185304660432.jpg"><img src="http://img.mukewang.com/52e4a2230001185304660432.jpg" alt="" /></a></p>
<p style="color: #1f2426;">在浏览器中显示的效果：</p>
<p style="color: #1f2426;"><a href="http://img.mukewang.com/52e4a23c0001c1cb06890362.jpg"><img src="http://img.mukewang.com/52e4a23c0001c1cb06890362.jpg" alt="" /></a></p>
<p style="color: #1f2426;">从图中可以看出，当点击“计算”按钮时，调用了自定义插件中的<code class="marker">$.addNum()</code>方法计算两个文本框中输入数值的和，并将该值显示在另一文本框中。</p>


<hr style="color: #1f2426;" />

<h2 class="code-head" style="color: #1f2426;" data-lang="Javascript">UI分为三个部分</h2>
<span style="color: #0000ff;">交互、小部件和效果库</span>

<span style="color: #0000ff;">交互包括：是一些与鼠标交互相关的内容</span>

<span style="color: #0000ff;">包括Draggable，Droppable，Resizable，Selectable和Sortable等</span>

&nbsp;

<span style="color: #0000ff;">小部件：界面扩展</span>

<span style="color: #0000ff;">包括：AutoComplete，ColorPicker ，Dialog，Slider，Tabs，ProgressBar，Spinner等</span>

<span style="color: #0000ff;">效果：丰富的动画效果</span>

<span style="color: #0000ff;">包括：Add Class, Color Animation,Toggle等</span>
<h2 class="code-head" style="color: #1f2426;" data-lang="Javascript"></h2>
resizeable

通过鼠标可以拖动调节尺寸长宽高

&nbsp;

Selectable选中可以做选择题用

$("#select").selectable();

if($("#right").hasClass("ui-selected")){

alert("恭喜你答对了")

}

&nbsp;

sortable上边有介绍，是拖拽排序

&nbsp;

Accordion  直接用 手风琴效果（列表承载在一个div中）

&nbsp;

AutoComplete 搜索自动补全

var autotags=["iwen","ime","html"]

$("#tags").autocomplete({

source:autotags最后不能有分号

})

&nbsp;

Dialog  这是一个对话框

这里可以放一个点击事件，然后产生下边的对话框

$("#div").dialog();

&nbsp;

Datepicker 日期

$("#div").datepicker

这样在输入框那键入就会弹出一个日历表，可以选择

&nbsp;

ProgressBar 进度条

//$("#div").progressbar({value:50})   默认是50

var pb;

var max = 100; 最大是100

var current = 0;  初始化为0

$(function(){

pb = $("#pb")

pb.progressbar({max:100})

setInterval(changepb，100)计时器来执行操作 每100毫秒刷新一次

})

function changepb(){

current++;

if(current&gt;=100){

current =0;   重新开始

}

pb.progressbar("option","value",current);

}

&nbsp;

menu：可以做子分类也

$("#div").menu({

position：{at：”left bottom“}  出现在右下方

})

用css来设置成横向菜单

通过浏览器console来查看所选中的css来做定义

.un-menu:after{

content:".";

display:block;

clear:both;

visibility:hidden

line-height:0

height:0;

}

ui-menu.ui-menu-item{

display:inline-block:     设置成1行显示

float：left；

margin：0

padding：0

width：auto

}

&nbsp;

Slider：可拖动的进度条

$("#slider")

slider=$("#slider")

valuespan =$("#span")

slider.slider({

slide:function(event,ui{

valuespan.text(slider.slider("option","value"))

})

})

&nbsp;

Spinner:微调菜单

$（function(){

$("#input").spinner()

$("#input").spinner(”value“，”10“)  默认是10

$("#input").on（”click“，function（）{

alert（$(#"input").spinner("value")）      这个是获得实时内容（输入框内）  直接调用value

}）

}）

&nbsp;

tabs：选项卡

html部分 用ul li做一个列表  还有div做3个

$("#tabs").tabs()；

直接就是一个选项卡了，很简单

&nbsp;
<h2 id="J_CodeLang" class="code-head" style="color: #1f2426;" data-lang="Javascript">拖曳插件——draggable</h2>
<p style="color: #1f2426;"><span style="color: #ff0000;">禁用是用display，重新开启是enable</span></p>
<p style="color: #1f2426;"><span style="color: #ff0000;">句式：$("#test").draggable("enable");</span></p>

<div id="J_CodeDescr" class="code-description">
<div class="code-desc co">
<p style="color: #1f2426;">拖曳插件draggable的功能是拖动被绑定的元素，当这个jQuery UI插件与元素绑定后，可以通过调用<code class="marker">draggable()</code>方法，实现各种拖曳元素的效果，调用格式如下：</p>
<p style="color: #1f2426;"><code class="marker"><strong>$(selector). draggable({options})</strong></code></p>
<p style="color: #1f2426;">options参数为方法调用时的配置对象，根据该对象可以设置各种拖曳效果，如“containment”属性指定拖曳区域，“axis”属性设置拖曳时的坐标方向。</p>
<p style="color: #1f2426;">例如，在页面中的&lt;div&gt;元素中添加两个子类&lt;div&gt;，通过与拖曳插件绑定，这两个子类&lt;div&gt;元素只能在外层的父&lt;div&gt;元素中任意拖曳，如下图所示：</p>
<p style="color: #1f2426;"><a href="http://img.mukewang.com/52e4b50c0001545304260177.jpg"><img src="http://img.mukewang.com/52e4b50c0001545304260177.jpg" alt="" /></a></p>
<p style="color: #1f2426;">在浏览器中显示的效果：</p>
<p style="color: #1f2426;"><a href="http://img.mukewang.com/52e4b5240001794706620379.jpg"><img src="http://img.mukewang.com/52e4b5240001794706620379.jpg" alt="" /></a></p>
<p style="color: #1f2426;">从图中可以看出，由于使用jQuery UI插件draggable绑定了两个子类&lt;div&gt;元素，并将配置对象的“containment”属性值设为“parent”，因此，这两个子类&lt;div&gt;元素只能在外层的父框中实现任意拖曳。</p>

<h2 id="J_CodeLang" class="code-head" style="color: #1f2426;" data-lang="Javascript">放置插件——droppable</h2>
<div id="J_CodeDescr" class="code-description">
<div class="code-desc co">
<p style="color: #1f2426;">除使用draggable插件拖曳任意元素外，还可以调用droppable UI插件将拖曳后的任意元素放置在指定区域中，类似购物车效果，调用格式如下：</p>
<p style="color: #1f2426;"><code class="marker"><strong>$(selector).droppable({options})</strong></code></p>
<p style="color: #1f2426;">selector参数为接收拖曳元素，options为方法的配置对象，在对象中，drop函数表示当被接收的拖曳元素完全进入接收元素的容器时，触发该函数的调用。</p>
<p style="color: #1f2426;">例如，在页面中，通过调用droppable插件将“产品区”中的元素拖曳至“购物车”中，同时改变“购物车”的背景色和数量值，如下图所示：</p>
<p style="color: #1f2426;"><a href="http://img.mukewang.com/52e4b7e000012af004800447.jpg"><img src="http://img.mukewang.com/52e4b7e000012af004800447.jpg" alt="" /></a></p>
<p style="color: #1f2426;">在浏览器中显示的效果：</p>
<p style="color: #1f2426;"><a href="http://img.mukewang.com/52e4b7fa0001435707090448.jpg"><img src="http://img.mukewang.com/52e4b7fa0001435707090448.jpg" alt="" /></a></p>
<p style="color: #1f2426;">从图中可以看出，先调用draggable插件任意拖曳“产品区”的元素，然后，调用droppable插件绑定“购物车”中接收元素，当“产品区”元素完全拖曳至“购物车”时，触发定义的drop函数，改变“购物车”中背景色和总数量值。</p>
<p style="color: #1f2426;">$("#rect1").draggable（）</p>
<p style="color: #1f2426;">$("#rect2").droggable（）</p>
<p style="color: #1f2426;">$("#rect2").on("droggable",function(event,ui){</p>
<p style="color: #1f2426;">//alert(event);     通过拖拽触发事件</p>
<p style="color: #1f2426;">$("#rect2").text("drop事件")  通过拖拽触发事件</p>
<p style="color: #1f2426;">})</p>

<h2 id="J_CodeLang" class="code-head" style="color: #1f2426;" data-lang="Javascript">拖曳排序插件——sortable</h2>
<div id="J_CodeDescr" class="code-description">
<div class="code-desc co">
<p style="color: #1f2426;">拖曳排序插件的功能是将序列元素（例如&lt;option&gt;、&lt;li&gt;）按任意位置进行拖曳从而形成一个新的元素序列，实现拖曳排序的功能，它的调用格式为：</p>
<p style="color: #1f2426;"><code class="marker"><strong>$(selector).sortable({options});</strong></code></p>
<p style="color: #1f2426;">selector参数为进行拖曳排序的元素，options为调用方法时的配置对象，</p>
<p style="color: #1f2426;">例如，在页面中，通过加载sortable插件将&lt;ul&gt;元素中的各个&lt;li&gt;表项实现拖曳排序的功能，如下图所示：</p>
<p style="color: #1f2426;"><a href="http://img.mukewang.com/52e4bb9b0001075303890385.jpg"><img src="http://img.mukewang.com/52e4bb9b0001075303890385.jpg" alt="" /></a></p>
<p style="color: #1f2426;">在浏览器中显示的效果：</p>
<p style="color: #1f2426;"><a href="http://img.mukewang.com/52e4bbb60001ae1606600393.jpg"><img src="http://img.mukewang.com/52e4bbb60001ae1606600393.jpg" alt="" /></a></p>
<p style="color: #1f2426;">从图中可以看出，由于使用sortable插件绑定了&lt;ul&gt;元素，并设置了拖曳时的透明度，因此，&lt;ul&gt;中的各个&lt;li&gt;元素则能指定的透明度进行任意的拖曳排序。</p>

<h2 id="J_CodeLang" class="code-head" style="color: #1f2426;" data-lang="Javascript">面板折叠插件——accordion</h2>
<div id="J_CodeDescr" class="code-description">
<div class="code-desc co">
<p style="color: #1f2426;">面板折叠插件可以实现页面中指定区域类似“手风琴”的折叠效果，即点击标题时展开内容，再点另一标题时，关闭已展开的内容，调用格式如下：</p>
<p style="color: #1f2426;"><code class="marker"><strong>$(selector).accordion({options});</strong></code></p>
<p style="color: #1f2426;">其中，参数selector为整个面板元素，options参数为方法对应的配置对象。</p>
<p style="color: #1f2426;">例如，通过accordion插件展示几个相同区域面板的折叠效果，如下图所示：</p>
<p style="color: #1f2426;"><a href="http://img.mukewang.com/52e4bd2c0001e58b03680467.jpg"><img src="http://img.mukewang.com/52e4bd2c0001e58b03680467.jpg" alt="" /></a></p>
<p style="color: #1f2426;">在浏览器中显示的效果：</p>
<p style="color: #1f2426;"><a href="http://img.mukewang.com/52e4bd4a0001b4ea06500371.jpg"><img src="http://img.mukewang.com/52e4bd4a0001b4ea06500371.jpg" alt="" /></a></p>
<p style="color: #1f2426;">从图中可以看出，由于绑定了折叠面板插件，默认为第一个面板的内容为展示状态，点击第二个面板主题时，展示主题对应内容，同时关闭上一个面板内容。</p>

<h2 id="J_CodeLang" class="code-head" style="color: #1f2426;" data-lang="Javascript">选项卡插件——tabs</h2>
<div id="J_CodeDescr" class="code-description">
<div class="code-desc co">
<p style="color: #1f2426;">使用选项卡插件可以将&lt;ul&gt;中的&lt;li&gt;选项定义为选项标题，在标题中，再使用&lt;a&gt;元素的“href”属性设置选项标题对应的内容，它的调用格式如下：</p>
<p style="color: #1f2426;"><code class="marker"><strong>$(selector).tabs({options});</strong></code></p>
<p style="color: #1f2426;">selector参数为选项卡整体外围元素，该元素包含选项卡标题与内容，options参数为<code class="marker">tabs()</code>方法的配置对象，通过该对象还能以ajax方式加载选项卡的内容。</p>
<p style="color: #1f2426;">例如，在页面中，添加选项卡的标题和内容元素，并绑定tabs插件，当点击标题时，以选项卡的方式切内容，如下图所示：</p>
<p style="color: #1f2426;"><a href="http://img.mukewang.com/52e4bea70001795c04470526.jpg"><img src="http://img.mukewang.com/52e4bea70001795c04470526.jpg" alt="" /></a></p>
<p style="color: #1f2426;">在浏览器中显示的效果：</p>
<p style="color: #1f2426;"><a href="http://img.mukewang.com/52e4bec4000174c706760344.jpg"><img src="http://img.mukewang.com/52e4bec4000174c706760344.jpg" alt="" /></a></p>
<p style="color: #1f2426;">从图中可以看出，在<code class="marker">tabs()</code>方法的配置对象中，通过“fx”属性设置了选项卡切换时的效果，“event”属性设置鼠标也可以切换选项卡，因此，当鼠标在移动至两个选项卡标题时，对应内容以动画的效果自动切换。</p>

<h2 id="J_CodeLang" class="code-head" style="color: #1f2426;" data-lang="Javascript">对话框插件——dialog</h2>
<div id="J_CodeDescr" class="code-description">
<div class="code-desc co">
<p style="color: #1f2426;">对话框插件可以用动画的效果弹出多种类型的对话框，实现JavaScript代码中<code class="marker">alert()</code>和<code class="marker">confirm()</code>函数的功能，它的调用格式为：</p>
<p style="color: #1f2426;"><code class="marker"><strong>$(selector).dialog({options});</strong></code></p>
<p style="color: #1f2426;">selector参数为显示弹出对话框的元素，通常为&lt;div&gt;，options参数为方法的配置对象，在对象中可以设置对话框类型、“确定”、“取消”按钮执行的代码等。</p>
<p style="color: #1f2426;">例如，当点击“提交”按钮时，如果文本框中的内容为空，则通过dialog插件弹出提示框，提示输入内容不能为空，如下图所示：</p>
<p style="color: #1f2426;"><a href="http://img.mukewang.com/52e4c1370001b0e805150562.jpg"><img src="http://img.mukewang.com/52e4c1370001b0e805150562.jpg" alt="" /></a></p>
<p style="color: #1f2426;">在浏览器中显示的效果：</p>
<p style="color: #1f2426;"><a href="http://img.mukewang.com/52e4c150000111de05350338.jpg"><img src="http://img.mukewang.com/52e4c150000111de05350338.jpg" alt="" /></a></p>
<p style="color: #1f2426;">从图中可以看出，当文本框的内容为空时，调用自定义的sys_Alert函数，在该函数中再调用dialog插件的<code class="marker">dialog()</code>方法，弹出带模式的显示信息对话框。</p>

<h2 id="J_CodeLang" class="code-head" style="color: #1f2426;" data-lang="Javascript">菜单工具插件——menu</h2>
<div id="J_CodeDescr" class="code-description">
<div class="code-desc co">
<p style="color: #1f2426;">菜单工具插件可以通过&lt;ul&gt;创建多级内联或弹出式菜单，支持通过键盘方向键控制菜单滑动，允许为菜单的各个选项添加图标，调用格式如下：</p>
<p style="color: #1f2426;"><code class="marker"><strong>$(selector).menu({options});</strong></code></p>
<p style="color: #1f2426;">selector参数为菜单列表中最外层&lt;ul&gt;元素，options为<code class="marker">menu()</code>方法的配置对象。</p>
<p style="color: #1f2426;">例如，在页面中，通过&lt;ul&gt;元素内联的方式构建一个三层结构的导航菜单，并将最外层&lt;ul&gt;元素通过<code class="marker">menu()</code>方法绑定插件，实现导航菜单的功能，如下图所示：</p>
<p style="color: #1f2426;"><a href="http://img.mukewang.com/52e4c2c10001b1a705160466.jpg"><img src="http://img.mukewang.com/52e4c2c10001b1a705160466.jpg" alt="" /></a></p>
<p style="color: #1f2426;">在浏览器中显示的效果：</p>
<p style="color: #1f2426;"><a href="http://img.mukewang.com/52e4c2dd0001b82505350338.jpg"><img src="http://img.mukewang.com/52e4c2dd0001b82505350338.jpg" alt="" /></a></p>
<p style="color: #1f2426;">从图中可以看出，通过&lt;ul&gt;内嵌的方式，构建一个三层结构的导航菜单，将&lt;li&gt;元素的class属性值设为“ui-state-disabled”，可将菜单选项置为不可用状态。</p>

<h2 id="J_CodeLang" class="code-head" style="color: #1f2426;" data-lang="Javascript">微调按钮插件——spinner</h2>
<div id="J_CodeDescr" class="code-description">
<div class="code-desc co">
<p style="color: #1f2426;">微调按钮插件不仅能在文本框中直接输入数值，还可以通过点击输入框右侧的上下按钮修改输入框的值，还支持键盘的上下方向键改变输入值，调用格式如下：</p>
<p style="color: #1f2426;"><code class="marker"><strong>$(selector).spinner({options});</strong></code></p>
<p style="color: #1f2426;">selector参数为文本输入框元素，可选项options参数为<code class="marker">spinner()</code>方法的配置对象，在该对象中，可以设置输入的最大、最小值，获取改变值和设置对应事件。</p>
<p style="color: #1f2426;">例如，将页面中的三个输入文本框都与微调插件相绑定，当改变三个文本框值时，对应的&lt;div&gt;元素的背景色也将随之发生变化，如下图所示：</p>
<p style="color: #1f2426;"><a href="http://img.mukewang.com/52e4c4ad0001d4e007610813.jpg"><img src="http://img.mukewang.com/52e4c4ad0001d4e007610813.jpg" alt="" /></a></p>
<p style="color: #1f2426;">在浏览器中显示的效果：</p>
<p style="color: #1f2426;"><a href="http://img.mukewang.com/52e4c4c70001205f05430305.jpg"><img src="http://img.mukewang.com/52e4c4c70001205f05430305.jpg" alt="" /></a></p>
<p style="color: #1f2426;">从图中可以看出，由于三个文本框输入元素都绑定微调插件，因此，无论是点击右侧的上下按钮，还是直接在文本框中输入值，都可以改变&lt;div&gt;元素的背景色。</p>

<h2 id="J_CodeLang" class="code-head" style="color: #1f2426;" data-lang="Javascript">工具提示插件——tooltip</h2>
<div id="J_CodeDescr" class="code-description">
<div class="code-desc co">
<p style="color: #1f2426;">工具提示插件可以定制元素的提示外观，提示内容支持变量、Ajax远程获取，还可以自定义提示内容显示的位置，它的调用格式如下：</p>
<p style="color: #1f2426;"><code class="marker"><strong>$(selector).tooltip({options});</strong></code></p>
<p style="color: #1f2426;">其中selector为需要显示提示信息的元素，可选项参数options为<code class="marker">tooltip()</code>方法的配置对象，在该对象中，可以设置提示信息的弹出、隐藏时的效果和所在位置。</p>
<p style="color: #1f2426;">例如，将三个&lt;a&gt;元素与工具提示插件相绑定，当把鼠标移动在&lt;a&gt;元素内容时，以动画效果弹出对应的提示图片，移出时，图片自动隐藏，如下图所示：</p>
<p style="color: #1f2426;"><a href="http://img.mukewang.com/52e4c6360001f38506900450.jpg"><img src="http://img.mukewang.com/52e4c6360001f38506900450.jpg" alt="" /></a></p>
<p style="color: #1f2426;">在浏览器中显示的效果：</p>
<p style="color: #1f2426;"><a href="http://img.mukewang.com/52e4c6530001236e05960553.jpg"><img src="http://img.mukewang.com/52e4c6530001236e05960553.jpg" alt="" /></a></p>
<p style="color: #1f2426;">从图中可以看出，由于各个&lt;a&gt;元素都绑定了工具提示插件，因此，将在指定的位置并以动画效果展示各个&lt;a&gt;元素中title属性所对应的内容。</p>


<hr style="color: #1f2426;" />

<h2 id="J_CodeLang" class="code-head" style="color: #1f2426;" data-lang="Javascript">获取浏览器的名称与版本信息</h2>
<div id="J_CodeDescr" class="code-description">
<div class="code-desc co">
<p style="color: #1f2426;">在jQuery中，通过<code class="marker">$.browser</code>对象可以获取浏览器的名称和版本信息，如<code class="marker">$.browser.chrome</code>为true，表示当前为Chrome浏览器，<code class="marker">$.browser.mozilla</code>为true，表示当前为火狐浏览器，还可以通过<code class="marker">$.browser.version</code>方式获取浏览器版本信息。</p>
<p style="color: #1f2426;">例如，调用$.browser对象，获取浏览器名称并显示在页面中，如下图所示：</p>
<p style="color: #1f2426;"><a href="http://img.mukewang.com/52e4cf7f0001d48b03770322.jpg"><img src="http://img.mukewang.com/52e4cf7f0001d48b03770322.jpg" alt="" /></a></p>
<p style="color: #1f2426;">在浏览器中显示的效果：</p>
<p style="color: #1f2426;"><a href="http://img.mukewang.com/52e4cf9800015ac505710448.jpg"><img src="http://img.mukewang.com/52e4cf9800015ac505710448.jpg" alt="" /></a></p>
<p style="color: #1f2426;">从图中可以看出，通过调用<code class="marker">$.browser</code>对象，检测当前浏览器的所属类型，并根据类型不同，将浏览器名称保存至变量中，最后将变量的内容显示在页面中。</p>

<h2 id="J_CodeLang" class="code-head" style="color: #1f2426;" data-lang="Javascript">检测浏览器是否属于W3C盒子模型</h2>
<div id="J_CodeDescr" class="code-description">
<div class="code-desc co">
<p style="color: #1f2426;">浏览器的盒子模型分为两类，一类为标准的w3c盒子模型，另一类为IE盒子模型，两者区别为在Width和Height这两个属性值中是否包含padding和border的值，w3c盒子模型不包含，IE盒子模型则包含，而在jQuery 中，可以通过<code class="marker">$.support.boxModel</code>对象返回的值，检测浏览器是否属于标准的w3c盒子模型。</p>
<p style="color: #1f2426;">例如，根据页面的特征，并通过<code class="marker">$.support.boxModel</code>属性的返回值，显示当前浏览器是否属于标准的w3c盒子模型，如下图所示：</p>
<p style="color: #1f2426;"><a href="http://img.mukewang.com/52e4d0e30001a31d03850323.jpg"><img src="http://img.mukewang.com/52e4d0e30001a31d03850323.jpg" alt="" /></a></p>
<p style="color: #1f2426;">在浏览器中显示的效果：</p>
<p style="color: #1f2426;"><a href="http://img.mukewang.com/52e4d0fa0001a4b704360230.jpg"><img src="http://img.mukewang.com/52e4d0fa0001a4b704360230.jpg" alt="" /></a></p>
<p style="color: #1f2426;">从图中可以看出，由于打开的页面属于标准的w3c盒子模型，因此，在调用<code class="marker">$.support.boxModel</code>属性时，返回true值。</p>
<p style="color: #1f2426;"><span style="color: #ff0000;">补充一个知识点：盒子模型</span></p>
<p style="color: #1f2426;"><span style="color: #ff0000;">可以用alert来查看值</span></p>
<p style="color: #1f2426;"><span style="color: #ff0000;">height：不包含padding</span></p>
<p style="color: #1f2426;"><span style="color: #ff0000;">innerHeight：包含padding但是不包含线宽</span></p>
<p style="color: #1f2426;"><span style="color: #ff0000;">outerHeight（）：包含线宽</span></p>
<p style="color: #1f2426;"><span style="color: #ff0000;">outerHeight（true）：包含margin</span></p>

<h2 id="J_CodeLang" class="code-head" style="color: #1f2426;" data-lang="Javascript">检测对象是否为空</h2>
<div id="J_CodeDescr" class="code-description">
<div class="code-desc co">
<p style="color: #1f2426;">在jQuery中，可以调用名为<code class="marker">$.isEmptyObject</code>的工具函数，检测一个对象的内容是否为空，如果为空，则该函数返回true，否则，返回false值，调用格式如下：</p>
<p style="color: #1f2426;"><code class="marker"><strong>$.isEmptyObject(obj);</strong></code></p>
<p style="color: #1f2426;">其中，参数obj表示需要检测的对象名称。</p>
<p style="color: #1f2426;">例如，通过<code class="marker">$.isEmptyObject()</code>函数，检测某个指定的对象是否为空，并将结果显示在页面中，如下图所示：</p>
<p style="color: #1f2426;"><a href="http://img.mukewang.com/52e4d28b0001b06c03810337.jpg"><img src="http://img.mukewang.com/52e4d28b0001b06c03810337.jpg" alt="" /></a></p>
<p style="color: #1f2426;">在浏览器中显示的效果：</p>
<p style="color: #1f2426;"><a href="http://img.mukewang.com/52e4d2a600014b6604360230.jpg"><img src="http://img.mukewang.com/52e4d2a600014b6604360230.jpg" alt="" /></a></p>
<p style="color: #1f2426;">从图中可以看出，由于对象obj的内容为空，因此，<code class="marker">$.isEmptyObject()</code>函数检测obj时，返回true，并根据返回的true值在页面中显示对应的文字内容。</p>

<h2 id="J_CodeLang" class="code-head" style="color: #1f2426;" data-lang="Javascript">检测对象是否为原始对象</h2>
<div id="J_CodeDescr" class="code-description">
<div class="code-desc co">
<p style="color: #1f2426;">调用名为<code class="marker">$.isPlainObject</code>的工具函数，能检测对象是否为通过<code class="marker">{}</code>或<code class="marker">new Object()</code>关键字创建的原始对象，如果是，返回true，否则，返回false值，调用格式为：</p>
<p style="color: #1f2426;"><code class="marker"><strong>$.isPlainObject (obj);</strong></code></p>
<p style="color: #1f2426;">其中，参数obj表示需要检测的对象名称。</p>
<p style="color: #1f2426;">例如，通过<code class="marker">$.isPlainObject()</code>函数，检测某个指定的对象是否为原始，并将结果显示在页面中，如下图所示：</p>
<p style="color: #1f2426;"><a href="http://img.mukewang.com/52e4d3be0001f46806190354.jpg"><img src="http://img.mukewang.com/52e4d3be0001f46806190354.jpg" alt="" /></a></p>
<p style="color: #1f2426;">在浏览器中显示的效果：</p>
<p style="color: #1f2426;"><a href="http://img.mukewang.com/52e4d3d500013c5004400241.jpg"><img src="http://img.mukewang.com/52e4d3d500013c5004400241.jpg" alt="" /></a></p>
<p style="color: #1f2426;">从图中可以看出，由于自定义的obj_a和obj_b都是属于原始对象，因此，当调用<code class="marker">$.isPlainObject()</code>函数检测这两个对象时，都返回true值。</p>

<h2 id="J_CodeLang" class="code-head" style="color: #1f2426;" data-lang="Javascript">检测两个节点的包含关系</h2>
<div id="J_CodeDescr" class="code-description">
<div class="code-desc co">
<p style="color: #1f2426;">调用名为<code class="marker">$.contains</code>的工具函数，能检测在一个DOM节点中是否包含另外一个DOM节点，如果包含，返回true，否则，返回false值，调用格式为：</p>
<p style="color: #1f2426;"><code class="marker"><strong>$.contains (container, contained);</strong></code></p>
<p style="color: #1f2426;">参数container表示一个DOM对象节点元素，用于包含其他节点的容器，contained是另一个DOM对象节点元素，用于被其他容器所包含。</p>
<p style="color: #1f2426;">例如，通过<code class="marker">$.contains()</code>函数，检测两个节点对象间是否存在包含关系，并将检测的结果显示在页面中，如下图所示：</p>
<p style="color: #1f2426;"><a href="http://img.mukewang.com/52e4d5fb000122c104540369.jpg"><img src="http://img.mukewang.com/52e4d5fb000122c104540369.jpg" alt="" /></a></p>
<p style="color: #1f2426;">在浏览器中显示的效果：</p>
<p style="color: #1f2426;"><a href="http://img.mukewang.com/52e4d61a0001923f05080306.jpg"><img src="http://img.mukewang.com/52e4d61a0001923f05080306.jpg" alt="" /></a></p>
<p style="color: #1f2426;">从图中可以看出，<code class="marker">documentElement</code>是DOM根结点，而body只是根结点下的子节点之一，它们之间存在包含关系，因此，返回true值，并显示“包含”字样。</p>

<h2 id="J_CodeLang" class="code-head" style="color: #1f2426;" data-lang="Javascript">字符串操作函数</h2>
<div id="J_CodeDescr" class="code-description">
<div class="code-desc co">
<p style="color: #1f2426;">调用名为<code class="marker">$.trim</code>的工具函数，能删除字符串中左右两边的空格符，但该函数不能删除字符串中间的空格，调用格式为：</p>
<p style="color: #1f2426;"><code class="marker"><strong>$.trim (str);</strong></code></p>
<p style="color: #1f2426;">参数str表示需要删除左右两边空格符的字符串。</p>
<p style="color: #1f2426;">例如，通过<code class="marker">$.contains()</code>函数，除掉一个两边均有空格符的字符串，并将其执行前后的字符长度都显示在页面中，如下图所示：</p>
<p style="color: #1f2426;"><a href="http://img.mukewang.com/52e4d72d0001a3c005630480.jpg"><img src="http://img.mukewang.com/52e4d72d0001a3c005630480.jpg" alt="" /></a></p>
<p style="color: #1f2426;">在浏览器中显示的效果：</p>
<p style="color: #1f2426;"><a href="http://img.mukewang.com/52e4d7470001abd205040320.jpg"><img src="http://img.mukewang.com/52e4d7470001abd205040320.jpg" alt="" /></a></p>
<p style="color: #1f2426;">从图中可以看出，由于文本框中的字符串前后分别有一个空格字符，因此，它的字符长度为13，调用<code class="marker">trim()</code>函数删除字符串前后空格之后，字符串长度则变为11。</p>

<h2 id="J_CodeLang" class="code-head" style="color: #1f2426;" data-lang="Javascript">URL操作函数</h2>
<div id="J_CodeDescr" class="code-description">
<div class="code-desc co">
<p style="color: #1f2426;">调用名为<code class="marker">$. param</code>的工具函数，能使对象或数组按照<code class="marker">key/value</code>格式进行序列化编码，该编码后的值常用于向服务端发送URL请求，调用格式为：</p>
<p style="color: #1f2426;"><code class="marker"><strong>$.</strong> <strong>param (obj);</strong></code></p>
<p style="color: #1f2426;">参数obj表示需要进行序列化的对象，该对象也可以是一个数组，整个函数返回一个经过序列化编码后的字符串。</p>
<p style="color: #1f2426;">例如，通过<code class="marker">$.param()</code>函数，对指定的对象进行序列化编码，使其成为可执行传值的URL地址，并将该地址显示在页面中，如下图所示：</p>
<p style="color: #1f2426;"><a href="http://img.mukewang.com/52e4d8a6000185af04750370.jpg"><img src="http://img.mukewang.com/52e4d8a6000185af04750370.jpg" alt="" /></a></p>
<p style="color: #1f2426;">在浏览器中显示的效果：</p>
<p style="color: #1f2426;"><a href="http://img.mukewang.com/52e4d8c00001965504850276.jpg"><img src="http://img.mukewang.com/52e4d8c00001965504850276.jpg" alt="" /></a></p>
<p style="color: #1f2426;">从图中可以看出，通过调用工具函数<code class="marker">$.param()</code>可以将一个对象进行序列化并编码成可以在地址栏中直接执行的URL字符串。</p>
<p style="color: #1f2426;">param和serialize的区别是什么？前者是对任意的参数进行URL地址格式的转换，而后者仅属于form提交的数据转换。</p>

<h2 id="J_CodeLang" class="code-head" style="color: #1f2426;" data-lang="Javascript">使用$.extend()扩展工具函数</h2>
<div id="J_CodeDescr" class="code-description">
<div class="code-desc co">
<p style="color: #1f2426;">调用名为<code class="marker">$. extend</code>的工具函数，可以对原有的工具函数进行扩展，自定义类级别的jQuery插件，调用格式为：</p>
<p style="color: #1f2426;"><code class="marker"><strong>$.</strong> <strong>extend ({options});</strong></code></p>
<p style="color: #1f2426;">参数options表示自定义插件的函数内容。</p>
<p style="color: #1f2426;">例如，调用<code class="marker">$.extend()</code>函数，自定义一个用于返回两个数中最大值的插件，并在页面中将插件返回的最大值显示在页面中，如下图所示：</p>
<p style="color: #1f2426;"><a href="http://img.mukewang.com/52e4d9d30001eb7305670594.jpg"><img src="http://img.mukewang.com/52e4d9d30001eb7305670594.jpg" alt="" /></a></p>
<p style="color: #1f2426;">在浏览器中显示的效果：</p>
<p style="color: #1f2426;"><a href="http://img.mukewang.com/52e4d9ee0001aad904820268.jpg"><img src="http://img.mukewang.com/52e4d9ee0001aad904820268.jpg" alt="" /></a></p>
<p style="color: #1f2426;">从图中可以看出，当点击“计算”按钮时，先调用自定义插件中名为“MaxNum”的方法，计算并返回两个数值中的最大值，然后，将该值显示在页面中。</p>
<p style="color: #1f2426;"><span style="color: #ff0000;">在myjq.js文件内添加下面代码</span></p>
<p style="color: #1f2426;"><span style="color: #ff0000;">$.myjq = function(){</span></p>
<p style="color: #1f2426;"><span style="color: #ff0000;">alert（”Hello“）</span></p>
<p style="color: #1f2426;"><span style="color: #ff0000;">}</span></p>
<p style="color: #1f2426;"><span style="color: #ff0000;">在正式的Extendsindex.js内添加下边代代码来实现调用</span></p>
<p style="color: #1f2426;"><span style="color: #ff0000;">$(function(){</span></p>
<p style="color: #1f2426;"><span style="color: #ff0000;">$.myjq()；</span></p>
<p style="color: #1f2426;"><span style="color: #ff0000;">})</span></p>
<p style="color: #1f2426;">在上边就相当于给jq制作了一个扩展了</p>
<p style="color: #1f2426;"><span style="color: #0000ff;">第二种方法：</span></p>
<p style="color: #1f2426;"><span style="color: #0000ff;">在myjq.js文件内添加下面代码</span></p>
<p style="color: #1f2426;"><span style="color: #0000ff;">$.fn.myjq=function(){</span></p>
<p style="color: #1f2426;"><span style="color: #0000ff;">$(this).text("Hello")</span></p>
<p style="color: #1f2426;"><span style="color: #0000ff;">}</span></p>
<p style="color: #1f2426;"><span style="color: #0000ff;">调用的方法也不同</span></p>
<p style="color: #1f2426;"><span style="color: #0000ff;">$(function(){</span></p>
<span style="color: #0000ff;"><span style="color: #ff0000;">$(”div“).myjq()</span></span>
<p style="color: #1f2426;"><span style="color: #0000ff;">})</span></p>

<h2 id="J_CodeLang" class="code-head" style="color: #1f2426;" data-lang="Javascript">使用$.extend()扩展Object对象</h2>
<div id="J_CodeDescr" class="code-description" style="color: #1f2426;">
<div class="code-desc co">

除使用<code class="marker">$.extend</code>扩展工具函数外，还可以扩展原有的<code class="marker">Object</code>对象，在扩展对象时，两个对象将进行合并，当存在相同属性名时，后者将覆盖前者，调用格式为：

<code class="marker"><strong>$.</strong> <strong>extend (obj1,obj2,…objN);</strong></code>

参数obj1至objN表示需要合并的各个原有对象。

例如，调用<code class="marker">$.extend()</code>函数对两个已有的对象进行合并，并将合并后的新对象元素内容显示在页面中，如下图所示：

<a href="http://img.mukewang.com/52e4dbff0001c35405140338.jpg"><img src="http://img.mukewang.com/52e4dbff0001c35405140338.jpg" alt="" /></a>

在浏览器中显示的效果：

<a href="http://img.mukewang.com/52e4dc1800012ce104770270.jpg"><img src="http://img.mukewang.com/52e4dc1800012ce104770270.jpg" alt="" /></a>

从图中可以看出，当两个对象通过<code class="marker">$.extend()</code>函数扩展合并后，返回一个包含两个对象中全部属性元素的新对象，相同名称的“name”属性，前者被后者覆盖。
<h2><span style="color: #0000ff;">noConflict来代替$的扩展</span></h2>
<span style="color: #0000ff;">防止不同框架都使用$来代替jq</span>

<span style="color: #0000ff;">$.noConflict();       </span>

<span style="color: #0000ff;">这句话就是让$消除掉$对jQuery的缩写，所以下边就不能再写$而必须用jQuery来代替</span>

<span style="color: #0000ff;">jQuery(function(){</span>

<span style="color: #0000ff;">jQuery("button").on("click",function(){</span>

<span style="color: #0000ff;">jQuery("div").text("new Hello")</span>

<span style="color: #0000ff;">})</span>

<span style="color: #0000ff;">})</span>

<span style="color: #ff0000;">如果觉得麻烦可以声明一下缩写，在最上边写</span>

<span style="color: #ff0000;">var myjq = $.noConflict();</span>

<span style="color: #ff0000;">以后就可以用myjq来替换了</span>

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