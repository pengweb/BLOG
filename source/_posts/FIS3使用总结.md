---
title: FIS3使用总结
date: 2016-03-21 23:06:16
tags: [others,fis3]

---
一、安装FIS3
<blockquote>npm install -g fis3</blockquote>
二、安装fis3的less插件
<blockquote>npm install -g fis-parser-less</blockquote>
三、配置fis-conf.js(以下为我自己的配置，放在要发布的app目录)
这个配置实现了，MD5戳，文件压缩，合并，Less预处理，Sprites雪碧图

``` js
//=========================================MD5======================================

// 加 md5

fis.match('*.{js,css,png}', {
  useHash: true
});

//时间戳设置

/* fis.set('date', new Date);

 fis.match('*.{js,css,png}', {
   query: '?t=' + (fis.get('date').getYear() + 1900)
          + (fis.get('date').getMonth() + 1)
          + (fis.get('date').getDate())
 });*/

/*     时间戳的另一种写法

 fis.set('new date', Date.now());
 fis.match('*.{js,css,png}', {
   query: '?=t' + fis.get('new date')
 });

*/

//======================================压缩=======================================

//     用了下边的打包合集，所以注释掉了这个

fis.match('*.js', {
  // fis-optimizer-uglify-js 插件进行压缩，已内置
  optimizer: fis.plugin('uglify-js')
});

fis.match('*.css', {
  // fis-optimizer-clean-css 插件进行压缩，已内置
  optimizer: fis.plugin('clean-css')
});

fis.match('*.png', {
  // fis-optimizer-png-compressor 插件进行压缩，已内置
  optimizer: fis.plugin('png-compressor')
});

//====================================合并打包====================================

fis.match('::packager', {
    postpackager: fis.plugin('loader', {
        //不同页面打包到不同的包内，如果去掉的话就是只有一个包，如果想指定打包文件，请看注释
        //allInOne: true
    })
});

//     这个是分别指定打包文件的方法

fis.match('/client/static/js/*.js', {
    packTo: '/client/static/js/aio.js'
});
fis.match('/client/static/lib/*.js', {
    packTo: '/client/static/lib/lib_aio.js'
});
fis.match('/client/static/css/*.{less,css}', {
    packTo: '/client/static/css/aio.css'
});
fis.match('/client/static/lib/*.{less,css}', {
    packTo: '/client/static/lib/lib_aio.css'
});


//====================================less预编译======================================

fis.match('*.less', {
    // fis-parser-less 插件进行解析
    parser: fis.plugin('less'),
    // .less 文件后缀构建后被改成 .css 文件
    rExt: '.css'
})


//==================================Sprites图合并=====================================

// 启用 fis-spriter-csssprites 插件

/*fis.match('::package', {
    spriter: fis.plugin('csssprites')
});

// 对 CSS 进行图片合并
fis.match('*.css', {
    // 给匹配到的文件分配属性 `useSprite`
    useSprite: true
});*/

//==============================禁用Sprites/添加md5/压缩============================

//因为是后边命令覆盖前边命令，所以这个放在最后边

fis.media('debug').match('*.{js,css,png}', {
    useHash: false,
    useSprite: false,
    optimizer: null
})
```
四、发布(进入要发布的目录)
<blockquote>fis3 release</blockquote>
五、打开发布后的文件夹
<blockquote>fis3 server open</blockquote>
六、运行
<blockquote>fis3 server start</blockquote>
七、调试(在这种情况下就可以修改源码自动发布显示了)
<blockquote>fis3 release -w</blockquote>
三大功能：
1.资源定位：
<blockquote>// 所有的 css---url和发布目录一致
fis.match('**.css', {
//发布到/static/css/xxx目录下
release : '/static/css$0'
});

// 所有的 css---url和发布目录不一致
fis.match('**.css', {
//发布到/static/css/xxx目录下
release : '/static/css$0',
//访问url是/pp/static/css/xxx
url : '/pp/static/css$0'
});</blockquote>
2.内容嵌入
给资源加 ?__inline 参数来标记资源嵌入需求
源码
<blockquote>&nbsp;</blockquote>
编译后

3.声明依赖
目的只是产出一张资源依赖的表给后端看，设置按需加载
要在根目录创建一个manifest.json，内容输入__RESOURCE_MAP__即可，产出依赖表就在这个文件内
html中注释内容（js，css注释内容也一样）
<blockquote><!-- @require demo.js @require "demo.css" --></blockquote>