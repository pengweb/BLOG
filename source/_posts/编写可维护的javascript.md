---
title: 编写可维护的javascript
date: 2016-04-28 23:54:09
tags: [javascript,js,note]

---
# 1.基本的格式化
1.缩进推荐用`tab`
2.语句结尾用`;`
3.return后边加一个空格之后跟`{`
4.每行不要超过80个字符
5.运算符`,`后换行，运算符不要放到第二行，且换行后用两个缩进
6.在`if`这种控制语句之前，`function`之间，`var`之后，注释之前，逻辑片段之间插入**空行**
7.变量名驼峰大小写
8.函数名前缀为动词
9.常量大写字母和下划线命名
10.构造函数，首字母也要大写
11.字符串最好用`""`,因为java通常都是双引号，来回切换的时候不会混
12.字符串需要换行的时候用`+`进行连接
13.数字不要省略小数点之前和之后的数字
14.禁用八进制
15.`null`最好的用法是当作对象的占位符，初始化一个对象。
16.没有被初始化的变量都有一个初始值`undefined`
17.定义对象和数组请用直接量`[]` `{}`

# 2.注释
1.注释之前有空行
2.单行注释用`//`，但是如果是注释代码的话，多行也可以用这个
3.多行注释用`/**/`,包含中文的多行也要用这个
4.注释要和下边被注释的代码对齐
5.注释`*`后加一个空格
6.用`@`表示属性
一般注释
```
/*
 * 一般注释
 *
 */
```
文档注释
/**
这里是文档说明，属性放在最后
@method 这里写注释
@param {Object} 被合并的一个或多个对象
@return {Object} 一个新合并的对象
**/
```

# 3.语句和表达式
1.花括号更在条件后边
2.圆括号两边没有空格，语句和左花括号之间都有空格,webstrom的默认格式(Ctrl+Alt+L)
3.switch语句case需要缩进
4.`case`之间无`break`且无语句，可以直接连续执行；
5.两个连续`case`语句都执行的话，需要在第二个之前加`/**/`注释才不会报错
6.`default`推荐不要写，但是加个注释`// 无 default`
7.`for`循环通过`break`退出整个循环，`continue`跳过此次循环，进入下一次循环
8.推荐用条件语句代替`continue`,使用continue的话JSLint会警告，JSHint不会
9.`for-in`是遍历对象的，不要用来遍历数组
10.`for-in`在循环体内最好做一个`hasOwnProperty()`的判断，如果没有会出现警告

# 4.变量、函数和运算符
1.`var`都放到最上边
2.没有初始值的变量，写在所有的var语句之后
3.函数声明也都写在最前边
4.函数声明不要出现在语句块中
5.函数调用时，函数名和左括号之间没有空格
6.被赋值的立即调用函数，为了能一眼看出是立即调用，应该在最外层加个`()`
7.严格模式最好加在函数内，防止合并的时候，造成全局严格模式
8.`use strict`出现在函数体之外的时候会出现警告
9.最好用`===` `!==`来进行判断
10.都会先转化为`Number()`进行比较,不行的话继续转化为`valueOf()`，还不行就转化为`toString()`

# 5.UI层的松耦合
## 5.1 将javascript从css中抽离
css中不要写javascript

## 5.2 CSS从javascript中抽离
都用`className` 来处理
```js
//原生
element.className += 'reveal' 
//HTML5
element.classList.add('reveal')
//jQuery
element.addClass("reveal")
```
## 5.3 javascript从HTML中抽离
通过监听事件，不要直接写在html中

## 5.4 将HTML从javascript中抽离
方法一：从服务器加载
将模板放置于远程服务器，然后通过ajax来调用，通过innerHTML来插入
方法二：简单客户端模板
原理：HTML模板中将给要添加数据的位置添加个占位符s%，然后在js中将这个占位符替换为真实数据sprintf()，然后再将数据插入到应该的位置。
模板HTML中存在有两种方式：
1.注释
2.script标签中，令type="text/x-my-template"

方法三：复杂客户端模板
handlebars模板引擎

# 6.避免使用全局变量
1.任何全局作用域中的声明的变量和函数都是`window`对象的属性
2.不加`var`的变量都是全局变量
## 6.3 单全局变量的方式
方法一：命名空间
```js
common.zhp={}    //这个zhp就是我自己的命名空间，所有我的属性和方法都定义到zhp上
```
方法二：模块
requirejs或者seajs等模快化工具
通过define()和require()来实现的
现在的webpack也同样可以实现
还有ES6也加入了模块API

方法三：零全局变量
定义一个自执行函数，在这个函数内就不会产生全局变量了

# 7.事件处理
1.隔离应用逻辑
2.不要分发事件对象，就是说event只能出现在处理事件程序里，不应该出现在应用逻辑内。
让事件处理程序称为接触到`event`对象的**唯一**的函数
```js
//P87
```

# 8.避免空比较
## 8.1 检测原始值
`typeof`检查，推荐后边无括号
只检查`string`,`number`,`boolean`,`undefined`用
判断`null`用`===`

## 8.2 检测引用值
`instanceof`检查是否是**的实例
因为**会检测原型链**，所以会不准确
所以检测函数和数组的时候都**不用这个**

## 8.3 检测函数
通过`in`运算符来检测，这是最安全的做法
```js
if("querySelectorAll" in document){
    //检测querySelectorAll是否是DOM的方法
}
```
## 8.4检测数组
```js
Object.prototype.toString.call(value) === "[object Array]"
```
自定义对象不要用这种方法（json）
**推荐**用 `isArray()`方法

## 8.5检测属性
检测属性是否存在是最好的方法是使用`in`运算符！
```js
if("count" in object){
    //
}
```
检测实例对象的时候记得使用hasOwnProperty()方法
且最好先判断下hasOwnProperty是否存在
```js
if("hasOwnProperty" in object && object.hasOwnProperty("related")){
    //
}
```
# 9.将配置数据从代码中分离出来
定义一个配置数据对象
```js
var default = {
    config1:'',
    config2:'',
}
```
*注意*自己在封装的时候，要给用户单设置一个配置文件，然后通过用户配置的和默认的配置文件比较进行初始化

# 10.抛出自定义错误
没细看，用的少

# 11.不是你的对象不要用
1.不覆盖
2.不新增
3.不删除（为null）

## 11.3 更好的途径
1.基于对象的继承
`Object.create()`

2.基于类型的继承
组合式继承（原型链+借用构造函数）
推荐看高级程序设计

## 11.5阻止修改
Object.preventExtension() 锁定，禁止扩展
Object.isExtensible()  检测是否禁止扩展
Object.seal() 封装
Object.isSealed() 检测是否封装
Object.freeze() 冻结
Object.isFrozen() 检测是否冻结

# 12.浏览器嗅探
用**特性检测**
不要用**特性推断**