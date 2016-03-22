---
title: npm常用命令
date: 2016-03-21 23:13:08
tags: [others,npm]

---
npm是一个node包管理和分发工具，已经成为了非官方的发布node模块（包）的标准。有了npm，可以很快的找到特定服务要使用的包，进行下载、安装以及管理已经安装的包。

1、安装Node模块

<blockquote>npm install moduleNames</blockquote>


安装完毕后会产生一个node_modules目录，其目录下就是安装的各个node模块。

node的安装分为全局模式和本地模式。
一般情况下会以本地模式运行，包会被安装到和你的应用程序代码的本地node_modules目录下。
在全局模式下，Node包会被安装到Node的安装目录下的node_modules下。

全局安装命令为

<blockquote>$npm install -g moduleName</blockquote>


获知使用

<blockquote>$npm set global=true</blockquote>

来设定安装模式，

<blockquote>$npm get global</blockquote>

可以查看当前使用的安装模式。

示例：


<blockquote>npm install express</blockquote>

 
默认会安装express的最新版本，也可以通过在后面加版本号的方式安装指定版本，如npm install express@3.0.6



<blockquote>npm install <name> -g </blockquote>


将包安装到全局环境中

但是代码中，直接通过require()的方式是没有办法调用全局安装的包的。全局的安装是供命令行使用的，就好像全局安装了vmarket后，就可以在命令行中直接运行vm命令



<blockquote>npm install <name> --save </blockquote>


安装的同时，将信息写入package.json中项目路径中如果有package.json文件时，直接使用npm install方法就可以根据dependencies配置安装所有的依赖包，这样代码提交到github时，就不用提交node_modules这个文件夹了。

2、查看node模块的package.json文件夹

<blockquote>npm view moduleNames</blockquote>

注意事项：如果想要查看package.json文件夹下某个标签的内容，可以使用$npm view moduleName labelName

3、查看当前目录下已安装的node包

<blockquote>npm list</blockquote>

注意事项：Node模块搜索是从代码执行的当前目录开始的，搜索结果取决于当前使用的目录中的node_modules下的内容。$ npm list parseable=true可以目录的形式来展现当前安装的所有node包

4、查看帮助命令

<blockquote>npm help</blockquote>


5、查看包的依赖关系

<blockquote>npm view moudleName dependencies</blockquote>


6、查看包的源文件地址

<blockquote>npm view moduleName repository.url</blockquote>


7、查看包所依赖的Node的版本

<blockquote>npm view moduleName engines</blockquote>


8、查看npm使用的所有文件夹

<blockquote>npm help folders</blockquote>


9、用于更改包内容后进行重建

<blockquote>npm rebuild moduleName</blockquote>


10、检查包是否已经过时，此命令会列出所有已经过时的包，可以及时进行包的更新

<blockquote>npm outdated</blockquote>


11、更新node模块

<blockquote>npm update moduleName</blockquote>


12、卸载node模块

<blockquote>npm uninstall moudleName</blockquote>


13、一个npm包是包含了package.json的文件夹，package.json描述了这个文件夹的结构。访问npm的json文件夹的方法如下：


<blockquote>$ npm help json</blockquote>

 
此命令会以默认的方式打开一个网页，如果更改了默认打开程序则可能不会以网页的形式打开。

14、发布一个npm包的时候，需要检验某个包名是否已存在


<blockquote>$ npm search packageName</blockquote>



15、会引导你创建一个package.json文件，包括名称、版本、作者这些信息等

<blockquote>npm init</blockquote>


16、查看当前包的安装路径

<blockquote>npm root</blockquote>

查看全局的包的安装路径
<blockquote>npm root -g</blockquote>


17、查看npm安装的版本

<blockquote>npm -v</blockquote>

18、发布模块
<blockquote>npm publish</blockquote>

19、撤销发布自己发布过的某个版本代码
<blockquote>npm unpublish <package>@<version></blockquote>

20、清空NPM本地缓存，用于对付使用相同版本号发布新版本代码的人
<blockquote>npm cache clear</blockquote>

<strong>接下来我们可以使用以下命令在 npm 资源库中注册用户（使用邮箱注册）：</strong>


<blockquote>$ npm adduser
Username: mcmohd
Password:
Email: (this IS public) mcmohd@gmail.com</blockquote>






可以撤销发布自己发布过的某个版本代码。
