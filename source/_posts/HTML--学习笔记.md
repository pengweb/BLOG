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
1.先要创建个画布
```
<canvas id=”myCanvas” width=”200″ height=”100″></canvas>
```
2.然后再用js来绘制图像（绘制线、盒、圆、字符以及添加图像）
参考文献：http://www.w3cschool.cc/html/html5-canvas.html 
3.可以直接用flase生成canvas动画
4.creat.js快速创建canvas

``` js

//基础图形
<!--
W3C标准：http://www.w3.org/TR/2dcontext/
canvas的边是可以设置的，可以设置成cxt.canvas.width和cxt.canvas.height这样就可以自动获取画布的大小了

ctx.moveTo(0,0);                 绘制线【起点】
ctx.lineTo(150,150);             绘制线【中间/结束点】
ctx.arc(50,50,20,0,2*Math.PI);   绘制圆
ctx.fillRect(0,0,150,150);       绘制矩形
ctx.font="30px Arial"            绘制文本
ctx.drawImage(img,10,10)         绘制图片

ctx.fillStylt=''   填充区域的属性（color,gradient,image,canvas,video）
ctx.strokeStyle=''   填充边框的属性
ctx.fill()是填充
ctx.stroke()是描边

---样式---
线性渐变色：
①var grd= ctx.createLinearGradient(xstart,ystart,xend,yend)   //设置渐变方向
②grd.addColorStop(stop,color)
径向渐变色：
①var grd=ctx.createRadialGradient(75,50,15,90,60,60);     //起始颜色的x,y,r和结束颜色的x,y,r
②grd.addColorStop(stop,color)
图片样式：creatPattern                           //其中img也可以是canvas,或者video
var grd= ctx.createPattern(img,repeat-style)  //repeat-style:no-repeat、repeat-x、repeat-y、repeat




---图像属性---
ctx.lineWidth=10;    设置线宽
ctx.lineCap = "butt"     其中butt是默认属性，round两边为半圆，square两边为矩形
ctx.lineJoin ="miter"     miter是默认的   bevel是平角的   round圆角
ctx.miterLimit=10        默认属性是10


--图形变换--
位移--translate(x,y)
旋转--rotate(deg)
缩放--scale(sx,sy)--缩放的时候边框会同时进行缩放，且X,Y轴坐标也会相应的进行缩放，都是按倍数缩放

做变换的时候需要保存和恢复，避免后边叠加前边的属性；
context.save();
进行图形操作
context.restore();

---变换矩阵[同时解决上边三个参数的效果]---
a c e
b d f
0 0 1
a：水平缩放
b: 水平倾斜
c: 垂直倾斜
d: 垂直缩放
e: 水平位移
f: 垂直位移

transform(a,b,c,d,e,f)----会发生级联效果，就是综合上边所有的效果相加
setTransform（a,b,c,d,e,f）----避免发生级联效果

____________________________________________________________
高级内容：
1.阴影的绘制
context.shadowColor
context.shadowOffsetX
context.shadowOffsetY
context.shadowBlur

2.透明度和图像遮挡时候的效果
context.globalAlpha
context.globalCompositeOperation= 一共有11种效果
source-over     后绘制的图形完全压盖在先绘制的图形上
source-atop     剪掉后绘制图超出先绘制图部分
source-in       剪掉后绘制图超出先绘制图部分且只显示后绘制图形，且不显示先绘制图形（显示后绘制图）
source-out      剪掉后绘制图和先绘制图重合部分即只显示超出部分，且不显示先绘制图形（显示后绘制图）
destination-over    先绘制的图形压盖在后绘制图形的上边
destination-atop    剪掉先绘制图形超出后绘制图部分，显示保留先绘制图颜色+后绘制图颜色
destination-in      显示先绘制和后绘制重合部分，且只显示先绘制图颜色
destination-out     剪掉后绘制图部分，只显示先绘制图颜色
lighter             重合部分，颜色进行中和
copy                完全且只复制一次后绘制图形
xor                 异或操作，重叠部分删除

3.剪辑区域
context.clip()

例子：在圆为路径内绘制文字
context.arc()          //圆不用绘制出来
context.clip()
context.fillText()     //需要绘制出来

4.非零环绕原则
从中间引出一条线，另相交线的方向相加，最终为非零区域显示颜色，为0区域显示为空，创建镂空效果，镂空阴影

5.isPointInpath
context.isPointInPath(x,y)    判断当前点 是否在所规划的路径内

//鼠标点击，获取在canvas中的坐标
var x=event.clientX-canvas.getBoundingClientRect().left;    //点击位置相对于显示器的x轴减去canvas盒子的x轴
var y=event.clientY-canvas.getBoundingClientRect().top;     //getBoundingClientRect() 是获得包围框的属性，是js的属性

function detect（event）{
    var x=event.clientX-canvas.getBoundingClientRect().left;
    var y=event.clientY-canvas.getBoundingClientRect().top;

    for(var i=0;i<balls.length;i++){
        context.begin();
        context.arc(balls[i].x,balls[i].y,ball[i].r,0,2*Math.PI)    //先循环查询所有绘制的圆的路径

        if(context.isPointInPath(x,y)){                     //判断所选的点是否在所绘制的圆内
            context.fillStyle="red";                        //如果在的话，就进行变色
            context.fill();                                 //将变色属性绘制出来
        }
    }
}


6.context的扩展--CanvasRenderingContext2D

CanvasRenderingContext2D.prototype.fillStar=function(r,R,x,y,rot){
    cxt.beginPath();
            for (var i = 0; i < 5; i++) {
                cxt.lineTo(Math.cos((18 + i * 72 - rot) * Math.PI / 180) * R + x,     //300是半径，cos内是弧度数，弧度数=圆心角*Math.PI/180
                        -Math.sin((18 + i * 72 - rot) * Math.PI / 180) * R + y
                )
                cxt.lineTo(Math.cos((54 + i * 72 - rot) * Math.PI / 180) * r + x,     //300是半径，cos内是弧度数，弧度数=圆心角*Math.PI/180
                        -Math.sin((54 + i * 72 - rot) * Math.PI / 180) * r + y
                )
            }
            cxt.closePath();

            context.fill();
}

上边就是定义了一个fillStar这样一个五角星，以后就可以通过下边这种方法调用了
context.fillStyle="#058"
context.fillStar(r,R,x,y,rot)


7.兼容性
if（context.ellipse）{}            //判断是否兼容ellipse函数
explorecanvas   这个插件库，可以引入我了兼容ie


8.Canvas图形库
①canvasplus
②Artisan JS     --野心大
③Rgraph         --柱状图，点状图


-->

<!--绘制矩形-->

    <canvas id="myCanvas" height="200" width="200" style="border:1px solid #000000">
    </canvas>
    <script>
        var c = document.getElementById("myCanvas");
        var ctx = c.getContext("2d");
        ctx.fillStyle="#000000";       //填充矩形内容颜色
        ctx.fillRect(0,0,150,150);     //绘制矩形
    </script>

<!--绘制线-->

    <canvas id="myCanvas1" height="200" width="200" style="border:1px solid #000000">
    </canvas>
    <script>
        var c = document.getElementById("myCanvas1");
        var ctx = c.getContext("2d");
        ctx.moveTo(0,0);              //线的起始位置
        ctx.lineTo(150,160);          //线的结束位置
        ctx.stroke();                 //线的宽度，变实线
        ctx.lineWidth=10;              //设置直线宽度

    </script>

<!--绘制圆-->

<canvas id="myCanvas2" height="200" width="200" style="border:1px solid #000000">
</canvas>
<script>
    var c = document.getElementById("myCanvas2");
    var ctx = c.getContext("2d");
    ctx.beginPath();                 //重置当前路径
    ctx.arc(50,50,20,0,2*Math.PI); //x,y,r,start，stop,anticlockwise(这个是顺时针false)
    ctx.fill();                 //设置为实心的
</script>

<!--绘制文本
context.textAlign = left/center/right      (都参考线在文字的左，中，右边)
context.textBaseline = top/middle/bottom/alphabetic(default)
context.measureText(string).width    //获得文字的宽度的数值，记得吧string换成文字叫""
-->

<canvas id="myCanvas3" height="200" width="200" style="border:1px solid #000000">
</canvas>
<script>
    var c = document.getElementById("myCanvas3");
    var ctx = c.getContext("2d");
    ctx.font="30px Arial" //font-style(italic斜体),font-variant(small-caps小型大写字母),font-weight(),fong-size(),font-family()
    ctx.fillText("Hello World",50,50)    //填充型文字，坐标为50,50，内容是helloworld
    //ctx.strokeText("Hello World",50,50)    这个是空心的
</script>

<!--
线性渐变和径向渐变
径向渐变改成var grd=ctx.createRadialGradient(75,50,15,90,60,60);
分别表示，起始颜色的x,y,r和结束颜色的x,y,r
-->

<canvas id="myCanvas4" height="200" width="200" style="border:1px solid #000000">
</canvas>
<script>
    var c = document.getElementById("myCanvas4");
    var ctx = c.getContext("2d");
    //下边创建渐变
    var grd= ctx.createLinearGradient(0,0,200,0)   //设置渐变方向
    grd.addColorStop(0.0,"red");           //设置起始颜色
    //这中间可以添加无数个属性，在0-1之间就可以
    grd.addColorStop(1.0,"white");         //设置结束颜色

    //下边填充图形，用之前设置好的渐变
    ctx.fillStyle=grd;                 //设置填充方法为渐变
    ctx.fillRect(10,10,150,150)       //设置填充的矩形大小

</script>

<!--背景用图片绘制，类似于渐变-->

<canvas id="myCanvas6" height="600" width="600" style="border:1px solid #000000">
</canvas>
<script>
    var c = document.getElementById("myCanvas6");
    var ctx = c.getContext("2d");
    //创建一个图片
    var backgroundimg = new Image();     //new一个image
    backgroundimg.src="4.jpg";

    //下边创建背景图片
    var grd= ctx.createPattern(backgroundimg,"repeat")   //设置背景图片,repeat用引号

    //下边填充图形，用之前设置好的背景图
    ctx.fillStyle=grd;                 //设置填充方法为渐变
    ctx.fillRect(0,0,600,600)       //设置填充的矩形大小

</script>

<!--上边那个img也可以换成canvas对象-->

<canvas id="myCanvas7" height="600" width="600" style="border:1px solid #000000">
</canvas>
<script>
    var c = document.getElementById("myCanvas7");
    var ctx = c.getContext("2d");
    //创建一个图片
    var backCanvas = createBackgroundCanvas();

    //下边创建背景图片
    var grd= ctx.createPattern(backCanvas,"repeat")   //设置背景图片,repeat用引号

    //下边填充图形，用之前设置好的背景图
    ctx.fillStyle=grd;                 //设置填充方法为渐变
    ctx.fillRect(0,0,600,600)       //设置填充的矩形大小

    function createBackgroundCanvas(){
        //在这里创建一个canvas对象，作为背景
        var backcanvas = document.createElement("canvas");
        //在这个地方添加一个星星，往下就不写了
    }

</script>

<!--绘制图片-->

<canvas id="myCanvas5" height="200" width="200" style="border:1px solid #000000">
</canvas>
<script>
    var c = document.getElementById("myCanvas5");
    var ctx = c.getContext("2d");
    var img=document.getElementById("scream");
    ctx.drawImage(img,10,10)
</script>
[iconheading type=”h4″ style=”glyphicon glyphicon-arrow-right” color=”#dd3333″]七巧板[/iconheading]

<canvas id="canvas" style="display: block; margin:50px auto;border:1px solid #000000">
    浏览器不支持canvas，请更换浏览器
</canvas>
<script>
    var tangram=[
        {p:[{x:0,y:0},{x:800,y:0},{x:400,y:400}],color:"#caff67"},
        {p:[{x:0,y:0},{x:400,y:400},{x:0,y:800}],color:"#67beef"},
        {p:[{x:800,y:0},{x:800,y:400},{x:600,y:600},{x:600,y:200}],color:"#ef3d61"},
        {p:[{x:600,y:200},{x:600,y:600},{x:400,y:400}],color:"#f9f1a"},
        {p:[{x:400,y:400},{x:600,y:600},{x:400,y:800},{x:200,y:600}],color:"#a594c0"},
        {p:[{x:200,y:600},{x:400,y:800},{x:0,y:800}],color:"#fa8ccc"},
        {p:[{x:800,y:400},{x:800,y:800},{x:400,y:800}],color:"#f6ca29"}
    ]
    window.onload = function(){
        var canvas = document.getElementById("canvas");
        var context = canvas.getContext("2d");
        canvas.width=800;
        canvas.height=800;
        for(i=0;i<tangram.length;i++){
            draw(tangram[i],context)

        }

    }
    function draw(tangram_this,ctx){
        ctx.beginPath();
        ctx.moveTo(tangram_this.p[0].x,tangram_this.p[0].y);
        for(var i=1;i< tangram_this.p.length;i++){
            ctx.lineTo(tangram_this.p[i].x,tangram_this.p[i].y);    //这里一定要只让line循环，下边不用循环
        }
        ctx.closePath();
        ctx.fillStyle=tangram_this.color;
        ctx.fill();

    }

</script>

<!-- 圆和弧线 -->

<canvas id="canvas" width="500" height="500" style="border:1px solid #aaa;display:block;margin:50px auto;"></canvas>
<script>
    //下边是arc属性
        var canvas = document.getElementById("canvas");
        var context = canvas.getContext("2d");
        canvas.width = 500;
        canvas.height = 500;
        context.beginPath();
        context.arc(50,50,40,40,0,2*Math.PI );     //这个是绘制圆，x,y,r,start，stop,anticlockwise(这个是顺时针false)
        context.closePath();
        context.fill();

</script>
<canvas id="canvas1" width="500" height="500" style="border:1px solid #aaa;display:block;margin:50px auto;"></canvas>
<script>
    //下边是arcTo属性,他的起点是之前画的moveTo的起点或者lineTo的结尾为起点，为x0，y0

        var canvas = document.getElementById("canvas1");
        var context = canvas.getContext("2d");
        canvas.width = 500;
        canvas.height = 500;
        context.beginPath();
        context.moveTo(5,5);
        context.arcTo(400,0,400,600,200 );    //这个是绘制圆弧，x1,y1,x2,y2,radius
        context.lineWidth=6;
        context.strokeStyle="#000000";
        context.stroke();
        context.closePath();


</script>

<!-- 通过直线画多边形 -->

<canvas id="canvas" width="1024" height="500"></canvas>
<!--    <script>
        window.onload=function(){
            var canvas=document.getElementById("canvas");
            var context=canvas.getContext("2d");
            canvas.width=1024;
            canvas.height=500;
            if(context){                        //判断context是否存在
                //使用canvas绘图
            }
            else{
                alert("当前浏览器不支持canvas")
            }
        }
    </script>-->
    <script>
        //画和多线直线
        window.onload=function(){
            var canvas=document.getElementById("canvas");
            var context=canvas.getContext("2d");
            canvas.width=1024;
            canvas.height=500;

            context.beginPath();    //用来包围不同的图形
            context.moveTo(100,100);
            context.lineTo(700,700);
            context.lineTo(100,700);   //当只有三个点的时候，会从上到下依次连接起来
            context.lineTo(100,100);   //又设置回去的话，那就是一个三角形了
            context.closePath();   //用来包围不同的图形

            context.fillStyle="rgb(2,100,30)";  //这个是给多边形着色
            context.strokeStyle="red";
            context.fill();
            context.stroke();

            context.beginPath();    //用来包围不同的图形
            context.moveTo(200,100);
            context.lineTo(700,600);
            context.closePath();   //用来包围不同的图形
            context.lineWidth = 15;   //因为是看状态的，所以这个要在stroke（）之前定义
            context.strokeStyle="black";
            context.stroke();
        }
    </script>

<!-- 贝塞尔曲线 -->

<!--
    二次曲线
    例题：http://tinyurl.com/html5quadratic
    context.moveTo(69, 263);                  //起始点
    context.quadraticCurveTo(x1,y1,x2,y2)    //控制点，终点

-->

<canvas id="canvas" width="500" height="500" style="border:1px solid #aaa;display:block;margin:50px auto;"></canvas>
<script>
    //下边是arc属性
    var canvas = document.getElementById("canvas");
    var context = canvas.getContext("2d");
    canvas.width = 500;
    canvas.height = 500;
    context.beginPath();
    context.arc(50,50,40,40,0,2*Math.PI );     //这个是绘制圆，x,y,r,start，stop,anticlockwise(这个是顺时针false)
    context.closePath();
    context.fill();

</script>

<!--
    三次曲线
    例题：http://tinyurl.com/html5bezier
    context.moveTo(x0, y0);                  //起始点
    context.bezierCurveTo(x1,y1,x2,y2，x3,y3)    //控制点，控制点，终点
-->

<!-- 五角星 -->

<canvas id="canvas" width="800" height="800" style="border:1px solid #aaa;display:block;margin:50px auto;"></canvas>
<script>
    window.onload = function(){
        var canvas = document.getElementById("canvas");
        var context = canvas.getContext("2d");
        canvas.width = context.canvas.width;
        canvas.height = context.canvas.height;
        drawStar(context,150,300,400,400,10)
        context.lineWidth = 10;
        context.stroke();
    }
    function drawStar(cxt,r,R,x,y,rot){   //最后一个是旋转
        cxt.beginPath();
        for(var i= 0; i<5; i++){
            cxt.lineTo(Math.cos((18+i*72-rot)*Math.PI/180)*R+x,     //300是半径，cos内是弧度数，弧度数=圆心角*Math.PI/180
                    -Math.sin((18+i*72-rot)*Math.PI/180)*R+y
            )
            cxt.lineTo(Math.cos((54+i*72-rot)*Math.PI/180)*r+x,     //300是半径，cos内是弧度数，弧度数=圆心角*Math.PI/180
                    -Math.sin((54+i*72-rot)*Math.PI/180)*r+y
            )
        }
        cxt.closePath();
    }
</script>

<!-- 圆角矩形 -->

<canvas id="myCanvas" height="800" width="800" style="border:1px solid #000000">
</canvas>
<script>
    CanvasRenderingContext2D.prototype.roundRect = function (x, y, w, h, r) {
        //if (w < 2 * r) r = w / 2;
        //if (h < 2 * r) r = h / 2;
        this.beginPath();
        this.moveTo(x+r, y);
        this.arcTo(x+w, y, x+w, y+h, r);
        this.arcTo(x+w, y+h, x, y+h, r);
        this.arcTo(x, y+h, x, y, r);
        this.arcTo(x, y, x+w, y, r);
        // this.arcTo(x+r, y);
        this.closePath();
        return this;
    }
    var c = document.getElementById("myCanvas");
    var ctx = c.getContext("2d");
    ctx.strokeStyle="#000000";       //填充矩形内容颜色
    ctx.lineWidth=1;
    ctx.roundRect(200,300,200,120,40).stroke();     //绘制矩形

</script>

<!-- 星空 -->

<canvas id="canvas" width="800" height="800" style="border:1px solid #aaa;display:block;margin:50px auto;"></canvas>
<script>
    window.onload = function() {
        var canvas = document.getElementById("canvas");
        var context = canvas.getContext("2d");
        canvas.width = context.canvas.width;
        canvas.height = context.canvas.height;

        var grd= context.createLinearGradient(0,0,0,canvas.height);
        grd.addColorStop(0.0,"#000");           //设置起始颜色
        grd.addColorStop(1.0,"#035");         //设置结束颜色
        context.fillStyle=grd;

        context.fillRect(0, 0, context.canvas.width, context.canvas.height);

        for (i = 0; i < 200; i++) {
            var R = Math.random() * 20;
            var x = Math.random() * canvas.width;
            var y = Math.random() * canvas.height*0.65;
            var rot = Math.random() * 72;
            drawStar(context,R, x, y, rot);
        }
        function drawStar(cxt,R,x,y,rot){
            cxt.save();

            cxt.translate(x,y);
            cxt.scale(R,R);
            cxt.rotate(rot/180*Math.PI);

            //这里可以进行图形变换，之后再进行绘制
            starPath(cxt);

            //这里可以进行图形变换，之后再进行绘制
            cxt.fillStyle = "#FFFF00";
            cxt.fill();
            //都画完了，再进行关闭路径
            cxt.restore();

        }

        //绘制一个标准五角星(然后通过缩放，旋转，位移，来增加图形)
        function starPath(cxt) {   //最后一个是旋转
            cxt.beginPath();
            for (var i = 0; i < 5; i++) {
                cxt.lineTo(Math.cos((18 + i * 72) * Math.PI / 180) ,     //300是半径，cos内是弧度数，弧度数=圆心角*Math.PI/180
                        -Math.sin((18 + i * 72) * Math.PI / 180)
                )
                cxt.lineTo(Math.cos((54 + i * 72) * Math.PI / 180) *0.5,     //300是半径，cos内是弧度数，弧度数=圆心角*Math.PI/180
                        -Math.sin((54 + i * 72) * Math.PI / 180) * 0.5
                )
            }
            cxt.closePath();

        }

        /*//绘制一个五角星
        function drawStar(cxt, r, R, x, y, rot) {   //最后一个是旋转
            cxt.beginPath();
            for (var i = 0; i < 5; i++) {
                cxt.lineTo(Math.cos((18 + i * 72 - rot) * Math.PI / 180) * R + x,     //300是半径，cos内是弧度数，弧度数=圆心角*Math.PI/180
                        -Math.sin((18 + i * 72 - rot) * Math.PI / 180) * R + y
                )
                cxt.lineTo(Math.cos((54 + i * 72 - rot) * Math.PI / 180) * r + x,     //300是半径，cos内是弧度数，弧度数=圆心角*Math.PI/180
                        -Math.sin((54 + i * 72 - rot) * Math.PI / 180) * r + y
                )
            }
            cxt.closePath();
            context.fillStyle = "#FFFF00"
            context.fill();
        }*/
    }
</script>

<!-- 倒计时实例 -->

<canvas id="canvas" style="width: 100%; height: 100%;"></canvas>
<script>
   
    var WINDOW_WIDTH = document.body.clientWidth;
    var WINDOW_HEIGHT = document.body.clientHeight;

    var MARGIN_LEFT = Math.round(WINDOW_WIDTH /10);
    var MARGIN_TOP = Math.round(WINDOW_HEIGHT /5);
    
    var RADIUS =Math.round(WINDOW_WIDTH*4/5/108)-1;

   console.log(RADIUS);
    var balls=[];
    const colors = ["#33B5E5","#0099CC","#AA66CC","#9933CC","#99CC00","#669900","#FFBB33","#FF8800","#FF4444","#CC0000"];

    window.onload = function(){
        var canvas = document.getElementById("canvas");
        var context = canvas.getContext("2d");
        canvas.width = WINDOW_WIDTH;
        canvas.height = WINDOW_HEIGHT;
        curShowTimeSeconds = getCurrentShowTimeSeconds();
        //第四步，让时间数开始循环，通过update()来更新
        setInterval(function(){
            render(context);
            update();
        },50);
    }
    //第五步，让这个电子钟循环起来，记得更新之前要清空矩形
    function update(){
        var nextShowTimeSeconds = getCurrentShowTimeSeconds();   //因为是在setInterval里循环，所以curShowTimenSeconds一直都是上边得到的值，必须通过update从新取一次才行，要不然是不变的

        //上边这些就已经足够让数字进行循环了，下边是为了方便出现彩色的小球才做的定义
        var nextHours =parseInt(nextShowTimeSeconds/3600);
        var nextMinutes = parseInt((nextShowTimeSeconds/60)%60);
        var nextSeconds = nextShowTimeSeconds%60;

        var curHours = parseInt( curShowTimeSeconds / 3600);
        var curMinutes = parseInt((curShowTimeSeconds/60)%60);
        var curSeconds = curShowTimeSeconds % 60;

        //第六步，来判断哪个数字变化了，给变化的数字增加彩色小球
        if(nextSeconds != curSeconds){
            //下边分别比较他们的时分秒，看是否相同，不同的话，来触发addBalls()
            if(parseInt(nextHours/10) != parseInt(curHours/10)){
                addBalls(MARGIN_LEFT,MARGIN_TOP,parseInt(nextHours/10));
            }
            if(parseInt(nextHours%10) != parseInt(curHours%10)){
                addBalls(MARGIN_LEFT+15*(RADIUS+1),MARGIN_TOP,parseInt(nextHours%10));
            }
            if(parseInt(nextMinutes/10) != parseInt(curMinutes/10)){
                addBalls(MARGIN_LEFT+39*(RADIUS+1),MARGIN_TOP,parseInt(nextMinutes/10));
            }
            if(parseInt(nextMinutes%10) != parseInt(curMinutes%10)){
                addBalls(MARGIN_LEFT+54*(RADIUS+1),MARGIN_TOP,parseInt(nextMinutes%10));
            }
            if(parseInt(nextSeconds/10) != parseInt(curSeconds/10)){
                addBalls(MARGIN_LEFT+78*(RADIUS+1),MARGIN_TOP,parseInt(nextSeconds/10));
            }
            if(parseInt(nextSeconds%10) != parseInt(curSeconds%10)){
                addBalls(MARGIN_LEFT+93*(RADIUS+1),MARGIN_TOP,parseInt(nextSeconds%10));
            }
            curShowTimeSeconds = nextShowTimeSeconds;

        }
        updateBalls();
        //console.log(balls.length)
    }

    //第七步，给变化的数字增加小球，推送到balls的数组内，只是推送到数组内把属性，并没有绘制小球，只是定义了一个数组，来存储属性，在第二步下边那给画出来了。

    function addBalls(x,y,num){
        for(i=0;i<digit[num].length;i++){
            for(j=0;j<digit[num][i].length;j++){
               if(digit[num][i][j]==1){
                    var aBall ={
                        x:x+2*j*(RADIUS+1)+(RADIUS+1),
                        y:y+2*i*(RADIUS+1)+(RADIUS+1),
                        g:1.5+Math.random(),
                        vx:Math.pow(-1,Math.ceil(Math.random()*10))*4,
                        vy:-5,
                        color: colors[ Math.floor( Math.random()*10 ) ]
                        };

                   balls.push(aBall);

               }
            }
        }
    }

    //第八步，来让数组内的属性，来分别组成小球并让小球动起来
    function updateBalls(){
        for(i=0;i<balls.length;i++){      //因为所有的小球都要表现出来，所以for出来
            balls[i].x+=balls[i].vx;
            balls[i].y+=balls[i].vy;
            balls[i].vy+=balls[i].g;
            if(balls[i].y>=WINDOW_HEIGHT-RADIUS){
                balls[i].y=WINDOW_HEIGHT-RADIUS;
                balls[i].vy=-balls[i].vy*0.75
            }
        }

        /*for(i=0;i<balls.length;i++){        //这种方法是自己想的，比较好理解
             if(balls[i].x>WINDOW_WIDTH||balls[i].x<0){
             balls.splice(i,1)   //超出后，删除当前值，splice的意思是删除角标为i的后1个数组（含角标元素），所以这个相当于删除其自身！！
             }
        }*/
        var cnt = 0
        for( var i = 0 ; i < balls.length ; i ++ )
            if( balls[i].x + RADIUS > 0 &amp;&amp; balls[i].x -RADIUS < WINDOW_WIDTH )
                balls[cnt++] = balls[i]

        while( balls.length > cnt ){
            //console.log(balls)
            balls.pop();     //删后push进去的，是因为删掉前边的就显得空了，不能还没走到头就给人家删掉，所以这里用的pop（）；完全可以把上边的push换成unshift，然后下边的用pop();
        }

    }

    //第三步，获取倒计时的具体时间数
    function getCurrentShowTimeSeconds(){
        var date_now = new Date();
        var date_after = new Date(2015,6,29,11,11,11);   //记住月份是要提前一个月的，1月是0
        var time_after = date_after.getTime();
        var time = Math.round((time_after-date_now.getTime())/1000);
        return time>=0?time:0;
    }
    function render(cxt){
        cxt.clearRect(0,0,WINDOW_WIDTH,WINDOW_HEIGHT);  //清空矩形，x,y,width,height

        var hours = parseInt(curShowTimeSeconds/3600);
        var minutes = parseInt((curShowTimeSeconds/60)%60);
        var seconds = curShowTimeSeconds%60;

    //（第二步，给出相应的变量，来设置数字的位置）这个是先给每个大数字来设定一个起始位置的初始值，通过renderDigit来分别将圆分布开
    renderDigit(MARGIN_LEFT,MARGIN_TOP,parseInt(hours/10),cxt);
    renderDigit(MARGIN_LEFT+15*(RADIUS+1),MARGIN_TOP,parseInt(hours%10),cxt);
    renderDigit(MARGIN_LEFT+30*(RADIUS+1),MARGIN_TOP,10,cxt);
    renderDigit(MARGIN_LEFT+39*(RADIUS+1),MARGIN_TOP,parseInt(minutes/10),cxt);
    renderDigit(MARGIN_LEFT+54*(RADIUS+1),MARGIN_TOP,parseInt(minutes%10),cxt);
    renderDigit(MARGIN_LEFT+69*(RADIUS+1),MARGIN_TOP,10,cxt);
    renderDigit(MARGIN_LEFT+78*(RADIUS+1),MARGIN_TOP,parseInt(seconds/10),cxt);
    renderDigit(MARGIN_LEFT+93*(RADIUS+1),MARGIN_TOP,parseInt(seconds%10),cxt)

        //（！！！！！！很重要！！！！！）之前那个数组只是小球的属性，在这里让他显示出来
        for( var i = 0 ; i < balls.length ; i ++ ){
            cxt.fillStyle=balls[i].color;

            cxt.beginPath();
            cxt.arc( balls[i].x , balls[i].y , RADIUS , 0 , 2*Math.PI , true );
            cxt.closePath();

            cxt.fill();
        }
    }
    //（第一步，先循环，试图画出整个图形）一共是三层，但是num就是第一层是通过上边的数据给出的，所以这里不去循环
    function renderDigit(x,y,num,cxt){
        for(i=0;i<digit[num].length;i++){
            for(j=0;j<digit[num][i].length;j++) {
                if(digit[num][i][j]==1){
                    cxt.beginPath();
                    cxt.arc(x+2*j*(RADIUS+1)+(RADIUS+1),y+2*i*(RADIUS+1)+(RADIUS+1),RADIUS,0,2*Math.PI);
                    cxt.closePath();
                    cxt.fillStyle="rgb(0,102,153)";
                    cxt.fill();
                }
            }

        }
    }
</script>
```


# 9.内联SVG

参考文献：http://www.w3school.com.cn/svg/index.asp（这个是教程）
SVGAPI：https://developer.mozilla.org/zh-CN/docs/Web/SVG/Element（这个是事例，可以直接引用）
可以直接用flash直接生成svg文件
**引入外部SVG文件：**
```
<iframe src=”svg.svg” width=”1000″ height=”1000″ frameborder=”no”><iframe>
```

``` js
<!--viewBox是建了一个层，这个层的尺寸大小，而width和height是画布的大小-->

<svg width="800" height="800" viewBox="0 0 800 600">
</svg>

<!--stroke属性是描述线框的

stroke            可以描述框颜色
stroke-width      线框宽度
stroke-linecap    线框两端形状，有butt（没有加长方框）round圆角框，square方框边
stroke-dasharray  虚线 stroke-dasharray="5,5"其中5,5是每段的宽度-->

<!--下边是对线框的演示，g是包裹所有的路径，来统一设置了属性值-->
<svg>
    <g fill="none" stroke="black">
        <path stroke-dasharray="20,10,5,3,9" d="M20 6 10 20"/>
    </g>
</svg>

<div class="svg">

    <!--绘制圆形，圆形坐标用cx,cy表示-->

<svg height="100">
    <circle id="redcircle" cx="50" cy="100" r="50" fill="red" />
</svg>

    <!--绘制矩形-->

<svg>
    <!--圆角矩形，矩形坐标用x,y来表示-->
    <rect x="50" y="20" rx="20" ry="20" width="150" height="150" style="fill:red;stroke:black;stroke-width:5;opacity:0.5"/>
    <rect width="200" height="800" x="10" y="20" style="fill:blue;stroke:pink;stroke-width:5;fill-opacity:0.1;
    stroke-opacity:0.9"/>
</svg>

    <!--绘制线-->

    <svg>
        <line x1="0" y1="0" x2="100" y2="100" style="stroke:red;stroke-width:2"/>
    </svg>

    <!--绘制椭圆，cx，cy设置坐标，rx为横向半径，ry为纵向半径-->

<svg>
    <ellipse cx="100" cy="50" rx="100" ry="50" fill="red"/>
</svg>

    <!--绘制多边形，多边形连接是有顺序的，按坐标的点来排列，可以同过stroke来增加边框查看走向,evenodd是空心，nonzero是实心-->
    <!--polygon:画多边形标签
    points：多边形组成的坐标点
    fill：长方形的填充颜色
    stroke：长方形的边框颜色
    stroke-width：边框宽带
    fill-opacity：长方形的透明度
    stroke-opacity：边框的透明度
    fill-rule：的属性值有nonzero，evenodd两种
    nonzero:本规则决定一个点是否在图形内部的方法是从该点向任意方向画直线，然后检查直线与图形的交叉。如果该点左右与图形交叉点数相同，则该点在图形外，否则在图形内。
    evenodd:本规则通过从一点向任意方向画直线然后计算该直线与图形的交叉电的数量来决定该点是否在图形内。如果交叉点数为奇数，则该点在图形内，否则在图形外。
    -->
    <svg>
        <polygon  points="20,10 300,20, 170,50" fill="red" />
        <polygon points="100,10 40,180 190,60 10,60 160,180" style="fill:lime;stroke:purple;stroke-width:5;fill-rule:evenodd;"/>
    </svg>

    <!--绘制折线（曲线）-->

    <svg>
        <polyline points="10,10 300,10 150,20 10,30 300,30 150,40 " fill="red"/>
    </svg>

    <!--绘制路径-->

    <!--
    M = moveto
    L = lineto
    H = horizontal lineto
    V = vertical lineto
    C = curveto
    S = smooth curveto
    Q = quadratic Bézier curve
    T = smooth quadratic Bézier curveto
    A = elliptical Arc
    Z = closepath
    所有命令均允许小写字母。大写表示绝对定位，小写表示相对定位
    -->
    <svg>
        <path d="M150 0 L75 200 L225 200 Z" />
    </svg>

    <!--二次贝塞尔曲线-->

    <svg xmlns="http://www.w3.org/2000/svg" version="1.1">
        <path id="lineAB" d="M 100 350 l 150 -300" stroke="red"
              stroke-width="3" fill="none" />
        <path id="lineBC" d="M 250 50 l 150 300" stroke="red"
              stroke-width="3" fill="none" />
        <path d="M 175 200 l 150 0" stroke="green" stroke-width="3"
              fill="none" />
        <path d="M 100 350 q 150 -300 300 0" stroke="blue"
              stroke-width="5" fill="none" />
        <!-- Mark relevant points -->
        <g stroke="black" stroke-width="3" fill="black">
            <circle id="pointA" cx="100" cy="350" r="3" />
            <circle id="pointB" cx="250" cy="50" r="3" />
            <circle id="pointC" cx="400" cy="350" r="3" />
        </g>
        <!-- Label the points -->
        <g font-size="30" font="sans-serif" fill="black" stroke="none"
           text-anchor="middle">
            <text x="100" y="350" dx="-30">A</text>
            <text x="250" y="50" dy="-10">B</text>
            <text x="400" y="350" dx="30">C</text>
        </g>
    </svg>

    <!--文本-->

    <svg>
        <text x="0" y="15" fill="red">I love SVG</text>
    </svg>

    <!--倾斜文本-->
    <!--rotate中的30是倾斜角度，20,40是设置的中心点坐标-->
    <!--transform="translate(100 200)"来设置图像移动，x轴是100，y轴是200-->
    <!--transform="scale(2)"或者transform="scale(2 0.5)"这个是将图像放大2倍，如果是正方形则，x轴增加2倍，y轴压缩0.5倍-->

    <text x="0" y="15" fill="red" transform="rotate(30 20,40)">I LOVE SVG</text>

    <!--路径上的文字,defs可以删除掉路径的黑底色-->

    <svg>
        <defs>
            <path id="path1" d="M75,20 a1,1 0 0,0 100,0"/>
        </defs>
        <text x="10" y="100" style="fill:red;">
            <textPath xlink:href="#path1">I LOVE SVG I LOVE SVG</textPath>
        </text>
    </svg>

    <!--文字元素可以分小组，来不同格式和位置,用tspan标签包裹-->

    <svg>
        <text x="10" y="10" fill="red">HELLO
            <tspan x="20" y="20">GAGA</tspan>
            <tspan x="20" y="20">HOHO</tspan>
        </text>
    </svg>

    <!--连接文本-->

    <svg>
        <a xlink:href="http://www.pengweb.net" target="_blank">
            <text x="10" y="10" fill="red">I LOVE SVG</text>
        </a>
    </svg>


    <!--svg滤镜

    feBlend - 与图像相结合的滤镜
    feColorMatrix - 用于彩色滤光片转换
    feComponentTransfer
    feComposite
    feConvolveMatrix
    feDiffuseLighting
    feDisplacementMap
    feFlood
    feGaussianBlur
    feImage
    feMerge
    feMorphology
    feOffset - 过滤阴影
    feSpecularLighting
    feTile
    feTurbulence
    feDistantLight - 用于照明过滤
    fePointLight - 用于照明过滤
    feSpotLight - 用于照明过滤

    -->

<!--下边只对高斯模糊和阴影做解释-->
<!--高斯模糊，所有的svg滤镜都要定义在defs内，filter来定义用什么滤镜-->

   <!-- filter的id是唯一的名称
    feGaussianBlur元素来定义模糊
    in=“SourceGraphic” 是来定义 整个 图像创建效果
    stdDeviation属性是来定义模糊量
    rect元素的滤镜属性用来把元素连接到f1滤镜中-->

    <svg>
        <defs>
            <filter id="f1" x="0" y="0">
                <feGaussianBlur in="SourceGraphic" stdDeviation="15"/>
            </filter>
        </defs>
        <rect width="90" height="90" stroke="green" stroke-width="3"
              fill="yellow" filter="url(#f1)" />
    </svg>

    <!--阴影效果-->

    <svg>
        <defs>
            <filter id="f1" x="0" y="0" width="200%" height="200%">
                <feOffset  in="SourceGraphic" dx="20" dy="20" />
                <feGaussianBlur   stdDeviation="10" />
                <feBlend in="SourceGraphic"   />
            </filter>
        </defs>
        <rect width="90" height="90" stroke="green" stroke-width="3" fill="yellow" filter="url(#f1)" />
    </svg>

<!--例子2，给阴影图上一层颜色-->

    <svg xmlns="http://www.w3.org/2000/svg" version="1.1">
        <defs>
            <filter id="f1" x="0" y="0" width="200%" height="200%">
                <feOffset  in="SourceGraphic" dx="20" dy="20" />
                <feColorMatrix  type = "matrix" values = "0.2 0 0 0 0 0 0.2 0 0 0 0 0 0.2 0 0 0 0 0 1 0"/>
                <feGaussianBlur   stdDeviation="10" />
                <feBlend in="SourceGraphic"   />
            </filter>
        </defs>
        <rect width="90" height="90" stroke="green" stroke-width="3" fill="yellow" filter="url(#f1)" />
    </svg>
    <!--

    渐变分为linear（线性）和radial（放射性）
    同样必须嵌套在<defs>内这个是definitions的缩写
    当y1和y2相等，而x1和x2不同时，可创建水平渐变
    当x1和x2相等，而y1和y2不同时，可创建垂直渐变
    当x1和x2不同，且y1和y2不同时，可创建角形渐变

    -->
    <!--

    绘制渐变
    水平：x1="0%" y1="0%" x2="100%" y2="0%"
    垂直：x1="0%" y1="0%" x2="0%" y2="100%"

    -->
    <svg>
        <defs>
            <linearGradient id="grad1" x1="0%" y1="0%" x2="100%" y2="0%">
                <stop offset="0%" style="stop-color:rgb(255,255,0);stop-opacity:1"/>
                <stop offset="100%" style="stop-color:rgb(255,0,0);stop-opacity:1"/>
            </linearGradient>
        </defs>
        <ellipse rx="100" ry="50" cx="100" cy="100" fill="url(#grad1)" />
    </svg>

    <!--在上边这个椭圆渐变内加文字-->

    <svg>
        <defs>
            <linearGradient id="grad1" x1="0%" y1="0%" x2="100%" y2="0%">
                <stop offset="0%" style="stop-color:rgb(255,255,0);stop-opacity:1"/>
                <stop offset="100%" style="stop-color:rgb(255,0,0);stop-opacity:1"/>
            </linearGradient>
        </defs>
        <ellipse rx="100" ry="50" cx="100" cy="100" fill="url(#grad1)" />
        <text fill="#ffffff" font-size="45" font-family="Verdana" x="150" y="86">
            SVG
        </text>
    </svg>

     <!--

     放射性渐变，主要区别就是坐标问题，还有起始的透明度，还有记得把linearGradient改成radialGradient
     cx和cy是移动整个里边变白的位置
     r是里边光圈所占比例
     fx和fy是光源点的移动

     -->
    <svg>
        <defs>
            <radialGradient id="grad2" cx="50%" cy="50%" r="50%" fx="50%" fy="50%">
                <stop offset="0%" style="stop-color:rgb(255,255,0);stop-opacity:0"/>
                <stop offset="100%" style="stop-color:rgb(255,0,0);stop-opacity:1"/>
            </radialGradient>
        </defs>
        <ellipse rx="100" ry="50" cx="100" cy="100" fill="url(#grad2)" />
    </svg>


</div>
```


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