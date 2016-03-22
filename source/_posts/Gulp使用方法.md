---
title: Gulp使用方法
date: 2016-03-21 22:53:54
tags: [others,gulp]

---
<h3>一.可以通过终端命令中安装glup运行工具</h3>

①将gulp安装到全局
<blockquote>npm install -g gulp</blockquote>
②打开工程目录，在工程目录下再安装一次gulp
<blockquote>npm install gulp</blockquote>
③如果想把gulp写进package.json内的话，再执行一次
<blockquote>npm install --save-dev gulp</blockquote>

<h3>二.建立gulpfile.js</h3>

直接在根目录下新建一个就可以，基本内容示例如下


<h3>三、gulp的API介绍</h3>

使用gulp，仅需知道4个API即可：gulp.task(),gulp.src(),gulp.dest(),gulp.watch()
gulp的使用流程一般是这样子的：首先通过gulp.src()方法获取到我们想要处理的文件流，然后把文件流通过pipe方法导入到gulp的插件中，最后把经过插件处理后的流再通过pipe方法导入到gulp.dest()中，gulp.dest()方法则把流中的内容写入到文件中

<h4>1.gulp.src()</h4>
方法是用来获取流的，但要注意这个流里的内容不是原始的文件流，而是一个虚拟文件对象流(Vinyl files)，这个虚拟文件对象中存储着原始文件的路径、文件名、内容等信息，其实主要就是用这个方法来读取你需要操作的文件，语法为：
<blockquote>gulp.src(globs\[, options])</blockquote>
globs参数是文件匹配模式(类似正则表达式)，用来匹配文件路径(包括文件名)，当然这里也可以直接指定某个具体的文件路径。当有多个匹配模式时，该参数可以为一个数组。
options为可选参数。通常情况下我们不需要用到。
示例：
<blockquote>gulp.src(\['js/\*.js','css/\*.css','\*.html'])    //使用数组的方式来匹配多种文件
gulp.src(\[\*.js,'!b\*.js']) //匹配所有js文件，但排除掉以b开头的js文件
gulp.src(\['!b\*.js',\*.js]) //不会排除任何文件，因为排除模式不能出现在数组的第一个元素中</blockquote>


<h4>2.gulp.dest()</h4>
方法是用来写文件的，其语法为：


<blockquote>gulp.dest(path\[,options])</blockquote>

path为写入文件的路径
options为一个可选的参数对象，通常我们不需要用到
使用示例：


<blockquote>gulp.src(script/lib/*.js) //没有配置base参数，此时默认的base路径为script/lib
    //假设匹配到的文件为script/lib/jquery.js
    .pipe(gulp.dest('build')) //生成的文件路径为 build/jquery.js

gulp.src(script/lib/*.js, {base:'script'}) //配置了base参数，此时base路径为script
    //假设匹配到的文件为script/lib/jquery.js
    .pipe(gulp.dest('build')) //此时生成的文件路径为 build/lib/jquery.js</blockquote>


<h4>3.gulp.task</h4>
方法用来定义任务，内部使用的是Orchestrator，其语法为：   
gulp.task(name\[, deps], fn)
name 为任务名
deps 是当前定义的任务所需要<strong>依赖</strong>的其他任务，为一个数组。依赖任务先执行，且从左至右依次执行，fn内为mytask执行的任务

<blockquote>gulp.task('mytask', \['array', 'of', 'task', 'names'], function() { //定义一个有依赖的任务
  // Do something
});</blockquote>

如果依赖的任务是<strong>异步</strong>的，当前定义的任务不会等到以来任务完成，而是直接向下进行

<blockquote>gulp.task('one',function(){
  //one是一个异步执行的任务
  setTimeout(function(){
    console.log('one is done')
  },5000);
});

//two任务虽然依赖于one任务,但并不会等到one任务中的异步操作完成后再执行
gulp.task('two',\['one'],function(){
  console.log('two is done');
});</blockquote>


<h4>4.gulp.watch()</h4>
用来监视文件的变化，当文件发生变化后，我们可以利用它来执行相应的任务，例如文件压缩等。其语法为


<blockquote>gulp.watch(glob\[, opts], tasks)</blockquote>
glob 为要监视的文件匹配模式，规则和用法与gulp.src()方法中的glob相同。
opts 为一个可选的配置对象，通常不需要用到
tasks 为文件变化后要执行的任务，为一个数组

<blockquote>gulp.task('uglify',function(){
  //do something
});
gulp.task('reload',function(){
  //do something
});
gulp.watch('js/**/*.js', \['uglify','reload']);</blockquote>


gulp.watch()还有另外一种使用方式：

<blockquote>gulp.watch(glob\[, opts, cb])</blockquote>


glob和opts参数与第一种用法相同
cb参数为一个函数。每当监视的文件发生变化时，就会调用这个函数,并且会给它传入一个对象，该对象包含了文件变化的一些信息，type属性为变化的类型，可以是added,changed,deleted；path属性为发生变化的文件的路径

gulp.watch('js/**/*.js', function(event){
    console.log(event.type); //变化类型 added为新增,deleted为删除，changed为改变 
    console.log(event.path); //变化的文件的路径
}); 

同时监听多个文件：
<blockquote>gulp.task('watch', function() {
  // Watch .scss files
  gulp.watch('src/styles/\*\*/\*.scss', \['styles']);
  // Watch .js files
  gulp.watch('src/scripts/\*\*/\*.js', \['scripts']);
  // Watch image files
  gulp.watch('src/images/\*\*/\*', \['images']);
});</blockquote>


<h3>四、设置默认任务（default）</h3>


我们在命令行下输入$ gulp执行的就是默认任务，现在我们为默认任务指定执行上面写好的三个任务：

<blockquote>gulp.task('default', \['clean'], function() {
    gulp.start('styles', 'scripts', 'images');
});</blockquote>

在这个例子里面，clean任务执行完成了才会去运行其他的任务，在gulp.start()里的任务执行的顺序是不确定的，所以将要在它们之前执行的任务写在数组里面。


<h3>五、插件配置</h3>

<p></p>



<h4>4.1 自动加载插件</h4>


使用gulp-load-plugins
安装：npm install --save-dev gulp-load-plugins
要使用gulp的插件，首先得用require来把插件加载进来，如果我们要使用的插件非常多，那我们的gulpfile.js文件开头可能就会是这个样子的：



<blockquote>var gulp = require('gulp'),
    //一些gulp插件,abcd这些命名只是用来举个例子
    a = require('gulp-a'), 
    b = require('gulp-b'),
    c = require('gulp-c'),
    d = require('gulp-d'),
    e = require('gulp-e'),
    f = require('gulp-f'),
    g = require('gulp-g'),
    //更多的插件...
    z = require('gulp-z');   </blockquote>


虽然这没什么问题，但会使我们的gulpfile.js文件变得很冗长，看上去不那么舒服。gulp-load-plugins插件正是用来解决这个问题。
gulp-load-plugins这个插件能自动帮你加载package.json文件里的gulp插件。例如假设你的package.json文件里的依赖是这样的:



<blockquote>{
  "devDependencies": {
    "gulp": "~3.6.0",
    "gulp-rename": "~1.2.0",
    "gulp-ruby-sass": "~0.4.3",
    "gulp-load-plugins": "~0.5.1"
  }
}</blockquote>


然后我们可以在gulpfile.js中使用gulp-load-plugins来帮我们加载插件：



<blockquote>var gulp = require('gulp');
//加载gulp-load-plugins插件，并马上运行它
var plugins = require('gulp-load-plugins')();</blockquote>


然后我们要使用gulp-rename和gulp-ruby-sass这两个插件的时候，就可以使用plugins.rename和plugins.rubySass来代替了,也就是原始插件名去掉gulp-前缀，之后再转换为驼峰命名。
实质上gulp-load-plugins是为我们做了如下的转换



<blockquote>plugins.rename = require('gulp-rename');
plugins.rubySass = require('gulp-ruby-sass');</blockquote>


gulp-load-plugins并不会一开始就加载所有package.json里的gulp插件，而是在我们需要用到某个插件的时候，才去加载那个插件。
最后要提醒的一点是，因为gulp-load-plugins是通过你的package.json文件来加载插件的，所以必须要保证你需要自动加载的插件已经写入到了package.json文件里，并且这些插件都是已经安装好了的。


<h4>4.2 重命名</h4>


使用gulp-rename
安装：


<blockquote>npm install --save-dev gulp-rename</blockquote>


用来重命名文件流中的文件。用gulp.dest()方法写入文件时，文件名使用的是文件流中的文件名，如果要想改变文件名，那可以在之前用gulp-rename插件来改变文件流中的文件名。


<blockquote>var gulp = require('gulp'),
    rename = require('gulp-rename'),
    uglify = require("gulp-uglify");
 
gulp.task('rename', function () {
    gulp.src('js/jquery.js')
    .pipe(uglify())  //压缩
    .pipe(rename('jquery.min.js')) //会将jquery.js重命名为jquery.min.js
    .pipe(gulp.dest('js'));
    //关于gulp-rename的更多强大的用法请参考https://www.npmjs.com/package/gulp-rename
});</blockquote>



<h4>4.3 js文件压缩</h4>


使用gulp-uglify
安装：

<blockquote>npm install --save-dev gulp-uglify</blockquote>


用来压缩js文件，使用的是uglify引擎



<blockquote>var gulp = require('gulp'),
    uglify = require("gulp-uglify");
 
gulp.task('minify-js', function () {
    gulp.src('js/*.js') // 要压缩的js文件
    .pipe(uglify())  //使用uglify进行压缩,更多配置请参考：
    .pipe(gulp.dest('dist/js')); //压缩后的路径
});</blockquote>



<h4>4.4 css文件压缩</h4>


使用gulp-minify-css
安装：


<blockquote>npm install --save-dev gulp-minify-css</blockquote>


要压缩css文件时可以使用该插件



<blockquote>var gulp = require('gulp'),
    minifyCss = require("gulp-minify-css");
 
gulp.task('minify-css', function () {
    gulp.src('css/*.css') // 要压缩的css文件
    .pipe(minifyCss()) //压缩css
    .pipe(gulp.dest('dist/css'));
});</blockquote>



<h4>4.5 html文件压缩</h4>


使用gulp-minify-html
安装：


<blockquote>npm install --save-dev gulp-minify-html</blockquote>


用来压缩html文件



<blockquote>var gulp = require('gulp'),
    minifyHtml = require("gulp-minify-html");
 
gulp.task('minify-html', function () {
    gulp.src('html/*.html') // 要压缩的html文件
    .pipe(minifyHtml()) //压缩
    .pipe(gulp.dest('dist/html'));
});</blockquote>



<h4>4.6 js代码检查</h4>


使用gulp-jshint
安装：


<blockquote>npm install --save-dev gulp-jshint</blockquote>


用来检查js代码



<blockquote>var gulp = require('gulp'),
    jshint = require("gulp-jshint");
 
gulp.task('jsLint', function () {
    gulp.src('js/*.js')
    .pipe(jshint())
    .pipe(jshint.reporter()); // 输出检查结果
});</blockquote>



<h4>4.7 文件合并</h4>


使用gulp-concat
安装：


<blockquote>npm install --save-dev gulp-concat</blockquote>


用来把多个文件合并为一个文件,我们可以用它来合并js或css文件等，这样就能减少页面的http请求数了



<blockquote>var gulp = require('gulp'),
    concat = require("gulp-concat");
 
gulp.task('concat', function () {
    gulp.src('js/*.js')  //要合并的文件
    .pipe(concat('all.js'))  // 合并匹配到的js文件并命名为 "all.js"
    .pipe(gulp.dest('dist/js'));
});</blockquote>



<h4>4.8 less和sass的编译</h4>


less使用gulp-less,
安装：


<blockquote>npm install --save-dev gulp-less</blockquote>

<blockquote>var gulp = require('gulp'),
    less = require("gulp-less");
 
gulp.task('compile-less', function () {
    gulp.src('less/*.less')
    .pipe(less())
    .pipe(gulp.dest('dist/css'));
});</blockquote>


sass使用gulp-sass,
安装：


<blockquote>npm install --save-dev gulp-sass</blockquote>

<blockquote>var gulp = require('gulp'),
    sass = require("gulp-sass");
 
gulp.task('compile-sass', function () {
    gulp.src('sass/*.sass')
    .pipe(sass())
    .pipe(gulp.dest('dist/css'));
});</blockquote>



<h4>4.9 图片压缩</h4>


可以使用gulp-imagemin插件来压缩jpg、png、gif等图片。
安装：


<blockquote>npm install --save-dev gulp-imagemin</blockquote>

<blockquote>var gulp = require('gulp');
var imagemin = require('gulp-imagemin');
var pngquant = require('imagemin-pngquant'); //png图片压缩插件

gulp.task('default', function () {
    return gulp.src('src/images/*')
        .pipe(imagemin({
            progressive: true,
            use: \[pngquant()] //使用pngquant来压缩png图片
        }))
        .pipe(gulp.dest('dist'));
});</blockquote>


gulp-imagemin的使用比较复杂一点，而且它本身也有很多插件，建议去它的项目主页看看文档


<h4>4.10 自动刷新</h4>


使用gulp-livereload插件，
安装:


<blockquote>npm install --save-dev gulp-livereload</blockquote>


当代码变化时，它可以帮我们自动刷新页面
该插件最好配合谷歌浏览器来使用，且要安装livereload chrome extension扩展插件,不能下载的请自行FQ。

<blockquote>var gulp = require('gulp'),
    less = require('gulp-less'),
    livereload = require('gulp-livereload');

gulp.task('less', function() {
  gulp.src('less/*.less')
    .pipe(less())
    .pipe(gulp.dest('css'))
    .pipe(livereload());
});

gulp.task('watch', function() {
  livereload.listen(); //要在这里调用listen()方法
  gulp.watch('less/*.less', \['less']);
});</blockquote>


<h3>下边是自己用的配置：</h3>

``` js
var gulp = require('gulp'),
    jshint = require('gulp-jshint'),
    concat = require('gulp-concat'),
    md5 = require("gulp-md5-plus"),
    uglify = require('gulp-uglify'),
    minifyCss = require('gulp-minify-css'),
    less = require('gulp-less');

// jshint
gulp.task('Lint', function () {
  gulp.src('client/static/js/*.js')
 .pipe(jshint())                                 //检验js
 .pipe(jshint.reporter()); // 输出检查结果
 });

gulp.task('less-css',function(){
    gulp.src('client/static/css/*.less')
        .pipe(less())                            //先将less转换成css
        .pipe(gulp.dest('client/static/css/'));
});
gulp.task('all-html',function(){
    gulp.src('client/page/*.html')
        .pipe(md5(10))                          //给html添加md5戳
        .pipe(gulp.dest('dist/page'))
});
gulp.task('all-css',function(){
    gulp.src('client/static/css/*.css')         //引入文件夹
        .pipe(concat('main.css'))               //将所有引入的css打包到main.css,因为引入md5戳，所以这里打包名一定要是html中引入过的，否则的话找不到，修改不了html内引入
        .pipe(minifyCss())                      //压缩CSS
        .pipe(md5(10,'client/page/*.html'))     //MD5的长度为10，并且自动修改引入增加md5文件的引入地址！！
        .pipe(gulp.dest('dist/css'))            //输入文件夹
});
gulp.task('all-js',function(){
    gulp.src('client/static/js/*.js')
        .pipe(concat('main.js'))
        .pipe(uglify())                         //压缩js
        .pipe(md5(10,'client/page/*.html'))
        .pipe(gulp.dest('dist/js'))
});
//default
gulp.task('default', ['Lint','all-html','less-css','all-css','all-js'], function() {
  gulp.start();                                 //这个里边也可以放入task任务名，但是这里边是没有顺序的
});
gulp.watch('client/static/css/*.less',['default']);
                                                //监听这个目录下的less文件，当变化时，执行default任务！

``` 
![](/images/Gulpjs01.jpg)
![](/images/Gulpjs02.jpg)

<h4>依赖webpack后</h4>
我可以在webpack将所有程序都转换成js，而gulp只进行js的验证打包压缩工作就可以了

下边是我自己写的一个包含了webpack且为流式的配置
``` js
var gulp = require('gulp'),
    jshint = require('gulp-jshint'),
    concat = require('gulp-concat'),
    md5 = require("gulp-md5-plus"),
    uglify = require('gulp-uglify'),
    webpack = require('webpack'),
    del = require('del')

//webpack引入头配置
var path = require('path');
//引入公共文件插件
var CommonsChunkPlugin = require("webpack/lib/optimize/CommonsChunkPlugin");
//定义了一些文件夹的路径
var ROOT_PATH = path.resolve(__dirname);    //webpack.config.js所在位置就是根目录
//var APP_PATH = path.resolve(ROOT_PATH, 'dropload/client');    //这个是根目录下的dropload目录
//var BUILD_PATH = path.resolve(ROOT_PATH, 'dropload/dist/dropload');  //根目录下的dist/dropload文件夹下

//--------------------------------dropload项目-----------------------------

gulp.task("clean",function(){
    del('./dropload/dist/dropload/')
})
gulp.task("webpack",['clean'], function(callback) {
    // run webpack
    webpack({
        //项目的文件夹 可以直接用文件夹名称 默认会找index.js 也可以确定是哪个文件名字
        entry:{
            dropload:"./dropload/client/js/dropload.js",
            style:"./dropload/client/style/style.less"
        },
        //输出的文件名 合并以后的js会命名为bundle.js
        output: {
            path: "./dropload/dist/dropload",
            filename: '[name].js'
        },
        module: {
            //加载器配置
            loaders: [
                //.jsx文件解析，同时转换es6和react
                {test: /\.jsx?$/,loader: 'babel',query: {presets: ['es2015', 'react']}},
                //.less文件解析
                { test: /\.less$/,loader:'style!css!less'},
                //.css文件解析
                {test:/\.css$/,loader:'style-loader!css-loader'}
            ]
        }
        /*plugins: [
         //new CommonsChunkPlugin("admin-commons.js", ["ap1", "ap2"]),
         //new CommonsChunkPlugin("commons.js", ["p1", "p2", "admin-commons.js"])
         ]*/
    }, function(err, stats) {
        //if(err) throw new gutil.PluginError("webpack", err);
        callback();
    });
});
gulp.task('dropload', ['webpack'],function () {
    gulp.src('./dropload/dist/dropload/*.js')
    .pipe(jshint())                                 //检验js
    .pipe(jshint.reporter()) // 输出检查结果
    .pipe(concat('bundle.js'))                //合并js
    .pipe(uglify())                         //压缩js
    .pipe(gulp.dest('./dropload/dist/dropload'))
    .pipe(md5(10,'./Dropload/client/pages/index.html'))    //md5戳(参数一定要放在一个括号内)  后边为index.html内包含的这个文件替换成这个带戳的文件
    .pipe(gulp.dest('./dropload/dist/dropload'))
 });
``` 
