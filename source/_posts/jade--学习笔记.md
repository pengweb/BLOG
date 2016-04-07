---
title: jade--学习笔记
date: 2016-03-21 23:15:04
tags: [jade,nodejs]

---
注：以下代码都没有做缩进处理···

安装
<blockquote>npm install -g jade</blockquote>
直接编译
<blockquote>jade index.jade</blockquote>
不压缩
<blockquote>jade -P index.jade</blockquote>
不压缩且监控
<blockquote>jade -P -w index.jade</blockquote>
语法：
<blockquote>h1.title(id="title",class="title2") //括号内一定要用这种写法，括号内一般都是html直接的写法
h1.title#title.title2</blockquote>
以上两种方法是一样的

标签中有大段的块内容

方式一：在标签后面添加 .

比如一段js代码，注意是script后面有一个.
<blockquote>script.
console.log('Welcome to join wandoujia-fe')
console.log('We want you')</blockquote>
方式二：每段前面添加|
<blockquote>script
| console.log('Welcome to join wandoujia-fe')
| console.log('We want you')</blockquote>
上边可以直接插入标签<strong>1<strong>,这个不会改变，会被浏览器解析</strong></strong>

注释：
单行会编译成<!-- -->、 //h3
多行不会编译 //-h3
块注释 //-
h3

不换行嵌套
<blockquote>:</blockquote>
兼容ie
<blockquote><!-- [if IE 8]><html class='ie8'><![endif]-->
<!-- [if !IE]><!--><!--<![endif]--> &lt;!-- \[if IE 8]&gt;&lt;html class='ie8'&gt;&lt;\!\[endif]--&gt;
&lt;!-- \[if !IE]&gt;&lt;!--&gt;&lt;!--&lt;\!\[endif]--&gt;</blockquote>
声明变量：
<blockquote>-var course = 'jade'
title #{course}
//支持js 例如写成
title #{course.toUpperCase()}</blockquote>
输出大写
引入：
1.内嵌-权重最高
2-命令行可以在命令行控制变量，当同时存在的时候文档内嵌权重最高
3-也可以从外部json文件引入
<blockquote>jade index.jade -P -w -O test.json //通过test.json来输入</blockquote>
转义：
<blockquote>-var data='test'
-var htmlData='&lt;script&gt;aler-t(1)&lt;/script&gt;'

p #{data} //test
p #{htmlData} // &lt;会被转义
p !{htmlData} // &lt;不会被转义
p=data //和#一样
p=htmlData //和#一样
p!=htmlData //和#一样
p \\#{htmlData} //避免编译#{}
p \\!{htmlData} //避免编译#{}</blockquote>
input (value='#{newData}') //当newData没有给赋值的时候，这里应该写成input (value=newData) 这样就不会初始一个undefined了

流程：
1、for
<blockquote>-var peng = {course:'jade',level:'high'}
-for(var k in peng) //遍历peng
p= peng\[k]; //显示jade 和high</blockquote>
2、each
<blockquote>-var peng = {course:'jade',level:'high'}
-each value,key in peng //遍历peng
p #{key}:#{value} //显示course:jade level:high</blockquote>
数组遍历
<blockquote>-var courses=\['node','jade','expess']
-each item in courses
p= item</blockquote>
嵌套循环
<blockquote>-var sections=\[{id:1,items:\['a','b']},{id:2,items:\['c','d']}]
dl
-each section in sections
dt= section.id
-each item in section.items
dd= item</blockquote>
显示结果
<blockquote><dl></dl>1ab2cd</blockquote>
while用法
<blockquote>-var n = 0
ul
while n&lt;4
li= n++</blockquote>
if else用法
<blockquote>-var isPeng = true
-var lessons = \['jade','node']
if lessons
if lessons.length&gt;2
p more than 2: #{lessons.join(',')}
else if lessons.length&gt;1
p more than 1: #{lessons.join(',')}
else
p no lesson
else
p no lesson</blockquote>
unless用法--其实就是if的反向判断
<blockquote>unless !isPeng
p #{lessons.length} //2</blockquote>
switch语句(用case和when代替)
<blockquote>-var name = 'jade'
case name
when 'java'
when 'node'
p Hi node!
when 'jade'
p Hi jade!
when 'express': p Hi express! //这个和jade的结果一样，就是写法不同
default
p #{name}</blockquote>
mixin-其实就和function差不多
<blockquote>mixin lesson
p peng jade study
+lesson //这个是调用，不调用，不显示</blockquote>
传参
<blockquote>mixin study(name,courses)
p #{name} stydy
ul.courses
each course in courses
li=course
+study('tom',\['jade','node'])</blockquote>
嵌套（接上）
<blockquote>mixin group(student)
h4 #{student.name}
+study(student.name,student.courses)
+group({name:'tom',courses:\['jade','node']})</blockquote>
显示结果：
<blockquote>tom stydy
<ul>
	<li>jade</li>
	<li>node</li>
</ul>
</blockquote>
内敛代码块
<blockquote>mixin team(slogon)
h4 #{slogon}
if block
block
p 在上边 //自己测试下上边那个block就是指的下边那个p Gbod job，显示的也是这个，这是判断team内是否有元素
else
p no team
+team('slogon')
p Gbod job!</blockquote>
可以传属性
<blockquote>mixin attr(name)
p(class!=attributes.class) #{name}
+attr('attr')(class='magic')</blockquote>
显示结果：
<blockquote>
<p class="magic">attr</p>
</blockquote>
简单一点写法
<blockquote>mixin attrs(name)
p$attributes(attributes) #{name}
+attrs('attrs')(class='magic2',id='attrid')</blockquote>
显示结果
<blockquote>
<p id="attrid" class="magic2">attrs</p>
</blockquote>
当不确定传参个数的时候
<blockquote>mixin magic(name,...items)
ul(class='#{name}')
each item in items
li= item
+magic('magic','node','jade')</blockquote>
显示结果
<blockquote>
<ul>
	<li>node</li>
	<li>jade</li>
</ul>
</blockquote>
继承（文件和文件共用）用的不多
<blockquote>block desc
p imooc jade study extends //定义
block desc //调用
block desc</blockquote>
引用文件
<blockquote>extend layout //这个layout是文件名，不是block的名，如果有层级关系，前边加/来寻址就行了
block content</blockquote>
被引用个文件
最下边写上
<blockquote>block content //这样引用才能接着写</blockquote>
如果在被引用文件内有
block desc
然后在引用文件内又定义了一次
block desc
那么引用文件内定义的新属性会覆盖掉被引用文件的属性

实例：

layout.jade
<pre>//继承-头部+尾部
doctype html
html(lang="en")
    head
        meta(charset="UTF-8")
    body
        block content
footer END
</pre>
index.jade
<pre>//这个用的是继承方法
extends layout
block content
    p 这里写内容</pre>
包含：文件和区块的内嵌关系
head.jade
<blockquote>//包含-头部
doctype html
html(lang="en")
head
meta(charset="UTF-8")
body
block content</blockquote>
footer.jade
<blockquote>//包含-尾部
footer END</blockquote>
index.jade
<blockquote>//这个用的是包含de方法
include head
p haha
include footer</blockquote>
render和renderFile

compile用法
<blockquote>var fn = jade.compile('div #{course}',{})
var html = fn({course:'jade'})
res.end(html)</blockquote>
结果
<blockquote>
<div>jade</div></blockquote>
render方法
<blockquote>var html=jade.render('div #{course}',{course:'jade'})</blockquote>
后边直接放入参数，结果和第一个相同

renderFile方法
<blockquote>var html=jade.renderFile('index.jade',{course:'jade'},pretty:true)</blockquote>
pretty:true格式化
改文件头就可以改变显示形式 content-type:text/plain 把plain改成html