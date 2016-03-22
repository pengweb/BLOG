---
title: 'offsetHeight,clientHeight,scrollHeight之间的区别'
date: 2016-03-21 22:29:13
tags: [javascript,js,offsetheight,clientheight,scrollheight]

---
网页可见区域宽： document.body.clientWidth;

网页可见区域高： document.body.clientHeight;

网页可见区域宽： document.body.offsetWidth   (包括边线的宽);

网页可见区域高： document.body.offsetHeight (包括边线的宽);

网页正文全文宽： document.body.scrollWidth;

网页正文全文高： document.body.scrollHeight;

网页被卷去的高： document.body.scrollTop;

网页被卷去的左： document.body.scrollLeft;

网页正文部分上： window.screenTop;

网页正文部分左： window.screenLeft;

屏幕分辨率的高： window.screen.height;

屏幕分辨率的宽： window.screen.width;

屏幕可用工作区高度： window.screen.availHeight;

当前对象到顶部（包含卷进去的）距离： document.body.offsetTop;

JQuery:

$(document).ready(function(){
alert($(window).height()); //浏览器当前窗口可视区域高度
alert($(document).height()); //浏览器当前窗口文档的高度
alert($(document.body).height());//浏览器当前窗口文档body的高度
alert($(document.body).outerHeight(true));//浏览器当前窗口文档body的总高度 包括border padding margin

alert($(window).width()); //浏览器当前窗口可视区域宽度
alert($(document).width());//浏览器当前窗口文档对象宽度
alert($(document.body).width());//浏览器当前窗口文档body的宽度
alert($(document.body).outerWidth(true));//浏览器当前窗口文档body的总宽度 包括border padding margin

})

<hr />

![](/images/54586e9b0001838b05000495.jpg)

![](/images/图解.jpg)

jQuery取鼠标高度用

$('body,html').scrollTop();和$(document.body).scrollTop()     火狐不兼容
<div>$(window).scrollTop();       这个火狐和chrome都兼容</div>
<div>例：</div>
<div>
<pre>$(function(){
  $(window).scroll(function(){
      var offsetTop =$(document.body).scrollTop();  /*$('body,html').scrollTop();也可以*/
      console.log(offsetTop);
  })
})</pre>
</div>
<div></div>
<div>js用：</div>
<div>完美的获取scrollTop 赋值短语 ：
var scrollTop = document.documentElement.scrollTop || window.pageYOffset || document.body.scrollTop;</div>
<div>例子：</div>
<div>
<pre>window.onload = function () {
    window.onscroll = function () {
        var mouseH = document.body.scrollTop;
        console.log(mouseH);
        }
    };
</pre>

<hr />

先总结下区别：

<strong>event.clientX、event.clientY</strong>

鼠标相对于浏览器窗口可视区域的X，Y坐标（窗口坐标），可视区域不包括工具栏和滚动条。IE事件和标准事件都定义了这2个属性

<strong>event.pageX、event.pageY</strong>

类似于event.clientX、event.clientY，但它们使用的是文档坐标而非窗口坐标。这2个属性不是标准属性，但得到了广泛支持。IE事件中没有这2个属性。

<strong>event.offsetX、event.offsetY</strong>

鼠标相对于事件源元素（srcElement）的X,Y坐标，只有IE事件有这2个属性，标准事件没有对应的属性。

<strong>event.screenX、event.screenY</strong>

鼠标相对于用户显示器屏幕左上角的X,Y坐标。标准事件和IE事件都定义了这2个属性

上图！！！！
![](/images/2014091409260873.png)

</div>