---
title: rem实现Sprite雪碧图
date: 2016-04-21 23:02:39
tags: [css,rem,sprite]

---
# 安装工具
```bash
npm gulp
npm install gulp.spritesmith --save
```

# 配置gulp
```js
var gulp = require('gulp'),
    spritesmith = require('gulp.spritesmith');
    
gulp.task('sprite', function () {
    var spriteData = gulp.src('static/sprites/*.png').pipe(spritesmith({     //这里是要合并的图片地址
        imgName: 'sprite.png',      //这个是输出的文件名
        cssName: 'sprite.css',      //这个是输出的css文件名
        padding: 4                  //间距为4px
    }));
    return spriteData.pipe(gulp.dest('path/to/output/'));       //输出文件的路径
});
```

# 执行
```js
gulp sprite
```

# 修改生成的文件（sprite.css）

1. 先将所有的`px`单位换为`*@n*`(这个单位是令rem的基础单位为1px，大家根据自己图稿来配置)
2. 然后将`width`和`height`修改为`background-size`
3. 然后将生成的`sprite.png`放到存放图片的文件夹
4. 然后将所有的`background-image`的地址修改正确
5. 最后将`sprite.css`中的属性，分别插入的真正应用的css中就可以了

操作确实繁琐，等node学好后，自己写一个插件好了，敬请期待~~~~
