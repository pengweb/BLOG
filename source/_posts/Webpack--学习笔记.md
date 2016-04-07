---
title: Webpack--学习笔记
date: 2016-04-07 15:41:21
tags: [others,笔记,note]

---
<strong>什么是 webpack？</strong>

webpack是近期最火的一款模块加载器兼打包工具，它能把各种资源，例如JS（含JSX）、coffee、样式（含less/sass）、图片等都作为模块来使用和处理。

<img src="http://images0.cnblogs.com/blog2015/561179/201507/161453372048661.jpg" alt="" />

我们可以直接使用 require(XXX) 的形式来引入各模块，即使它们可能需要经过编译（比如JSX和sass），但我们无须在上面花费太多心思，因为 webpack 有着各种健全的加载器（loader）在默默处理这些事情，这块我们后续会提到。

你可以不打算将其用在你的项目上，但没有理由不去掌握它，因为以近期 Github 上各大主流的（React相关）项目来说，它们仓库上所展示的示例已经是基于 webpack 来开发的，比如 <a href="https://github.com/react-bootstrap/react-bootstrap" target="_blank">React-Bootstrap</a> 和 <a href="https://github.com/gaearon/redux" target="_blank">Redux</a>。

webpack的官网是 <a href="http://webpack.github.io/" target="_blank">http://webpack.github.io/</a> ，文档地址是 <a href="http://webpack.github.io/docs/" target="_blank">http://webpack.github.io/docs/</a> ，想对其进行更详细了解的可以点进去瞧一瞧。

<img src="http://images.cnblogs.com/cnblogs_com/vajoy/558869/o_div.jpg" alt="" />

<strong>webpack 的优势</strong>

其优势主要可以归类为如下几个：

1. webpack 是以 commonJS 的形式来书写脚本滴，但对 AMD/CMD 的支持也很全面，方便旧项目进行代码迁移。

2. 能被模块化的不仅仅是 JS 了。

3. 开发便捷，能替代部分 grunt/gulp 的工作，比如打包、压缩混淆、图片转base64等。

4. 扩展性强，插件机制完善，特别是支持 React 热插拔（见 <a href="https://github.com/gaearon/react-hot-loader" target="_blank">react-hot-loader</a> ）的功能让人眼前一亮。

我们谈谈第一点。以 AMD/CMD 模式来说，鉴于模块是异步加载的，所以我们常规需要使用 define 函数来帮我们搞回调：

<pre>define(['package/lib'], function(lib){
 
    function foo(){
        lib.log('hello world!');
    } 
 
    return {
        foo: foo
    };
});</pre>

另外为了可以兼容 commonJS 的写法，我们也可以将 define 这么写：

<pre>define(function (require, exports, module){
    var someModule = require("someModule");
    var anotherModule = require("anotherModule");    

    someModule.doTehAwesome();
    anotherModule.doMoarAwesome();

    exports.asplode = function (){
        someModule.doTehAwesome();
        anotherModule.doMoarAwesome();
    };
});</pre>

然而对 webpack 来说，我们可以直接在上面书写 commonJS 形式的语法，无须任何 define （毕竟最终模块都打包在一起，webpack 也会最终自动加上自己的加载器）：

<pre>    var someModule = require("someModule");
    var anotherModule = require("anotherModule");    

    someModule.doTehAwesome();
    anotherModule.doMoarAwesome();

    exports.asplode = function (){
        someModule.doTehAwesome();
        anotherModule.doMoarAwesome();
    };</pre>

这样撸码自然更简单，跟回调神马的说 byebye~

不过即使你保留了之前 define 的写法也是可以滴，毕竟 webpack 的兼容性相当出色，方便你旧项目的模块直接迁移过来。

<img src="http://images.cnblogs.com/cnblogs_com/vajoy/558869/o_div.jpg" alt="" />

<strong>安装和配置</strong>

<strong>一. 安装</strong>

我们常规直接使用 npm 的形式来安装：
<p class="VJ_note">$ npm install webpack -g</p>
当然如果常规项目还是把依赖写入 package.json 包去更人性化：
<p class="VJ_note">$ npm init
$ npm install webpack --save-dev</p>
&nbsp;

<strong>二. 配置</strong>

每个项目下都必须配置有一个 webpack.config.js ，它的作用如同常规的 gulpfile.js/Gruntfile.js ，就是一个配置项，告诉 webpack 它需要做什么。

我们看看下方的示例：

<pre>var webpack = require('webpack');
var commonsPlugin = new webpack.optimize.CommonsChunkPlugin('common.js');

module.exports = {
    //插件项
    plugins: [commonsPlugin],
    //页面入口文件配置
    entry: {
        index : './src/js/page/index.js'
    },
    //入口文件输出配置
    output: {
        path: 'dist/js/page',
        filename: '[name].js'
    },
    module: {
        //加载器配置
        loaders: [
            { test: /\.css$/, loader: 'style-loader!css-loader' },
            { test: /\.js[x]?$/, loader: 'jsx-loader?harmony' },
            { test: /\.scss$/, loader: 'style!css!sass?sourceMap'},
            { test: /\.(png|jpg)$/, loader: 'url-loader?limit=8192'}
        ]
    },
    //其它解决方案配置
    resolve: {
        root: 'E:/github/flux-example/src', //绝对路径
        extensions: ['', '.js', '.json', '.scss'],
        alias: {
            AppStore : 'js/stores/AppStores.js',
            ActionType : 'js/actions/ActionType.js',
            AppAction : 'js/actions/AppAction.js'
        }
    }
};</pre>

⑴ plugins 是插件项，这里我们使用了一个 CommonsChunkPlugin 的插件，它用于提取多个入口文件的公共脚本部分，然后生成一个 common.js 来方便多页面之间进行复用。

⑵ entry 是页面入口文件配置，output 是对应输出项配置<em>（即入口文件最终要生成什么名字的文件、存放到哪里）</em>，其语法大致为：

<pre>{
    entry: {
        page1: "./page1",
        //支持数组形式，将加载数组中的所有模块，但以最后一个模块作为输出
        page2: ["./entry1", "./entry2"]
    },
    output: {
        path: "dist/js/page",
        filename: "[name].bundle.js"
    }
}</pre>

该段代码最终会生成一个 page1.bundle.js 和 page2.bundle.js，并存放到 ./dist/js/page 文件夹下。

⑶ module.loaders 是最关键的一块配置。它告知 webpack 每一种文件都需要使用什么加载器来处理：

<pre>    module: {
        //加载器配置
        loaders: [
            //.css 文件使用 style-loader 和 css-loader 来处理
            { test: /\.css$/, loader: 'style-loader!css-loader' },
            //.js 文件使用 jsx-loader 来编译处理
            { test: /\.js[x]?$/, loader: 'jsx-loader?harmony' },
            //.scss 文件使用 style-loader、css-loader 和 sass-loader 来编译处理
            { test: /\.scss$/, loader: 'style!css!sass?sourceMap'},
            //.less 文件使用 style-loader、css-loader 和 less-loader 来编译处理
            { test: /\.less$/, loader: 'style!css!less?sourceMap'},
            //图片文件使用 url-loader 来处理，小于8kb的直接转为base64
            { test: /\.(png|jpg)$/, loader: 'url-loader?limit=8192'}
        ]
    }</pre>

如上，"-loader"其实是可以省略不写的，多个loader之间用“!”连接起来。

注意所有的加载器都需要通过 npm 来加载，并建议查阅它们对应的 readme 来看看如何使用。

拿最后一个 <a href="https://github.com/webpack/url-loader" target="_blank">url-loader</a> 来说，它会将样式中引用到的图片转为模块来处理，使用该加载器需要先进行安装：
<p class="VJ_note">npm install url-loader -save-dev</p>
配置信息的参数“?limit=8192”表示将所有小于8kb的图片都转为base64形式<em>（其实应该说超过8kb的才使用 url-loader 来映射到文件，否则转为data url形式）</em>。

你可以<a href="http://webpack.github.io/docs/list-of-loaders.html" target="_blank">点这里</a>查阅全部的 loader 列表。

⑷ 最后是 resolve 配置，这块很好理解，直接写注释了：

<pre>    resolve: {
        //查找module的话从这里开始查找
        root: 'E:/github/flux-example/src', //绝对路径
        //自动扩展文件后缀名，意味着我们require模块可以省略不写后缀名
        extensions: ['', '.js', '.json', '.scss'],
        //模块别名定义，方便后续直接引用别名，无须多写长长的地址
        alias: {
            AppStore : 'js/stores/AppStores.js',//后续直接 require('AppStore') 即可
            ActionType : 'js/actions/ActionType.js',
            AppAction : 'js/actions/AppAction.js'
        }
    }</pre>

关于 webpack.config.js 更详尽的配置可以参考<a href="http://webpack.github.io/docs/configuration.html" target="_blank">这里</a>。

<img src="http://images.cnblogs.com/cnblogs_com/vajoy/558869/o_div.jpg" alt="" />

<strong>运行 webpack</strong>

webpack 的执行也很简单，直接执行
<p class="VJ_note">$ webpack --display-error-details</p>
即可，后面的参数“--display-error-details”是推荐加上的，方便出错时能查阅更详尽的信息（比如 webpack 寻找模块的过程），从而更好定位到问题。

其他主要的参数有：

<pre>$ webpack --config XXX.js   //使用另一份配置文件（比如webpack.config2.js）来打包

$ webpack --watch   //监听变动并自动打包

$ webpack -p    //压缩混淆脚本，这个非常非常重要！

$ webpack -d    //生成map映射文件，告知哪些模块被最终打包到哪里了</pre>

其中的 <em>-p</em> 是很重要的参数，曾经一个未压缩的 700kb 的文件，压缩后直接降到 180kb<em>（主要是样式这块一句就独占一行脚本，导致未压缩脚本变得很大）</em>。

<img src="http://images.cnblogs.com/cnblogs_com/vajoy/558869/o_div.jpg" alt="" />

<strong>模块引入</strong>

上面唠嗑了那么多配置和执行方法，下面开始说说寻常页面和脚本怎么使用呗。

<strong>一. HTML</strong>

直接在页面引入 webpack 最终生成的页面脚本即可，不用再写什么 data-main 或 seajs.use 了：

<pre>
<!DOCTYPE html>
<html>
<head lang="en">
  <meta charset="UTF-8">
  <title>demo</title>
</head>
<body>
  <script src="dist/js/page/common.js"></script>
  <script src="dist/js/page/index.js"></script>
</body>
</html>
</pre>

可以看到我们连样式都不用引入，毕竟脚本执行时会动态生成&lt;style&gt;并标签打到head里。

<strong>二. JS</strong>

各脚本模块可以直接使用 commonJS 来书写，并可以直接引入未经编译的模块，比如 JSX、sass、coffee等（只要你在 webpack.config.js 里配置好了对应的加载器）。

我们再看看编译前的页面入口文件（index.js）：

<pre>require('../../css/reset.scss'); //加载初始化样式
require('../../css/allComponent.scss'); //加载组件样式
var React = require('react');
var AppWrap = require('../component/AppWrap'); //加载组件
var createRedux = require('redux').createRedux;
var Provider = require('redux/react').Provider;
var stores = require('AppStore');

var redux = createRedux(stores);

var App = React.createClass({
    render: function() {
        return (
            &lt;Provider redux={redux}&gt;
                {function() { return &lt;AppWrap /&gt;; }}
            &lt;/Provider&gt;
        );
    }
});

React.render(
    &lt;App /&gt;, document.body
);</pre>

一切就是这么简单么么哒~ 后续各种有的没的，webpack 都会帮你进行处理。

<img src="http://images.cnblogs.com/cnblogs_com/vajoy/558869/o_div.jpg" alt="" />

<strong>其他</strong>

至此我们已经基本上手了 webpack 的使用，下面是补充一些有用的技巧。

<strong>一. shimming</strong>

在 AMD/CMD 中，我们需要对不符合规范的模块（比如一些直接返回全局变量的插件）进行 shim 处理，这时候我们需要使用 <a href="https://github.com/webpack/exports-loader" target="_blank">exports-loader</a> 来帮忙：
<div class="cnblogs_code">
<pre>{ test: require.resolve("./src/js/tool/swipe.js"),  loader: "exports?swipe"}</pre>
</div>
之后在脚本中需要引用该模块的时候，这么简单地来使用就可以了：
<div class="cnblogs_code">
<pre>require('./tool/swipe.js');
swipe();</pre>
</div>
<img src="http://images.cnblogs.com/cnblogs_com/vajoy/558869/o_div.jpg" alt="" />

<strong>二. 自定义公共模块提取</strong>

在文章开始我们使用了 CommonsChunkPlugin 插件来提取多个页面之间的公共模块，并将该模块打包为 common.js 。

但有时候我们希望能更加个性化一些，我们可以这样配置：

<pre>var CommonsChunkPlugin = require("webpack/lib/optimize/CommonsChunkPlugin");
module.exports = {
    entry: {
        p1: "./page1",
        p2: "./page2",
        p3: "./page3",
        ap1: "./admin/page1",
        ap2: "./admin/page2"
    },
    output: {
        filename: "[name].js"
    },
    plugins: [
        new CommonsChunkPlugin("admin-commons.js", ["ap1", "ap2"]),
        new CommonsChunkPlugin("commons.js", ["p1", "p2", "admin-commons.js"])
    ]
};
// &lt;script&gt;s required:
// page1.html: commons.js, p1.js
// page2.html: commons.js, p2.js
// page3.html: p3.js
// admin-page1.html: commons.js, admin-commons.js, ap1.js
// admin-page2.html: commons.js, admin-commons.js, ap2.js</pre>

<img src="http://images.cnblogs.com/cnblogs_com/vajoy/558869/o_div.jpg" alt="" />

<strong>三. 独立打包样式文件</strong>

有时候可能希望项目的样式能不要被打包到脚本中，而是独立出来作为.css，然后在页面中以&lt;link&gt;标签引入。这时候我们需要 <a href="https://github.com/webpack/extract-text-webpack-plugin" target="_blank">extract-text-webpack-plugin</a> 来帮忙：

<pre>    var webpack = require('webpack');
    var commonsPlugin = new webpack.optimize.CommonsChunkPlugin('common.js');
    var ExtractTextPlugin = require("extract-text-webpack-plugin");

    module.exports = {
        plugins: [commonsPlugin, new ExtractTextPlugin("[name].css")],
        entry: {
        //...省略其它配置</pre>

最终 webpack 执行后会乖乖地把样式文件提取出来：

<img src="http://images0.cnblogs.com/blog2015/561179/201507/161159531266643.png" alt="" />

<img src="http://images.cnblogs.com/cnblogs_com/vajoy/558869/o_div.jpg" alt="" />

<strong>四. 使用CDN/远程文件</strong>

有时候我们希望某些模块走CDN并以&lt;script&gt;的形式挂载到页面上来加载，但又希望能在 webpack 的模块中使用上。

这时候我们可以在配置文件里使用 externals 属性来帮忙：

<pre>{
    externals: {
        // require("jquery") 是引用自外部模块的
        // 对应全局变量 jQuery
        "jquery": "jQuery"
    }
}</pre>

需要留意的是，得确保 CDN 文件必须在 webpack 打包文件引入之前先引入。

我们倒也可以使用 <a href="https://github.com/ded/script.js" target="_blank">script.js</a> 在脚本中来加载我们的模块：
<div class="cnblogs_code">
<pre>var $script = require("scriptjs");
$script("//ajax.googleapis.com/ajax/libs/jquery/2.0.0/jquery.min.js", function() {
  $('body').html('It works!')
});</pre>
</div>
<img src="http://images.cnblogs.com/cnblogs_com/vajoy/558869/o_div.jpg" alt="" />

<strong>五. 与 grunt/gulp 配合</strong>

以 gulp 为示例，我们可以这样混搭：

<pre>gulp.task("webpack", function(callback) {
    // run webpack
    webpack({
        // configuration
    }, function(err, stats) {
        if(err) throw new gutil.PluginError("webpack", err);
        gutil.log("[webpack]", stats.toString({
            // output options
        }));
        callback();
    });
});</pre>

当然我们只需要把配置写到 webpack({ ... }) 中去即可，无须再写 webpack.config.js 了。

更多参照信息请参阅：<a href="http://webpack.github.io/docs/usage-with-grunt.html" target="_blank">grunt配置</a> / <a href="http://webpack.github.io/docs/usage-with-gulp.html" target="_blank">gulp配置</a> 。

<img src="http://images.cnblogs.com/cnblogs_com/vajoy/558869/o_div.jpg" alt="" />

<strong>六. React 相关</strong>

⑴ 推荐使用 <em>npm install react</em> 的形式来安装并引用 React 模块，而不是直接使用编译后的 react.js，这样最终编译出来的 React 部分的脚本会减少 10-20 kb左右的大小。

⑵ <a href="https://github.com/gaearon/react-hot-loader" target="_blank">react-hot-loader</a> 是一款非常好用的 React 热插拔的加载插件，通过它可以实现修改-运行同步的效果，配合 <a href="http://webpack.github.io/docs/webpack-dev-server.html" target="_blank">webpack-dev-server</a> 使用更佳！

<pre>
webpack-dev-server --hot  
</pre>
 

类似于监听的热插拔功能

&nbsp;

基于 webpack 的入门指引就到这里，希望本文能对你有所帮助，你也可以参考下述的文章来入门：

<a href="http://segmentfault.com/a/1190000002551952" target="_blank">webpack入门指谜</a>

<a href="https://github.com/petehunt/webpack-howto" target="_blank">webpack-howto</a>

<a href="http://zhuanlan.zhihu.com/FrontendMagazine/20367175" target="_blank">傻瓜教程1</a>

<a href="http://zhuanlan.zhihu.com/FrontendMagazine/20397902" target="_blank">傻瓜教程2</a>


<h3>总结</h3>
webpack就是向react这种存在依赖关系的工具才用这种个打包工具（需要require这种）
只是解决依赖库的打包，其他的还是用gulp来完成的
不过可以都通过这个工具打包成js文件，最后用gulp来打包成一个js就行了



