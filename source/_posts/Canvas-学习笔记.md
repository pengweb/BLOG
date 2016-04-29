---
title: Canvas--学习笔记
date: 2016-04-29 13:50:14
tags: [canvas,html5,note]

---
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
