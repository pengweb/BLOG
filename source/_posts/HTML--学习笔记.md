---
title: HTML--学习笔记
date: 2016-03-20 14:13:20
tags: [html,笔记,note]

---
# 1.HTML5新特性
1.DOCTYPE及字符编码变简洁了
2.不分大小写
3.布尔值（看下边checked）
4.不分单双引号，也可以不加引号省略掉
5.可以省略标签
6.脚本和链接无需type
7.新增语义标签header、footer、nav、section、article、aside、figcaption、figure
8.Hgroup
9.标记元素 mark
10.图形元素figcaption、figure
11.占位符 Placeholder
12.必填属性 Required
13.自动聚焦 Autofocus
14.视频音频
15.视频预载 reload="preload"
16.视频控制条 Controls
17.正规表达式 pattern="[A-Za-z]{4,10}"

# 2.HTML5元素标记释义
<table border="1"><tbody><tr><td width="100"><strong>标记</strong></td><td><strong>类型</strong></td><td><strong>意义</strong></td><td><strong>介绍</strong></td></tr><tr><td colspan="4"><strong>文件标记</strong></td></tr><tr><td>&lt;html&gt;</td><td>●</td><td>根文件标记</td><td>让浏览器知道这是HTML 文件</td></tr><tr><td colspan="4"><strong>META标记</strong></td></tr><tr><td>&lt;head&gt;</td><td>●</td><td>开头</td><td>提供文件整体信息</td></tr><tr><td>&lt;title&gt;</td><td>●</td><td>标题</td><td>定义文件标题，显示于浏览器顶端</td></tr><tr><td>&lt;base&gt;</td><td>o</td><td>基准标记</td><td>可将相对URL转绝对及指定链接</td></tr><tr><td>&lt;link&gt;</td><td>o</td><td>外部资源连接</td><td>必须带rel属性描述</td></tr><tr><td>&lt;meta&gt;</td><td>o</td><td>其它META数据</td><td>不能被title, base, link, style, 和script元素描述的META数据</td></tr><tr><td>&lt;style&gt;</td><td>●</td><td>嵌入文档风格信息</td><td></td></tr><tr><td colspan="4"><strong>部件标记</strong></td></tr><tr><td>&lt;body&gt;</td><td>●</td><td>文档主体开始</td><td>文档内容容器</td></tr><tr><td>&lt;section&gt;</td><td>●</td><td>代表通用文档或应用部件</td><td></td></tr><tr><td>&lt;nav&gt;</td><td>●</td><td>导航链接</td><td>外部链接或文档内部链接</td></tr><tr><td>&lt;article&gt;</td><td>●</td><td>页面模块</td><td>类似文章、摘要或留言POST等形式的记录</td></tr><tr><td>&lt;aside&gt;</td><td>●</td><td>孤立模块</td><td>一般作为边栏广告、说明、引用、导航等，aside围堵部分一般与正文耦合较小</td></tr><tr><td>&lt;h1&gt;</td><td>●</td><td>标题标记</td><td>此外还有h2, h3, h4, h5, h6</td></tr><tr><td>&lt;hgroup&gt;</td><td>●</td><td>群组标题</td><td>用在一组h1-h6这样的元素集合时使用，用来区分主副标题？？</td></tr><tr><td>&lt;header&gt;</td><td>●</td><td>组说明或组导航</td><td>也可叫页头标题</td></tr><tr><td>&lt;footer&gt;</td><td>●</td><td>页脚标题</td><td>作用范围跟最近部件元素有关</td></tr><tr><td>&lt;address&gt;</td><td>●</td><td>地址或联系信息</td><td></td></tr><tr><td><strong>分组内容标记</strong></td><td></td><td></td><td></td></tr><tr><td>&lt;p&gt;</td><td>●</td><td>段落标记</td><td></td></tr><tr><td>&lt;hr&gt;</td><td>o</td><td>水平分割线</td><td></td></tr><tr><td>&lt;br&gt;</td><td>o</td><td>换行</td><td></td></tr><tr><td>&lt;pre&gt;</td><td>●</td><td>预格式化分本块</td><td></td></tr><tr><td>&lt;blockquote&gt;</td><td>●</td><td>块引用</td><td></td></tr><tr><td>&lt;ol&gt;</td><td>●</td><td>编号列表</td><td></td></tr><tr><td>&lt;ul&gt;</td><td>●</td><td>项目列表</td><td></td></tr><tr><td>&lt;li&gt;</td><td>●</td><td>列表项</td><td></td></tr><tr><td>&lt;dl&gt;</td><td>●</td><td>定义列表</td><td></td></tr><tr><td>&lt;dt&gt;</td><td>●</td><td>定义名称</td><td></td></tr><tr><td>&lt;dd&gt;</td><td>●</td><td>定义说明</td><td></td></tr><tr><td>&lt;figure&gt;</td><td>●</td><td>流内容区块说明</td><td>多结合figcaption使用</td></tr><tr><td>&lt;figcaption&gt;</td><td>●</td><td>figure内容属性</td><td></td></tr><tr><td>&lt;div&gt;</td><td>●</td><td>定位标记</td><td>无实际意义</td></tr><tr><td></td><td></td><td></td><td></td></tr><tr><td colspan="4"><strong>文本层次语义标记</strong></td></tr><tr><td>&lt;a&gt;</td><td>●</td><td>链接标记</td><td></td></tr><tr><td>&lt;em&gt;</td><td>●</td><td>强调标记</td><td></td></tr><tr><td>&lt;strong&gt;</td><td>●</td><td>加重标记</td><td></td></tr><tr><td>&lt;small&gt;</td><td>●</td><td>字体缩小</td><td></td></tr><tr><td>&lt;cite&gt;</td><td>●</td><td>斜体标记</td><td></td></tr><tr><td>&lt;q&gt;</td><td>●</td><td>引用标记内容</td><td>原文是phrasing content，暂不清楚如何翻译</td></tr><tr><td>&lt;dfn&gt;</td><td>●</td><td>术语定义</td><td></td></tr><tr><td>&lt;abbr&gt;</td><td>●</td><td>缩略语</td><td></td></tr><tr><td>&lt;time&gt;</td><td>●</td><td>日期时间</td><td></td></tr><tr><td>&lt;code&gt;</td><td>●</td><td>程序代码</td><td></td></tr><tr><td>&lt;var&gt;</td><td>●</td><td>变量</td><td></td></tr><tr><td>&lt;samp&gt;</td><td>●</td><td>范例</td><td></td></tr><tr><td>&lt;kbd&gt;</td><td>●</td><td>键盘字</td><td></td></tr><tr><td>&lt;sub&gt;&lt;sups&gt;</td><td>●</td><td>上标字/下标字</td><td></td></tr><tr><td>&lt;i&gt;</td><td>●</td><td>斜体标记</td><td></td></tr><tr><td>&lt;b&gt;</td><td>●</td><td>粗体标记</td><td></td></tr><tr><td>&lt;mark&gt;</td><td>●</td><td>标记或高亮</td><td></td></tr><tr><td>&lt;ruby&gt;</td><td>●</td><td>注解标记</td><td></td></tr><tr><td>&lt;rt&gt;</td><td>●</td><td>ruby子元素</td><td>结合ruby使用，比如:&lt;ruby&gt;天&lt;rt&gt;Tian&lt;/rt&gt;缘&lt;rt&gt;Yuan&lt;/rt&gt;&lt;/ruby&gt;</td></tr><tr><td>&lt;rp&gt;</td><td>●</td><td>ruby子元素</td><td>一般做rt元素注释使用</td></tr><tr><td>&lt;bdo&gt;</td><td>●</td><td></td><td></td></tr><tr><td>&lt;span&gt;</td><td>●</td><td>自定义标记</td><td></td></tr><tr><td colspan="4"><strong>编辑标记</strong></td></tr><tr><td>&lt;ins&gt;</td><td>●</td><td></td><td></td></tr><tr><td>&lt;del&gt;</td><td>●</td><td></td><td></td></tr><tr><td colspan="4"><strong>嵌入内容标记</strong></td></tr><tr><td>&lt;img&gt;</td><td>●</td><td>图片标记</td><td></td></tr><tr><td>&lt;iframe&gt;</td><td>●</td><td>框架标记</td><td></td></tr><tr><td>&lt;embed&gt;</td><td>●</td><td>嵌入标记</td><td></td></tr><tr><td>&lt;object&gt;</td><td>●</td><td>对象标记</td><td></td></tr><tr><td>&lt;param&gt;</td><td>●</td><td>参数标记</td><td></td></tr><tr><td>&lt;video&gt;</td><td>●</td><td>视频标记</td><td></td></tr><tr><td>&lt;audio&gt;</td><td>●</td><td>音频标记</td><td></td></tr><tr><td>&lt;source&gt;</td><td>●</td><td>来源标记</td><td></td></tr><tr><td>&lt;canvas&gt;</td><td>●</td><td>制图标记</td><td></td></tr><tr><td>&lt;map&gt;</td><td>●</td><td>地图标记</td><td></td></tr><tr><td>&lt;area&gt;</td><td>●</td><td>区域标记</td><td></td></tr><tr><td></td><td></td><td></td><td></td></tr><tr><td colspan="4"><strong>表格标记</strong></td></tr><tr><td>&lt;table&gt;</td><td>●</td><td>表格标记</td><td>设定该表格的各项参数</td></tr><tr><td>&lt;caption&gt;</td><td>●</td><td>表格标题</td><td>做成一打通列以填入表格标题</td></tr><tr><td>&lt;colgroup&gt;</td><td>●</td><td></td><td></td></tr><tr><td>&lt;col&gt;</td><td>●</td><td></td><td></td></tr><tr><td>&lt;tbody&gt;</td><td>●</td><td></td><td></td></tr><tr><td>&lt;thread&gt;</td><td>●</td><td></td><td></td></tr><tr><td>&lt;tfoot&gt;</td><td>●</td><td></td><td></td></tr><tr><td>&lt;tr&gt;</td><td>●</td><td>表格列</td><td>设定该表格的列</td></tr><tr><td>&lt;td&gt;</td><td>●</td><td>表格栏</td><td>设定该表格的栏</td></tr><tr><td>&lt;th&gt;</td><td>●</td><td>表格标头</td><td>相等于&lt;TD&gt;，但其内文字字体会变粗</td></tr><tr><td colspan="4"><strong>表单标记</strong></td></tr><tr><td>&lt;form&gt;</td><td>●</td><td>表单标记</td><td>决定该表单的运作模式</td></tr><tr><td>&lt;fieldset&gt;</td><td>●</td><td></td><td></td></tr><tr><td>&lt;legend&gt;</td><td>●</td><td></td><td></td></tr><tr><td>&lt;input&gt;</td><td>●</td><td>输入标记</td><td></td></tr><tr><td>&lt;label&gt;</td><td>●</td><td></td><td></td></tr><tr><td>&lt;button&gt;</td><td>●</td><td>按钮</td><td></td></tr><tr><td>&lt;select&gt;</td><td>●</td><td>选择标记</td><td></td></tr><tr><td>&lt;datalist&gt;</td><td>●</td><td></td><td></td></tr><tr><td>&lt;optgroup&gt;</td><td>●</td><td></td><td></td></tr><tr><td>&lt;option&gt;</td><td>●</td><td>选项</td><td></td></tr><tr><td>&lt;textarea&gt;</td><td>●</td><td></td><td></td></tr><tr><td>&lt;keygen&gt;</td><td>●</td><td></td><td></td></tr><tr><td>&lt;output&gt;</td><td>●</td><td></td><td></td></tr><tr><td>&lt;progress&gt;</td><td>●</td><td></td><td></td></tr><tr><td>&lt;meter&gt;</td><td>●</td><td></td><td></td></tr><tr><td></td><td></td><td></td><td></td></tr><tr><td colspan="4"><strong>互动元素</strong></td></tr><tr><td>&lt;details&gt;</td><td>●</td><td></td><td></td></tr><tr><td>&lt;summary&gt;</td><td>●</td><td></td><td></td></tr><tr><td>&lt;command&gt;</td><td>●</td><td></td><td></td></tr><tr><td>&lt;menu&gt;</td><td>●</td><td></td><td></td></tr><tr><td colspan="4"><strong>其他标记</strong></td></tr><tr><td>&lt;script&gt;</td><td>●</td><td></td><td></td></tr><tr><td>&lt;noscript&gt;</td><td>●</td><td></td><td></td></tr><tr><td></td><td></td><td></td><td></td></tr></tbody></table>

# 3.表格

```
<dl>（一级）
  <dt>helloworld</dt>（二级）
  <dd>每一门语言</dd>（三级）
</dl>
```
```
<thead>  //定义表格页眉
```

```
<tbody>          //定义表格主体 
```

```
<tfoot>  //定义表格页脚
```

```
<col>    //定义表格的列属性-居中
```

```
<caption>  //这里是标题，显示在表格的居中
```

```
cellpadding=“10”   //这个是定义单元格边距的
```

```
cellspacing=“10”  //这是单元格的边距
```

```
<table summary="这里写一下这个表格的描述有利于收录">
<tbody>           //定义表格主体
  <!--表格大的时候保证一次显示出来而不是一点一点的显示-->
  <!--第一行：开始-->
  <tr>                                                    
    <th>班级</th>                                  <!--头行的列都是用th其实都是td-->
    <th>学生数</th>
    <th>平均成绩</th>
  </tr>                                                   
  <!--第一行：结束-->
  <tr>
    <td>二班</td>
    <td>35</td>
    <td>85</td>
  </tr>
</tbody>
</table>
```


# 4.链接
```
<a href=”连接地址” title=”鼠标滑过文字” target=”_blank” >需要连接的文字</a>
```
```
//跳转到当前页id为tips位置
<a href="#tips">跳转到</a>
```

```
<a href=”mailto:445138773@qq.com?cc=445@qq.com&bcc=138@qq.com& subjet=主题名&body=内容”  >需要连接的文字</a>
<!–发邮件给445138773@qq.com抄送给445@qq.com密送给138@qq.com–>
```

```
<img src=”图片地址” alt=”图片没有显示出来显示的问题” title=”提示文字”>
```

# 5.表单

## 表单元素

```
<form>  //表单
```

```
<input>  //输入域
```

```
<textarea>  //文本域
```

```
<lable>  //控制标签，做说明用
```

```
<fieldset>  //定义域
```

```
<legend>  //域的标题
```

```
<select>  //选择列表
```

```
<optgroup>  //选项组
```

```
<option>  //下拉列表中的选项
```

```
<button>  //按钮
```

```
//会自动跳转到action页
<form method="传送方式分为post和get" action="服务器文件名，和这个文件进行对话">交互内容</form>
```

```
<!--定义输入框大小-->
<textarea rows="行50" cols="列10">在这里输入文字</textarea>                
```

```
<!--定义  确定  按钮 name是给后台程序用-->
<input type="submit" value="确定" name="submit">                    
```

```
<!--定义重置按钮-->
<input type="reset" value="重置" name="reset">                             
```

```
//datalist 定义选项列表
<input list=”browsers”>
<datalist id=”browsers”>
  <option value=”Internet Explorer”>
  <option value=”Firefox”>
  <option value=”Chrome”>
  <option value=”Opera”>
  <option value=”Safari”>
</datalist>
//这个input的list必须存在而且要和datalist的id是相同的
```

//keygen 当提交表单时，会生成两个键，一个是私钥，一个公钥
```
<form action=”demo_keygen.asp” method=”get”>
  用户名: <input type=”text” name=”usr_name”>
  加密: <keygen name=”security”>
  <input type=”submit”>
</form>
```
```

//output  用于不同类型的输出，比如计算或脚本输出：
<form oninput=”x.value=parseInt(a.value)+parseInt(b.value)”>0
  <input type=”range” id=”a” value=”50″>100 +
  <input type=”number” id=”b” value=”50″>=
  <output name=”x” for=”a b”></output>
</form>
//output里的for=“a b”写不写都可以，还有这里的name可以用id替代
```

## 表单类型
text文本类型
password密码类型
radio 单选类型
checkbox 多选类型
file 文件类型
submit 提交按钮
reset重置按钮
button定义按钮
image 定义图片按钮
hidden定义隐藏域
下边是HTML5新增的
email邮件类型
number数字类型
range数字滑动条
date日期类型
url地址类型
search搜索类型
用法参考：http://www.w3school.com.cn/html5/att_input_type.asp

## 新的 form 属性

autocomplete
novalidate

## 新的 input 属性

autocomplete
autofocus
form
form overrides (formaction, formenctype, formmethod, formnovalidate, formtarget)
height 和 width
list
min, max 和 step
multiple            //多选
pattern (regexp)
placeholder
required

用法参考：http://www.w3school.com.cn/html5/html_5_form_attributes.asp

## 使用范例

例：单选或者多选
```
<form name="iForm" method="post" action="save.php">
你喜欢运动吗？
  <!--单选选中喜欢，name必须相同-->
  <input type="radio" value="喜欢" name="radiolove" checked="checked">喜欢
  <input type="radio" value="不喜欢" name="radiolove">不喜欢              
  <input type="radio" value="无所谓" name="radiolove">无所谓
喜欢什么运动呢？
  <!--多选中篮球和乒乓球，name不能相同，也可以相同，留作js调用用-->
  <input type="checkbox" value="篮球" name="checkbox1" checked="checked">篮球
  <input type="checkbox" value="足球" name="checkbox2" >足球     
  <input type="checkbox" value="乒乓球" name="checkbox3" checked=checked>乒乓球
</form>
```
例：下拉菜单的单选和多选（多选要按Ctrl+鼠标左键）
```
<form name="iform" method="post" action="save.php">
   <!--现在是多选，要按ctrl才能选中多个，去掉multiple="multiple"就是单选-->
  <select multiple="multiple">             
  <option value="看书">看书</option>
  <option value="画画">画画</option>
  <option value="写字">写字</option>
</select>
</form>
```
例：lable···for
```
<!--for必须和id是相同的而且如果有一个被标注了，两个就都要标注，缺一不可。name可相同也可不同，label也可以放到input的前边-->
<form action"#" method="post" name="List">
  <label for="xiao">这里输入显示文字香蕉<label>
  <input type="checkbox" name="typeList" id="xiao">
  <label for="xiao">这里输入显示文字苹果<label>
  <input type="checkbox" name="typeList" id="xiao">
  <label for="xiao">这里输入显示文字草莓<label>
  <input type="checkbox" name="typeList" id="xiao">
</form>
```
例：html5新增
```
<!--accesskey是键盘快捷键，支持它的标签有<a>, <area>, <button>, <input>, <label>, <legend> 以及 <textarea>-->
    <a href="http://www.w3school.com.cn/html/" accesskey="h">HTML</a>

<!--contenteditable 这是一个可编辑段落，看着都可以替代input这种表单了-->
    <p contenteditable="true">这是一个可编辑段落。</p>

<!--contextmenu 这个是鼠标右键出现菜单-->

<!--hidden="hidden"  在xhtml中是禁止简写的-- >

<!-- item条目列表-->
    document.body.childNodes[0];

<!--item来写-->
    documetn.body.childNodes.item(0);

<!--tabindex TAB切换键切换顺序-->
    <a href="http://www.pengweb.net/" tabindex="2">2</a><br />
    <a href="http://www.pengweb.net/" tabindex="1">1</a><br />
    <a href="http://www.pengweb.net/" tabindex="3">3</a>
```

例：与PHP交互
```
<form action="这里放交互的PHP文件地址" method="get/post(get地址栏会显示用户名和密码)" name=“typelist”>
用户名：
  <input type="text" name=“name” >     <!--输入表单-->
密码：
  <input type="password" name=“password”>
  <input type="submit" value="提交">
</form>
```
PHP的写法：
```
<?php
echo "用户名："$_GET['name'].“密码：”$_GET['password'];
```


# 6.窗口(框架)
```
<frameset cols="20%,30%,50%" noresize>    //禁止调大小，不能将这个写在body内，上一级是html
<frame src="要引入网页地址1"></frame>
<frame src="要引入网页地址2"></frame>
</frameset>
```
内联框架：
```
<iframe src="要引入网页地址" iframeborder="0" width="400" height="400">
</iframe>
```

# 7.视频插入（音频只是将video换成audio）
```
<video width=”320″ height=”240″ controls=”controls”>
  <source src=”movie.ogg” type=”video/ogg”>
  <source src=”movie.mp4″ type=”video/mp4″>
  Your browser does not support the video tag.
</video>
```
autoplay   //如果出现该属性，则视频在就绪后马上播放。
controls    //如果出现该属性，则向用户显示控件，比如播放按钮。
height    //设置视频播放器的高度。
loop    //如果出现该属性，则当媒介文件完成播放后再次开始播放。
preload    //如果出现该属性，则视频在页面加载时进行加载，并预备播放。如果使用 “autoplay”，则忽略该属性。
src    //要播放的视频的 URL。
width  //显示宽度

**通过dom控制事例**
```
<div style=”text-align:center;”>
 <button onclick=”playPause()”>播放/暂停</button>
 <button onclick=”makeBig()”>大</button>
 <button onclick=”makeNormal()”>中</button>
 <button onclick=”makeSmall()”>小</button>
 <br />
 <video id=”video1″ width=”420″ style=”margin-top:15px;”>
 <source src=”/example/html5/mov_bbb.mp4″ type=”video/mp4″ />
 <source src=”/example/html5/mov_bbb.ogg” type=”video/ogg” />
 Your browser does not support HTML5 video.
 </video>
 </div>
 <script type=”text/javascript”>
	 var myVideo=document.getElementById(“video1”);
	 function playPause()
		 {
		 	if (myVideo.paused)
		 		myVideo.play();
		 	else
		 		myVideo.pause();
		 }
	 function makeBig()
		 {
		 	myVideo.width=560;
		 }
	 function makeSmall()
		 {
		 	myVideo.width=320;
		 }
	 function makeNormal()
		 {
		 	myVideo.width=420;
		 }
 </script>
```

# 8.Canvas
单提出来做了一篇文章

# 9.内联SVG
单提出来做了一篇文章

# 10.拖放（Drag 和 drop）
1.设置元素为可拖放
```
<img draggable=”true”>
```
2.拖动什么
ondragstart 和 .dataTransfer.setData()
3.放到何处
ondragover
4.进行放置
ondrop
例：
```
 <!--
    先设置draggable="true"声明这个对象是可以拖放的
    ondragstart="drag(ev)"这是说调用一个函数drag（ev）
    ev.dataTransfer.setData是设置被拖拽的数据类型和值，例子中数据类型是text，值是拖拽id （“drag1”）记得加引号
    ondragover是放置目标，默认是不无法将数据放到其他元素中的，所以这里给他一个事件，将他设置允许，
    需要event.preventDefault();
    ondrop是放置动作，触发事件
    ev.target.appendChild(document.getElementById(data));这句话中的ev.target是指的当前被放置的目标位置，
    document.getElementById(data)是拖动的元素，其中data可以改写成“drag1”记得双引号
    -->
    <div id="div1" ondrop="drop(event)" ondragover="allowDrop(event)">
        <img src="http://www.gbtags.com/gb/laitu/336x69" draggable="true" ondragstart="drag(event)" 
id="drag1" width="88" height="31">
    </div>
    <div id="div2" ondrop="drop(event)" ondragover="allowDrop(event)"></div>
    <script>
        function allowDrop(ev)
        {
            ev.preventDefault();
        }

        function drag(ev)
        {
            ev.dataTransfer.setData("Text",ev.target.id);
        }

        function drop(ev)
        {
            ev.preventDefault();
            var data=ev.dataTransfer.getData("Text");
            ev.target.appendChild(document.getElementById(data));
        }
    </script>
```


# 11.语义元素
！[](/images/QQ截图20150420172104.png)


# 12.WEB存储--应用程序缓存--WEB worker--indexed DB
这些内容将在javascript高级程序设计进行总结，分别为第23章和第25章


# 13.HTML5浏览器兼容问题

第一种：调用js文件来解决（支持IE9以下版本）
```
//写在head内
<!--[if lt IE 9]>
  <script src="http://apps.bdimg.com/libs/html5shiv/3.7/html5shiv.min.js"></script>
<![endif]-->
```
注意：html5shiv.js 引用代码必须放在元素中，因为 IE 浏览器在解析 HTML5 新元素时需要先加载该文件。 

第三种方法：分别给新标签设置成块级元素
```
header, section, footer, aside, nav, main, article, figure {
    display: block; 
}
```


# 14.HTML属性书写顺序-推荐不强制

class → id,name → data → src,for,type,href → title,alt → aria → role


# 15.块状元素和内联元素
<table border="1" cellspacing="0" cellpadding="0"><tbody><tr><th scope="col" height="40"><br><div><strong>块状元素</strong></div></th><th scope="col"><br><div><strong>内联元素</strong></div></th></tr><tr><td valign="top" width="50%"><br><div>address - 地址<br>blockquote - 块引用<br>center - 举中对齐块<br>dir - 目录列表<br>div - 常用块级容易，也是CSS layout的主要标签<br>dl - 定义列表<br>fieldset - form控制组<br>form - 交互表单<br>h1 - 大标题<br>h2 - 副标题<br>h3 - 3级标题<br>h4 - 4级标题<br>h5 - 5级标题<br>h6 - 6级标题<br>hr - 水平分隔线<br>isindex - input prompt<br>menu - 菜单列表<br>noframes - frames可选内容，（对于不支持frame的浏览器显示此区块内容<br>noscript - 可选脚本内容（对于不支持script的浏览器显示此内容）<br>ol - 有序表单<br>p - 段落<br>pre - 格式化文本<br>table - 表格<br>ul - 无序列表</div></td><td valign="top" width="50%"><br><div>a - 锚点<br>abbr - 缩写<br>acronym - 首字<br>b - 粗体(不推荐)<br>bdo - bidi override<br>big - 大字体<br>br - 换行<br>cite - 引用<br>code - 计算机代码(在引用源码的时候需要)<br>dfn - 定义字段<br>em - 强调<br>font - 字体设定(不推荐)<br>i - 斜体<br>img - 图片<br>input - 输入框<br>kbd - 定义键盘文本<br>label - 表格标签<br>q - 短引用<br>s - 中划线(不推荐)<br>samp - 定义范例计算机代码<br>select - 项目选择<br>small - 小字体文本<br>span - 常用内联容器，定义文本内区块<br>strike - 中划线<br>strong - 粗体强调<br>sub - 下标<br>sup - 上标<br>textarea - 多行文本输入框<br>tt - 电传文本<br>u - 下划线<br>var - 定义变量</div></td></tr></tbody></table>

# 16.相近元素区分
1、em 把文本定义为强调的内容

em 标签告诉浏览器把其中的文本表示为强调的内容。对于所有浏览器来说，这意味着要把这段文字用斜体来显示。

尽管现在 em 标签修饰的内容都是用斜体字来显示，但这些内容也具有更广泛的含义，将来的某一天，浏览器也可能会使用其他的特殊效果来显示强调的文本。如果你只想使用斜体字来显示文本的话，请使用 i 标签。除此之外，文档中还可以包括用来改变文本显示的级联样式定义。

2、i 显示斜体文本效果

i 标签和基于内容的样式标签 em 类似。它告诉浏览器将包含其中的文本以斜体字（italic）或者倾斜（oblique）字体显示。如果这种斜体字对该浏览器不可用的话，可以使用高亮、反白或加下划线等样式。

3、dfn 定义一个定义项目

dfn 标签可标记那些对特殊术语或短语的定义。
现在流行的浏览器通常用斜体来显示 dfn 中的文本。将来，dfn 还可能有助于创建文档的索引或术语表。
与其他许多基于内容的样式和物理样式标签一样，dfn 标签尽量少用为妙


# 17.绝对路径和相对路径

假设你的这个html文件的路径是www.example.com/path/to/html/a.html

### 绝对路径
```
src="/js/ibanner.js"
```
指向www.example.com/js/ibanner.js


### 相对路径
```
src="js/ibanner.js"
```

指向www.example.com/path/to/html/js/ibanner.js
```
src="./js/ibanner.js"
```
指向www.example.com/path/to/html/js/ibanner.js


### 相对路径（返回上一级目录）
```
src="../js/ibanner.js"
```
指向www.example.com/path/to/js/ibanner.js


### 相对路径（返回上二级目录）
```
src="../../js/ibanner.js"
```
指向www.example.com/path/js/ibanner.js


# 18.地理定位
``` js
<p id="demo">点击按钮获取您当前坐标（可能需要比较长的时间获取）：</p>
<button onclick="getLocation()">点我</button>
<script>
    var x=document.getElementById("demo");
    function getLocation()
    {
        if (<span style="color: #008000;">navigator.geolocation</span>)
        {
            //getCurrentPosition可以换成watchPosition来实时更新位置,做导航用，清除的话用clearWatch()
            <span style="color: #008000;">navigator.geolocation.getCurrentPosition(showPosition,showError);</span>
        }
        else{x.innerHTML="Geolocation is not supported by this browser.";}
    }
    function showPosition(position)
    {
        //这里的coords后边可以接的还有很多，具体参考手册
        x.innerHTML="纬度: " + <span style="color: #008000;">position.coords.latitude</span> +
                "<br>经度: " + <span style="color: #008000;">position.coords.longitude</span>;
    }
    function showError(error)
    {
        switch(error.code)
        {
            case error.PERMISSION_DENIED:
                x.innerHTML="用户拒绝对获取地理位置的请求。"
                break;
            case error.POSITION_UNAVAILABLE:
                x.innerHTML="位置信息是不可用的。"
                break;
            case error.TIMEOUT:
                x.innerHTML="请求用户地理位置超时。"
                break;
            case error.UNKNOWN_ERROR:
                x.innerHTML="未知错误。"
                break;
        }
    }
</script>
```

# 19.data_*自定义属性

将在jacascript高级程序设计第11章进行详细解释

# 20.SSE
将在jacascript高级程序设计第21章进行详细解释

# 21.实践补充
checked="checked"     //简写成checked