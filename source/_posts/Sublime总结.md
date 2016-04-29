---
title: Sublime总结
date: 2016-03-21 23:30:00
tags: [others,sublime]

---
# 1. 常用快捷键

## Ctrl+Shift+P
   功能很强大，可以设置语法，也可以安装插件

## Ctrl+H
    替换

## Ctrl+D
   选中一个后,按下快捷键，一个一个选中，之后一起操作   (Ctrl+K跳过)

## Alt+F3
   选中**所有**聚焦词，之后一起操作

## Ctrl+Alt+L
   先选中然后再按这个快捷键，就会在选区的所有后边加上操作符

## Ctrl+Shift+D
   和idea的Ctrl+D一样复制

## Ctrl+L
   选中整行，**重复可选下一行**

## Ctrl+Shift+M
   选中括号内元素

## Ctrl+M
   选中括号另外一边

## Ctrl+X
   **删除**整行

## Ctrl+W
   关闭当前标签页

## Ctrl+Shift+W
   关闭所有标签页

## Ctrl+PageDown
向左切换当前窗口的标签页

## Ctrl+PageUp
 向右切换当前窗口的标签页

## Ctrl+Shift+'
同时选中开始和闭合标签--要先选中一个 

## Ctrl+P
1、输入当前项目中的文件名，快速搜索文件
2、输入@和关键字，查找文件中函数名
3、输入:和数字，跳转到文件中该行代码  (Ctrl+G)
4、输入#和关键字，查找变量名

# 2. 不常用快捷键
## Ctrl+Alt+;
移除未闭合标签

## Ctrl+Shift+W
插入一个p标签

# 3. 插件
1. Side Bar               //边栏右键增强
2. AutoFileName           //自动填充文件地址
3. SublimeLinter          //提示错误
需安装插件(sublimeLinter-csslint和sublimeLinter-jshint)
```bash
npm install -g jshint
npm install -g csslint
```
4. SublimeCodeIntel       //自动补全   (Ctrl+Shift+Space)
5. BracketHighlighter     //显示在哪个区块内
6. DocBlockr              //注释插件
7. AdvancedNewFile        //创建文件或文件夹  (Ctrl+Alt+n)
8. Git                    //git init是初始化一个配置
9. Autoprefixer           //自动补全CSS3的前缀
10. Markdown Preview      //查看markdown文件
11. Java​Script Snippets   //js片段缩写
12. Babel                 //ES6+JSX语法
13. 其他库和框架 (Nodejs,jQuery,Html5,Css3)

# 4. 安装卸载更新
安装：install
卸载：remove
更新：upgrade
禁用：disable

# 5. 补充
1. 忽略依赖目录
  有时候我们要用 Sublime Text 的文件检索功能找到特定的文件，如果项目目录下面有 node_modules、bower_components 之类的文件夹则会影响输出结果，再加上这些文件夹中的文件平时不会去改动，我们可以修改配置把这些目录忽略掉。
```js
  "folder_exclude_patterns":
   [
  	".svn",
  	".git",
  	".hg",
  	"CVS",
  	"node_modules",
  	"bower_components"
  ],
```
2. 同步
复制`User`目录就可以了