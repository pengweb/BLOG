---
title: Mongoose--学习笔记
date: 2016-04-07 15:42:43
tags: [nodejs,笔记,note,mongoose]

---
##一、快速通道

###1.1 名词解释
<ul>
	<li><code>Schema</code> ： 一种以文件形式存储的数据库模型骨架，不具备数据库的操作能力</li>
	<li><code>Model</code> ： 由<code>Schema</code>发布生成的模型，具有抽象属性和行为的数据库操作对</li>
	<li><code>Entity</code> ： 由<code>Model</code>创建的实体，他的操作也会影响数据库</li>
</ul>
<strong>注意</strong>：

1.本学习文档采用严格命名方式来区别不同对象，例如：
<pre class="prettyprint language-javascript"><code>    <span class="kwd">var</span> <span class="typ">PersonSchema</span><span class="pun">;</span>   <span class="com">//Person的文本属性</span>
    <span class="kwd">var</span> <span class="typ">PersonModel</span><span class="pun">;</span>    <span class="com">//Person的数据库模型</span>
    <span class="kwd">var</span> <span class="typ">PersonEntity</span><span class="pun">;</span>   <span class="com">//Person实体</span></code></pre>
2.<code>Schema</code>、<code>Model</code>、<code>Entity</code>的关系请牢记，<code>Schema</code>生成<code>Model</code>，<code>Model</code>创造<code>Entity</code>，<code>Model</code>和<code>Entity</code>都可对数据库操作造成影响，但<code>Model</code>比<code>Entity</code>更具操作性。

##1.2 准备工作

1.首先你必须安装<a href="http://www.mongodb.org/" target="_blank">MongoDB</a>和<a href="http://nodejs.org/" target="_blank">NodeJS</a>

2.在项目只能够创建一个数据库连接，如下:
<pre class="prettyprint language-javascript"><code>    <span class="kwd">var</span><span class="pln"> mongoose </span><span class="pun">=</span> <span class="kwd">require</span><span class="pun">(</span><span class="str">'mongoose'</span><span class="pun">);</span>    <span class="com">//引用mongoose模块</span>
    <span class="kwd">var</span><span class="pln"> db </span><span class="pun">=</span><span class="pln"> mongoose</span><span class="pun">.</span><span class="pln">createConnection</span><span class="pun">(</span><span class="str">'localhost'</span><span class="pun">,</span><span class="str">'test'</span><span class="pun">);</span> <span class="com">//创建一个数据库连接</span></code></pre>
3.打开本机<code>localhost</code>的<code>test</code>数据库时，我们可以监测是否有异常
<pre class="prettyprint language-javascript"><code><span class="pln">    db</span><span class="pun">.</span><span class="pln">on</span><span class="pun">(</span><span class="str">'error'</span><span class="pun">,</span><span class="pln">console</span><span class="pun">.</span><span class="pln">error</span><span class="pun">.</span><span class="pln">bind</span><span class="pun">(</span><span class="pln">console</span><span class="pun">,</span><span class="str">'连接错误:'</span><span class="pun">));</span><span class="pln">
    db</span><span class="pun">.</span><span class="pln">once</span><span class="pun">(</span><span class="str">'open'</span><span class="pun">,</span><span class="kwd">function</span><span class="pun">(){</span>
      <span class="com">//一次打开记录</span>
    <span class="pun">});</span></code></pre>
<strong>注意</strong>：

成功开启数据库后，就可以执行数据库相应操作，假设以下代码都在回调中处理

4.定义一个<code>Schema</code>
<pre class="prettyprint language-javascript"><code>    <span class="kwd">var</span> <span class="typ">PersonSchema</span> <span class="pun">=</span> <span class="kwd">new</span><span class="pln"> mongoose</span><span class="pun">.</span><span class="typ">Schema</span><span class="pun">({</span><span class="pln">
      name</span><span class="pun">:</span><span class="typ">String</span>   <span class="com">//定义一个属性name，类型为String</span>
    <span class="pun">});</span></code></pre>
5.将该<code>Schema</code>发布为<code>Model</code>
<pre class="prettyprint language-javascript"><code>    <span class="kwd">var</span> <span class="typ">PersonModel</span> <span class="pun">=</span><span class="pln"> db</span><span class="pun">.</span><span class="pln">model</span><span class="pun">(</span><span class="str">'Person'</span><span class="pun">,</span><span class="typ">PersonSchema</span><span class="pun">);</span>
    <span class="com">//如果该Model已经发布，则可以直接通过名字索引到，如下：</span>
    <span class="com">//var PersonModel = db.model('Person');</span>
    <span class="com">//如果没有发布，上一段代码将会异常</span></code></pre>
6.用<code>Model</code>创建<code>Entity</code>
<pre class="prettyprint language-javascript"><code>    <span class="kwd">var</span><span class="pln"> personEntity </span><span class="pun">=</span> <span class="kwd">new</span> <span class="typ">PersonModel</span><span class="pun">({</span><span class="pln">name</span><span class="pun">:</span><span class="str">'Krouky'</span><span class="pun">});</span>
    <span class="com">//打印这个实体的名字看看</span><span class="pln">
    console</span><span class="pun">.</span><span class="pln">log</span><span class="pun">(</span><span class="pln">personEntity</span><span class="pun">.</span><span class="pln">name</span><span class="pun">);</span> <span class="com">//Krouky</span></code></pre>
7.我们甚至可以为此<code>Schema</code>创建方法
<pre class="prettyprint language-javascript"><code>    <span class="com">//为Schema模型追加speak方法</span>
    <span class="typ">PersonSchema</span><span class="pun">.</span><span class="pln">methos</span><span class="pun">.</span><span class="pln">speak </span><span class="pun">=</span> <span class="kwd">function</span><span class="pun">(){</span><span class="pln">
      console</span><span class="pun">.</span><span class="pln">log</span><span class="pun">(</span><span class="str">'我的名字叫'</span><span class="pun">+</span><span class="kwd">this</span><span class="pun">.</span><span class="pln">name</span><span class="pun">);</span>
    <span class="pun">}</span>
    <span class="kwd">var</span> <span class="typ">PersonModel</span> <span class="pun">=</span><span class="pln"> db</span><span class="pun">.</span><span class="pln">model</span><span class="pun">(</span><span class="str">'Person'</span><span class="pun">,</span><span class="typ">PersonSchema</span><span class="pun">);</span>
    <span class="kwd">var</span><span class="pln"> personEntity </span><span class="pun">=</span> <span class="kwd">new</span> <span class="typ">PersonModel</span><span class="pun">({</span><span class="pln">name</span><span class="pun">:</span><span class="str">'Krouky'</span><span class="pun">});</span><span class="pln">
    personEntity</span><span class="pun">.</span><span class="pln">speak</span><span class="pun">();</span><span class="com">//我的名字叫Krouky</span></code></pre>
8.<code>Entity</code>是具有具体的数据库操作<code>CRUD</code>的
<pre class="prettyprint language-javascript"><code><span class="pln">    personEntity</span><span class="pun">.</span><span class="pln">save</span><span class="pun">();</span>  <span class="com">//执行完成后，数据库就有该数据了</span></code></pre>
9.如果要执行查询，需要依赖<code>Model</code>，当然<code>Entity</code>也是可以做到的
<pre class="prettyprint language-javascript"><code>    <span class="typ">PersonModel</span><span class="pun">.</span><span class="pln">find</span><span class="pun">(</span><span class="kwd">function</span><span class="pun">(</span><span class="pln">err</span><span class="pun">,</span><span class="pln">persons</span><span class="pun">){</span>
      <span class="com">//查询到的所有person</span>
    <span class="pun">});</span></code></pre>
<strong>注意</strong>：

1. 具体的如何配置<code>Schema</code>、<code>Model</code>以及<code>Model</code>和<code>Entity</code>的相关操作，我们会在后面进行

2. <code>Model</code>和<code>Entity</code>都有能影响数据库的操作，但仍有区别，后面我们也会做解释

##二、新手指引

<em>如果您还不清楚<code>Mongoose</code>是如何工作的，请参看第一章快速通道快速浏览他的用法吧</em>

###1. Schema——纯洁的数据库原型

####1.1 什么是Schema
<ul>
	<li>我理解<code>Schema</code>仅仅只是一断代码，他书写完成后程序依然无法使用，更无法通往数据库端</li>
	<li>他仅仅只是数据库模型在程序片段中的一种表现，或者是数据属性模型</li>
</ul>
####1.2 如何定义Schema
<pre class="prettyprint language-javascript"><code>    <span class="kwd">var</span> <span class="typ">BlogSchema</span> <span class="pun">=</span> <span class="kwd">new</span> <span class="typ">Schema</span><span class="pun">({</span><span class="pln">
      title</span><span class="pun">:</span><span class="typ">String</span><span class="pun">,</span><span class="pln">
      author</span><span class="pun">:</span><span class="typ">String</span>
      <span class="com">//new Schema()中传入一个JSON对象，该对象形如 xxx:yyyy ,</span>
      <span class="pun">/</span><span class="pln">xxx</span><span class="pun">是一个字符串，定义了属性，</span><span class="pln">yyy</span><span class="pun">是一个</span><span class="typ">Schema</span><span class="pun">.</span><span class="typ">Type</span><span class="pun">，定义了属性类型</span>
    <span class="pun">});</span></code></pre>
####1.3 什么是Schema.Type

<code>Schema.Type</code>是由<code>Mongoose</code>内定的一些数据类型，基本数据类型都在其中，他也内置了一些<code>Mongoose</code>特有的<code>Schema.Type</code>。当然，你也可以自定义<code>Schema.Type</code>，只有满足<code>Schema.Type</code>的类型才能定义在<code>Schema</code>内。

####1.4 Schema.Types

<code>NodeJS</code>中的基本数据类型都属于<code>Schema.Type</code>，另外<code>Mongoose</code>还定义了自己的类型
<pre class="prettyprint language-javascript"><code>    <span class="com">//举例：</span>
    <span class="kwd">var</span> <span class="typ">ExampleSchema</span> <span class="pun">=</span> <span class="kwd">new</span> <span class="typ">Schema</span><span class="pun">({</span><span class="pln">
      name</span><span class="pun">:</span><span class="typ">String</span><span class="pun">,</span><span class="pln">
      binary</span><span class="pun">:</span><span class="typ">Buffer</span><span class="pun">,</span><span class="pln">
      living</span><span class="pun">:</span><span class="typ">Boolean</span><span class="pun">,</span><span class="pln">
      updated</span><span class="pun">:</span><span class="typ">Date</span><span class="pun">,</span><span class="pln">
      age</span><span class="pun">:</span><span class="typ">Number</span><span class="pun">,</span><span class="pln">
      mixed</span><span class="pun">:</span><span class="typ">Schema</span><span class="pun">.</span><span class="typ">Types</span><span class="pun">.</span><span class="typ">Mixed</span><span class="pun">,</span> <span class="com">//该混合类型等同于nested</span><span class="pln">
      _id</span><span class="pun">:</span><span class="typ">Schema</span><span class="pun">.</span><span class="typ">Types</span><span class="pun">.</span><span class="typ">ObjectId</span><span class="pun">,</span>  <span class="com">//主键</span><span class="pln">
      _fk</span><span class="pun">:</span><span class="typ">Schema</span><span class="pun">.</span><span class="typ">Types</span><span class="pun">.</span><span class="typ">ObjectId</span><span class="pun">,</span>  <span class="com">//外键</span><span class="pln">
      array</span><span class="pun">:[],</span><span class="pln">
      arrOfString</span><span class="pun">:[</span><span class="typ">String</span><span class="pun">],</span><span class="pln">
      arrOfNumber</span><span class="pun">:[</span><span class="typ">Number</span><span class="pun">],</span><span class="pln">
      arrOfDate</span><span class="pun">:[</span><span class="typ">Date</span><span class="pun">],</span><span class="pln">
      arrOfBuffer</span><span class="pun">:[</span><span class="typ">Buffer</span><span class="pun">],</span><span class="pln">
      arrOfBoolean</span><span class="pun">:[</span><span class="typ">Boolean</span><span class="pun">],</span><span class="pln">
      arrOfMixed</span><span class="pun">:[</span><span class="typ">Schema</span><span class="pun">.</span><span class="typ">Types</span><span class="pun">.</span><span class="typ">Mixed</span><span class="pun">],</span><span class="pln">
      arrOfObjectId</span><span class="pun">:[</span><span class="typ">Schema</span><span class="pun">.</span><span class="typ">Types</span><span class="pun">.</span><span class="typ">ObjectId</span><span class="pun">]</span><span class="pln">
      nested</span><span class="pun">:{</span><span class="pln">
        stuff</span><span class="pun">:</span><span class="typ">String</span><span class="pun">,</span>
      <span class="pun">}</span>
    <span class="pun">});</span></code></pre>
####1.5 关于Buffer

<code>Buffer</code>和<code>ArrayBuffer</code>是<code>Nodejs</code>两种隐藏的对象，相关内容请查看<code>NodeJS-API</code>

####1.6 关于Mixed

<code>Schema.Types.Mixed</code>是<code>Mongoose</code>定义个混合类型，该混合类型如果未定义具体形式。因此,如果定义具体内容，就直接使用<code>{}</code>来定义，以下两句等价
<pre class="prettyprint language-javascript"><code>    <span class="kwd">var</span> <span class="typ">AnySchema</span> <span class="pun">=</span> <span class="kwd">new</span> <span class="typ">Schema</span><span class="pun">({</span><span class="pln">any</span><span class="pun">:{}});</span>
    <span class="kwd">var</span> <span class="typ">AnySchema</span> <span class="pun">=</span> <span class="kwd">new</span> <span class="typ">Schema</span><span class="pun">({</span><span class="pln">any</span><span class="pun">:</span><span class="typ">Schema</span><span class="pun">.</span><span class="typ">Types</span><span class="pun">.</span><span class="typ">Mixed</span><span class="pun">});</span></code></pre>
混合类型因为没有特定约束，因此可以任意修改，一旦修改了原型，则必须调用<code>markModified()</code>
<pre class="prettyprint language-javascript"><code><span class="pln">    person</span><span class="pun">.</span><span class="pln">anything </span><span class="pun">=</span> <span class="pun">{</span><span class="pln">x</span><span class="pun">:[</span><span class="lit">3</span><span class="pun">,</span><span class="lit">4</span><span class="pun">,{</span><span class="pln">y</span><span class="pun">:</span><span class="str">'change'</span><span class="pun">}]}</span><span class="pln">
    person</span><span class="pun">.</span><span class="pln">markModified</span><span class="pun">(</span><span class="str">'anything'</span><span class="pun">);</span><span class="com">//传入anything，表示该属性类型发生变化</span><span class="pln">
    person</span><span class="pun">.</span><span class="pln">save</span><span class="pun">();</span></code></pre>
####1.7 关于ObjectId

主键，一种特殊而且非常重要的类型，每个<code>Schema</code>都会默认配置这个属性，属性名为<code>_id</code>，除非自己定义，方可覆盖
<pre class="prettyprint language-javascript"><code>    <span class="kwd">var</span><span class="pln"> mongoose </span><span class="pun">=</span> <span class="kwd">require</span><span class="pun">(</span><span class="str">'mongoose'</span><span class="pun">);</span>
    <span class="kwd">var</span> <span class="typ">ObjectId</span> <span class="pun">=</span><span class="pln"> mongoose</span><span class="pun">.</span><span class="typ">Schema</span><span class="pun">.</span><span class="typ">Types</span><span class="pun">.</span><span class="typ">ObjectId</span><span class="pun">;</span>
    <span class="kwd">var</span> <span class="typ">StudentSchema</span> <span class="pun">=</span> <span class="kwd">new</span> <span class="typ">Schema</span><span class="pun">({});</span> <span class="com">//默认会有_id:ObjectId</span>
    <span class="kwd">var</span> <span class="typ">TeacherSchema</span> <span class="pun">=</span> <span class="kwd">new</span> <span class="typ">Schema</span><span class="pun">({</span><span class="pln">id</span><span class="pun">:</span><span class="typ">ObjectId</span><span class="pun">});</span><span class="com">//只有id:ObjectId</span></code></pre>
该类型的值由系统自己生成，从某种意义上几乎不会重复，生成过程比较复杂，有兴趣的朋友可以查看源码。

####1.8 关于Array

<code>Array</code>在<code>JavaScript</code>编程语言中并不是数组，而是集合，因此里面可以存入不同的值，以下代码等价：
<pre class="prettyprint language-javascript"><code>    <span class="kwd">var</span> <span class="typ">ExampleSchema1</span> <span class="pun">=</span> <span class="kwd">new</span> <span class="typ">Schema</span><span class="pun">({</span><span class="pln">array</span><span class="pun">:[]});</span>
    <span class="kwd">var</span> <span class="typ">ExampleSchema2</span> <span class="pun">=</span> <span class="kwd">new</span> <span class="typ">Schema</span><span class="pun">({</span><span class="pln">array</span><span class="pun">:</span><span class="typ">Array</span><span class="pun">});</span>
    <span class="kwd">var</span> <span class="typ">ExampleSchema3</span> <span class="pun">=</span> <span class="kwd">new</span> <span class="typ">Schema</span><span class="pun">({</span><span class="pln">array</span><span class="pun">:[</span><span class="typ">Schema</span><span class="pun">.</span><span class="typ">Types</span><span class="pun">.</span><span class="typ">Mixed</span><span class="pun">]});</span>
    <span class="kwd">var</span> <span class="typ">ExampleSchema4</span> <span class="pun">=</span> <span class="kwd">new</span> <span class="typ">Schema</span><span class="pun">({</span><span class="pln">array</span><span class="pun">:[{}]});</span></code></pre>
####1.9 附言

<code>Schema</code>不仅定义了<code>文档结构</code>和<code>使用性能</code>，还可以有<code>扩展插件</code>、<code>实例方法</code>、<code>静态方法</code>、<code>复合索引</code>、<code>文档生命周期钩子</code>

<code>Schema</code>可以定义插件，并且插件具有良好的可拔插性，请有兴趣的读者继续往后阅读或者查阅官方资料。

###2. Schema的扩展

####2.1 实例方法

有的时候，我们创造的<code>Schema</code>不仅要为后面的<code>Model</code>和<code>Entity</code>提供公共的属性，还要提供公共的方法。

下面例子比快速通道的例子更加高级，可以进行高级扩展：
<pre class="prettyprint language-javascript"><code>    <span class="kwd">var</span> <span class="typ">PersonSchema</span> <span class="pun">=</span> <span class="kwd">new</span> <span class="typ">Schema</span><span class="pun">({</span><span class="pln">name</span><span class="pun">:</span><span class="typ">String</span><span class="pun">,</span><span class="pln">type</span><span class="pun">:</span><span class="typ">String</span><span class="pun">});</span>
    <span class="com">//查询类似数据</span>
    <span class="typ">PersonSchema</span><span class="pun">.</span><span class="pln">methods</span><span class="pun">.</span><span class="pln">findSimilarTypes </span><span class="pun">=</span> <span class="kwd">function</span><span class="pun">(</span><span class="pln">cb</span><span class="pun">){</span>
      <span class="kwd">return</span> <span class="kwd">this</span><span class="pun">.</span><span class="pln">model</span><span class="pun">(</span><span class="str">'Person'</span><span class="pun">).</span><span class="pln">find</span><span class="pun">({</span><span class="pln">type</span><span class="pun">:</span><span class="kwd">this</span><span class="pun">.</span><span class="pln">type</span><span class="pun">},</span><span class="pln">cb</span><span class="pun">);</span>
    <span class="pun">}</span></code></pre>
使用如下：
<pre class="prettyprint language-javascript"><code>    <span class="kwd">var</span> <span class="typ">PersonModel</span> <span class="pun">=</span><span class="pln"> mongoose</span><span class="pun">.</span><span class="pln">model</span><span class="pun">(</span><span class="str">'Person'</span><span class="pun">,</span><span class="typ">PersonSchema</span><span class="pun">);</span>
    <span class="kwd">var</span><span class="pln"> krouky </span><span class="pun">=</span> <span class="kwd">new</span> <span class="typ">PersonSchema</span><span class="pun">({</span><span class="pln">name</span><span class="pun">:</span><span class="str">'krouky'</span><span class="pun">,</span><span class="pln">type</span><span class="pun">:</span><span class="str">'前端工程师'</span><span class="pun">});</span><span class="pln">
    krouky</span><span class="pun">.</span><span class="pln">findSimilarTypes</span><span class="pun">(</span><span class="kwd">function</span><span class="pun">(</span><span class="pln">err</span><span class="pun">,</span><span class="pln">persons</span><span class="pun">){</span>
      <span class="com">//persons中就能查询到其他前端工程师</span>
    <span class="pun">});</span></code></pre>
####2.2 静态方法

静态方法在<code>Model</code>层就能使用，如下：
<pre class="prettyprint language-javascript"><code>  <span class="typ">PersonSchema</span><span class="pun">.</span><span class="pln">statics</span><span class="pun">.</span><span class="pln">findByName </span><span class="pun">=</span> <span class="kwd">function</span><span class="pun">(</span><span class="pln">name</span><span class="pun">,</span><span class="pln">cb</span><span class="pun">){</span>
    <span class="kwd">this</span><span class="pun">.</span><span class="pln">find</span><span class="pun">({</span><span class="pln">name</span><span class="pun">:</span><span class="kwd">new</span> <span class="typ">RegExp</span><span class="pun">(</span><span class="pln">name</span><span class="pun">,</span><span class="str">'i'</span><span class="pun">),</span><span class="pln">cb</span><span class="pun">});</span>
  <span class="pun">}</span>
  <span class="kwd">var</span> <span class="typ">PersonModel</span> <span class="pun">=</span><span class="pln"> mongoose</span><span class="pun">.</span><span class="pln">model</span><span class="pun">(</span><span class="str">'Person'</span><span class="pun">,</span><span class="typ">PersonSchema</span><span class="pun">);</span>
  <span class="typ">PersonModel</span><span class="pun">.</span><span class="pln">findByName</span><span class="pun">(</span><span class="str">'krouky'</span><span class="pun">,</span><span class="kwd">function</span><span class="pun">(</span><span class="pln">err</span><span class="pun">,</span><span class="pln">persons</span><span class="pun">){</span>
    <span class="com">//找到所有名字叫krouky的人</span>
  <span class="pun">});</span></code></pre>
####2.3 索引

索引或者复合索引能让搜索更加高效，默认索引就是主键索引<code>ObjectId</code>，属性名为<code>_id</code>， <em>索引会作为一个专题来讲解</em>

####2.4 虚拟属性

<code>Schema</code>中如果定义了虚拟属性，那么该属性将不写入数据库，例如：
<pre class="prettyprint language-javascript"><code>    <span class="kwd">var</span> <span class="typ">PersonSchema</span> <span class="pun">=</span> <span class="kwd">new</span> <span class="typ">Schema</span><span class="pun">({</span><span class="pln">
      name</span><span class="pun">:{</span><span class="pln">
        first</span><span class="pun">:</span><span class="typ">String</span><span class="pun">,</span>
        <span class="kwd">last</span><span class="pun">:</span><span class="typ">String</span>
      <span class="pun">}</span>
    <span class="pun">});</span>
    <span class="kwd">var</span> <span class="typ">PersonModel</span> <span class="pun">=</span><span class="pln"> mongoose</span><span class="pun">.</span><span class="pln">model</span><span class="pun">(</span><span class="str">'Person'</span><span class="pun">,</span><span class="typ">PersonSchema</span><span class="pun">);</span>
    <span class="kwd">var</span><span class="pln"> krouky </span><span class="pun">=</span> <span class="kwd">new</span> <span class="typ">PersonModel</span><span class="pun">({</span><span class="pln">
      name</span><span class="pun">:{</span><span class="pln">first</span><span class="pun">:</span><span class="str">'krouky'</span><span class="pun">,</span><span class="kwd">last</span><span class="pun">:</span><span class="str">'han'</span><span class="pun">}</span>
    <span class="pun">});</span></code></pre>
如果每次想使用全名就得这样
<pre class="prettyprint language-javascript"><code><span class="pln">    console</span><span class="pun">.</span><span class="pln">log</span><span class="pun">(</span><span class="pln">krouky</span><span class="pun">.</span><span class="pln">name</span><span class="pun">.</span><span class="pln">first </span><span class="pun">+</span> <span class="str">' '</span> <span class="pun">+</span><span class="pln"> krouky</span><span class="pun">.</span><span class="pln">name</span><span class="pun">.</span><span class="kwd">last</span><span class="pun">);</span></code></pre>
显然这是很麻烦的，我们可以定义<code>虚拟属性</code>：
<pre class="prettyprint language-javascript"><code>    <span class="typ">PersonSchema</span><span class="pun">.</span><span class="kwd">virtual</span><span class="pun">(</span><span class="str">'name.full'</span><span class="pun">).</span><span class="kwd">get</span><span class="pun">(</span><span class="kwd">function</span><span class="pun">(){</span>
      <span class="kwd">return</span> <span class="kwd">this</span><span class="pun">.</span><span class="pln">name</span><span class="pun">.</span><span class="pln">first </span><span class="pun">+</span> <span class="str">' '</span> <span class="pun">+</span> <span class="kwd">this</span><span class="pun">.</span><span class="pln">name</span><span class="pun">.</span><span class="kwd">last</span><span class="pun">;</span>
    <span class="pun">});</span></code></pre>
那么就能用<code>krouky.name.full</code>来调用全名了，反之如果知道full，也可以反解<code>first</code>和<code>last</code>属性
<pre class="prettyprint language-javascript"><code>    <span class="typ">PersonSchema</span><span class="pun">.</span><span class="kwd">virtual</span><span class="pun">(</span><span class="str">'name.full'</span><span class="pun">).</span><span class="kwd">set</span><span class="pun">(</span><span class="kwd">function</span><span class="pun">(</span><span class="pln">name</span><span class="pun">){</span>
      <span class="kwd">var</span><span class="pln"> split </span><span class="pun">=</span><span class="pln"> name</span><span class="pun">.</span><span class="pln">split</span><span class="pun">(</span><span class="str">' '</span><span class="pun">);</span>
      <span class="kwd">this</span><span class="pun">.</span><span class="pln">name</span><span class="pun">.</span><span class="pln">first </span><span class="pun">=</span><span class="pln"> split</span><span class="pun">[</span><span class="lit">0</span><span class="pun">];</span>
      <span class="kwd">this</span><span class="pun">.</span><span class="pln">name</span><span class="pun">.</span><span class="kwd">last</span> <span class="pun">=</span><span class="pln"> split</span><span class="pun">[</span><span class="lit">1</span><span class="pun">];</span>
    <span class="pun">});</span>
    <span class="kwd">var</span> <span class="typ">PersonModel</span> <span class="pun">=</span><span class="pln"> mongoose</span><span class="pun">.</span><span class="pln">model</span><span class="pun">(</span><span class="str">'Person'</span><span class="pun">,</span><span class="typ">PersonSchema</span><span class="pun">);</span>
    <span class="kwd">var</span><span class="pln"> krouky </span><span class="pun">=</span> <span class="kwd">new</span> <span class="typ">PersonModel</span><span class="pun">({});</span><span class="pln">
    krouky</span><span class="pun">.</span><span class="pln">name</span><span class="pun">.</span><span class="pln">full </span><span class="pun">=</span> <span class="str">'krouky han'</span><span class="pun">;</span><span class="com">//会被自动分解</span><span class="pln">
    console</span><span class="pun">.</span><span class="pln">log</span><span class="pun">(</span><span class="pln">krouky</span><span class="pun">.</span><span class="pln">name</span><span class="pun">.</span><span class="pln">first</span><span class="pun">);</span><span class="com">//krouky</span></code></pre>
####2.5 配置项

在使用<code>new Schema(config)</code>时，我们可以追加一个参数<code>options</code>来配置<code>Schema</code>的配置，形如：
<pre class="prettyprint language-javascript"><code>    <span class="kwd">var</span> <span class="typ">ExampleSchema</span> <span class="pun">=</span> <span class="kwd">new</span> <span class="typ">Schema</span><span class="pun">(</span><span class="pln">config</span><span class="pun">,</span><span class="pln">options</span><span class="pun">);</span></code></pre>
或者使用
<pre class="prettyprint language-javascript"><code>    <span class="kwd">var</span> <span class="typ">ExampleSchema</span> <span class="pun">=</span> <span class="kwd">new</span> <span class="typ">Schema</span><span class="pun">(</span><span class="pln">config</span><span class="pun">);</span>
    <span class="typ">ExampleSchema</span><span class="pun">.</span><span class="kwd">set</span><span class="pun">(</span><span class="pln">option</span><span class="pun">,</span><span class="pln">value</span><span class="pun">);</span></code></pre>
可供配置项有：<code>safe</code>、<code>strict</code>、<code>capped</code>、<code>versionKey</code>、<code>autoIndex</code>

#####2.5.1 safe——安全属性（默认安全）

一般可做如下配置：
<pre class="prettyprint language-javascript"><code>    <span class="kwd">new</span> <span class="typ">Schema</span><span class="pun">({...},{</span><span class="pln">safe</span><span class="pun">:</span><span class="kwd">true</span><span class="pun">});</span></code></pre>
当然我们也可以这样
<pre class="prettyprint language-javascript"><code>    <span class="kwd">new</span> <span class="typ">Schema</span><span class="pun">({...},{</span><span class="pln">safe</span><span class="pun">:{</span><span class="pln">j</span><span class="pun">:</span><span class="lit">1</span><span class="pun">,</span><span class="pln">w</span><span class="pun">:</span><span class="lit">2</span><span class="pun">,</span><span class="pln">wtimeout</span><span class="pun">:</span><span class="lit">10000</span><span class="pun">}});</span></code></pre>
<code>j</code>表示做1份日志，<code>w</code>表示做2个副本（尚不明确），超时时间10秒

#####2.5.2 strict——严格配置（默认启用）

确保<code>Entity</code>的值存入数据库前会被自动验证，如果你没有充足的理由，请不要停用，例子：
<pre class="prettyprint language-javascript"><code>    <span class="kwd">var</span> <span class="typ">ThingSchema</span> <span class="pun">=</span> <span class="kwd">new</span> <span class="typ">Schema</span><span class="pun">({</span><span class="pln">a</span><span class="pun">:</span><span class="typ">String</span><span class="pun">});</span>
    <span class="kwd">var</span> <span class="typ">ThingModel</span> <span class="pun">=</span><span class="pln"> db</span><span class="pun">.</span><span class="pln">model</span><span class="pun">(</span><span class="str">'Thing'</span><span class="pun">,</span><span class="typ">SchemaSchema</span><span class="pun">);</span>
    <span class="kwd">var</span><span class="pln"> thing </span><span class="pun">=</span> <span class="kwd">new</span> <span class="typ">Thing</span><span class="pun">({</span><span class="pln">iAmNotInTheThingSchema</span><span class="pun">:</span><span class="kwd">true</span><span class="pun">});</span><span class="pln">
    thing</span><span class="pun">.</span><span class="pln">save</span><span class="pun">();</span><span class="com">//iAmNotInTheThingSchema这个属性将无法被存储</span></code></pre>
如果取消严格选项，<code>iAmNotInTheThingSchema</code>将会被存入数据库

该选项也可以在构造实例时使用，例如：
<pre class="prettyprint language-javascript"><code>    <span class="kwd">var</span> <span class="typ">ThingModel</span> <span class="pun">=</span><span class="pln"> db</span><span class="pun">.</span><span class="pln">model</span><span class="pun">(</span><span class="str">'Thing'</span><span class="pun">);</span>
    <span class="kwd">var</span><span class="pln"> thing1 </span><span class="pun">=</span> <span class="kwd">new</span> <span class="typ">ThingModel</span><span class="pun">(</span><span class="pln">doc</span><span class="pun">,</span><span class="kwd">true</span><span class="pun">);</span>  <span class="com">//启用严格</span>
    <span class="kwd">var</span><span class="pln"> thing2 </span><span class="pun">=</span> <span class="kwd">new</span> <span class="typ">ThingModel</span><span class="pun">(</span><span class="pln">doc</span><span class="pun">,</span><span class="kwd">false</span><span class="pun">);</span> <span class="com">//禁用严格</span></code></pre>
<strong>注意：</strong>

<code>strict</code>也可以设置为<code>throw</code>，表示出现问题将会抛出错误

#####2.5.3 shardKey

需要<code>mongodb</code>做分布式，才会使用该属性

#####2.5.4 capped——上限设置

如果有数据库的批量操作，该属性能限制一次操作的量，例如：
<pre class="prettyprint language-javascript"><code>    <span class="kwd">new</span> <span class="typ">Schema</span><span class="pun">({...},{</span><span class="pln">capped</span><span class="pun">:</span><span class="lit">1024</span><span class="pun">});</span>  <span class="com">//一次操作上线1024条数据</span></code></pre>
当然该参数也可是JSON对象，包含size、max、autiIndexId属性
<pre class="prettyprint language-javascript"><code>    <span class="kwd">new</span> <span class="typ">Schema</span><span class="pun">({...},{</span><span class="pln">capped</span><span class="pun">:{</span><span class="pln">size</span><span class="pun">:</span><span class="lit">1024</span><span class="pun">,</span><span class="pln">max</span><span class="pun">:</span><span class="lit">100</span><span class="pun">,</span><span class="pln">autoIndexId</span><span class="pun">:</span><span class="kwd">true</span><span class="pun">}});</span></code></pre>
#####2.5.5 versionKey——版本锁

版本锁是<code>Mongoose</code>默认配置（__v属性）的，如果你想自己定制，如下：
<pre class="prettyprint language-javascript"><code>    <span class="kwd">new</span> <span class="typ">Schema</span><span class="pun">({...},{</span><span class="pln">versionKey</span><span class="pun">:</span><span class="str">'__someElse'</span><span class="pun">});</span></code></pre>
此时存入数据库的版本锁就不是<code>__v</code>属性，而是<code>__someElse</code>，相当于是给版本锁取名字。

具体怎么存入都是由<code>Mongoose</code>和<code>MongoDB</code>自己决定，当然，这个属性你也可以去除
<pre class="prettyprint language-javascript"><code>  <span class="kwd">new</span> <span class="typ">Schema</span><span class="pun">({...},{</span><span class="pln">versionKey</span><span class="pun">:</span><span class="kwd">false</span><span class="pun">});</span></code></pre>
除非你知道你在做什么，并且你知道这样做的后果

#####2.5.6 autoIndex——自动索引

<em>该内容将在索引章节单独讲解</em>

###3. Documents

<code>Document</code>是与<code>MongoDB</code>文档一一对应的模型，<code>Document</code>可等同于<code>Entity</code>，具有属性和操作性

<strong>注意：</strong>

<code>Document</code>的`CRUD都必须经过严格验证的，参看<strong>2.5.2 Schema的strict严格配置</strong>

####3.1 查询

查询内容过多，专题讲解

####3.2 更新

有许多方式来更新文件，以下是常用的传统方式：
<pre class="prettyprint language-javascript"><code>    <span class="typ">PersonModel</span><span class="pun">.</span><span class="pln">findById</span><span class="pun">(</span><span class="pln">id</span><span class="pun">,</span><span class="kwd">function</span><span class="pun">(</span><span class="pln">err</span><span class="pun">,</span><span class="pln">person</span><span class="pun">){</span><span class="pln">
      person</span><span class="pun">.</span><span class="pln">name </span><span class="pun">=</span> <span class="str">'MDragon'</span><span class="pun">;</span><span class="pln">
      person</span><span class="pun">.</span><span class="pln">save</span><span class="pun">(</span><span class="kwd">function</span><span class="pun">(</span><span class="pln">err</span><span class="pun">){});</span>
    <span class="pun">});</span></code></pre>
这里，利用<code>Model</code>模型查询到了<code>person</code>对象，该对象属于<code>Entity</code>，可以有<code>save操作，如果使用</code>Model`操作，需注意：
<pre class="prettyprint language-javascript"><code>    <span class="typ">PersonModel</span><span class="pun">.</span><span class="pln">findById</span><span class="pun">(</span><span class="pln">id</span><span class="pun">,</span><span class="kwd">function</span><span class="pun">(</span><span class="pln">err</span><span class="pun">,</span><span class="pln">person</span><span class="pun">){</span><span class="pln">
      person</span><span class="pun">.</span><span class="pln">name </span><span class="pun">=</span> <span class="str">'MDragon'</span><span class="pun">;</span>
      <span class="kwd">var</span><span class="pln"> _id </span><span class="pun">=</span><span class="pln"> person</span><span class="pun">.</span><span class="pln">_id</span><span class="pun">;</span> <span class="com">//需要取出主键_id</span>
      <span class="kwd">delete</span><span class="pln"> person</span><span class="pun">.</span><span class="pln">_id</span><span class="pun">;</span>    <span class="com">//再将其删除</span>
      <span class="typ">PersonModel</span><span class="pun">.</span><span class="pln">update</span><span class="pun">({</span><span class="pln">_id</span><span class="pun">:</span><span class="pln">_id</span><span class="pun">},</span><span class="pln">person</span><span class="pun">,</span><span class="kwd">function</span><span class="pun">(</span><span class="pln">err</span><span class="pun">){});</span>
      <span class="com">//此时才能用Model操作，否则报错</span>
    <span class="pun">});</span></code></pre>
<code>update</code>第一个参数是查询条件，第二个参数是更新的对象，但不能更新主键，这就是为什么要删除主键的原因。

当然这样的更新很麻烦，可以使用<code>$set</code>属性来配置，这样也不用先查询，如果更新的数据比较少，可用性还是很好的：
<pre class="prettyprint language-javascript"><code>    <span class="typ">PersonModel</span><span class="pun">.</span><span class="pln">update</span><span class="pun">({</span><span class="pln">_id</span><span class="pun">:</span><span class="pln">_id</span><span class="pun">},{</span><span class="pln">$set</span><span class="pun">:{</span><span class="pln">name</span><span class="pun">:</span><span class="str">'MDragon'</span><span class="pun">}},</span><span class="kwd">function</span><span class="pun">(</span><span class="pln">err</span><span class="pun">){});</span></code></pre>
需要注意，<code>Document</code>的<code>CRUD</code>操作都是异步执行，<code>callback</code>第一个参数必须是<code>err</code>，而第二个参数各个方法不一样，<code>update</code>的<code>callback</code>第二个参数是更新的数量，如果要返回更新后的对象，则要使用如下方法
<pre class="prettyprint language-javascript"><code>    <span class="typ">Person</span><span class="pun">.</span><span class="pln">findByIdAndUpdate</span><span class="pun">(</span><span class="pln">_id</span><span class="pun">,{</span><span class="pln">$set</span><span class="pun">:{</span><span class="pln">name</span><span class="pun">:</span><span class="str">'MDragon'</span><span class="pun">}},</span><span class="kwd">function</span><span class="pun">(</span><span class="pln">err</span><span class="pun">,</span><span class="pln">person</span><span class="pun">){</span><span class="pln">
      console</span><span class="pun">.</span><span class="pln">log</span><span class="pun">(</span><span class="pln">person</span><span class="pun">.</span><span class="pln">name</span><span class="pun">);</span> <span class="com">//MDragon</span>
    <span class="pun">});</span></code></pre>
类似的方法还有<code>findByIdAndRemove</code>，如同名字，只能根据id查询并作<code>update</code>/<code>remove</code>操作，操作的数据仅一条

####3.3 新增

如果是<code>Entity</code>，使用<code>save</code>方法，如果是<code>Model</code>，使用<code>create</code>方法
<pre class="prettyprint language-javascript"><code>    <span class="com">//使用Entity来增加一条数据</span>
    <span class="kwd">var</span><span class="pln"> krouky </span><span class="pun">=</span> <span class="kwd">new</span> <span class="typ">PersonModel</span><span class="pun">({</span><span class="pln">name</span><span class="pun">:</span><span class="str">'krouky'</span><span class="pun">});</span><span class="pln">
    krouky</span><span class="pun">.</span><span class="pln">save</span><span class="pun">(</span><span class="pln">callback</span><span class="pun">);</span>
    <span class="com">//使用Model来增加一条数据</span>
    <span class="kwd">var</span> <span class="typ">MDragon</span> <span class="pun">=</span> <span class="pun">{</span><span class="pln">name</span><span class="pun">:</span><span class="str">'MDragon'</span><span class="pun">};</span>
    <span class="typ">PersonModel</span><span class="pun">.</span><span class="pln">create</span><span class="pun">(</span><span class="typ">MDragon</span><span class="pun">,</span><span class="pln">callback</span><span class="pun">);</span></code></pre>
两种新增方法区别在于，如果使用<code>Model</code>新增时，传入的对象只能是纯净的<code>JSON</code>对象，不能是由<code>Model</code>创建的实体，原因是：由<code>Model</code>创建的实体<code>krouky</code>虽然打印是只有<code>{name:'krouky'}</code>，但是<code>krouky</code>属于<code>Entity</code>，包含有<code>Schema</code>属性和<code>Model</code>数据库行为模型。如果是使用<code>Model</code>创建的对象，传入时一定会将隐藏属性也存入数据库，虽然<code>3.x</code>追加了默认严格属性，但也不必要增加操作的报错

####3.4 删除

和新增一样，删除也有2种方式，但<code>Entity</code>和<code>Model</code>都使用<code>remove</code>方法

###4.Sub Docs

如同<code>SQL</code>数据库中2张表有主外关系，<code>Mongoose</code>将2个<code>Document</code>的嵌套叫做<code>Sub-Docs</code>（子文档）

简单的说就是一个<code>Document</code>嵌套另外一个<code>Document</code>或者<code>Documents</code>:
<pre class="prettyprint language-javascript"><code>    <span class="kwd">var</span> <span class="typ">ChildSchema1</span> <span class="pun">=</span> <span class="kwd">new</span> <span class="typ">Schema</span><span class="pun">({</span><span class="pln">name</span><span class="pun">:</span><span class="typ">String</span><span class="pun">});</span>
    <span class="kwd">var</span> <span class="typ">ChildSchema2</span> <span class="pun">=</span> <span class="kwd">new</span> <span class="typ">Schema</span><span class="pun">({</span><span class="pln">name</span><span class="pun">:</span><span class="typ">String</span><span class="pun">});</span>
    <span class="kwd">var</span> <span class="typ">ParentSchema</span> <span class="pun">=</span> <span class="kwd">new</span> <span class="typ">Schema</span><span class="pun">({</span><span class="pln">
      children1</span><span class="pun">:</span><span class="typ">ChildSchema1</span><span class="pun">,</span>   <span class="com">//嵌套Document</span><span class="pln">
      children2</span><span class="pun">:[</span><span class="typ">ChildSchema2</span><span class="pun">]</span>  <span class="com">//嵌套Documents</span>
    <span class="pun">});</span></code></pre>
<code>Sub-Docs</code>享受和<code>Documents</code>一样的操作，但是<code>Sub-Docs</code>的操作都由父类去执行
<pre class="prettyprint language-javascript"><code>    <span class="kwd">var</span> <span class="typ">ParentModel</span> <span class="pun">=</span><span class="pln"> db</span><span class="pun">.</span><span class="pln">model</span><span class="pun">(</span><span class="str">'Parent'</span><span class="pun">,</span><span class="pln">parentSchema</span><span class="pun">);</span>
    <span class="kwd">var</span><span class="pln"> parent </span><span class="pun">=</span> <span class="kwd">new</span> <span class="typ">ParentModel</span><span class="pun">({</span><span class="pln">
      children2</span><span class="pun">:[{</span><span class="pln">name</span><span class="pun">:</span><span class="str">'c1'</span><span class="pun">},{</span><span class="pln">name</span><span class="pun">:</span><span class="str">'c2'</span><span class="pun">}]</span>
    <span class="pun">});</span><span class="pln">
    parent</span><span class="pun">.</span><span class="pln">children2</span><span class="pun">[</span><span class="lit">0</span><span class="pun">].</span><span class="pln">name </span><span class="pun">=</span> <span class="str">'d'</span><span class="pun">;</span><span class="pln">
    parent</span><span class="pun">.</span><span class="pln">save</span><span class="pun">(</span><span class="pln">callback</span><span class="pun">);</span></code></pre>
<code>parent</code>在执行保存时，由于包含<code>children2</code>，他是一个数据库模型对象，因此会先保存<code>chilren2[0]</code>和<code>chilren2[1]</code>。

如果子文档在更新时出现错误，将直接报在父类文档中，可以这样处理：
<pre class="prettyprint language-javascript"><code>    <span class="typ">ChildrenSchema</span><span class="pun">.</span><span class="pln">pre</span><span class="pun">(</span><span class="str">'save'</span><span class="pun">,</span><span class="kwd">function</span><span class="pun">(</span><span class="kwd">next</span><span class="pun">){</span>
      <span class="kwd">if</span><span class="pun">(</span><span class="str">'x'</span> <span class="pun">===</span> <span class="kwd">this</span><span class="pun">.</span><span class="pln">name</span><span class="pun">)</span> <span class="kwd">return</span> <span class="kwd">next</span><span class="pun">(</span><span class="kwd">new</span> <span class="typ">Error</span><span class="pun">(</span><span class="str">'#err:not-x'</span><span class="pun">));</span>
      <span class="kwd">next</span><span class="pun">();</span>
    <span class="pun">});</span>
    <span class="kwd">var</span><span class="pln"> parent </span><span class="pun">=</span> <span class="kwd">new</span> <span class="typ">ParentModel</span><span class="pun">({</span><span class="pln">children1</span><span class="pun">:{</span><span class="pln">name</span><span class="pun">:</span><span class="str">'not-x'</span><span class="pun">}});</span><span class="pln">
    parent</span><span class="pun">.</span><span class="pln">save</span><span class="pun">(</span><span class="kwd">function</span><span class="pun">(</span><span class="pln">err</span><span class="pun">){</span><span class="pln">
      console</span><span class="pun">.</span><span class="pln">log</span><span class="pun">(</span><span class="pln">err</span><span class="pun">.</span><span class="pln">message</span><span class="pun">);</span> <span class="com">//#err:not-x</span>
    <span class="pun">});</span></code></pre>
####4.1 查询子文档

如果<code>children</code>是<code>parent</code>的子文档，可以通过如下方法查询到<code>children</code>
<pre class="prettyprint language-javascript"><code>    <span class="kwd">var</span><span class="pln"> child </span><span class="pun">=</span><span class="pln"> parent</span><span class="pun">.</span><span class="pln">children</span><span class="pun">.</span><span class="pln">id</span><span class="pun">(</span><span class="pln">id</span><span class="pun">);</span></code></pre>
####4.2 新增、删除、更新

子文档是父文档的一个属性，因此按照属性的操作即可，不同的是在新增父类的时候，子文档是会被先加入进去的。

如果<code>ChildrenSchema</code>是临时的一个子文档，不作为数据库映射集合，可以这样：
<pre class="prettyprint language-javascript"><code>    <span class="kwd">var</span> <span class="typ">ParentSchema</span> <span class="pun">=</span> <span class="kwd">new</span> <span class="typ">Schema</span><span class="pun">({</span><span class="pln">
      children</span><span class="pun">:{</span><span class="pln">
        name</span><span class="pun">:</span><span class="typ">String</span>
      <span class="pun">}</span>
    <span class="pun">});</span>
    <span class="com">//其实就是匿名混合模式</span></code></pre>
###5.Model

####5.1 什么是Model

<code>Model</code>模型，是经过<code>Schema</code>构造来的，除了<code>Schema</code>定义的数据库骨架以外，还具有数据库行为模型，他相当于管理数据库属性、行为的类

####5.2 如何创建Model

你必须通过<code>Schema</code>来创建，如下：
<pre class="prettyprint language-javascript"><code>    <span class="com">//先创建Schema</span>
    <span class="kwd">var</span> <span class="typ">TankSchema</span> <span class="pun">=</span> <span class="kwd">new</span> <span class="typ">Schema</span><span class="pun">({</span><span class="pln">
      name</span><span class="pun">:</span><span class="str">'String'</span><span class="pun">,</span><span class="pln">
      size</span><span class="pun">:</span><span class="str">'String'</span> 
    <span class="pun">});</span>
    <span class="com">//通过Schema创建Model</span>
    <span class="kwd">var</span> <span class="typ">TankModel</span> <span class="pun">=</span><span class="pln"> mongoose</span><span class="pun">.</span><span class="pln">model</span><span class="pun">(</span><span class="str">'Tank'</span><span class="pun">,</span><span class="typ">TankSchema</span><span class="pun">);</span></code></pre>
####5.2 操作Model

该模型就能直接拿来操作，具体查看<code>API</code>，例如：
<pre class="prettyprint language-javascript"><code>    <span class="kwd">var</span><span class="pln"> tank </span><span class="pun">=</span> <span class="pun">{</span><span class="str">'something'</span><span class="pun">,</span><span class="pln">size</span><span class="pun">:</span><span class="str">'small'</span><span class="pun">};</span>
    <span class="typ">TankModel</span><span class="pun">.</span><span class="pln">create</span><span class="pun">(</span><span class="pln">tank</span><span class="pun">);</span></code></pre>
<strong>注意：</strong>

你可以使用<code>Model</code>来创建<code>Entity</code>，<code>Entity</code>实体是一个特有<code>Model</code>具体对象，但是他并不具备<code>Model</code>的方法，只能用自己的方法。
<pre class="prettyprint language-javascript"><code>  <span class="com">//通过Model创建Entity</span>
  <span class="kwd">var</span><span class="pln"> tankEntity </span><span class="pun">=</span> <span class="kwd">new</span> <span class="typ">TankModel</span><span class="pun">(</span><span class="str">'someother'</span><span class="pun">,</span><span class="str">'size:big'</span><span class="pun">);</span><span class="pln">
  tankEntity</span><span class="pun">.</span><span class="pln">save</span><span class="pun">();</span></code></pre>
###6.Query

查询是数据库中运用最多也是最麻烦的地方，这里对<code>Query</code>解读的并不完善，仅仅是自己的一点领悟而已。

####6.1 查询的方式

通常有2种查询方式，一种是<code>直接查询</code>，一种是<code>链式查询</code>（2种查询都是自己命名的）

#####6.1.1 直接查询

在查询时带有回调函数的，称之为直接查询，查询的条件往往通过<code>API</code>来设定，例如：
<pre class="prettyprint language-javascript"><code>    <span class="typ">PersonModel</span><span class="pun">.</span><span class="pln">findOne</span><span class="pun">({</span><span class="str">'name.last'</span><span class="pun">:</span><span class="str">'dragon'</span><span class="pun">},</span><span class="str">'some select'</span><span class="pun">,</span><span class="kwd">function</span><span class="pun">(</span><span class="pln">err</span><span class="pun">,</span><span class="pln">person</span><span class="pun">){</span>
      <span class="com">//如果err==null，则person就能取到数据</span>
    <span class="pun">});</span></code></pre>
具体的查询参数，请查询<code>API</code>

#####6.1.2 链式查询

在查询时候，不带回调，而查询条件通过<code>API</code>函数来制定，例如：
<pre class="prettyprint language-javascript"><code>    <span class="kwd">var</span><span class="pln"> query </span><span class="pun">=</span> <span class="typ">PersonModel</span><span class="pun">.</span><span class="pln">findOne</span><span class="pun">({</span><span class="str">'name.last'</span><span class="pun">:</span><span class="str">'dragon'</span><span class="pun">});</span><span class="pln">
    query</span><span class="pun">.</span><span class="kwd">select</span><span class="pun">(</span><span class="str">'some select'</span><span class="pun">);</span><span class="pln">
    query</span><span class="pun">.</span><span class="kwd">exec</span><span class="pun">(</span><span class="kwd">function</span><span class="pun">(</span><span class="pln">err</span><span class="pun">,</span><span class="pln">pserson</span><span class="pun">){</span>
    <span class="com">//如果err==null，则person就能取到数据</span>
  <span class="pun">});</span></code></pre>
这种方式相对直接查询，分的比较明细，如果不带<code>callback</code>，则返回<code>query</code>，<code>query</code>没有执行的预编译查询语句，该<code>query</code>对象执行的方法都将返回自己，只有在执行<code>exec</code>方法时才执行查询，而且必须有回调。

因为<code>query</code>的操作始终返回自身，我们可以采用更形象的链式写法
<pre class="prettyprint language-javascript"><code>    <span class="typ">Person</span>
      <span class="pun">.</span><span class="pln">find</span><span class="pun">({</span><span class="pln"> occupation</span><span class="pun">:</span> <span class="str">/host/</span> <span class="pun">})</span>
      <span class="pun">.</span><span class="kwd">where</span><span class="pun">(</span><span class="str">'name.last'</span><span class="pun">).</span><span class="pln">equals</span><span class="pun">(</span><span class="str">'Ghost'</span><span class="pun">)</span>
      <span class="pun">.</span><span class="kwd">where</span><span class="pun">(</span><span class="str">'age'</span><span class="pun">).</span><span class="pln">gt</span><span class="pun">(</span><span class="lit">17</span><span class="pun">).</span><span class="pln">lt</span><span class="pun">(</span><span class="lit">66</span><span class="pun">)</span>
      <span class="pun">.</span><span class="kwd">where</span><span class="pun">(</span><span class="str">'likes'</span><span class="pun">).</span><span class="kwd">in</span><span class="pun">([</span><span class="str">'vaporizing'</span><span class="pun">,</span> <span class="str">'talking'</span><span class="pun">])</span>
      <span class="pun">.</span><span class="pln">limit</span><span class="pun">(</span><span class="lit">10</span><span class="pun">)</span>
      <span class="pun">.</span><span class="pln">sort</span><span class="pun">(</span><span class="str">'-occupation'</span><span class="pun">)</span>
      <span class="pun">.</span><span class="kwd">select</span><span class="pun">(</span><span class="str">'name occupation'</span><span class="pun">)</span>
      <span class="pun">.</span><span class="kwd">exec</span><span class="pun">(</span><span class="pln">callback</span><span class="pun">);</span></code></pre>
###7.Validation

数据的存储是需要验证的，不是什么数据都能往数据库里丢或者显示到客户端的，数据的验证需要记住以下规则：
<ul>
	<li>验证始终定义在<code>SchemaType</code>中</li>
	<li>验证是一个内部中间件</li>
	<li>验证是在一个<code>Document</code>被保存时默认启用的，除非你关闭验证</li>
	<li>验证是异步递归的，如果你的<code>SubDoc</code>验证失败，<code>Document</code>也将无法保存</li>
	<li>验证并不关心错误类型，而通过<code>ValidationError</code>这个对象可以访问</li>
</ul>
####7.1 验证器
<ol>
	<li><code>required</code> 非空验证</li>
	<li><code>min</code>/<code>max</code> 范围验证（边值验证）</li>
	<li><code>enum</code>/<code>match</code> 枚举验证/匹配验证</li>
	<li><code>validate</code> 自定义验证规则</li>
</ol>
以下是综合案例：
<pre class="prettyprint language-javascript"><code>    <span class="kwd">var</span> <span class="typ">PersonSchema</span> <span class="pun">=</span> <span class="kwd">new</span> <span class="typ">Schema</span><span class="pun">({</span><span class="pln">
      name</span><span class="pun">:{</span><span class="pln">
        type</span><span class="pun">:</span><span class="str">'String'</span><span class="pun">,</span><span class="pln">
        required</span><span class="pun">:</span><span class="kwd">true</span> <span class="com">//姓名非空</span>
      <span class="pun">},</span><span class="pln">
      age</span><span class="pun">:{</span><span class="pln">
        type</span><span class="pun">:</span><span class="str">'Nunmer'</span><span class="pun">,</span><span class="pln">
        min</span><span class="pun">:</span><span class="lit">18</span><span class="pun">,</span>       <span class="com">//年龄最小18</span><span class="pln">
        max</span><span class="pun">:</span><span class="lit">120</span>     <span class="com">//年龄最大120</span>
      <span class="pun">},</span><span class="pln">
      city</span><span class="pun">:{</span><span class="pln">
        type</span><span class="pun">:</span><span class="str">'String'</span><span class="pun">,</span>
        <span class="kwd">enum</span><span class="pun">:[</span><span class="str">'北京'</span><span class="pun">,</span><span class="str">'上海'</span><span class="pun">]</span>  <span class="com">//只能是北京、上海人</span>
      <span class="pun">},</span><span class="pln">
      other</span><span class="pun">:{</span><span class="pln">
        type</span><span class="pun">:</span><span class="str">'String'</span><span class="pun">,</span><span class="pln">
        validate</span><span class="pun">:[</span><span class="pln">validator</span><span class="pun">,</span><span class="pln">err</span><span class="pun">]</span>  <span class="com">//validator是一个验证函数，err是验证失败的错误信息</span>
      <span class="pun">}</span>
    <span class="pun">});</span></code></pre>
####7.2 验证失败

如果验证失败，则会返回<code>err</code>信息，<code>err</code>是一个对象该对象属性如下
<pre class="prettyprint language-javascript"><code><span class="pln">    err</span><span class="pun">.</span><span class="pln">errors                </span><span class="com">//错误集合（对象）</span><span class="pln">
    err</span><span class="pun">.</span><span class="pln">errors</span><span class="pun">.</span><span class="pln">color          </span><span class="com">//错误属性(Schema的color属性)</span><span class="pln">
    err</span><span class="pun">.</span><span class="pln">errors</span><span class="pun">.</span><span class="pln">color</span><span class="pun">.</span><span class="pln">message  </span><span class="com">//错误属性信息</span><span class="pln">
    err</span><span class="pun">.</span><span class="pln">errors</span><span class="pun">.</span><span class="pln">path             </span><span class="com">//错误属性路径</span><span class="pln">
    err</span><span class="pun">.</span><span class="pln">errors</span><span class="pun">.</span><span class="pln">type             </span><span class="com">//错误类型</span><span class="pln">
    err</span><span class="pun">.</span><span class="pln">name                </span><span class="com">//错误名称</span><span class="pln">
    err</span><span class="pun">.</span><span class="pln">message                 </span><span class="com">//错误消息</span></code></pre>
一旦验证失败，<code>Model</code>和<code>Entity</code>都将具有和<code>err</code>一样的<code>errors</code>属性

###8.Middleware中间件

####8.1 什么是中间件

中间件是一种控制函数，类似插件，能控制流程中的<code>init</code>、validate<code>、</code>save<code>、</code>remove`方法

####8.2 中间件的分类

中间件分为两类

#####8.2.1 Serial串行

串行使用<code>pre</code>方法，执行下一个方法使用<code>next</code>调用
<pre class="prettyprint language-javascript"><code>    <span class="kwd">var</span><span class="pln"> schema </span><span class="pun">=</span> <span class="kwd">new</span> <span class="typ">Schema</span><span class="pun">(...);</span><span class="pln">
    schema</span><span class="pun">.</span><span class="pln">pre</span><span class="pun">(</span><span class="str">'save'</span><span class="pun">,</span><span class="kwd">function</span><span class="pun">(</span><span class="kwd">next</span><span class="pun">){</span>
      <span class="com">//做点什么</span>
      <span class="kwd">next</span><span class="pun">();</span>
    <span class="pun">});</span></code></pre>
#####8.2.2 Parallel并行

并行提供更细粒度的操作
<pre class="prettyprint language-javascript"><code>    <span class="kwd">var</span><span class="pln"> schema </span><span class="pun">=</span> <span class="kwd">new</span> <span class="typ">Schema</span><span class="pun">(...);</span><span class="pln">
    schema</span><span class="pun">.</span><span class="pln">pre</span><span class="pun">(</span><span class="str">'save'</span><span class="pun">,</span><span class="kwd">function</span><span class="pun">(</span><span class="kwd">next</span><span class="pun">,</span><span class="kwd">done</span><span class="pun">){</span>
      <span class="com">//下一个要执行的中间件并行执行</span>
      <span class="kwd">next</span><span class="pun">();</span><span class="pln">
      doAsync</span><span class="pun">(</span><span class="kwd">done</span><span class="pun">);</span>
    <span class="pun">});</span></code></pre>
####8.3 中间件特点

一旦定义了中间件，就会在全部中间件执行完后执行其他操作，使用中间件可以雾化模型，避免异步操作的层层迭代嵌套

####8.4 使用范畴
<ol>
	<li>复杂的验证</li>
	<li>删除有主外关联的<code>doc</code></li>
	<li>异步默认</li>
	<li>某个特定动作触发异步任务，例如触发自定义事件和通知</li>
</ol>
例如，可以用来做自定义错误处理
<pre class="prettyprint language-javascript"><code><span class="pln">    schema</span><span class="pun">.</span><span class="pln">pre</span><span class="pun">(</span><span class="str">'save'</span><span class="pun">,</span><span class="kwd">function</span><span class="pun">(</span><span class="kwd">next</span><span class="pun">){</span>
      <span class="kwd">var</span><span class="pln"> err </span><span class="pun">=</span> <span class="kwd">new</span> <span class="typ">Eerror</span><span class="pun">(</span><span class="str">'some err'</span><span class="pun">);</span>
      <span class="kwd">next</span><span class="pun">(</span><span class="pln">err</span><span class="pun">);</span>
    <span class="pun">});</span><span class="pln">
    entity</span><span class="pun">.</span><span class="pln">save</span><span class="pun">(</span><span class="kwd">function</span><span class="pun">(</span><span class="pln">err</span><span class="pun">){</span><span class="pln">
      console</span><span class="pun">.</span><span class="pln">log</span><span class="pun">(</span><span class="pln">err</span><span class="pun">.</span><span class="pln">message</span><span class="pun">);</span> <span class="com">//some err</span>
    <span class="pun">});</span></code></pre>
<pre class="prettyprint language-js"><code><span class="com">// mongoose 链接</span> <span class="kwd">var</span><span class="pln"> mongoose </span><span class="pun">=</span><span class="pln"> require</span><span class="pun">(</span><span class="str">'mongoose'</span><span class="pun">);</span> <span class="kwd">var</span><span class="pln"> db </span><span class="pun">=</span><span class="pln"> mongoose</span><span class="pun">.</span><span class="pln">createConnection</span><span class="pun">(</span><span class="str">'mongodb://127.0.0.1:27017/NodeJS'</span><span class="pun">);</span> </code></pre>
<pre class="prettyprint language-js"><code><span class="com">// 链接错误</span><span class="pln">
db</span><span class="pun">.</span><span class="pln">on</span><span class="pun">(</span><span class="str">'error'</span><span class="pun">,</span> <span class="kwd">function</span><span class="pun">(</span><span class="pln">error</span><span class="pun">)</span> <span class="pun">{</span><span class="pln">
    console</span><span class="pun">.</span><span class="pln">log</span><span class="pun">(</span><span class="pln">error</span><span class="pun">);</span>
<span class="pun">});</span></code></pre>
<pre class="prettyprint language-js"><code><span class="com">// Schema 结构</span>
<span class="kwd">var</span><span class="pln"> mongooseSchema </span><span class="pun">=</span> <span class="kwd">new</span><span class="pln"> mongoose</span><span class="pun">.</span><span class="typ">Schema</span><span class="pun">({</span><span class="pln">
    username </span><span class="pun">:</span> <span class="pun">{</span><span class="pln">type </span><span class="pun">:</span> <span class="typ">String</span><span class="pun">,</span> <span class="kwd">default</span> <span class="pun">:</span> <span class="str">'匿名用户'</span><span class="pun">},</span><span class="pln">
    title    </span><span class="pun">:</span> <span class="pun">{</span><span class="pln">type </span><span class="pun">:</span> <span class="typ">String</span><span class="pun">},</span><span class="pln">
    content  </span><span class="pun">:</span> <span class="pun">{</span><span class="pln">type </span><span class="pun">:</span> <span class="typ">String</span><span class="pun">},</span><span class="pln">
    time     </span><span class="pun">:</span> <span class="pun">{</span><span class="pln">type </span><span class="pun">:</span> <span class="typ">Date</span><span class="pun">,</span> <span class="kwd">default</span><span class="pun">:</span> <span class="typ">Date</span><span class="pun">.</span><span class="pln">now</span><span class="pun">},</span><span class="pln">
    age      </span><span class="pun">:</span> <span class="pun">{</span><span class="pln">type </span><span class="pun">:</span> <span class="typ">Number</span><span class="pun">}</span>
<span class="pun">});</span></code></pre>
<pre class="prettyprint language-js"><code><span class="com">// 添加 mongoose 实例方法</span><span class="pln">
mongooseSchema</span><span class="pun">.</span><span class="pln">methods</span><span class="pun">.</span><span class="pln">findbyusername </span><span class="pun">=</span> <span class="kwd">function</span><span class="pun">(</span><span class="pln">username</span><span class="pun">,</span><span class="pln"> callback</span><span class="pun">)</span> <span class="pun">{</span>
    <span class="kwd">return</span> <span class="kwd">this</span><span class="pun">.</span><span class="pln">model</span><span class="pun">(</span><span class="str">'mongoose'</span><span class="pun">).</span><span class="pln">find</span><span class="pun">({</span><span class="pln">username</span><span class="pun">:</span><span class="pln"> username</span><span class="pun">},</span><span class="pln"> callback</span><span class="pun">);</span>
<span class="pun">}</span></code></pre>
<pre class="prettyprint language-js"><code><span class="com">// 添加 mongoose 静态方法，静态方法在Model层就能使用</span><span class="pln">
mongooseSchema</span><span class="pun">.</span><span class="pln">statics</span><span class="pun">.</span><span class="pln">findbytitle </span><span class="pun">=</span> <span class="kwd">function</span><span class="pun">(</span><span class="pln">title</span><span class="pun">,</span><span class="pln"> callback</span><span class="pun">)</span> <span class="pun">{</span>
    <span class="kwd">return</span> <span class="kwd">this</span><span class="pun">.</span><span class="pln">model</span><span class="pun">(</span><span class="str">'mongoose'</span><span class="pun">).</span><span class="pln">find</span><span class="pun">({</span><span class="pln">title</span><span class="pun">:</span><span class="pln"> title</span><span class="pun">},</span><span class="pln"> callback</span><span class="pun">);</span>
<span class="pun">}</span></code></pre>
<pre class="prettyprint language-js"><code><span class="com">// model</span>
<span class="kwd">var</span><span class="pln"> mongooseModel </span><span class="pun">=</span><span class="pln"> db</span><span class="pun">.</span><span class="pln">model</span><span class="pun">(</span><span class="str">'mongoose'</span><span class="pun">,</span><span class="pln"> mongooseSchema</span><span class="pun">);</span></code></pre>
<pre class="prettyprint language-js"><code><span class="com">// 增加记录 基于 entity 操作</span>
<span class="kwd">var</span><span class="pln"> doc </span><span class="pun">=</span> <span class="pun">{</span><span class="pln">username </span><span class="pun">:</span> <span class="str">'emtity_demo_username'</span><span class="pun">,</span><span class="pln"> title </span><span class="pun">:</span> <span class="str">'emtity_demo_title'</span><span class="pun">,</span><span class="pln"> content </span><span class="pun">:</span> <span class="str">'emtity_demo_content'</span><span class="pun">};</span>
<span class="kwd">var</span><span class="pln"> mongooseEntity </span><span class="pun">=</span> <span class="kwd">new</span><span class="pln"> mongooseModel</span><span class="pun">(</span><span class="pln">doc</span><span class="pun">);</span><span class="pln">
mongooseEntity</span><span class="pun">.</span><span class="pln">save</span><span class="pun">(</span><span class="kwd">function</span><span class="pun">(</span><span class="pln">error</span><span class="pun">)</span> <span class="pun">{</span>
    <span class="kwd">if</span><span class="pun">(</span><span class="pln">error</span><span class="pun">)</span> <span class="pun">{</span><span class="pln">
        console</span><span class="pun">.</span><span class="pln">log</span><span class="pun">(</span><span class="pln">error</span><span class="pun">);</span>
    <span class="pun">}</span> <span class="kwd">else</span> <span class="pun">{</span><span class="pln">
        console</span><span class="pun">.</span><span class="pln">log</span><span class="pun">(</span><span class="str">'saved OK!'</span><span class="pun">);</span>
    <span class="pun">}</span>
    <span class="com">// 关闭数据库链接</span><span class="pln">
    db</span><span class="pun">.</span><span class="pln">close</span><span class="pun">();</span>
<span class="pun">});</span></code></pre>
<pre class="prettyprint language-js"><code><span class="com">// 增加记录 基于model操作</span>
<span class="kwd">var</span><span class="pln"> doc </span><span class="pun">=</span> <span class="pun">{</span><span class="pln">username </span><span class="pun">:</span> <span class="str">'model_demo_username'</span><span class="pun">,</span><span class="pln"> title </span><span class="pun">:</span> <span class="str">'model_demo_title'</span><span class="pun">,</span><span class="pln"> content </span><span class="pun">:</span> <span class="str">'model_demo_content'</span><span class="pun">};</span><span class="pln">
mongooseModel</span><span class="pun">.</span><span class="pln">create</span><span class="pun">(</span><span class="pln">doc</span><span class="pun">,</span> <span class="kwd">function</span><span class="pun">(</span><span class="pln">error</span><span class="pun">){</span>
    <span class="kwd">if</span><span class="pun">(</span><span class="pln">error</span><span class="pun">)</span> <span class="pun">{</span><span class="pln">
        console</span><span class="pun">.</span><span class="pln">log</span><span class="pun">(</span><span class="pln">error</span><span class="pun">);</span>
    <span class="pun">}</span> <span class="kwd">else</span> <span class="pun">{</span><span class="pln">
        console</span><span class="pun">.</span><span class="pln">log</span><span class="pun">(</span><span class="str">'save ok'</span><span class="pun">);</span>
    <span class="pun">}</span>
    <span class="com">// 关闭数据库链接</span><span class="pln">
    db</span><span class="pun">.</span><span class="pln">close</span><span class="pun">();</span>
<span class="pun">});</span></code></pre>
<pre class="prettyprint language-js"><code><span class="com">// 修改记录</span><span class="pln">
mongooseModel</span><span class="pun">.</span><span class="pln">update</span><span class="pun">(</span><span class="pln">conditions</span><span class="pun">,</span><span class="pln"> update</span><span class="pun">,</span><span class="pln"> options</span><span class="pun">,</span><span class="pln"> callback</span><span class="pun">);</span>
<span class="kwd">var</span><span class="pln"> conditions </span><span class="pun">=</span> <span class="pun">{</span><span class="pln">username </span><span class="pun">:</span> <span class="str">'model_demo_username'</span><span class="pun">};</span>
<span class="kwd">var</span><span class="pln"> update     </span><span class="pun">=</span> <span class="pun">{</span><span class="pln">$set </span><span class="pun">:</span> <span class="pun">{</span><span class="pln">age </span><span class="pun">:</span> <span class="lit">27</span><span class="pun">,</span><span class="pln"> title </span><span class="pun">:</span> <span class="str">'model_demo_title_update'</span><span class="pun">}};</span>
<span class="kwd">var</span><span class="pln"> options    </span><span class="pun">=</span> <span class="pun">{</span><span class="pln">upsert </span><span class="pun">:</span> <span class="kwd">true</span><span class="pun">};</span><span class="pln">
mongooseModel</span><span class="pun">.</span><span class="pln">update</span><span class="pun">(</span><span class="pln">conditions</span><span class="pun">,</span><span class="pln"> update</span><span class="pun">,</span><span class="pln"> options</span><span class="pun">,</span> <span class="kwd">function</span><span class="pun">(</span><span class="pln">error</span><span class="pun">){</span>
    <span class="kwd">if</span><span class="pun">(</span><span class="pln">error</span><span class="pun">)</span> <span class="pun">{</span><span class="pln">
        console</span><span class="pun">.</span><span class="pln">log</span><span class="pun">(</span><span class="pln">error</span><span class="pun">);</span>
    <span class="pun">}</span> <span class="kwd">else</span> <span class="pun">{</span><span class="pln">
        console</span><span class="pun">.</span><span class="pln">log</span><span class="pun">(</span><span class="str">'update ok!'</span><span class="pun">);</span>
    <span class="pun">}</span>
    <span class="com">//关闭数据库链接</span><span class="pln">
    db</span><span class="pun">.</span><span class="pln">close</span><span class="pun">();</span>
<span class="pun">});</span></code></pre>
<pre class="prettyprint language-js"><code><span class="com">// 查询</span>
<span class="com">// 基于实例方法的查询</span>
<span class="kwd">var</span><span class="pln"> mongooseEntity </span><span class="pun">=</span> <span class="kwd">new</span><span class="pln"> mongooseModel</span><span class="pun">({});</span><span class="pln">
mongooseEntity</span><span class="pun">.</span><span class="pln">findbyusername</span><span class="pun">(</span><span class="str">'model_demo_username'</span><span class="pun">,</span> <span class="kwd">function</span><span class="pun">(</span><span class="pln">error</span><span class="pun">,</span><span class="pln"> result</span><span class="pun">){</span>
    <span class="kwd">if</span><span class="pun">(</span><span class="pln">error</span><span class="pun">)</span> <span class="pun">{</span><span class="pln">
        console</span><span class="pun">.</span><span class="pln">log</span><span class="pun">(</span><span class="pln">error</span><span class="pun">);</span>
    <span class="pun">}</span> <span class="kwd">else</span> <span class="pun">{</span><span class="pln">
        console</span><span class="pun">.</span><span class="pln">log</span><span class="pun">(</span><span class="pln">result</span><span class="pun">);</span>
    <span class="pun">}</span>
    <span class="com">//关闭数据库链接</span><span class="pln">
    db</span><span class="pun">.</span><span class="pln">close</span><span class="pun">();</span>
<span class="pun">});</span></code></pre>
<pre class="prettyprint language-js"><code><span class="com">// 基于静态方法的查询</span><span class="pln">
mongooseModel</span><span class="pun">.</span><span class="pln">findbytitle</span><span class="pun">(</span><span class="str">'emtity_demo_title'</span><span class="pun">,</span> <span class="kwd">function</span><span class="pun">(</span><span class="pln">error</span><span class="pun">,</span><span class="pln"> result</span><span class="pun">){</span>
    <span class="kwd">if</span><span class="pun">(</span><span class="pln">error</span><span class="pun">)</span> <span class="pun">{</span><span class="pln">
        console</span><span class="pun">.</span><span class="pln">log</span><span class="pun">(</span><span class="pln">error</span><span class="pun">);</span>
    <span class="pun">}</span> <span class="kwd">else</span> <span class="pun">{</span><span class="pln">
        console</span><span class="pun">.</span><span class="pln">log</span><span class="pun">(</span><span class="pln">result</span><span class="pun">);</span>
    <span class="pun">}</span>
    <span class="com">//关闭数据库链接</span><span class="pln">
    db</span><span class="pun">.</span><span class="pln">close</span><span class="pun">();</span>
<span class="pun">});</span></code></pre>
<pre class="prettyprint language-js"><code><span class="com">// mongoose find</span>
<span class="kwd">var</span><span class="pln"> criteria </span><span class="pun">=</span> <span class="pun">{</span><span class="pln">title </span><span class="pun">:</span> <span class="str">'emtity_demo_title'</span><span class="pun">};</span> <span class="com">// 查询条件</span>
<span class="kwd">var</span><span class="pln"> fields   </span><span class="pun">=</span> <span class="pun">{</span><span class="pln">title </span><span class="pun">:</span> <span class="lit">1</span><span class="pun">,</span><span class="pln"> content </span><span class="pun">:</span> <span class="lit">1</span><span class="pun">,</span><span class="pln"> time </span><span class="pun">:</span> <span class="lit">1</span><span class="pun">};</span> <span class="com">// 待返回的字段</span>
<span class="kwd">var</span><span class="pln"> options  </span><span class="pun">=</span> <span class="pun">{};</span><span class="pln">
mongooseModel</span><span class="pun">.</span><span class="pln">find</span><span class="pun">(</span><span class="pln">criteria</span><span class="pun">,</span><span class="pln"> fields</span><span class="pun">,</span><span class="pln"> options</span><span class="pun">,</span> <span class="kwd">function</span><span class="pun">(</span><span class="pln">error</span><span class="pun">,</span><span class="pln"> result</span><span class="pun">){</span>
    <span class="kwd">if</span><span class="pun">(</span><span class="pln">error</span><span class="pun">)</span> <span class="pun">{</span><span class="pln">
        console</span><span class="pun">.</span><span class="pln">log</span><span class="pun">(</span><span class="pln">error</span><span class="pun">);</span>
    <span class="pun">}</span> <span class="kwd">else</span> <span class="pun">{</span><span class="pln">
        console</span><span class="pun">.</span><span class="pln">log</span><span class="pun">(</span><span class="pln">result</span><span class="pun">);</span>
    <span class="pun">}</span>
    <span class="com">//关闭数据库链接</span><span class="pln">
    db</span><span class="pun">.</span><span class="pln">close</span><span class="pun">();</span>
<span class="pun">});</span></code></pre>
<pre class="prettyprint language-js"><code><span class="com">// 删除记录</span>
<span class="kwd">var</span><span class="pln"> conditions </span><span class="pun">=</span> <span class="pun">{</span><span class="pln">username</span><span class="pun">:</span> <span class="str">'emtity_demo_username'</span><span class="pun">};</span><span class="pln">
mongooseModel</span><span class="pun">.</span><span class="pln">remove</span><span class="pun">(</span><span class="pln">conditions</span><span class="pun">,</span> <span class="kwd">function</span><span class="pun">(</span><span class="pln">error</span><span class="pun">){</span>
    <span class="kwd">if</span><span class="pun">(</span><span class="pln">error</span><span class="pun">)</span> <span class="pun">{</span><span class="pln">
        console</span><span class="pun">.</span><span class="pln">log</span><span class="pun">(</span><span class="pln">error</span><span class="pun">);</span>
    <span class="pun">}</span> <span class="kwd">else</span> <span class="pun">{</span><span class="pln">
        console</span><span class="pun">.</span><span class="pln">log</span><span class="pun">(</span><span class="str">'delete ok!'</span><span class="pun">);</span>
    <span class="pun">}</span>

    <span class="com">//关闭数据库链接</span><span class="pln">
    db</span><span class="pun">.</span><span class="pln">close</span><span class="pun">();</span>
<span class="pun">});</span></code></pre>
学习参考文档
http://ourjs.com/detail/53ad24edb984bb4659000013