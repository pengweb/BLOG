---
title: SVG--学习笔记
date: 2016-04-29 13:48:23
tags: [svg,html5,note]

---
# 1. 优势：
1.SVG 图像可通过文本编辑器来创建和修改
2.可以用CSS样式来自由定义图标颜色，比如颜色/尺寸等效果。
3.SVG 图像可被搜索、索引、脚本化或压缩（例如做地图）
4.由于SVG也是一种XML节点的文件，所以可以使用gzip的方式把文件压缩到很小。
5.SVG是矢量图形文件，可以随意改变大小，而不影响图标质量。
6.所有的SVG可以全部在一个文件中，节省HTTP请求 。
7.使用SMIL、CSS或者是javascript可以制作充满灵性的交互动画效果。
8.比flash与其他标准（XSL和DOM）兼容性更好一些

# 2. 直接生成SVG 
用`flash`可以直接**生成**svg文件

# 3.引入SVG
方法一：
```js
<img src="data:image/svg+xml;base64,[data]>
```
方法二：
```js
.logo {
  background: url(data:image/svg+xml;base64,[data]);
}
```
方法三：
```js
<object data="rect.svg" width="300" height="100" 
type="image/svg+xml"
codebase="http://www.adobe.com/svg/viewer/install/" />
```
方法四：(支持更广泛)
```js
<iframe src=”svg.svg” width=”1000″ height=”1000″ frameborder=”no”><iframe>
```
方法五：
```js
<embed src="rect.svg" width="300" height="100" 
type="image/svg+xml"
pluginspage="http://www.adobe.com/svg/viewer/install/" />
```
[参考文献](http://www.webhek.com/demo/svg)

# 4.练习

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
参考文献：http://www.w3school.com.cn/svg/index.asp（这个是教程）
SVGAPI：https://developer.mozilla.org/zh-CN/docs/Web/SVG/Element（这个是事例，可以直接引用）