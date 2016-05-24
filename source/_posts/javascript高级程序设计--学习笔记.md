---
title: javascript高级程序设计--学习笔记
date: 2016-03-20 14:12:30
tags: [javascript,笔记,note,js]

---
3.4.1 typeof没总结 在4.1.4 检查数据类型补全

# 1.javascript简介
#### 1.2.2.2 DOM级别
DOM1级由两个模块组成：
DOM核心：规定是如何映射基于XML的文档结构，以便简化对文档中任意部分的访问和操作。
DOM HTML：在DOM核心基础上加以扩展，添加了针对HTML的对象和方法。

DOM2又扩充了鼠标和用户界面事件、范围、遍历等细分模块。
DOM2新模块：DOM视图、DOM事件、DOM样式、DOM遍历和范围

DOM3又进一步扩展了DOM，引入了以统一方式加载和保存文档的方法、新增了验证文档的方法、支持XML1.0规范

# 2.在HTML中使用javascript
## 2.1 script
带有src属性的script标签，开始结束标签之间包含的额外javascript代码，将被忽略不执行。
### 2.1.2 延迟脚本
defer属性的脚本，延迟到遇到`</html>`标签后执行，且会先于DOMContentLoaded执行。
同样带有defer属性的脚本，HTML5规范要求脚本是按顺序执行的，但现实中却无法按顺序执行，无法判断谁先执行。
### 2.1.3 异步脚本
async属性的脚本，一定会在页面的load事件前执行，但可能会在DOMContentloaded事件触发之前或之后执行。
理论和现实中都是无法控制顺序的。
## 2.4 noscript
不支持js的浏览器，平稳退化
``` html
<noscript>本页面不支持javascript</noscript>
```

# 3.基本概念
## 3.1 语法
### 3.1.2 标识符
标识符：变量、函数、属性的名字或者函数的参数。
### 3.1.4严格模式
"use strict"
ES3中不确定的行为将得到处理，对某些不安全的操作会抛出错误。
## 3.2 关键字
具有特殊用途的关键字：var、new 等等
## 3.4 数据类型
基本数据类型：`Undefined`、`Null`、`Boolean`、`Number`、`String`
引用数据类型：`Object`
### 3.4.2 Undefined类型
只声明，并未初始化的值
var声明，但不赋值（不初始化）
### 3.4.3 Null类型
不存在的值，但是他表示的是一个**空对象**指针，所以typeof返回的是'object'
如果定义变量准备在将来用于保存**对象**，那么最好将该变量初始化为null。
undefined**派生**自null，所以 null == undefined   //true
### 3.4.4 Boolean类型
区分大小写
true不一定等于1，false也不一定等于0
`Boolean()`  可以转化Boolean值
**转化为false的值有：**
false、""、0或NAN、null、undefined
**转换为true的值有：**
任何非空字符串、任何非零数字值(包括无穷大)、任何对象、n/a-意思是不适用
### 3.4.5 Number类型
浮点值也叫双精度数值
八进制第一位必须是0，如果字面值中的数值超出范围，那么前导零将被忽略，后面数值将被当作十进制数值进行解析
八进制字面量在严格模式下是无效的，抛出异常
十六进制前两位必须是0x，后边字符可大写也可小写
进行计算时，所有八进制和十六进制都会转换成十进制数值
+0 和 -0 是相等的
#### 3.4.5.1 浮点值
必须包含一个小数点，小数点后至少有一位数字
1.1、0.1、.1  都有效
浮点值占用内存空间是整数值的**两倍**
10.0这个浮点数，系统会在动转换为10这个整数值
极大或者极小可以用e（科学记数法）表示浮点值
e表示10的7次幂
3.125e7     //3.1250000
ES会将小数点后面至少6位的数值转化为e表示法
浮点值最高精度为17位小数，虽然到了17位但精度却远远不如证书。
0.1+0.2 = 0.30000000000000004   //判断测试将不通过，所以永远不要测试某个特定的浮点数值
#### 3.4.5.2 数值范围
最小数值保存在Number.MIN_VALUE中，为`5e-324`
最大数值保存在Number.MAX_VALUE中，为`1.7976931348623157e+308`
如果超出这个值用`Infinity`表示，负数用-Infinity表示
#### 3.4.5.3 NaN
特殊数值，表示要返回数值的操作数未返回数值的情况
1.任何数值除以**非数值**会返回NaN
2.**NaN与任何值都不相等，包括自身**
isNaN(),尝试将这个值**转化为数值**，确定这个参数是否"不是数值"。不能转化的为true
``` js
isNaN("blue")   //true
isNaN("true")   //false
isNaN("10")     //false
```
3.当判断对象的时候，先执行valueOf()，再执行toString(),再测试返回值。
#### 3.4.5.4 数值转化
非数值转化数值方法：
`Number()`    //将**任何类型**转化为数值  *+的操作符操作与它相同*
`parseInt()`  //将**字符串**转化为数值--**整数**忽略小数点后
`parseFloat()`//将**字符串**转化为数值--**浮点数**忽略第二个小数点后

Number():
Number(null) //0
Number(undefined) //NaN
Number('hello world')  //NaN
Number('')    //0
Number('0011')  //11
Number('1.1')  //1.1
Number(true)    //1

parseInt()   //0  字符串为空的时候为0
1.忽略前导零
2.自动转化为十进制
3.如果是对象，先调用`valueoOf()`,如果为NaN则调用`toString()`,然后再转化返回的字符串
4.转化为整数，忽略小数点以后的数字，因小数点以后不是有效的数字字符
5.可以识别十六进制和八进制，首位0x为十六进制，0数字为八进制

parseInt('')   //NaN
parseInt(22.5)  //22
parseInt('0xA')  //10   十六进制
parseInt('070')  //56  ES3-八进制 
parseInt('070')  //70  ES5-十进制-忽略前导零
因为上边这种情况，所以引入第二个参数
parseInt('070',10)   //这样就可以确定是几进制了

parseFloat()
1.忽略第二个小数点后的值
2.忽略前导零
3.只解析十进制--十六进制被转化为0

parseFloat(0xA);   //0
parseFloat(22.3.4);  //22.3
parseFloat(07);   //7
parseFloat(3.1e2);   //310

### 3.4.6 String类型
""和''效果是一模一样的
转义序列  \n表示换行----P33
length可以返回字符的数目，如果字符串中包含双字节字符，length可能不会精确的返回字符串中的字符数目
字符串一经创建就不能改变，要改变某个变量保存的字符串，首先要销毁，再扩充该变量
```js
var lang = 'hel';
var lang = lang + 'low';   //前边的lang会被销毁
```
老浏览器--先扩充一个6字节的内存，然后分别存入hel和low，然后销毁之前这两个值（慢的原因）
新浏览器--直接在lang内进行扩充3个字节

#### 3.4.6.3 转换为字符串
`toString()`    
每个字符串都有这个方法，但是**null和undefined没有这个方法**
toString(8)     //**参数**以八进制输出
例：num.toString(8)

`String()`   //不知道是否是null和undefined的时候可以用这个方法
1.如果值有toString方法，则调用toString
2.如果值为null，则返回"null"
3.如果职位undefined，则返回"underfined"
例：String(num)

### 3.4.7 Object类型
var o = new Object();  //创建一个新对象
**如果不传参数可以不要Object后边的(),但不推荐**
每个实例都有下列属性的方法
`constructor`：保存用于创建当前对象的函数，就是new Object中的Object
` hasOwnProperty(propertyName)`:检查属性在当前实例中，而不再原型中
o.hasOwnProperty("name")   //name是o实例对象上的属性
`isPrototypeOf(object)`:检查是否为对象的原型
`propertyIsEnumerable(propertyName)`: 检查给定的属性是否能够使用for-in语句来枚举，参数以字符串形式指定。
`toLocaleString()`:返回对象的字符串表示，该字符串与执行环境的地区对应。
`toString`：返回对象的字符串形式
`valueOf()`: 返回对象的字符串、数值或布尔值表示，通常与toString返回值**相同**

## 3.5 操作符
操作符通常会调用对象的valueOf()和(或)toString()方法，以便取得可以操作的值。
### 3.5.1 一元操作符
只能操作一个值得操作符叫一元操作符。
#### 3.5.1.1 递增和递减
++  --   分为前置和后置
不仅适用于整数，还可以用于字符串、布尔值、浮点数值和对象
1.包含有效数字字符的字符串时，**先将其转换为数字值**，再执行加减1的操作
2.不包含有效数字字符的字符串，将变量值设为**NaN**
3.布尔值会转化为0/1然后再进行++--操作
4.浮点值可以++--操作
5.对象先调用valueOf(),如果结果为NaN，则调用toString();
#### 3.5.1.2 一元+和-操作符
非数值型的一元操作符会想Number()转换函数一样对这个值执行转换。
var s = +'hello'  //NaN    翻看Number()
### 3.5.2 位操作符
ES中所有数值都以IEEE-754B64位格式存储，但位操作符并不直接操作64位的值。而是先将64位的值转换为32位的整数，然后执行操作，最后再将结果转换回64位。
有符号的整数，32位中前31位用于表示整数的值。第32位用于表示数值的符号。**0表示正，1表示负**
*更新中···*
### 3.5.3 布尔操作符
与(AND)或(OR)非(NOT)
#### 3.5.3.1 逻辑非 `!` 
先将操作数转换为布尔值，然后再取反--*参照Boolean*
1.如果操作数是一个对象，返回false
2.如果操作数是一个空字符串，返回true
3.如果操作数是一个非空字符串，返回false
4.如果操作数是数值0，返回true
5.如果操作数是任意非0的值（包括Infinity）,返回false
6.如果操作数是null/NaN/undefined，返回true
*使用两个!!就相当于Boolean()*
#### 3.5.3.2 逻辑与 `&&`
当有一个操作数不是布尔值的时候
短路操作，第一个为false就不往下进行了
1.第一个操作数是对象，返回第二个操作数
2.第二个操作数是对象，只有在第一个值为true的时候，才返回这个对象
3.两个操作数都是对象，返回第二个操作数
4.如果有一个操作数是null/NaN/undefined，则返回null/NaN/undefined
**两个都为false时也执行**
按正常理解就行

#### 3.5.3.3 逻辑或 `||`
也是短路操作，第一个为true的话，就不往下进行了
1.第一个操作数是对象，则返回第一个操作数
2.第一个操作数的求值结果为false，则返回第二个操作数
3.如果两个操作数都是对象，则返回第一个操作数
4.两个操作数都是null/NaN/undefined则返回null/NaN/undefined

### 3.5.4 乘法操作符
乘法、除法、求模
非数值的情况下会执行自动类型转换`Number()`转换
#### 3.5.4.1 乘法
1.一个操作数为NaN，结果为NaN
2.Infinity与0相乘，结果NaN
3.Infinity与非0相乘，结果为Infinity
4.Infinity和Infinity相乘结果是Infinity

#### 3.5.4.2 除法
1.零被零除，结果是NaN
2.非零的有限数被0除，结果是Infinity
3.Infinity和Infinity相除结果是NaN

#### 3.5.4.3 求模（余数%）
1.被除数为0的时候，结果为0

### 3.5.5 加性操作符
#### 3.5.5.1 加法 
1.如果一个操作符是NaN,结果是NaN
2.Infinity加-Infinity，结果为NaN
3.如果有一个是字符串，则**执行字符串拼接操作**

#### 3.5.5.2 减法
1.如果有一个为NaN,则结果为NaN
2.Infinity减Infinity，结果为NaN
3.-Infinity减-Infinity，结果为NaN
4.Infinity减-Infinity，结果为Infinity
5.-Infinity减Infinity，结果为-Infinity

### 3.5.6 关系操作符
< > <= >=  //返回布尔值
1.两个都是字符串的话，比较**字符编码值**
2.布尔值将其转化为数值后，再比较

### 3.5.7 相等操作符
== 和 !=     //先**转换**为相似的类型再比较
1.如果一个操作符为NaN,相等操作符返回false，不相等操作符返回true
2.如果两个操作符为NaN,相等操作符返回false，不相等操作符返回true
null == undefined  //true

=== 和!==    //仅比较
'55' === 55  //false

### 3.5.8 条件操作符-三元运算符
variable = boolean_expression ? true_value : false_value
判断boolean_expression，正确执行true_value，错误执行false_value

### 3.5.9 赋值操作符
=   //赋值
复合赋值
*=
+=
%=
<<=    //左移赋值
=>>    //右移赋值

### 3.5.10 逗号操作符
在一个语句中执行多个操作
var num1 = 1,num2 =2,num3 = 3;
赋值时候，只返回**最后一个**表达式
var num = (5,1,4,8)   //num的值为8

## 3.6 语句
### 3.6.5
使用for-in循环之前，先**检查**确认该对象的值**不是null或undefined**
**判断undefined** 用typeof(x) == "undefined"
**判断null**   用 x == null

### 3.6.7 break和continue语句
break 立即跳出循环，强制继续执行循环后面的语句
continue 立即跳出循环，从循环顶部继续执行

### 3.6.9 switch语句
switch(i){
    case 20:
        alert('25');
        break;
    case 22:
    case 23:
        alert('22或23');
        break;
    default:
        alert('没有相应的值');
}
**i和case的值不一定是数值，可以是任何数据类型**
case 是用来判断i的

## 3.7 函数
任何函数在任何时候都可以通过`return`语句后跟要返回的值来实现返回值
位于`return`语句之后的任何代码都永远不会被执行
`return`语句可以不带任何返回值。这种情况下，函数在停止执行后将返回`undefined`

### 3.7.1 理解参数
参数只提供便利，但不是必须的。
参数用arguments表示，可以通过arguments[]来取值
arguments[0]和传入的第一个参数所占用的**内存空间是不同**的，但他们的**值会同步**
没有传入参数的命名参数会被自动设置为`undefined`
```js
function foo(num1,num2){}
foo(10)      //此时num2就是undefined
```

### 3.8.2 没有重载
重载的意思就是可以存在两个相同名字的函数，但是js并不具备重载能力
出现两个相同名字的函数时，该名字只**属于后定义**的函数。

# 4. 变量、作用域和内存问题
## 4.1 基本类型和引用类型
基本类型和引用类型在3.4数据类型的时候已经说过，不再赘述
基本类型指的是简单的数据段
引用类型指的是那些可能由多个值构成的对象
引用类型的值保存在内存中的对象。javascript不允许直接访问内存中的位置，也就是说不能直接操作对象的内存空间。
在操作对象时，实际上是在操作对象的引用而不是实际的对象。

### 4.1.1 动态属性
不能给基本类型的值添加属性，尽管这样做不会导致任何错误。

### 4.1.2 复制变量值
从一个变量向另一个变量赋值基本类型的值，会在变量对象上创建一个新值，然后把该值复制到为新变量分配的位置上。
var num1 = 5;
var num2 = num1;

num2的值是5，但是这个5只是num1的一个副本，和num1的5是完全独立的，不会互相影响。
但是如果赋值的是一个引用类型，那么这个副本就是一个指针，一改变都改变。

### 4.1.3 传递参数
函数的参数都是按值传递的，引用类型的参数也是按值传递的。
如果传递的参数是引用类型，那在函数内部参数值改变，那外边的值也就改变了，就乱套了！
**下边例子很重要**
```js
function setName(obj){
    obj.name = 'Nicholas';
    obj = new Object();    //重点在这里，参数，参数，参数被重写在这里是一个局部变量(如果不是重写参数就不一样了)，是局部变量，所以在执行完毕的时候，这个局部变量就会自动销毁，不影响外边的obj
    obj.name = 'Greg';
}
var person = new Object();
setName(person);
alert(person.name);    //'Nicholas'
```
 
### 4.1.4 检查数据类型
typeof返回的字符串有`undefined`、`boolean`、`string`、`number`、`object`、`function`
typeof(null)   //object,因为被作为一个空对象使用
typeof(正则表达式)   //function  因为内部实现`[[Call]]`方法的对象都返回function

instanceof判断引用类型，**判断是否是实例**返回值为`true`和`false`
person instanceof Object  //判断是不是对象
person instanceof Array
person instanceof RegExp
person instanceof Function

## 4.2 执行环境及作用域
所有的全局变量和函数都是作为window对象的属性和方法创建的！
全局变量只有在关闭网页或浏览器的时候才会销毁。
局部变量在执行完毕后自动销毁
函数执行的时候，就会被推入一个环境栈内，执行完成后，栈就将其环境弹出
环境执行时，会创建一个作用域链，最开始只包含一个变量，即`arguments`对象，这个对象在全局环境中是不存在的
最外层为全局变量
标识符解析是沿着作用域链一级一级的搜索标识符的过程，从前端开始向后回溯查找，找到为止。
外部环境不能访问内部环境中的任何变量和函数

### 4.2.1 延长作用域链
try-catch语句的catch块
with语句
这两种语句会改变作用域链，不推荐使用

### 4.2.2 没有块级作用域
if语句和for语句都没有作用域
所以在它们内部定义的变量，一直存在于它们外部的执行环境中

#### 4.2.2.1 声明变量
使用var声明的变量会自动被添加到最接近的环境中。
但是如果没有使用var声明，则被添加到全局环境。

### 4.2.2.2 查询标识符
从最前端开始找一直追溯到全局环境
访问局部变量要比访问全局变量跟快，因为不用向上搜索作用域链

## 4.3垃圾收集
### 4.3.1 标记清除
当变量进入环境的时候标记为"进入环境"，当离开环境时，标记为"离开环境"
垃圾收集器在运行的时候会给存储在内存中的**所有变量**都加上标记。
然后它会去掉**环境中的变量**，以及**被环境中的变量引用的变量**的标记。
再此之后所有被加上标记的和已经含有标记的所有变量将被视为**准备删除**的变量。

### 4.3.2 引用计数
被引用一次标记为+1，替换为别的变量的时候-1
闭包永远不为0，所以会常驻内存

不使用的时候，最好手工断开DOM和原生javascript之间的联系，用`null`
当垃圾收集器**下次**运行时，会删除这些值并回收内存。
```js
var element = document.getElementById("hehe");
var myObject = new Object();
myObject.element = element;
element.someObject = myObject

//上边两句循环引用，无法回收，下边进行清除
myObject.element = null;
element.someObject = null;
```

### 4.3.3 性能问题
256个变量、4096个对象或数组或者64KB的字符串打到这个临界值，启动垃圾收集器
IE 在回收内存不到15%的时候，变量、字面量或数组的临界值就会加倍。
IE 在回收内存超过85%的时候，则将各种临界值重置回默认值

强制执行垃圾收集器
IE: window.CollectGarbage()
Opera7: window.opera.collect()

### 4.3.4 管理内存
通常分配给Web浏览器的可用内存数要比分配给桌面应用程序的少，这样主要是出于安全方面考虑，防止js网页耗尽系统内存导致崩溃。
内存限制不仅会影响给变量分配内存，还影响调用栈以及在一个线程中能够同时执行的语句数量。

优化：一点数据不再有用，最好通过将其值设置为null来释放其引用--解除引用
一般全局变量不使用他的时候，手工接触引用。
解除一个值的引用并不意味着自动回收该值所占用的内存。
接触引用的真正作用是让值**脱离执行环境**，以便垃圾收集器**下次**运行时将其回收。

# 5 引用类型
引用类型的值(对象)是引用类型的一个**实例**，常被成为类。
JS是面向对象的语言，但不具备传统的面向对象语言所支持的类和接口等基本结构

新对象是使用`new`操作符后跟一个构造函数来创建的，构造函数本身就是一个函数。

## 5.1 Object类型
创建Object实例有**两种方法**
1.var person = new Object();      //构造函数
2.var person = {};                //对象字面量
*通过对象字面量定义的对象，不会调用Object构造函数*
**对象字面量是向函数传递大量可选参数的首选方式**
```js
displayInfo(
    {
        name:'pengzhang',
        age:29
    }
)
```

访问对象属性，两种方法：
1.点
2.方括号  --可以通过变量访问属性

## 5.2 Array 类型
创建数组的基本方式有**两种方法**
1.构造函数
var colors = new Array();
var colors = new Array(3);    //数组长度
var colors = new Array("red","green");   //数组内容
*可以省略new，结果是一样的 var colors = new Array(3)*

2.数组字面量表示法
var colors = [];
var colors = \[1,2,]     //IE8及之前认为有3项，1，2，undefined。之后的浏览器都认为有两项
var colors = \[,,,,,]    //5或者6个数组,都是undefined

*通过对象字面量定义的数组，不会调用Array构造函数*

移除数组可以通过**减少数组长度**来实现
在位置99插入一个值得话，数组的长度就是99了，中间项用undefined来代替！

### 5.2.1 检查数组
因为instanceof判断数组的条件是，假定只有一个全局执行环境，如果网页包含多个框架(有多个全局环境)，
从而存在两个以上不同版本的Array构造函数。
ES5增加了`Array.isArray()`方法，最终确定某个值到底是不是数组，而不用管他是在哪个全局执行环境中创建的。
更高级的判断的方法可以参考P22.1.1

### 5.2.2 转换方法
对象的属性上边有说，下边利用这些属性来进行转换
var colors = \['red','blue','green'];
colors.toString();    //red,blue,green    转化为字符串
colors.valueOf();     //red,blue,green    转化为字符串
alert(colors)        //alert这个方法接受必须字符串参数，所以数组会先转化为字符串在传入，所以打印的也是red,blue,green
**在转化的默认情况都是用,来进行分割的，其实是内部调用了join()方法，可以修改分割符**
colors.toString().join("||")    //结果就是   red||blue||green

`toLocaleString()`方法和上边两种不同的地方是，这次是每一项都进行toLocaleString()而不是toString()，这个也可以用来转化为本地时间用。

### 5.2.3 栈方法
栈是一种LIFO的数据结构(后进先出)，也就是最新添加的项最早被移除。
栈中项的推入和弹出都发生在栈的顶部。
可以通过`push()` `pop()` 方法进行操作

### 5.2.4 队列的方法
队列的访问规则是FIFO(先进先出)
实现这一操作的方法`push()` `shift()`

ES还为数组提供了一个unshift()方法。在最**前端添加**任意个项，返回长度

### 5.2.5 重排序方法
reverse()按降序排列
sort()按升序排列   **转化为字符串后进行比较，比较的是字符串，因为比较的字符串，所以比较的就是字符编码，所以就会不准确，10就会位于5的前面**
所以推荐用比较函数来**替代**`sort()`
下边这个表示**升序** 降序在判断时候取反就对了
```js
function compare(a,b){
    if(a<b){
        return -1;
    }else if(a>b){
        return 1;
    }else{
        return 0;
    }
}
```
如果比较的数值类型的话，可以用下边这个比较函数(升序)降序是b-a
```js
function compare(a,b){
    return a - b ;
}
```
**调用方法**
values.sort(compare)   //作为参数不用带()

### 5.2.6 操作方法
`concat()` 合并数组。先创建当前数组一个**副本**，然后将接收的参数添加到这个副本的末尾。
var colors = \['red'];
colors.concat('green',\['blue','black'])

`slice()`基于当前组中的一个或多个项创建一个新数组。
可接受一个或者两个参数，即要返回的**起始和结束的位置**
slice()不会影响原始数组

`splice`可以实现`插入` `删除` `替换`
删除：两个参数
第一个参数为第一项的**位置**，第二个参数为删除的**项数**
插入：两个参数(第二个参数为0)+插入项
splice(2,0,"red")
替换：两个参数+替换项
splice(2,1,"red")

### 5.2.7 位置方法
ES5添加了`indexOf()`方法和`lastIndexOf()`方法
从开始向后查找和从后向前查找
两个参数：要查找的项+查找的起点位置
没有找到的话返回`-1`
**只返回第一个找到的位置**
var numbers = \[1,2,3,4]
numbers.indexOf(4)  //3  返回的是位置

### 5.2.8 迭代方法
ES5定义了5个迭代方法P96
`some()`有一项返回true，就返回**true**
`every()`每一项都返回true，则返回**true**,一项不是就返回**false**
`filter()`所有返回true的**数组**
`forEach()`对每一项进行操作
`map()`对每一项进行操作，返回**数组**
```js
//every
var numbers = [1,2,3,4,3]
var everyResult = numbers.every(function(item,index,array){
    return (item>2)
})
alert(everyResutl)    //false  因为不是所有的项都大于2

//filter
var filterResult = numbers.filter(function(item,index,array){
    return (itme>2)
})
alert(filterResult)   //[3,4,3]

//map
var mapResult = numbers.map(function(item,index,array){
    return (item*2*)
})
alert(mapRsult)    //[2,4,6,8,6]

//forEach
numbers.forEach(function(item,index,array){
    //执行某些操作
})
```

### 5.2.9 归并方法
ES5新增了两种方法 `reduce()`和`reduceRight()`
他们都是迭代数组项，然后构建一个最终返回值
reduce() 从数组第一项开始
reduceRight() 从数组最后一项开始
接收两个参数：调用的函数+归并初始值
传给reduce()和reduceRight()的函数接收4个参数：前一个值、当前值、项的索引、数组对象
```js
var values = [1,2,3,4,5];
var sum = values.reduce(function(prev,cur,index,array){
    return prev+cur
})
alert(sum);    //15
```
第一次prev是1，cur是2
第二次prev是3，cur是3
第三次prev是6，cur是4
第四次prev是10，cur是5
第五次prev是15，返回15

### 5.2.10 数组去重的5个方法
#### 5.2.10.1 遍历数组法
最简单的去重方法
**实现思路**：新建一新数组，遍历传入数组，**值不在新数组就加入该新数组中**；
**注意点**：判断值是否在数组的方法“indexOf”是ECMAScript5 方法，IE8以下不支持，需多写一些兼容低版本浏览器代码，源码如下：
```js
// 最简单数组去重法
function unique1(array){
  var n = []; //一个新的临时数组
  //遍历当前数组
  for(var i = 0; i < array.length; i++){
    //如果当前数组的第i已经保存进了临时数组，那么跳过，
    //否则把当前项push到临时数组里面
    if (n.indexOf(array[i]) == -1) n.push(array[i]);
  }
  return n;
}
```
```js
// 判断浏览器是否支持indexOf ，indexOf 为ecmaScript5新方法 IE8以下（包括IE8， IE8只支持部分ecma5）不支持
if (!Array.prototype.indexOf){
  // 新增indexOf方法
  Array.prototype.indexOf = function(item){
    var result = -1, a_item = null;
    if (this.length == 0){
      return result;
    }
    for(var i = 0, len = this.length; i < len; i++){
      a_item = this[i];
      if (a_item === item){
        result = i;
        break;
      }  
    }
    return result;
  }
}
```
#### 5.2.10.2 对象键值对法
该方法执行的速度比其他任何方法都快， 就是占用的内存大一些
**实现思路**：新建一js对象以及新数组，遍历传入数组时，**判断值是否为js对象的键**，不是的话给对象新增该键并放入新数组。
注意点： 判断是否为js对象键时，会自动对传入的键执行“toString()”，不同的键可能会被误认为一样；例如： a\[1]、a\[“1”] 。解决上述问题还是得调用“indexOf”。
```js
// 速度最快， 占空间最多（空间换时间）
function unique2(array){
  var n = {}, r = [], len = array.length, val, type;
    for (var i = 0; i < array.length; i++) {
        val = array[i];
        type = typeof val;
        if (!n[val]) {
            n[val] = [type];
            r.push(val);
        } else if (n[val].indexOf(type) < 0) {
            n[val].push(type);
            r.push(val);
        }
    }
    return r;
}
```
#### 5.2.10.3 数组下标判断法
还是得调用“indexOf”性能跟方法1差不多
**实现思路**：如果当前数组的第i项在当前数组中第一次出现的位置不是i，那么表示第i项是重复的，忽略掉。否则存入结果数组。
```js
function unique3(array){
  var n = [array[0]]; //结果数组
  //从第二项开始遍历
  for(var i = 1; i < array.length; i++) {
    //如果当前数组的第i项在当前数组中第一次出现的位置不是i，
    //那么表示第i项是重复的，忽略掉。否则存入结果数组
    if (array.indexOf(array[i]) == i) n.push(array[i]);
  }
  return n;
}
```
#### 5.2.10.4 排序后相邻去除法
虽然原生数组的”sort”方法排序结果不怎么靠谱，但在不注重顺序的去重里该缺点毫无影响。
**实现思路**：给传入数组排序，排序后相同值相邻，然后遍历时新数组只加入不与前一值重复的值。
```js
// 将相同的值相邻，然后遍历去除重复值
function unique4(array){
  array.sort(); 
  var re=[array[0]];
  for(var i = 1; i < array.length; i++){
    if( array[i] !== re[re.length-1])
    {
      re.push(array[i]);
    }
  }
  return re;
}
```
#### 5.2.10.5 优化遍历数组法
源自外国博文，该方法的实现代码相当酷炫；实现思路：获取没重复的最右一值放入新数组。（检测到有重复值时终止当前循环同时进入顶层循环的下一轮判断）
```js
// 思路：获取没重复的最右一值放入新数组
function unique5(array){
    var r = [];
    for(var i = 0, l = array.length; i < l; i++) {
        for(var j = i + 1; j < l; j++){
            if (array[i] === array[j]){
                ++i;                   //这里++i中断了for循环，让顶层的for循环从1开始
            }
        }
        r.push(array[i]);
    }
    return r;
}
```
## 5.3 Date类型
使用自UTC1970年1月1日午夜开始
创建一个日期对象
var now = new Date();
不传参数话：自动获得当前日期和时间。
传入参数：获得1970到传入参数时间的毫秒数
ES提供两个方法简化计算：`Date.parse()` `Date.UTC()`
传入Date.parse()的字符串不能表示日期，则返回`NaN`
直接传递给Date构造函数，后台也是调用的这个
var someDate = new Date(Date.parse("May 25,2004"));
var someDate = new Date("May 25,2004");
上边两个相等的
Date.UTC()对象表示的是GMT时间
ES5添加了`Date.now()`方法：返回调用这个方法时的时间毫秒数，一般用于测试
```js
var start = Date.now();
doSomething();
var stop = Date.now();
result = stop-star;
```

### 5.3.1 继承的方法
Date重写了toLocalString、toString、valueOf()方法
toLocalString会按照与浏览器设置的地区相适应的格式返回日期和时间，包含AM\PM，但不会包含时区信息
toString返回带有时区信息的日期和时间，一般以军用时间表示。

valueOf()方法，根本不返回字符串，而是返回日期的**毫秒**。
7月1日小于7月2日 返回true

### 5.3.3 组件方法
getFullYear()
setFullYear()
getMonth()-月
getDate() -日
getDay()  -星期
getHours()
getMinutes()
getSeconds()
getMilliseconds()

## 5.4 RegExp 类型
g 全局-所有字符串，而非找到第一个就停止
i 不区分大小写
m 多行模式

更新中···

## 5.5 Function类型
函数声明：
function foo(){}
函数表达式
var foo = function(){}
构造函数
var foo = new Function('num1','num2','return num1+num2')
**最后一个参数为函数体，函数体，函数体。前边的为参数**
从技术上讲构造函数是函数表达式，不推荐这么写，因为这样会执行两次（第一次是解析常规ES代码，第二次是解析传入构造函数中的字符串）从而影响性能
**一个函数可能会有多个名字--因为操作的是指针，而非对象。**

### 5.5.1 没有重载
后命名的函数覆盖之前的同名函数，因为命名的是指针，指针位置改变了，所以函数体也就变了

### 5.5.2 函数声明与函数表达式
解析器会**先读取函数声明**
函数声明，在执行任何代码之前可用，解析器会将其放在源代码树顶部。
函数表达式，只有在调用的时候才可用。

### 5.5.3 作为值得函数
ES中的函数名本身就是变量，所以函数可以作为值来使用。

### 5.5.4 函数的内部属性
函数内部有两个特殊的`对象`：`arguments` 和 `this`
`arguments`这个属性还有一个名叫`callee`的属性，该属性是一个指针，指向用友这个arguments对象的函数。
`this`引用的是函数据以执行的环境对象。全局对象的时候引用的是windows
`caller`这个属性中保存着调用当前函数的函数的引用。如果是全局作用域中调用当前函数，它的值为null。
为了实现更松散的耦合，也可以通过arguments.callee.caller来访问相同的信息。
严格模式下：
arguments.callee会导致错误。
arguments.caller也会导致错误。
不能为arguments.caller属性赋值，否则会导致错误。
非严格模式：
arguments.caller这个属性始终是undefined。这么定义主要为了区分arguments.caller和函数本身的caller属性

### 5.5.5函数的属性和方法
`prototype`保存所有实例方法的真正所在。例如toString和valueOf实际上都保存在prototype。
ES5中prototype属性不可以枚举的，因此使用`for-in`无法发现
每个函数都含有两个非继承而来的的方法`apply()` `call()`.
这两个值实际上等于设置函数体·`this`对象的值
`applay()`两个参数分别是，在其中运行函数的作用域+另一个是参数数组(可以使Array的实例，也可以是arguments对象)。
`call()`区别仅在接收参数方式不同。这个传递给函数的参数，必须逐个列出。
其实这两个属性最大的作用是：扩充函数赖以运行的作用域。**通常就是继承的用法**
ES5还定义了`bind()`方法。这个方法会创建一个函数的实例，其中this值会被绑定到传给bind()函数的值。

## 5.6基本包装类型
为了便于操作基本类型值，ES提供了3个特殊的引用类型：Boolean、Number、String.
他们具有引用类型的特性，同时也具有与各自的基本类型相应的特殊行为。
每读取一个基本类型的时候，后台都会创建一个对应的基本包装类型的对象。
例如： var s2 = s1.substring(2);
因为基本类型**不是对象**，所以不该有方法的，但是确实有，下边是后台自动完成的处理。
1.创建String类型的一个实例
2.在实例上调用指定的方法
3.销毁这个实例
上边三个步骤都适用于Number和Boolean。

引用类型和包装类型的主要区别就是对象的生存期。
引用类型一直存在于内存中。
包装对象值存在于一行代码的执行瞬间，然后立即销毁。
```js
var s1 = "text"
s1.color = "red"
alert(s1.red)   //undefined
```
基本包装类型的实例调用`typeof`返回object，而且所有基本包装类型对象都会被转换为布尔值`true`
**用new调用基本包装类型的构造函数，与直接调用同名的转型函数是不一样的。**
```js
var value = '25'
var number = Number(value);   //转型函数    保存的是数值25
alert(typeof number)    //number

var obj = new Number(value);  //构造函数    保存的是实例对象
alert(typeof obj)       //object
alert(obj instanceof Number)   //true
alert(obj instanceof Object)   //true   
```
*不建议显式的创建基本包装类型的对象*

### 5.6.1 Boolean类型
创建Boolean对象
```js
var booleanObject = new Boolean(true)
```
Boolean类型的实例重写了valueOf()方法，返回基本类型值true或false
重写了toString()方法，返回字符串"true"或"false"
```js
var falseObject = new Boolean(false);       //将false重写了，相当于true
var result = falseObject && true;
alert(result)                              //true
```
*布尔值与Blooean对象之间区别很重要，建议永远不要使用Boolean对象*

### 5.6.2 Number类型
也重写了vauleOf()和toString()和toLocalString方法
valueOf返回的是基本类型的数值
toString和toLocalString返回的是字符串形式的数值
toString传递一个表示基本的参数，告诉是几进制数值的字符串形式
```js
var num = 10;
alert(num.toString(2))   //1010  转换为二进制
```
将数值转化为字符串的方法
`toFixed`按指定的小数位返回数值的字符串形式
```js
var num = 10.005;
alert(num.toFixed(2))   //10.00  转换为二进制
```
*超过指定位数会自动舍入，不同浏览器舍入值不同*
`toExponential()`该方法返回科学记数法(e)。
`toPrecision()`返回固定大小格式。接收一个参数，表示数值的所有数字位数（不好考指数部分）。这个方法**兼容**上边两种方法,选择上边两种最适合的方法进行使用转化
```js
var num = 99;
alert(num.toPrecision(1))   //1e+2  以一位来表示99，因为一位无法准确的表达99，所以进行舍入
alert(num.toPrecision(2))   //99
```
*同样不建议使用Numer实例化对象，最最最主要的原因是在判断Number的typeof的时候会有两个不同的值*
### 5.6.3 String类型
String包装类型的创建
var stringObject = new String("hello world")
继承的toString、toLocalString、valueOf返回对象所表示的基本字符串值
#### 5.6.3.1字符方法
`charAt()` `charCodeAt()`访问字符串中特定字符的方法.
都接收一个参数，即基于0的字符位置。
charAt() 返回**字符**
```js
var stringValue = 'hello';
alert(stringValue.charAt(1));   //"e"
```
以上结果也可以通过stringValue\[1]来获得
charCodeAt()是返回**字符编码**
```js
var stringValue = 'hello';
alert(stringValut.charCodeAt(1));   //"101"
```
#### 5.6.3.2 字符串操作方法
`concat()`  字符串拼接，实际中还是使用`+`更简便一些
基于子字符串创建新字符串方法，第一个参数都是指开始位置
`slice()`   第二个参数指最后一个字符串的**位置**
`substring` 第二个参数指最后一个字符串的**位置**
`substr()`  第二个参数指最后一个字符串的**个数**

以上三个数最大区别在传入**负数**的时候
`slice()`将传入的负值与字符串长度相加
`substr()`将负的第一个参数与字符串长度相加，而将负的第二个参数转换为0.
`substring`把所有负值参数转换为0
```js
var stringValue = 'hello world'  
stringValue.slice(-3)    //rld     -3+11
stringValue.substring(-3)   //hello world    0
stringValue.substr(-3)   //rld     -3+11
stringValue.slice(3,-4)   //lo w    3,-3+11
stringValue.substring(3,-4)  //hel    3,0
stringValue.substr(3,-4)     //""     3,0
```
#### 5.6.3.3 字符串位置方法
`indexOf()` `lastIndexOf()` 查找字符串位置，只能得到**第一个**出现的位置
这两个方法可接受可选的**第二个参数**，表示**从字符串中哪个位置开始搜索**
**通过增加查找位置来遍历长字符串**
```js
var stringValue = "lsdjklasjdflajpjwpejkgljlsjflsajweiotu"
var positions = [];
var pos = stringValue.indexOf("e");
while(pos>-1){
    positions.push(pos);
    pos = stringValue.indeOf("e",pos+1)    //向下继续找
}
alert(positions);;
```

#### 5.6.3.4 trim()方法--删除前置及后缀所有空格
ES5属性，直接调用.trim()

#### 5.6.3.5 字符串大小写转换
`toLowerCase()`    全小写
`toLocaleLowerCase()`    全小写
`toUpperCase()`     全大写
`toLocaleUpperCase()`    全大写

#### 5.6.3.6 字符串的匹配方法
`match()`本质上和调用RegExp的exec()方法相同。
只接受一个参数，要么是正则表达式，要么是RegExp对象
```js
var pattern = /.at/;
var matches = text.match(pattern);    //得到的是一个数组
```
`search()`查找模式，返回字符串中第一个匹配项的`索引`，如果没有找到返回`-1`
```js
var text = 'cat,bat,sat'
var pos = text.search(/at/);    //1
```
`replace()`第一个参数是一个字符串，第二个参数可以是一个字符串或者一个**函数**。
```js
result = text.replace(/at/g, 'ond')   //'cond,bond,sond,fond' 
```
#### 5.6.3.7 localeCompare()方法
`localeCompare()`比较两个字符串，并返回下列值中的一个。
字符串在字母表中牌子字符串参数之前，返回-1
等于，返回0
之后，返回1
```js
var stringValue = 'yellow';
stringVaule.localCompare("brick")   //1   yellow在字母表中排在brick之后
```
#### 5.6.3.8 fromCharCode()方法
`fromCharCode()` 接收一或多个字符编码，然后将他们转化成一个字符串。与`charCodeAt()`作用相反
```js
String.fromCharCode(104,101,108,111); //'hello'
```

## 5.7 单体内置对象
由ES实现提供的、不依赖于**宿主环境**的对象，在程序执行**之前**就已经存在了。
### 5.7.1 Global对象
这是一个终极的"兜底儿"对象，不属于任何其他对象的属性和方法，最终都是它的属性和方法。
所有在全局作用域中定义的属性和函数，都是Global对象的属性。
#### 5.7.1.1 URL编码方法
`encodeURI()`对URI进行编码。不会对本身属于URI的特殊字符进行编码，例如冒号、正斜杠、问好和井号
`encodeURIComponent()`会对非标准字符进行编码----**最常用**
```js
var uri = "http://www.wrox.com/illegal value.htm#start";
        
//"http://www.wrox.com/illegal%20value.htm#start"
alert(encodeURI(uri));
        
//"http%3A%2F%2Fwww.wrox.com%2Fillegal%20value.htm%23start"
alert(encodeURIComponent(uri));
```
`decodeURI()`  对encodeURI()解码
`decodeURIComponent()` 对encodeURIComponent()解码

#### 5.7.1.2 eval()方法
它就像一个完整的ES**解析器**，只接受一个参数。
```js
eval("alert('hehe')")    //hehe
```
通过eval()执行的代码可以引用在包含环境中定义的变量。
```js
var a = 'haha'
eval(alert(a))
```
**在eval()中创建的任何变量或函数都不会被提升**
严格模式下，在外部访问不到eval()中创建的任何变量和函数。

#### 5.7.1.3 Global对象的属性
`undefined` `NaN` `Infinity` `Object` `Array` `Function` `Boolean` `String` `Number` `Date` `RegExp` `Error` `EvalError` `RangeError` `ReferenceError` `SyntaxError` `TypeError` `URIError`

#### 5.7.1.4 window对象
Web浏览器将Global这个全局对象作为window对象的一部分加以实现。
所以Global的所有变量和函数就都成为了window对象的属性。

### 5.7.2 Math对象
**Math 对象属性**
属性	描述
E	返回算术常量 e，即自然对数的底数（约等于2.718）。
LN2	返回 2 的自然对数（约等于0.693）。
LN10	返回 10 的自然对数（约等于2.302）。
LOG2E	返回以 2 为底的 e 的对数（约等于 1.414）。
LOG10E	返回以 10 为底的 e 的对数（约等于0.434）。
PI	返回圆周率（约等于3.14159）。
SQRT1_2	返回返回 2 的平方根的倒数（约等于 0.707）。
SQRT2	返回 2 的平方根（约等于 1.414）。
**Math 对象方法**
方法	描述
abs(x)	返回数的绝对值。
acos(x)	返回数的反余弦值。
asin(x)	返回数的反正弦值。
atan(x)	以介于 -PI/2 与 PI/2 弧度之间的数值来返回 x 的反正切值。
atan2(y,x)	返回从 x 轴到点 (x,y) 的角度（介于 -PI/2 与 PI/2 弧度之间）。
ceil(x)	对数进行上舍入。
cos(x)	返回数的余弦。
exp(x)	返回 e 的指数。
floor(x)	对数进行下舍入。
log(x)	返回数的自然对数（底为e）。
max(x,y)	返回 x 和 y 中的最高值。
min(x,y)	返回 x 和 y 中的最低值。
pow(x,y)	返回 x 的 y 次幂。
random()	返回 0 ~ 1 之间的随机数。
round(x)	把数四舍五入为最接近的整数。
sin(x)	返回数的正弦。
sqrt(x)	返回数的平方根。
tan(x)	返回角的正切。
toSource()	返回该对象的源代码。
valueOf()	返回 Math 对象的原始值。

```js
Math.ceil(25.9)   //26
Math.floor(25.9)  //25
```
# 6.面向对象的程序设计
ES把对象定义为：**无序属性集合**。
本章总结：
**创建对象:工厂模式/组合模式（构造函数+原型模式）**
**继承方法：原型链/组合继承（原型链+借用构造函数）/原型式/寄生组合式（原型链+借用构造函数+原型式+寄生式）**
**补充：new是创建了一个副本。组合和寄生组合都是借用了覆盖的原理**
## 6.1 理解对象
键值对形式存在
### 6.1.1 属性类型
ES5定义了只有**内部才用的特性**，这些是给js引擎用的，js不能*直接*访问他们。为了表示是内部值用**[]**来表示！！
#### 6.1.1.1 数据属性
数据属性包含一个数据值的**位置**
在这个位置可以读取和写入值。数据属性有4个描述其行为的特性
`[[Configurable]]`表示能否通过delete删除属性从而重新定义属性。默认为true，表示可以。
`[[Enumerable]]`表示能否for-in循环返回属性。默认是true。
`[[Writable]]`表示能否改写属性的值，默认为true
`[[Value]]`包含这个属性的数据值。默认值为undefined。读写都是从这个位置查找的。
```js
var person = {
    name: "Nicholas";
}
//Configurable\Enumerable\Writable 都是默认值为true，Value被设置为Nicholas
```
要**修改**默认的特性，必须使用ES的`Object.defineProperty()`方法。
包含三个参数：属性所在对象+属性的名字+描述符的对象
```js
var person = {};
Object.defineProperty(person, "name", {
    writable: false,        //只读的，非严格模式下，赋值被忽略，严格模式下报错
    value: "Nicholas"
});

alert(person.name);
person.name = "Michael";
alert(person.name);
```
`[[Configurable]]`一旦设置成false，**就不能再把它变回可配置了**
配置为false后，修改除`writeable`之外的特性，都会报错。

#### 6.1.1.2 访问器属性
访问器属性不包含数据值。
`[[Configurable]]` 能否通过delete删除属性从而重新定义属性。默认为true
`[[Enumerable]]`能否通过for-in循环返回属性。默认为true
`[[Get]]`在读取属性时调用的函数。默认为undefined
`[[Set]]`在写入属性时调用的函数。默认为undefined
访问器不能直接定义，必须使用`Object.defineProperty()`方法来定义
```js
var book = {
    _year: 2004,
    edition: 1
};
  
Object.defineProperty(book, "year", {
    get: function(){
        return this._year;
    },
    set: function(newValue){
    
        if (newValue > 2004) {
            this._year = newValue;
            this.edition += newValue - 2004;
        
        }
    }
});

book.year = 2005;
alert(book.edition);   //2
```
不一定非要同时指定getter和setter。
只指定getter意味着**属性不能写**，尝试写入属性会被忽略。严格模式下，抛出错误。
只指定setter意味着**属性不能读**，尝试读取属性会返回undefined，严格模式报错。

### 6.1.2 定义多个属性
```js
var book = {};
        
Object.defineProperties(book, {
    _year: {                //数据属性
        value: 2004           
    },
    
    edition: {              //数据属性
        value: 1
    },
    
    year: {            
        get: function(){        //访问器属性
            return this._year;
        },
        
        set: function(newValue){        //访问器属性
            if (newValue > 2004) {
                this._year = newValue;
                this.edition += newValue - 2004;
            }                  
        }            
    }        
});
   
book.year = 2005;
alert(book.edition);   //2
```

### 6.1.3 读取属性的特性
ES的`Object.getOwnPropertyDescriptor()`方法，可以取得给定属性的描述符。
接收两个参数：属性所在对象+要读取其描述符的属性名称
```js
var book = {};
        
Object.defineProperties(book, {
    _year: {
        value: 2004
    },
    
    edition: {
        value: 1
    },
    
    year: {            
        get: function(){
            return this._year;
        },
        
        set: function(newValue){
            if (newValue > 2004) {
                this._year = newValue;
                this.edition += newValue - 2004;
            }                  
        }            
    }        
});
   
var descriptor = Object.getOwnPropertyDescriptor(book, "_year");   //★主要是通过这个属性来访问的
alert(descriptor.value);          //2004
alert(descriptor.configurable);   //false
alert(typeof descriptor.get);     //"undefined"

var descriptor = Object.getOwnPropertyDescriptor(book, "year");
alert(descriptor.value);          //undefined
alert(descriptor.enumerable);     //false
alert(typeof descriptor.get);     //"function"
```

## 6.2 创建对象
共同的缺点：同一个接口创建很多对象，会产生很多的重复代码

### 6.2.1 工厂模式
```js
function createPerson(name, age, job){
    var o = new Object();
    o.name = name;
    o.age = age;
    o.job = job;
    o.sayName = function(){
        alert(this.name);
    };    
    return o;        //★ return
}

var person1 = createPerson("Nicholas", 29, "Software Engineer");
var person2 = createPerson("Greg", 27, "Doctor");

person1.sayName();   //"Nicholas"
person2.sayName();   //"Greg"
```
**工厂模式虽然解决了创建多个相似对象的问题，但却没有解决对象识别的问题（即怎么知道一个对象的类型）。**

### 6.2.2 构造函数模式
```js
function Person(name, age, job){
    this.name = name;
    this.age = age;
    this.job = job;
    this.sayName = function(){
        alert(this.name);
    };    
}

var person1 = new Person("Nicholas", 29, "Software Engineer");
var person2 = new Person("Greg", 27, "Doctor");

person1.sayName();   //"Nicholas"
person2.sayName();   //"Greg"

alert(person1 instanceof Object);  //true
alert(person1 instanceof Person);  //true
alert(person2 instanceof Object);  //true
alert(person2 instanceof Person);  //true

alert(person1.constructor == Person);  //true
alert(person2.constructor == Person);  //true

alert(person1.sayName == person2.sayName);  //false        
```
优点：
没有显式的创建对象
直接将属性和方法赋给了this对象
没有return属性
实例标识为一种特定的类型
缺点：
**必须大写**P

#### 6.2.2.1 构造函数当作函数
只要通过`new`操作符来调用，那它就可以作为构造函数
如果不通过new调用，就和普通函数一样，普通函数`this`指向`window`

#### 6.2.2.2 构造函数的问题
每个方法都要在实例上重新创建一遍，导致创建很多没必要的函数方法。

### 6.2.3 原型模式
每个函数都有一个prototype属性，这个属性是一个**指针**，指向一个对象，这个对象包含所有实例共享的属性和方法。
```js
function Person(){
        }
        
Person.prototype.name = "Nicholas";
Person.prototype.age = 29;
Person.prototype.job = "Software Engineer";
Person.prototype.sayName = function(){
    alert(this.name);
};

var person1 = new Person();
person1.sayName();   //"Nicholas"

var person2 = new Person();
person2.sayName();   //"Nicholas"

alert(person1.sayName == person2.sayName);  //true

alert(Person.prototype.isPrototypeOf(person1));  //true
alert(Person.prototype.isPrototypeOf(person2));  //true

//only works if Object.getPrototypeOf() is available
if (Object.getPrototypeOf){
    alert(Object.getPrototypeOf(person1) == Person.prototype);  //true
    alert(Object.getPrototypeOf(person1).name);  //"Nicholas"
}
```
#### 6.2.3.1 理解原型对象
所有原型对象都会自动获得一个constructor（构造函数）属性，这个属性包含一个指向prototype属性所在函数的指针。
**实例对象**也包含一个指针，指向构造函数的原型对象，这个指针叫\[\[Prototype]],Firefox、Safari、Chrome在每个对象上都支持一个属性__proto__;在其他中是完全不可见的。
Person.prototype指向了原型对象，而Person.prototype.constructor又指回了Person。

`isPrototypeOf()`方法来确定对象之间是否在原型上。
`hasOwnProperty()`检查是否存在于实例中。
`Object.getPrototypeOf()`返回\[\[Prototype]]的值。
```js
alert(Object.getPrototypeOf(person1) == Person.prototype); //true
alert(Object.getPrototypeOf(person1).name);         //"Nicholas"
```
原型最初**只包含**`constructor`属性，而该属性也是共享的，因此可以通过对象实例访问。
`delete`删除实例属性。
```js
delete person1.name;
```
#### 6.2.3.2 原型与in操作符
`for-in`可以访问实例+原型中的属性，返回true
```js
"name" in person1  //true
```
判断是否在原型上
```js
function hasPrototypeProperty(object, name){
            return !object.hasOwnProperty(name) && (name in object);
        }
```
在**原型**上定义了**\[\[Enumerable]]标记为false的属性**（不可枚举），但在**实例**属性也会在for-in循环中返回，因为规定，所有开发人员定义的属性都是可以枚举的。
`Object.keys()`取得对象上所有可枚举的**实例**属性,返回的是一个**数组**
```js
function Person(){
}

Person.prototype.name = "Nicholas";
Person.prototype.age = 29;
Person.prototype.job = "Software Engineer";
Person.prototype.sayName = function(){
    alert(this.name);
};

var keys = Object.keys(Person.prototype);
alert(keys);   //"name,age,job,sayName"

var p1 = new Person();
p1.name = 'Rob';
p1.age = 31;
var p1keys = Object.key('p1');   //查看的是实例的属性
alert(p1keys);      //"name,age"
```
`Object.getOwnPropertyNames()`得到所有实例属性，无论**是否可枚举**
```js
var keys = Object.getOwnPropertyNames(Person.prototype);
alert(keys);   //"constructor,name,age,job,sayName"
```
*包含了不可枚举的constructor*

#### 6.2.3.3 更简单的原型语法
```js
function Person(){
}

Person.prototype = {  //这个是创建的新对象，所以它重新定义了constructor，不再指向Person，而是（Object构造函数）
    constructor : Person,    //因为上边注释的原因，所以在这里重新定义一下，就可以将constructor重新定义回Person了
    name : "Nicholas",
    age : 29,
    job: "Software Engineer",
    sayName : function () {
        alert(this.name);
    }
};

var friend = new Person();

alert(friend instanceof Object);  //true
alert(friend instanceof Person);  //true
alert(friend.constructor == Person);  //true    //如果上边没有重新定义的话，这里是false
alert(friend.constructor == Object);  //false   //如果上边没有重新定义的话，这里是true
```
**原生的constructor是不可以枚举的，但是重新定义的这个是可以枚举的\[\[Enumerable]]为true**
`Object.defineProperty()`ES5的重设构造函数
```js
Object.defineProperty(Person.prototype,"constructor",{
    enumerable:false,
    value: Person
})
```
#### 6.2.3.4 原型的动态性
实例与原型之间的链接只不过是一个**指针**，而非一个副本。
可以**随时**给原型添加属性和方法，并且能立即反映出来。但是如果原型被修改为另外一个对象，就等于切断了构造函数与最初原型之间的联系。
**实例中的指针仅指向原型，而不指向构造函数**
```js
function Person(){
}

var friend = new Person();
        
Person.prototype = {
    constructor: Person,
    name : "Nicholas",
    age : 29,
    job : "Software Engineer",
    sayName : function () {
        alert(this.name);
    }
};

//如果var friend = new Person();写在这里，下边就不会报错了，因为按顺序执行，上边重定义后，这里访问的就是新的对象了
friend.sayName();   //error   ★这里报错是因为Person.prototype被重写了，所以friend已经调不到属性了

```
#### 6.2.3.5 原型对象的原型
可以像修改自定义对象的原型一样修改原生对象的原型。
**不推荐重写对象**
```js
String.prototype.startsWith = function (text) {   //进行重写
    return this.indexOf(text) == 0;
};

var msg = "Hello world!";
alert(msg.startsWith("Hello"));   //true
```
#### 6.2.3.6 原型对象的问题
共享属性被修改，所有都被修改，没有私有属性。

### 6.2.4 组合使用构造函数模式和原型模式  ★★★★★
构造函数模式用于定义实例属性，而原型模式用于定义方法和共享的属性。
**使用最广泛，认同度最高**的一种创建自定义类型的方法
```js
function Person(name, age, job){                   //构造函数模式
    this.name = name;
    this.age = age;
    this.job = job;
    this.friends = ["Shelby", "Court"];
}

Person.prototype = {                               //原型模式         
    constructor: Person,
    sayName : function () {
        alert(this.name);
    }
};

var person1 = new Person("Nicholas", 29, "Software Engineer");
var person2 = new Person("Greg", 27, "Doctor");

person1.friends.push("Van");

alert(person1.friends);    //"Shelby,Court,Van"
alert(person2.friends);    //"Shelby,Court"
alert(person1.friends === person2.friends);  //false
alert(person1.sayName === person2.sayName);  //true
```
### 6.2.5 动态原型模式
通过检查某个应该存在的方法是否有效，来决定是否初始化原型。--按需初始化
```js
function Person(name, age, job){
        
//properties
this.name = name;
this.age = age;
this.job = job;

//methods
if (typeof this.sayName != "function"){      //只在sayName这个方法不存在的情况下，才会将它添加到原型中

    Person.prototype.sayName = function(){
        alert(this.name);
    };
    
}
}
var friend = new Person("Nicholas", 29, "Software Engineer");
friend.sayName();   //弹出Nicholas
```
这个方法不能使用对象字面量重写原型，重写会切断现有实例与新原型之间的联系。
#### 6.2.6 寄生构造函数模式
前述几种都不适用的情况下，可以使用寄生构造函数模式
该函数作用仅仅是封装创建对象，然后返回新创建的对象。
**不推荐用**
```js
function SpecialArray(){       
 
    //create the array
    var values = new Array();
    
    //add the values
    values.push.apply(values, arguments);
    
    //assign the method
    values.toPipedString = function(){
        return this.join("|");
    };
    
    //return it
    return values;        
}

var colors = new SpecialArray("red", "blue", "green");     //唯一和工厂模式的区别是，多了一个new！！！
alert(colors.toPipedString()); //"red|blue|green"

alert(colors instanceof SpecialArray);    //不能通过instanceof确定类型
```
### 6.2.7 稳妥构造函数模式
所谓稳妥，指的是没有公共属性，而且其方法也不引用this对象。
适用于安全环境中，这个环境禁用this和new
```js
function Person(name, age, job){
    //添加方法
    o.sayName = function(){
        alert(this.name);
    };    
    return o;        //★ return
}

var friend = Person("Nicholas", 29, "Software Engineer");
friend.sayName();  //Nicholas
```
friend中保存的是一个稳妥对象，除了调用sayName()方法外，没有别的方式可以访问其数据成员。
instanceof也没有意义(好像只有new才会产生关系，瞎猜的)

## 6.3 继承
### 6.3.1 原型链
原型链作为继承的主要方法。
利用原型让一个引用类型继承另一个引用类型的属性和方法。
```js
function SuperType(){
    this.property = true;
}

SuperType.prototype.getSuperValue = function(){
    return this.property;
};

function SubType(){
    this.subproperty = false;
}

//inherit from SuperType
SubType.prototype = new SuperType();     //这里非常非常非常重要，这里重写了SubType的原型，所以之前的原型就断掉了，以后也不要查找了。

SubType.prototype.getSubValue = function (){
    return this.subproperty;
};

var instance = new SubType();
alert(instance.getSuperValue());   //true    查找顺序：1：实例 2：SubType.prototype(已变更) 3：SuperType.prototype

alert(instance instanceof Object);      //true
alert(instance instanceof SuperType);   //true
alert(instance instanceof SubType);     //true

alert(Object.prototype.isPrototypeOf(instance));    //true
alert(SuperType.prototype.isPrototypeOf(instance)); //true
alert(SubType.prototype.isPrototypeOf(instance));   //true
```
#### 6.3.1.1别忘了默认的原型
所有函数的默认原型都是Object的实例。
默认原型都会包含一个内部指针，指向Object.prototype。
这也正是所有自定义类型都会继承toString()、valueOf()等默认方法的根本原因。

#### 6.3.1.2 确定原型和实例的关系
`instanceof`确定**原型和实例**的关系
`isPrototypeOf()`判断原型链中出现过的原型

#### 6.3.1.3 谨慎地定义方法
给原型添加方法的代码，一定要放在**替换（重写）原型**的语句**之后**
```js
function SuperType(){
    this.property = true;
}

SuperType.prototype.getSuperValue = function(){
    return this.property;
};

function SubType(){
    this.subproperty = false;
}

//inherit from SuperType
SubType.prototype = new SuperType();

//new method 添加新方法
SubType.prototype.getSubValue = function (){
    return this.subproperty;
};

//override existing method   重写超类
SubType.prototype.getSuperValue = function (){
    return false;
};


//try to add new methods � this nullifies the previous line
SubType.prototype = {           //重写原型
    getSubValue : function (){
        return this.subproperty;
    },

    someOtherMethod : function (){
        return false;
    }
};

var instance = new SubType();
alert(instance.getSuperValue());   //error!  //SubType.prototype已经被重写了，getSuperValue方法已经丢失了
```
#### 6.3.1.4 原型链的问题
1.还是共享问题
2.创建子类型的实例时，不能向超类型的构造函数中传递参数

### 6.3.2借用构造函数
apply()和call()
```js
function SuperType(name){
    this.name = name;
}

function SubType(){  
    //inherit from SuperType passing in an argument
    SuperType.call(this, "Nicholas");      
    
    //instance property
    this.age = 29;
}

var instance = new SubType();
alert(instance.name);    //"Nicholas";
alert(instance.age);     //29
```
#### 6.3.2.1传递参数
相对原型链有一个很大的优势，在子类构造函数中向超类型构造函数传递参数。
#### 6.3.2.2借用构造函数问题
同构造函数：方法都在构造函数中定义，函数复用无从谈起。

### 6.3.3 组合继承 
伪经典继承：**原型链+借用构造函数**
```js
            
function SuperType(name){                     //构造函数-创建对象
    this.name = name;
    this.colors = ["red", "blue", "green"];                    
}

SuperType.prototype.sayName = function(){    //原型模式-创建对象
    alert(this.name);
};

function SubType(name, age){  
    SuperType.call(this, name);              //借用构造函数-继承  第二次调用SuperType()
    
    this.age = age;
}

SubType.prototype = new SuperType();         //原型链-继承   第一次调用SuperType()
SubType.prototype.constructor = SubType;
SubType.prototype.sayAge = function(){
    alert(this.age);
};

var instance1 = new SubType("Nicholas", 29);
instance1.colors.push("black");
alert(instance1.colors);  //"red,blue,green,black"       
instance1.sayName();      //"Nicholas";
instance1.sayAge();       //29


var instance2 = new SubType("Greg", 27);
alert(instance2.colors);  //"red,blue,green"
instance2.sayName();      //"Greg";
instance2.sayAge();       //27
```
`instanceof`和`isPrototypeOf()`都是可用的
调用两次构造函数：
一次是创建子类型原型的时候
另一次是在子类型构造函数内部

### 6.3.4 原型式继承-浅复制
浅复制原理：
```js
function object(o){
    function F(){}
    F.prototype = o;
    return new F();
}
//上边那几句就是浅复制的原理
var person = {
    name: "Nicholas",
    friends: ["Shelby", "Court", "Van"]
};

var anotherPerson = object(person);
anotherPerson.name = "Greg";
anotherPerson.friends.push("Rob");

var yetAnotherPerson = object(person);
yetAnotherPerson.name = "Linda";
yetAnotherPerson.friends.push("Barbie");

alert(person.friends);   //"Shelby,Court,Van,Rob,Barbie"
```
`Object.create()`是ES5新增的原型式继承方法。
两个参数：新对象原型的对象+新对象定义额外属性的对象
```js
var person = {
    name: "Nicholas",
    friends: ["Shelby", "Court", "Van"]
};

var anotherPerson = Object.create(person);      //用法
anotherPerson.name = "Greg";
anotherPerson.friends.push("Rob");

var yetAnotherPerson = Object.create(person);
yetAnotherPerson.name = "Linda";
yetAnotherPerson.friends.push("Barbie");

alert(person.friends);   //"Shelby,Court,Van,Rob,Barbie"
```
第二个参数与Object.defineProperties()方法格式相同
```js
var person = {
    name: "Nicholas",
    friends: ["Shelby", "Court", "Van"]
};
                   
var anotherPerson = Object.create(person, {
    name: {
        value: "Greg"
    }
});

alert(anotherPerson.name);  //"Greg"
```
缺点：
1：每个构造函数只有一个原型，不能实现多重继承
2：不能很好的支持多参数或动态参数的父类
3：隐私性比较差，易被修改

### 6.3.5寄生式继承
寄生式就是在原型式的基础上（不一定），对原型式进行扩充，然后放到一个**函数内**。
```js
function createAnother(original){
    var clone = object(original);    //创建一个新对象-不一定用原型式
    clone.sayHi = function(){        //增强这个对象
        alert("hi");
    };
    return clone;                   //返回这个对象
}
var person = {
    name:"Nicholas",
    friends: ["Shelby", "Court", "Van"]
}
var anotherPerson = createAnother(person);
anotherPerson.sayHi();  //"hi"
```
缺点：**函数复用率低**

### 6.3.6 寄生组合式继承★★★★★
**原型式继承+原型链+借用构造函数**
```js

//原型式继承--浅复制 可以用Object.create()代替
function object(o){
    function F(){}
    F.prototype = o;
    return new F();
}
//原型链继承--下边这个和（组合技成中的）SubType.prototype = new SuperType();的作用相同，但是下边这么写的意思是为了避免多次创建SuperType()的实例
function inheritPrototype(subType, superType){
    var prototype = object(superType.prototype);   //prototype.prototype == superType.prototype
    prototype.constructor = subType;               //augment object
    subType.prototype = prototype;                 //subType.prototype.prototype == superType.prototype
}
//父对象/父类/超类-的属性
function SuperType(name){
    this.name = name;
    this.colors = ["red", "blue", "green"];
}
//超类的方法写在原型上
SuperType.prototype.sayName = function(){
    alert(this.name);
};
//借用构造函数-SubType本身指向Super,拥有了colors属性。SubType原型也指向了SuperType的原型，但后边会被重写
function SubType(name, age){
    SuperType.call(this, name);
    this.age = age;
}
//让SubType的prototype继承SuperType，使得之前SubType的prototype被覆盖
inheritPrototype(SubType, SuperType);
//一定要在上边重写SubType的prototype被重写之后再定义方法，否则会被覆盖
SubType.prototype.sayAge = function(){
    alert(this.age);
};
//运用
//先创建一个实例副本，是副本副本副本（副本会复制本身，但是不会复制原型链）
var instance1 = new SubType("Nicholas", 29);
//这样修改的就是副本本身，而不是原型链了
instance1.colors.push("black");
alert(instance1.colors);  //"red,blue,green,black"
//再创建一个新副本，新副本是从SubType本身复制过来的，不是从其他副本复制过来的
var instance2 = new SubType("Greg", 27);
alert(instance2.colors);  //"red,blue,green"
```
### 6.3.7 浅拷贝
```js
function extendCopy(p) {
　　　　var c = {};
　　　　for (var i in p) { 
　　　　　　c[i] = p[i];
　　　　}
　　　　c.uber = p;
　　　　return c;
　　}

//调用
var Doctor = extendCopy(Chinese);
```
### 6.3.8 深拷贝
```js
//p是
function deepCopy(p, c) {
　　　　var c = c || {};
　　　　for (var i in p) {
　　　　　　if (typeof p[i] === 'object') {
　　　　　　　　c[i] = (p[i].constructor === Array) ? [] : {};
　　　　　　　　deepCopy(p[i], c[i]);
　　　　　　} else {
　　　　　　　　　c[i] = p[i];
　　　　　　}
　　　　}
　　　　return c;

//调用
var Doctor = deepCopy(Chinese);
```

# 7.函数表达式
函数声明和函数表达式
函数声明**提升**
** 本章重点：私有变量/模块模式**

## 7.1 递归
```js
function factorial(num){
    if (num <= 1){
        return 1;
    } else {
        return num * factorial(num-1);
    }
}

var anotherFactorial = factorial;           //指针指向factorial
factorial = null;                          //指针被指向了null
alert(anotherFactorial(4));  //error!
```
`arguments.callee`指向**正在执行**的函数的指针。
上个代码解决方法
```js
 function factorial(num){
    if (num <= 1){
        return 1;
    } else {
        return num * arguments.callee(num-1);    //★ argument.callee总比使用函数名更保险
    }
}

var anotherFactorial = factorial;     //★ 赋值其实就是创建了一个副本
factorial = null;
alert(anotherFactorial(4));  //24    因为上边是副本，所以anotherFactorial = factorial还是存在的。但是修改anotherFactorial属性会反映到facotrial
```
严格模式下，通过脚本访问`arguments.callee`会导致错误。
不过可以通过使用命名函数表达式来达成相同结果
```js
var factorial = (function f(num){
    if(num<=1){
        return 1；
    }else{
        return num*f(num-1);
    }
})
```
f()为**命名函数表达式**

## 7.2 闭包
闭包是指有权访问另一个函数作用域的变量的函数。
最终作用域链内部\[\[Scope]]属性中
作用域链本质上是一个指向变量对象的指针列表，只引用但不实际包含变量对象。
外层函数在执行完毕后，不会被销毁，因为作用域链仍然在引用内部函数，直到内部匿名函数被销毁后，外层函数才会被销毁（表达严重问题）
通过compareNames = null 来接触对匿名函数的引用，以便释放内存。

**闭包用途：设计私有的方法和变量--匿名函数自执行、面向对象的对象、封装-创建特权方法、缓存**
当内部函数被调用的时候就会形成闭包
[参考链接](http://blog.csdn.net/sunlylorn/article/details/6534610)

### 7.2.1 闭包与变量
作用域链副作用：闭包只能取得包含函数中任何变量的**最后一个**值（for循环的时候总是最大值）。
解决上述问题：创建另一个匿名函数强制让闭包的行为符合预期
```js
function createFunctions(){
    var result = new Array();
    
    for (var i=0; i < 10; i++){
        result[i] = (function(num){
            return function(){      //★★★★★匿名函数形成闭包，访问的是外层函数传过来的i，这个i每次传进来都是最后一个值
                return num;
            };
        })(i);          //给自执行函数传入值
    }
    
    return result;
}

var funcs = createFunctions();

//every function outputs 10
for (var i=0; i < funcs.length; i++){
    document.write(funcs[i]() + "<br />");
}
```
面试遇到的：
```js
var a = (function () {          //必须自执行，要不然返回的是一个函数
    var name = 'zhang';
    return (function (){        //必须自执行，要不然返回的是一个函数
        var name = 'peng';
        return name;
    })();
})();
console.log(a);
```
### 7.2.2 关于this对象
this被某个对象调用的时候，就指向那个对象
把外部作用域中的this对象保存在一个闭包能够访问到的变量（that）里，就可以让闭包访问该对象了。
**this**和**arguments**存在相同的问题，解决办法也是相同的
```js
var name = "The Window";
            
var object = {
    name : "My Object",

    getNameFunc : function(){
        var that = this;             //如果这里不把this传给that，那么下边的return this.name中的this就是指向的window，结果将是The Window
        return function(){
            return that.name;
        };
    }
};

alert(object.getNameFunc()());  //"MyObject"
```
this值可能意外转变
```js
var name = "The Window";
            
var object = {
    name : "My Object",

    getName: function(){
        return this.name;
    }
};

alert(object.getName());     //"My Object"
alert((object.getName)());   //"My Object"
alert((object.getName = object.getName)());   //"The Window" in non-strict mode    因为被重新赋值了
```

### 7.2.3 内存泄漏
闭包内循环引用导致内存泄漏
解决办法：使循环引用的元素在运行完后设置为`null`

## 7.3 模仿块级作用域
下边这个例子可以看出for循环是没有作用域的
```js
function outputNumbers(count){
    for (var i=0; i < count; i++){
        alert(i);                       //0,1,2,3,4
    }
//因为没有作用域，所以下边可以取到for中的i
    alert(i);   //count                //5
}

outputNumbers(5);
```
下边说明光声明也是没有作用的
```js
function outputNumbers(count){
    for (var i=0; i < count; i++){
        alert(i);                //0,1,2,3,4
    }

    var i;    //variable re-declared   这里只是声明的话，不影响结果，赋值的话，会影响下边取到的值
    alert(i);   //count          //5
}

outputNumbers(5);
```
将函数声明包含在一对**圆括号中**，表示它实际上是一个**函数表达式**。
函数声明的后边不能加(),但是函数表达式后边加(),表示立即调用。
如果**临时**需要一些**变量**，就可以使用私有作用域。
```js
function outputNumbers(count){
            
    (function () {                               //创建私有作用域
        for (var i=0; i < count; i++){
            alert(i);
        }
    })();
    
    alert(i);   //causes an error
}

outputNumbers(5);
```
在匿名函数中定义的任何变量，都会在执行结束时被销毁，所以上述例子error，这是一种不污染全局变量的很好的办法。
** 这种做法可以减少闭包占用的内存问题，因为没有指向匿名函数的引用。**
** 只要函数执行完毕，就可以立即销毁其作用域链了。**

## 7.4 私有变量
js没有私有成员改变，但是有私有变量的概念。
任何在**函数中**定义的变量（参数，局部变量和其他内部定义的其他函数），都可以认为是私有变量。

我们把有权访问私有变量和私有函数的公有方法成为**特权方法**。
有两种创建特权方法的方式：
1.构造函数中定义特权方法
```js
function MyObject(){
    //私有变量和私有函数
    var privateVariable = 10;
    function privateFunction(){
        return false;
    }
    
    //特权方法   重点就是this
    this.publicMethod = function(){
        privateVariable++;
        return privateFunction();
    }
}
```
** 利用私有和特权成员，可以隐藏那些不应该被直接修改的数据**
2.构造函数传递参数
```js
function Person(name){     
    this.getName = function(){
        return name;
    };
    this.setName = function (value) {
        name = value;
    };
}
var person = new Person("Nicholas");
alert(person.getName());   //"Nicholas"
person.setName("Greg");
alert(person.getName());   //"Greg"
```
缺点：同构造函数，每个实例都要创建一个新方法
静态私有变量解决这个问题

### 7.4.1 静态私有变量--不推荐
利用私有作用于中定义私有变量或函数，同样可以创建特权方法。
注意：
1.不使用函数声明，因为函数声明只能创建局部函数
2.不适用var关键字，也是因为只能创建局部的，如果没有var 就是全局的，私有作用域外也可以访问到
*注意：严格模式下未经声明的变量赋值会导致错误*
```js
(function(){
            
    var name = "";
    
    Person = function(value){                //没有var是全局的
        name = value;                
    };
    
    Person.prototype.getName = function(){
        return name;
    };
    
    Person.prototype.setName = function (value){
        name = value;
    };
})();

var person1 = new Person("Nicholas");
alert(person1.getName());   //"Nicholas"
person1.setName("Greg");
alert(person1.getName());   //"Greg"
                   
var person2 = new Person("Michael");
alert(person1.getName());   //"Michael"    //原型链上name被改变
alert(person2.getName());   //"Michael"
```
特权方法是在**原型**上定义的，因此所有实例都使用同一个函数，避免了重复创建。
而特权方法，作为一个闭包，**总是保存着对包含作用域的引用**
缺点：每个实例都没有自己的私有变量，而且不带var的写法，总是让人很担心，我觉得这个方法很糟糕！！

### 7.4.2 模块模式--★★★★★经常使用
js是以对象字面量方式来创建单例对象的。
主要是通过**将一个对象字面量作为函数的值返回**，返回的对象字面量中只包含可以公开的属性和方法。
**这种模式在需要对单例进行某些初始化，同时又需要维护其私有变量时是非常有用的。**
```js
function BaseComponent(){
}
function OtherComponent(){
}
var application = function(){
    //private variables and functions
    var components = new Array();
    //initialization
    components.push(new BaseComponent());
    //public interface
    return {                            //return  这个要返回到外部
        getComponentCount : function(){
            return components.length;
        },
        registerComponent : function(component){
            if (typeof component == "object"){
                components.push(component);
            }
        }
    };
}();                                    //★这个()很重要
application.registerComponent(new OtherComponent());
alert(application.getComponentCount());  //2
```
**单例通常都是作为全局对象存在的**

### 7.4.3  增强的模块模式
这种增强模式适合那些单例必须是某种类型的实例
**区别就是在模块内部又创建了一个对象**
```js
function BaseComponent(){
}

function OtherComponent(){
}

var application = function(){

    //private variables and functions
    var components = new Array();

    //initialization
    components.push(new BaseComponent());

    //create a local copy of application
    var app = new BaseComponent();            //★唯一的区别

    //public interface
    app.getComponentCount = function(){
        return components.length;
    };

    app.registerComponent = function(component){
        if (typeof component == "object"){
            components.push(component);
        }
    };

    //return it
    return app;
}();

alert(application instanceof BaseComponent);
application.registerComponent(new OtherComponent());
alert(application.getComponentCount());  //2
```
# 8.BOM
## 8.1 window对象
BOM核心对象是window.
既是窗口的一个接口，又是ES规定的Global对象。

### 8.1.1 全局作用域
所有在全局作用域中声明的变量、函数都会变成window 对象的属性和方法
**全局变量不能通过delete 操作符删除，而直接在window 对象上的定义的属性可以。**
尝试访问未声明的变量会抛出错误，但是通过查询window 对象，则返回"undefined"

### 8.1.2 窗口关系及框架
如果页面中包含框架，则每个框架都拥有自己的window 对象，并且保存在frames 集合中。
在frames集合中，可以通过数值索引（从0 开始，从左至右，从上到下）或者框架名称来访问相应的window 对象。

### 8.1.3 窗口位置
兼容模式：
```js
var leftPos = (typeof window.screenLeft == "number") ?
    window.screenLeft : window.screenX;
var topPos = (typeof window.screenTop == "number") ?
    window.screenTop : window.screenY;
```
移动方法：
`moveTo()`接收的是新位置的x 和y 坐标值
`moveBy()`接收的是在水平和垂直方向上移动的像素数。
```js
//将窗口移动到屏幕左上角
window.moveTo(0,0);
//将窗向下移动100 像素
window.moveBy(0,100);
```
### 8.1.4 窗口大小
兼容模式：
```js
var pageWidth = window.innerWidth,
    pageHeight = window.innerHeight;
if (typeof pageWidth != "number"){
    if (document.compatMode == "CSS1Compat"){
        pageWidth = document.documentElement.clientWidth;
        pageHeight = document.documentElement.clientHeight;
    } else {
        pageWidth = document.body.clientWidth;
        pageHeight = document.body.clientHeight;
    }
}
```
调整窗口大小：
`resizeTo()`接收浏览器窗口的新宽度和新高度
`resizeBy()`接收新窗口与原窗口的宽度和高度之差
```js
//调整到100×100
window.resizeTo(100, 100);
//调整到200×150
window.resizeBy(100, 50);
```

### 8.1.5 导航和打开窗口
`window.open()`打开一个窗口到一个指定URL中
4个参数：要加载的URL+窗口目标+一个特性字符串+一个表示新页面是否取代浏览器历史记录中当前加载页面的布尔值。
可以只写一个参数/两个参数
```js
//等同于< a href="http://www.wrox.com" target="topFrame"></a>
window.open("http://www.wrox.com/", "topFrame");
```
第二个参数可以是：_self、_parent、_top 或_blank。

#### 8.1.5.1弹出窗口
第三个参数的设置选项：
`fullscreen` yes或no 表示浏览器窗口是否最大化。仅限IE
`height` 数值表示新窗口的高度。不能小于100
`left` 数值表示新窗口的左坐标。不能是负值
`location` yes或no 表示是否在浏览器窗口中显示地址栏。不同浏览器的默认值不同。如果设置为no，地址栏可能会隐藏，也可能会被禁用（取决于浏览器）
`menubar` yes或no 表示是否在浏览器窗口中显示菜单栏。默认值为no
`resizable` yes或no 表示是否可以通过拖动浏览器窗口的边框改变其大小。默认值为no
`scrollbars` yes或no 表示如果内容在视口中显示不下，是否允许滚动。默认值为no
`status` yes或no 表示是否在浏览器窗口中显示状态栏。默认值为no
`toolbar` yes或no 表示是否在浏览器窗口中显示工具栏。默认值为no
`top` 数值表示新窗口的上坐标。不能是负值
`width` 数值表示新窗口的宽度。不能小于100
```js
var wroxWin = window.open("http://www.wrox.com/","wroxWindow",
"height=400,width=400,top=10,left=10,resizable=yes");
//调整大小
wroxWin.resizeTo(500,500);
//移动位置
wroxWin.moveTo(100,100);
//调用 close()方法还可以关闭新打开的窗口。
wroxWin.close();
```
`opener`属性，指向打开当前页面的原始窗口对象
```js
alert(wroxWin.opener == window); //true
```
禁止和原窗口通信的话设置为`null`

#### 8.1.5.2 安全限制
不允许在屏幕之外创建弹出窗口、不允许将弹出窗口移动到屏幕以外、不允许关闭状态栏等

#### 8.1.5.3 弹出窗口屏蔽程序
屏蔽掉的话，window.open()会返回null

### 8.1.6 间歇调用和超时调用
超时调用：`setTimeout()`
取消超时调用：`clearTimeout()`
```js
//设置超时调用
var timeoutId = setTimeout(function() {    //虽然是变量，但是也会执行
    alert("Hello world!");
}, 1000);
//注意：把它取消
clearTimeout(timeoutId);
```
间歇调用：`setInterval()`
取消间歇调用：`clearInterval()`
用法相同

### 8.1.7 系统对话框
`alert()` `confirm()`和`prompt()`方法可以调用系统对话框向用户显示消息
`confirm()`确认对话框，很像一个警告
```js
if (confirm("Are you sure?")) {
    alert("I'm so glad you're sure! ");
} else {
    alert("I'm sorry to hear you're not sure. ");
}
```
`prompt()`这是一个“提示”框，用于提示用户输入一些文本。
两个参数：要显示给用户的文本提示和文本输入域的默认值（可以是一个空字符串）。
```js
var result = prompt("What is your name? ", "");
    if (result !== null) {
        alert("Welcome, " + result);
}
```
还有两个对话框
```js
//显示“打印”对话框
window.print();
//显示“查找”对话框
window.find();
```

## 8.2 location 对象
`window.location`和`document.location`引用的是同一个对象。
所有属性图示：
![](/images/53605c5a0001b26909900216.jpg)
所有属性：
![](/images/5354b1d00001c4ec06220271.jpg)
所有方法：
![](/images/5354b1eb00016a2405170126.jpg)

### 8.2.1 查询字符串参数
`location.search`
```js
function getQueryStringArgs(){   //保留这个函数
        
    //取得查询字符串并去掉开头的问号
    var qs = (location.search.length > 0 ? location.search.substring(1) : ""),
    
       //保存数据的对象
        args = {},
    
        //取得每一项
        items = qs.length ? qs.split("&") : [],
        item = null,
        name = null,
        value = null,
        
        //在for 循环中使用
        i = 0,
        len = items.length;
    
    //逐个将每一项添加到args 对象中
    for (i=0; i < len; i++){
        item = items[i].split("=");
        name = decodeURIComponent(item[0]);
        value = decodeURIComponent(item[1]);
        
        if (name.length){
            args[name] = value;
        }
    }
    
    return args;
}

//assume query string of ?q=javascript&num=10

var args = getQueryStringArgs();

alert(args["q"]);     //"javascript"
alert(args["num"]);   //"10"
```

### 8.2.2 位置操作
```js
var local = location.href;   //返回当前页面完整URL
//假设初始URL 为http://www.wrox.com/WileyCDA/
//将URL 修改为"http://www.wrox.com/WileyCDA/#section1"
location.hash = "#section1";
//将URL 修改为"http://www.wrox.com/WileyCDA/?q=javascript"
location.search = "?q=javascript";
//将URL 修改为"http://www.yahoo.com/WileyCDA/"
location.hostname = "www.yahoo.com";
//将URL 修改为"http://www.yahoo.com/mydir/"
location.pathname = "mydir";
//将URL 修改为"http://www.yahoo.com:8080/WileyCDA/"
location.port = 8080;
```

## 8.3 navigator对象
识别客户端的事实标准
`navigator`对象的属性和方法：
![](/images/5354cff70001428b06880190.jpg)

### 8.3.1 检测插件
```js
//plugin detection - doesn't work in IE
function hasPlugin(name){
    name = name.toLowerCase();
    for (var i=0; i < navigator.plugins.length; i++){
        if (navigator.plugins[i].name.toLowerCase().indexOf(name) > -1){
            return true;
        }
    }

    return false;
}        

//plugin detection for IE
function hasIEPlugin(name){
    try {
        new ActiveXObject(name);
        return true;
    } catch (ex){
        return false;
    }
}

//detect flash for all browsers
function hasFlash(){
    var result = hasPlugin("Flash");
    if (!result){
        result = hasIEPlugin("ShockwaveFlash.ShockwaveFlash");
    }
    return result;
}

//detect quicktime for all browsers
function hasQuickTime(){
    var result = hasPlugin("QuickTime");
    if (!result){
        result = hasIEPlugin("QuickTime.QuickTime");
    }
    return result;
}

//detect flash
alert(hasFlash());

//detect quicktime
alert(hasQuickTime());

```
`refresh()`刷新plugins反映最新安装的插件
设置为true，则会重新加载页面

### 8.3.2 注册处理程序
Firefox 2 为navigator 对象新增了`registerContentHandler()`和`registerProtocolHandler()`方法
这两个方法可以让一个站点指明它可以处理特定类型的信息。
`registerContentHandler()`方法接收三个参数：要处理的MIME 类型+可以处理该MIME类型的页面的URL+应用程序的名称。
例子：要将一个站点注册为处理RSS 源的处理程序
```js
navigator.registerContentHandler("application/rss+xml",
"http://www.somereader.com?feed=%s", "Some Reader");
```
第一个参数是RSS 源的MIME 类型。
第二个参数是应该接收RSS 源URL 的URL，其中的%s 表示RSS 源URL，由浏览器自动插入。
当下一次请求RSS 源时，浏览器就会打开指定的URL，
而相应的Web 应用程序将以适当方式来处理该请求。
`registerProtocolHandler()`方法，它也接收三个参数：要处理的协议（例如，mailto 或ftp）+处理该协议的页面的URL +应用程序的名称
例子：要想将一个应用程序注册为默认的邮件客户端
```js
navigator.registerProtocolHandler("mailto",
"http://www.somemailclient.com?cmd=%s", "Some Mail Client");
```
这个例子注册了一个mailto 协议的处理程序，该程序指向一个基于Web 的电子邮件客户端。
同样，第二个参数仍然是处理相应请求的URL，而%s 则表示原始的请求。

## 8.4 screen 对象
screen对象基本上只用来表明客户端的能力，包括显示器的信息，如像素宽度和高度等。
属性：
![](/images/5354d2810001a47706210213.jpg)
```js
window.resizeTo(screen.availWidth, screen.availHeight);
```

## 8.5 history 对象
```js
//后退一页
history.go(-1);
//前进一页
history.go(1);
//前进两页
history.go(2);
//跳转到最近的wrox.com 页面
history.go("wrox.com");
//后退一页
history.back();
//前进一页
history.forward();
```
`length`保存着历史纪录的数量，为**0**时，表示用户打开的第一个页面
![](/images/53548c200001228206210123.jpg)

# 10.DOM
### 10.1.1 Node类型
Javascript中所有节点类型都继承自Node类型，因为**所有节点**都共享着相同的基本属性和方法。
每个节点都有一个`nodeType`属性，用于表明节点类型
Node.ELEMENT_NODE(1);                 //元素节点
Node.ATTRIBUTE_NODE(2);               //属性节点
Node.TEXT_NODE(3);                    //文本节点
Node.CDATA_SECTION_NODE(4);
Node.ENTITY_REFERENCE_NODE(5);
Node.ENTITY_NODE(6);
Node.PROCESSING_INSTRUCTION_NODE(7);
Node.COMMENT_NODE(8);
Node.DOCUMENT_NODE(9);                  //文档节点
Node.DOCUMENT_TYPE_NODE(10);
Node.DOCUMENT_FRAGMENT_NODE(11);
Node.NOTATION_NODE(12);

#### 10.1.1.1 了解节点具体信息：
`nodeName`元素的标签名
`nodeValue` 内容

#### 10.1.1.2 节点关系
`childNodes`每个节点都有一个这个属性，其中保存着一个`NodeList`对象.
`NodeList`是一个**类数组**元素
访问的时候通过`[]` `item()`来访问
**将类数组转化为数组**
`Array.prototype.slice()`方法
```js
var arrayOfNodes = Array.prototype.slice(someNode.childNodes,0)
```
`parentNode`每个节点都有一个这个属性
`previousSibling`访问相邻的上一个节点，第一个节点的previousSibling为`null`
`nextSibling`访问相邻的下一个节点，最后一个节点的nextSibling为`null`
`firstChild`
`lastChild`
`hasChildNode`这个方法在节点包含**一或多个**子节点的情况下返回true。
`length`也可以查看是否有子节点
`ownerDocument`所有节点都有的最后一个属性。该属性指向表示整个文档的文档节点，指向`Document`

#### 10.1.1.3 操作节点
`appendChild()`向末位添加一个节点，如果是已经存在的节点，那么这个就会将旧的节点**移动**到最后的位置
`insertBefore()`将节点插入参考节点的前边，两个参数（要插入的节点+参考节点）如果参考节点为`null`则插入最后一个节点，和appChild相同
```js
//插入第一个节点
var returnedNode = someNode.insertBefore(newNode,someNdode.firstChild)
```
`replaceChild`替换节点，两个参数（要插入的节点+要替换的节点），要替换的节点将被删除。
被替换的节点还在文档中，只是没有了它的位置而已
`removeChild`移除节点
被删除的节点还在文档中，只是没有了它的位置而已
`cloneNode()`接收一个布尔值参数，表示是否执行**深复制**。
参数为true为深复制，也就是复制节点**及其整个子节点树**
参数为false为浅复制，只复制节点本身
`normalize()`查找内部节点，如果找到了为空文本节点，则**删除它**，如果找到相邻的文本节点，则将他们合并为一个文本节点。

### 10.1.2 Document类型
js通过Document类型表示文档
浏览器中，document对象是`HTMLDocument`(继承自Document类型)的一个**实例**，表示整个HTML页面。
docment对象是window对象的一个属性，作为全局对象来访问。
nodeType值为9
nodeName值为#document
nodeValue值为null
parentNode值为null
ownerDocument值为null
子节点可能是一个DocumentType(最多一个)、Element(最多一个)、ProcessimgInstruction或Comment

#### 10.1.2.1 文档的子节点
访问子节点的属性：
`documentElement` 指向`<html>`元素
document.documentElement      对html元素的引用
`childNodes`
document.childNodes\[0]访问子节点
`body` 
document.body        对body元素的引用
`doctype`
document.doctype    对`<!DOCTYPE>`的引用，不同浏览器返回值不同，不推荐
html外部的**注释**应该算是文档的子节点，但是不同浏览器返回值不同，所以不做讨论了

#### 10.1.2.2 文档信息
`title` 获取或设置文档标题
document.title
`URL` 包含页面完整的URL
document.URL
`domain`只包含页面的域名    （只有它可以单独设置）
document.domain      //设置的时候必须和来时候的域名是同一个域。当两个子域被设成相同的wrox.com的时候，可以互相访问，但是不能再改回去了，否则会报错
`referrer`返回键返回的页面地址
document.referrer

#### 10.1.2.3 查找元素
`getElementById()`    如果不存在带有ID的元素，则返回null。区分大小写，如果存在多个，返回第一个。name不要和ID相同，IE7会识别name并提前。
`getElementsByTagName()`返回的是一个HTMLCollection对象，和nodeList类似。
有两种方法可以访问含有`name`的项
```js
<img src="myimage.gif" name="myImage">
//方法一
var myImage = images.namedItem("myImage");    //.namedItem()获取
//方法二
var myImage = images["myImage"]
```
取得文档中**所有**元素
```js
var allImages = document.getElementsByTagName("**")     //用*
```
`getElementsByname()`返回带有name的所有元素。和getElementsByTagName其他方法都一样

#### 10.1.2.4 特殊集合
`document.anchors` 所有带有**name**的`a`标签元素
`document.applets` 所有**applet**标签元素
`document.forms`   所有**form**标签元素
`document.images`  所有**img**标签元素
`document.links`   所有带有`href`的标签元素

*src 的内容，是页面必不可少的一部分，是引入。href 的内容，是与该页面有关联，是引用。区别就是，引入和引用。*
#### 10.1.2.5 DOM一致性检测
`document.implementation`属性提供浏览器对DOM的实现的**相应信息**和**功能的对象**
这个属性有一个方法`hasFeature()`。
有两个参数（要检查的DOM功能名称+版本号）
```js
var hasXmlDom = document.implementation.hasFeature("XML","1.0");   //判断是否为true
```
有的浏览器对这个支持还不是很好，现代浏览器差不多都没问题了，还是推荐**能力检测（像监听）**

#### 10.1.2.6 文档写入
`write()`写入到输出流文本
()内部会解析代码，所以要注意**转义字符\**的使用
如果在文档加载结束后再调用，那么输出的内容将会**重写整个页面**
如果在文档中加载就不会重写整个页面
```js
<script>
    window.onload = function(){
        document.write("hello")   //重写整个页面
    }
</script>
```
`writeln()`在字符串的末尾添加一个换行符(\n)
`open()` 打开网页输出流
`close()`关闭网页输出流

### 10.1.3 Element类型
`nodeType`的值是1
`nodeName`的值为元素或标签名
`nodeValue`的值为null
`parentNode`可能是Document或Element
子节点可能是`Element` `Text` `Comment` `ProcessingInstruction` `CDATASection` `EntityReference`

`nodeName`和`tagName`属性是相同的，都是返回访问元素的标签名，且都为**大写**，在XML和源码保持大小一致

#### 10.1.3.1 HTML元素
所有HTML元素都由HTMLElement类型表示。HTMLElement类型直接继承自Element并添加了一些属性
`id` 文档中的**唯一**标识符
`title` 有关元素的附加说明信息
`lang` 元素内容的语言代码，很少使用
`dir` 语言的方向，ltr(从左至右)rtl(从右至左)
`className` 元素指定的CSS类

```js
<div id="myDiv" class="bd" title="Body text" lang="en" dir="ltr">Some text</div>
alert(div.id);         //"myDiv"
alert(div.className);  //"bd"   ★这里必须是className不能是class
alert(div.title);      //"Body text"
alert(div.lang);       //"en"
alert(div.dir);        //"ltr"
```

#### 10.1.3.2 取得特性
`getAttribute()`
`setAttribute()`
`removeAttribute()`
如果给定的特性值不存在getAttribute()返回**null**---这点很重要来判断是否有这个属性
```js
if(getAttribute(disabled)==null){
    //没有找到disabled的时候执行
}
```
特性的名称是**不区分大小写的**
非自定义的叫**公认特性**
有两个**特殊的特性**属性值与个体Attribute()返回的值不同
`style`
通过getAttribute()返回的是CSS**文本**
通过.style返回的是CSS**对象**
`onclick`事件处理程序
通过getAttribute()访问，返回响应代码的**字符串**
访问onclick属性时，返回一个javascript函数（如果未在元素中指定相应特性，则返回null）
所以建议**只有访问自定义属性的时候才用**getAttribute()

#### 10.1.3.3 设置特性
setAttribute()
两个参数：要设置的特性名+值
通过这个方法设置的特性名会被统一**转换为小写**

removeAttribute()
不仅清除属性值，也会完全删除特性

#### 10.1.3.4 attributes属性
只有Element有attributes属性。
attributes包含一个`NamedNodeMap`，与`NodeList`类似！也是一个动态集合。
方法：
`getNamedItem(name)` 返回nodeName属性等于name的节点
`removeNamedItem(name)`从列表中移除nodeName属性等于name的节点
`setNamedItem(node)`向列表中添加节点，以节点的nodeName属性为索引
`item(pos)`返回数字pos位置的节点
nodeName就是**特性的名称**，nodeValue就是**特性的值**
```js
var id = element.attributes.getNamedItem("id").nodeValue;
//简写
var id = element.attributes["id"].nodeValue;
```
也可以通过上述方法来设置新值。
removeNamedItem()和removeAttribute()效果相同，唯一区别就是前者返回表示被删除特性的Attr**节点**。
```js
var oldAttr = element.attributes.removeNamedItem("id");
```
**通常attributes都是在遍历节点属性才用**
将`specified`属性设置为true，表示在HTML中指定了相应特性（用上了这个特性）

#### 10.1.3.5 创建元素
`document.createElement()`
在创建新元素的同时，也为新元素设置了ownerDocument属性（指向document文本节点）
可以通过appendChild、insertBefore、replaceChild等属性来添加元素
也可以**直接插入**元素标签
```js
var div = document.createElement("<div id=\"myDiv\"></div>")
```

#### 10.1.3.6 元素的子节点
子节点有可能是元素、文本节点、注释或处理指令
不同浏览器看待这些节点不同
```js
<ul id="muList"> //第一个节点
    <li>1</li>   //第二个节点
    <li>2</li>   //第三个节点
    <li>3</li>   //第四个节点
</ul>
```
上式
IE：3个节点
其他：7个元素\[4个文本节点(空白符)+3个元素]
所以在执行操作前，通常要**检查一下nodeType**属性是否为**1**
```js
for(var i=0; len=element.childNodes.length; i<len; i++){
    if(element.childNodes[i].nodeType == 1){                  //重要
        //执行某些操作
    }
}
```
还有一种解决方法就是用`getElementsByTagName()`，这个方法也是推荐的

### 10.1.4 Text类型
纯文本内容
`nodeType`的值是3
`nodeName`的值为"#text"
`nodeValue`的值为节点所包含的文本
`parentNode`是一个Element
没有子节点
`data`和`nodeValue`一样可以访问节点包含的文本

操作节点文本方法：
`appendData(text)`  将text添加到节点的末尾
`deleteData(offset,count)` 从offset指定的位置开始删除count个字符
`insertData(offset,text)`在offset指定的位置插入text
`replaceData(offset,count,text)`用text替换从offset指定的位置开始到offset+count为止出的文本
`splitText(offset)`从offset指定的位置将当前文本节点分成两个文本节点
`substringData(offset,count)`提取从offset指定的位置开始到offset+count位置处的字符串。

nodeValue.length == data.length
访问**子节点**的方法
```js
var textNode = div.firstChild;  //或者div.childNodes[0]
//修改
div.firstChild.nodeValue = "hello"
```
*注意：大于小于符号或引号都会被转义*

#### 10.1.4.1 创建文本节点
`document.createTextNode()` 创建文本节点同时，也会为其设置ownerDocument属性。
```js
var textNode = document.createTextNode("<strong>Hello</strong>world!")
```
每个元素一般只有一个文本子节点，不过也有例外
```js
function addNode(){
        
    var element = document.createElement("div");
    element.className = "message";
    
    var textNode = document.createTextNode("Hello world!");
    element.appendChild(textNode);
    
    var anotherTextNode = document.createTextNode("Yippee!");
    element.appendChild(anotherTextNode);
    
    document.body.appendChild(element);    //两个子节点连起来，★中间有空格
}
```

#### 10.1.4.2 规范化文本节点
`normalize()`在一个包含两个或多个文本节点的父元素上调用这个方法，则会将所有文本节点**合并**成一个节点。
```js
//上边的例子，在底下直接添加
element.normalize();
alert(element.childNodes.length);  //1
alert(element.firstChild.nodeValue);  //"Hello World!Yippee!"
```

#### 10.1.4.3 分割文本节点
`splitText()`将一个文本节点分成两个文本节点
原来的文本节点将包含从开始到指定位置之前的内容。
新文本节点将包含剩下的文本。
```js
function addNode(){
        
    var element = document.createElement("div");
    element.className = "message";
    
    var textNode = document.createTextNode("Hello world!");
    element.appendChild(textNode);
    
    document.body.appendChild(element);
    
    var newNode = element.firstChild.splitText(5);     //进行分割
    alert(element.firstChild.nodeValue);  //"Hello"
    alert(newNode.nodeValue);             //" world!"
    alert(element.childNodes.length);     //2
        
}
```
**文本切割是从文本节点中提取数据的一种常用DOM解析技术**

### 10.1.5 Comment 类型
注释 通过Comment来表示
`nodeType`的值是8
`nodeName`的值为"#comment"
`nodeValue`的值为注释的内容
`parentNode`可能是Element或Document
没有子节点

Comment类型与Text类型继承自**相同的基类**，因此拥有除了`splitText()`之外的所有操作。
同样通过data和nodeValue来访问注释内容
```js
function getComment(){
        
    var div = document.getElementById("myDiv");
    var comment = div.firstChild;
    alert(comment.data);
    
}
```

`document.createComment()` 创建注释节点  很少用

### 10.1.6 CDATASection 类型
这种类型只针对XML文档，表示的是CDATA区域，同样是继承自Text类型，拥有出splitText()之外的苏哦有操作。
`nodeType`的值是4
`nodeName`的值为"#cdata-section"
`nodeValue`的值是CDATA区域中的内容
`parentNode`可能是Element或Document
没有子节点
```js
<div id="myDiv"><![CDATA[This is some content.]]></div>
```
现在四大主流浏览器都无法正确解析他，所以略过
`document.createCDataSection()` 创建CDATA区域

### 10.1.7 DocumentType 类型
不常用，包含着`doctype`有关的所有信息
`nodeType`的值是10
`nodeName`的值为doctype的名称
`nodeValue`的值是null
`parentNode`是Document
没有子节点

不能动态创建
DocumentType对象保存在document.doctype中。
三个属性:
`name` 文档类型的名称
`entities` 文档类型描述的**实体**的`NamedNodeMap`对象
`notations` 由文档类型描述的**符号**的`NamedNodeMap`对象

### 10.1.8 DocumentFragment类型
只有`DocumentFragment`在文档中没有对应的标记。
是轻量级文档，可以包含和控制节点，但**不占用资源**
`nodeType`的值是11
`nodeName`的值为"#document-fragment"
`nodeValue`的值是null
`parentNode`是null
子节点可以是所有类型

可以当作**仓库**来使用--很好用
`document.createDocumentFragment()`创建仓库
```js
function addItems(){
        
    var fragment = document.createDocumentFragment();
    var ul = document.getElementById("myList");
    var li = null;
    
    for (var i=0; i < 3; i++){
        li = document.createElement("li");
        li.appendChild(document.createTextNode("Item " + (i+1)));
        fragment.appendChild(li);
    }
    
    ul.appendChild(fragment);    

    
}
```
文档片段的所有子节点都**被删除**并转移到了被插入的节点中。

### 10.1.9 Attr类型
元素的特性在DOM中以Attr类型来表示。特性存在于元素的attributes属性中的节点
`nodeType`的值是2
`nodeName`的值是特性的名称
`nodeValue`的值是特性的值
`parentNode`是null

有3个属性
`name` 特性的名称同nodeName
`value` 特性的值同nodeValue
`specified` 区别特性在代码中是指定的还是默认的

`document.createAttribute()` 创建新属性
```js
function assignAttribute(){
    var element = document.getElementById("myDiv");
    var attr = document.createAttribute("align");
    attr.value = "left";
    element.setAttributeNode(attr);
    
    alert(element.attributes["align"].value);       //"left"  返回节点
    alert(element.getAttributeNode("align").value); //"left"--新方法，返回节点
    alert(element.getAttribute("align"));           //"left"  返回特性的值

    
}
```

## 10.2 DOM操作技术

### 10.2.1 动态脚本
动态加载的外部js文件能**立即**运行
```js
function loadScript(url){
    var script = document.createElement("script");
    script.type = "text/javascript";
    script.src = url;
    document.body.appendChild(script);
}
```
缺点：**无法判断是否加载完成**

嵌入式：
IE不允许DOM访问`script`的子节点，不过可以使用script的`text`属性来指定js代码
```js
function loadScriptString(code){
    var script = document.createElement("script");
    script.type = "text/javascript";
    try {
        script.appendChild(document.createTextNode(code));   //兼容Safari,因为不支持text
    } catch (ex){
        script.text = code;           //兼容IE
    }
    document.body.appendChild(script);
}

function addScript(){
    loadScriptString("function sayHi(){alert('hi');}");
    sayHi();
}
```

### 10.2.2 动态样式
和script类似
必须将`link`添加到`head`而不是`body`
```js
function loadStyles(url){
    var link = document.createElement("link");
    link.rel = "stylesheet";
    link.type = "text/css";
    link.href = url;
    var head = document.getElementsByTageName("head")[0];
    head.appendChild(link)
}
```
加载外部样式文件的过程是**异步**的，所以知不知道样式已经加载完成并不重要。

嵌入式（同script）：
```js
function loadStyleString(css){
    var style = document.createElement("style");
    style.type = "text/css";
    try{
        style.appendChild(document.createTextNode(css));
    } catch (ex){
        style.styleSheet.cssText = css;
    }
    var head = document.getElementsByTagName("head")[0];
    head.appendChild(style);
}

function addStyle(){
    loadStyleString("body{background-color:red}"); 
}
```

### 10.2.3 操作表格
P282   略过

### 10.2.4 使用NodeList
理解`NodeList`及`NamedNodeMap`和`HTMLCollection`。
这三个集合都是动态的，实时查询更新
所以最好用变量赋值做一下缓存，如果不做的话会出现死循环。
```js
var divs = docuemnt.getElementsByTagName("div"),
    i,
    div;

var len = divs.length;     //这里做了个缓存快照，就不会死循环了
for(i=0;i<len;i++){
    div = document.createElement("div");
    document.body.appendChild(div);
}
```

# 11.DOM扩展
## 11.1 选择符API
### 11.1.1 querySelector()方法
接收一个CSS选择符，返回与该模式匹配的**第一个元素**，如果没有则返回null。
```js
if (document.querySelector){
        
    //get the body element
    var body = document.querySelector("body");
    alert(body.tagName);
                       
    //get the element with the ID "myDiv"
    var myDiv = document.querySelector("#myDiv");
    alert(myDiv);
                       
    //get first element with a class of "selected"
    var selected = document.querySelector(".selected");
    alert(selected.innerHTML);
                       
    //get first image with class of "button"
    var img = document.body.querySelector("img.button");   //★可以这么用
    alert(img);


} else {
    alert("Selectors API not supported in this browser");
}
```

### 11.1.2 querySelectorAll()方法
接收的参数和上边的方法相同，但返回的是一个NodeList的实例。
```js
if (document.querySelectorAll){
            
    //get all <em> elements in a <div> (similar to getElementsByTagName("em"))
    var ems = document.getElementById("myDiv").querySelectorAll("em");
    alert(ems.length);
                       
    //get all elements with class of "selected"
    var selecteds = document.querySelectorAll(".selected");
    alert(selecteds.length);
    
    //get all <strong> elements inside of <p> elements
    var strongs = document.querySelectorAll("p strong");     //可以这么用
    alert(strongs.length);


} else {
    alert("Selectors API not supported in this browser");
}
```
访问可以通过`item()`和`[]`

### 11.1.3 matchesSelector()方法
用来匹配dom元素是否匹配某css selector。
如果调用元素与该选择符匹配，则返回true，否则返回false。
```js

<body class="page1">

    <script type="text/javascript">
    //兼容
        function matchesSelector(element, selector){
            if (element.matchesSelector){
                return element.matchesSelector(selector);
            } else if (element.msMatchesSelector){
                return element.msMatchesSelector(selector);
            } else if (element.mozMatchesSelector){
                return element.mozMatchesSelector(selector);
            } else if (element.webkitMatchesSelector){
                return element.webkitMatchesSelector(selector);
            } else {
                throw new Error("Not supported.");
            }
        }
        
        if (matchesSelector(document.body, "body.page1")){
            alert("It's page 1!");
        }


    </script>
</body>
```

## 11.2 元素遍历
因为有些浏览器会将**空白符**当作文本节点
为了**弥补这个差异**，Element Traversal 规范新定义了一组属性
`childElementCount` 返回子元素的个数
`firstElementChild` 指向第一个字元素;firstChild的元素版
`lastElementChild` 指向最后一个子元素；lastChild的元素版
`previousElementSibling` 指向前一个同辈元素
`nextElementSibling` 指向后一个同辈元素
利用这些元素就不必担心空白文本节点。
用了这个属性就不用判断nodeType了
```js
var i,
    len,
    child = element.firstElementChild;
    while(child != element.lastChild){
        processChild(child);         //加工处理这个元素，替换成自己需要的
        child = child.nextElementSibling;
    }
```

## 11.3 HTML5
### 11.3.1 与类相关的扩展
#### 11.3.1.1 getElementsByClassName()方法
接收一个参数，即一个包含一个或多个类名的字符串，返回NodeList。
传入多个类名时，类名的先后顺序不重要。
```js
//取得所有类中包含"username"和"current"的元素
var allCurrentUsernames = document.getElementsByClassName("username current")
```
和其他返回NodeList型的DOM方法一样都具有性能问题

#### 11.3.1.2 classList属性
这个属性是新集合类型`DOMToenList`的实例
定义了如下方法
`add(value)` 添加
`contains(value)` 是否存在给定值，存在返回true
`remove(value)` 删除
`toggle(value)` 存在则删除，不存在则添加
```js
<div class="bd user disabled"><div>

//删除disabled类
div.classList.remove("disabled");
//其他也类似
//确定元素中是否包含既定的类名

if(div.classList.contains("bd")){
    //执行操作
}
```
有了上边这些方法，className一般就只用在**删除所有类**和**重写所有类**的时候用了

### 11.3.2 焦点管理
html5添加了辅助管理DOM焦点的功能
`document.activeElement`引用DOM当前获得了焦点的元素。
获得焦点的方式有：页面加载、用户输入、在代码中调用focus()
```js
var button = document.getElementById("myButton");
button.focus();
alert(document.activeElement === button);   //true
```
刚刚加载完成时，document.activeElement保存的是`document.body`。
加载期间，保存的是`null`
`document.hasFocus()`方法，确定文档是否获得了焦点
```js
var button = document.getElementById("myButton");
button.focus();
alert(document.hasFocus());   //true
```
**通过检测文档是否获得了焦点，可以知道用户是不是正在与页面交互**
无障碍用的比较多，上边两个属性

### 11.3.3 HTMLDocument的变化
#### 11.3.3.1 readyState属性
这个属性有两个可能的值：
`loading`正在加载文档
`complete`已经加载完文档

#### 11.3.3.2 兼容模式
渲染页面模式分为：标准和混杂
`document.compatMode`检查渲染模式
`CSS1Compat` 标准模式
`BackCompat` 混杂模式

#### 11.3.3.3 head属性
`document.head`新增的引用head元素方法
```js
var head = document.head ||document.getElementsByTagName("head")[0];
```

### 11.3.4 字符集属性
`document.charset`访问或修改字符集属性
document.charset = "UTF-8"
`document.defaultCharset`根据默认浏览器及操作系统的设置来确定字符集是什么

### 11.3.5 自定义数据属性 ★
`data-` 自定义数据属性写法
`dataset`当问自定义属性
dataset属性的值是DOMStringMap的一个实例，也就是名值对而的映射
```js
//取得自定义属性的值
var appId = div.dataset.appId;
//设置自定义属性的值
div.dataset.appId = "myId"
//是否存在appId
if(div.dataset.appId){
    //执行操作
}
```

### 11.3.6 插入标记
#### 11.3.6.1 innerHTML属性
新的DOM树完全**替换**原先的所有子元素
在读取innerHTML返回的是经过序列化之后的结果。
**通过innerHTML插入的`script`元素并不会执行其中的脚本**
innerHTML插入的字符串开头就是一个"无作用域的元素(script)"，那么IE会在解析这个字符串前先删除该元素。
```js
div.innerHTML = "_<script defer>alert('hi');</script>";
div.innerHTML = "<div>&nbsp;</div><script defer>alert('hi');</script>";
div.innerHTML = "<input type=\"hidden\"><script defer>alert('hi');</script>";  //首选
```
不支持innerHTML的元素有：col/colgroup/frameset/head/html/style/table/tbody/thead/tfoot/tr
插入的时候**记得用转义字符**
读取的时候**会转化成字符编码**

#### 11.3.6.2 outerHTML属性
返回调用它的元素及所有子节点的HTML标签。
和innerHTML唯一的区别就是**它包含自身**

#### 11.3.6.3 insertAdjacentHTML()方法
接收两个参数：插入位置+插入的HTML文本
`beforebegin`当前元素之前插入一个同辈元素
`afterbegin`当前元素子元素-插入第一个
`beforeend`当前元素子元素-插入最后一个
`afterend`当前元素之后插入一个同辈元素

```js
element.insertAdjacentHTML("beforebegin","<p>hello</p>")
```

#### 11.3.6.2 内存与性能问题
使用前面的属性时，如果将该元素从文档树中删除，元素与事件处理程序之间的绑定关系在内存中并**没有一并删除**，
如果这种情况频繁出现，占用内存会明显增加。
13章提供解决方案

#### 11.3.7 scrollIntoView()方法
滚动窗口，调用元素就可以出现在视口中
```js
//滚动窗口，突出输入框--让元素可见吸引用户注意力
document.form[0].scrollIntoView()
```
## 11.4 专用扩展
### 11.4.1 文档模式
文档模式决定了：你可以使用哪个级别的CSS+在js中使用那些API+如何对待文档类型(doctype)
标准模式+混杂模式
强制浏览器以某种模式渲染页面：
```js
    <meta http-equiv="X-UA-Compatible" content="IE=IEVersion">   //IEVersion有不同的值
```
`Edge` 始终以最新的文档模式来渲染页面
`EmulateIE9`如果有文档类型声明，则以IE9标准模式渲染页面，否则将文档模式设置为IE5
`EmulateIE8`
`EmulateIE7`
`9` 强制以IE9标准模式渲染页面，忽略文档类型声明
`8`
`7`
`5`

默认情况下，浏览器会通过文档类型声明来确定使用最佳的可用文档模式，还是混杂模式，
不是必须设置X-UA-Compatible
`document.documentMode` 获得给定页面使用什么文档模式。

### 11.4.2 children属性
这个属性是HTMLCollection的实例
和childNodes没什么区别
区别就在于它不包含**空白符**，IE9之后不包含注释

### 11.4.3 contains()方法
某个节点是不是另一个节点的后代
```js
//body元素是不是html的后代
alert(document.documentElement.contains(document.body)); //true
```
`compareDocumentPosition()`确定节点间的关系
1  无关
2  居前
4  居后
8  包含
16 被包含

实现和contains()相同的方法
```js
var result = document.documentElement.compareDocumentPosition(document.body);
alert(!!(result & 16))   //两个逻辑非操作符会将该数值转换成布尔值
```
contains()的兼容模式
```js
function contains(refNode, otherNode){
    if (typeof refNode.contains == "function" && 
            (!client.engine.webkit || client.engine.webkit >= 522)){
        return refNode.contains(otherNode);
    } else if (typeof refNode.compareDocumentPosition == "function"){
        return !!(refNode.compareDocumentPosition(otherNode) & 16);
    } else {
        var node = otherNode.parentNode;
        do {
            if (node === refNode){
                return true;
            } else {
                node = node.parentNode;
            }
        } while (node !== null);
        return false;
    }
}

function getContains(){
    alert(contains(document.documentElement, document.body));
    
}
```

### 11.4.4 插入文本
#### 11.4.4.1 innerText
innerText会**先删除**元素的所有子节点，然后再插入。
不同浏览器处理空白符方式不同，所以输出的文本可能会有，也可能没有**缩进**
和innerHTML一样需要转义字符
读取的时候会字符编码形式输出
技巧：通过innerText过滤掉HTML标签
```js
//用原来的文本内容替换了容器元素中的所有内容
div.innerText = div.innerText
```
Firefox不支持这个属性，但是有个类似的属性`textContent`
兼容模式：
```js
function getInnerText(element){
    return (typeof element.textContent == "string") ? 
        element.textContent : element.innerText;
}

function setInnerText(element, text){
    if (typeof element.textContent == "string"){
        element.textContent = text;
    } else {
        element.innerText = text;
    }
}
```
innerText返回会忽略脚本和样式代码，textContent**不会**，所以最好从不包含这些代码。

#### 11.4.4.2 outerText属性
区别：包含自身节点

### 11.4.5 滚动
`scrollIntoView`是所有浏览器都支持的方法
以下是个别浏览器支持的方法
`scrollIntoViewIfNeeded(alignCenter)`当前元素在当前视窗不可见的情况下，滚动让它可见
`scrollByLines(lineCount)` 将元素的内容滚到指定的行高
`scrollByPages(pageCount)` 将元素的内容滚动指定的页面高度

# 12 DOM2和DOM3
## 12.1 DOM变化
检查浏览器是否支持
```js
var supportsDOM2Core = document.implementation.hasFeature("Core","2.0");
var supportsDOM3Core = document.implementation.hasFeature("Core","3.0");
var supportsDOM2HTML = document.implementation.hasFeature("HTML","2.0");
var supportsDOM2Views = document.implementation.hasFeature("Views","2.0");
var supportsDOM2XML = document.implementation.hasFeature("XML","2.0");
```
### 12.1.1 针对XML命名空间的变化
XML不做讨论

### 12.1.2 其他方面的变化
#### 12.1.2.1 DocumentType类型的变化
新增3个属性
`publicId`
`systemId`
`internalSubset`
```js
<!DOCTYPE HTML PUBLIC "-//W3C//DTD HTML 4.01//EN" "http://w3.org/TR/html4/strict.dtd" [<!ELEMENT name (#PCDATA)>]>
```
访问通过
```js
document.doctype.publicId;  //"-//W3C//DTD HTML 4.01//EN"
document.doctype.systemId;  //"http://w3.org/TR/html4/strict.dtd"
document.doctype.internalSubset;  //[<!ELEMENT name (#PCDATA)>]

```

#### 12.1.2.2 Document 类型的变化
`importNode()`从一个文档中**取得一个节点**，然后将其导入到另一个文档，使其成为这个文档结构的一部分。
与Elementde cloneNode()方法非常相似
接受两个参数：要复制的节点+是否复制子节点的布尔值
```js
var newNode = document.importNode(oldNode,true);//导入节点及其所有子节点
document.body.appendChild(newNode);
```
`defaultView`保存着一个指针，指向拥有给定文档的窗口。
```js
//确定文档的归属窗口--兼容IE
var parentWindow = document.defaultView || document.parentWindow;  //后边为IE
```
为`document.implementation`新增两个方法
`createDocumentType()`创建一个新的DocumentType节点，接收三个参数：文档类型名称(html)+publicId+systemId
`createDocument()` 创建新文档时用，接收三个参数：针对文档中元素的namespaceURI+文档元素的标签名+新文档的文档类型
```js
//创建一个XHTML文档
var doctype = document.implementation.createDocumentType("html",
    "-//W3C//DTD XHTML 1.0 Strict//EN",
    "http://www.w3.org/TR/xhtml1/DTD/xhtmll-strict.dtd");
    
var doc = document.implementation.createDocument("http://www.w3.org/1999/xhtml",
    "html",doctype);
```
`createHTMLDocument`创建一个完整的HTML文档，包括html/head/title/body
他是HTMLDocument类型的实例，所以具有该类型的所有属性和方法，包括title和body方法
只接受一个参数，即新创建文档的标题
```js
var htmldoc = document.implementation.createHTMLDocument("New Doc");
alert(htmldoc.title);   //New Doc
alert(typeof htmldoc.body);  //object
```
#### 12.1.2.3 Node类型的变化
`isSupported()`确定当前结点具有什么能能力，和hasFeature类似
```js
if(document.body.isSupported("HTML","2.0")){
    //执行操作
}
```
建议使用能力检测，而不用这个
辅助比较节点方法：
`isSameNode()`  相同
`isEqualNode()` 相等
传入节点与引用的节点相同或相等时返回true。
相同：两个节点引用的是同一个对象
相等：两个节点是相同的类型，且具有相等的属性（nodeName/nodeValue/attributes/childNodes）

`setUserData()`添加额外数据
`getUserData()`读取额外数据
三个参数:要设置的键+实际的数据+处理函数
```js
//设置
document.body.setUserData("name","Nicholas",function(){})
//读取
var data = document.body.getUserData("name")
```
处理函数接收5个参数：
operation操作类型的数值（1.复制 2.导入 3.删除 4.重命名）
key数据键
value数据值
src源节点
dest目标节点
```js
var div = document.createElement("div");
div.setUserData("name", "Nicholas", function(operation, key, value, src, dest){
    if (operation == 1){
        dest.setUserData(key, value, function(){});
    }
});

var newDiv = div.cloneNode(true);
alert(newDiv.getUserData("name"));    //"Nicholas"
```
#### 12.1.2.4 框架的变化
`HTMLFrameElement` 框架
`HTMLIFrameElement` 内嵌框架
他们的新属性`contentDocument`,包含一个指针，指向表示框架内容的**文档对象**
```js
var iframe = document.getElementById("myIframe");
var iframeDoc = iframe.contentDocument || iframe.contentWindow.document;   //后边为了兼容IE8
alert(iframeDoc);
```
所有浏览器都支持`contentWindow`属性

## 12.2 样式
### 12.2.1 访问元素的样式
`style`属性，这个对象是`CSSStyleDeclaration`的实例
**短划线的属性名必须用驼峰大小写形式**，例如background-image
**特殊**
`cssFloat`表示浮动，因为float是js保留字
设置和获取都是一样的用法

#### 12.2.1.1 DOM样式属性和方法
style定义了一些属性和方法
`cssText` 访问style特性的CSS代码--某个元素的所有样式，方便重写
`length` 应用元素的CSS属性的数量 --和item()配合使用
`parentRule` CSS信息的CSSRule对象
`getPropertyCSSvalue(propertyName)` 返回包含给定属性值的CSSValue对象--获取cssText所有属性的值，cssValueType属性则是一个数值常量（0:继承的值 1:基本的值 2:值列表 3:自定义的值）
`getPropertyPriority(propertyName)` 如果给定的属性使用了!important则返回"important",否则返回空字符
`getPropertyValue(propertyName)` 给定属性的字符串值--获取item(i)的值
`item(index)` 给定位置的CSS属性的名称
`removeProperty(propertyName)` 从样式中删除给定的属性---删除给定的属性
`setProperty(propertyName,value,priority)` 将给定属性设置为相应的值，并加上优先权标识(important或者一个空字符串)

```js
function changeStyles(){
    var myDiv = document.getElementById("myDiv");
    
    //set the background color
    myDiv.style.setProperty("background-color", "red", "");;
    
    //change the dimensions
    myDiv.style.setProperty("width", "100px", "");
    myDiv.style.setProperty("height", "200px", "");
    
    //assign a border
    myDiv.style.setProperty("border", "1px solid black", "");
}

function getStyles(){
    var myDiv = document.getElementById("myDiv");
    alert(myDiv.style.getPropertyValue("background-color"));
    alert(myDiv.style.getPropertyValue("width"));
    alert(myDiv.style.getPropertyValue("height"));
}

function getCSS(){
    var myDiv = document.getElementById("myDiv");
    alert(myDiv.style.cssText);
}

function changeCSS(){
    var myDiv = document.getElementById("myDiv");
    myDiv.style.cssText ="width: 25px; height: 100px; background-color: green";
}

function enumerateCSS(){
    var myDiv = document.getElementById("myDiv");
    var props = new Array();
    for (var i=0, len=myDiv.style.length; i < len; i++){
        var prop = myDiv.style[i];     //or myDiv.style.item(i)
        var value = myDiv.style.getPropertyValue(prop);
        props.push(prop + " : " + value); 
    }
    alert(props.join("\n"));

}

function enumerateCSSValues(){
    var myDiv = document.getElementById("myDiv");
    var props = new Array();
    for (var i=0, len=myDiv.style.length; i < len; i++){
        var prop = myDiv.style[i];     //or myDiv.style.item(i)
        var value = myDiv.style.getPropertyCSSValue(prop);
        props.push(prop + " : " + value.cssText + " (" + value.cssValueType + ")"); 
    }
    alert(props.join("\n"));

}

function removeBorder(){
    var myDiv = document.getElementById("myDiv");
    myDiv.style.removeProperty("border");
}
```

#### 12.2.1.2 计算的样式
style样式**不包括**那些从其他央视表层叠而来并影响到当前元素的样式信息
DOM2增强了`document.defaultView`提供了`getComputedStyle()`方法
`getComputedStyle()`返回一个CSSStyleDeclaration对象，包含了所有计算的样式
接收两个参数：最终显示属性的元素+伪元素字符串（不需要的话为null）
```js
var myDiv = document.getElementById("myDiv");
var computedStyle = document.defaultView.getComputedStyle(myDiv, null);
alert(computedStyle.backgroundColor);   //"red"
alert(computedStyle.width);             //"100px"
```

IE没有这个方法，但是有个代替方法`currentStyle`
```js
var myDiv = document.getElementById("myDiv");
var computedStyle = myDiv.currentStyle;
alert(computedStyle.backgroundColor);   //"red"
alert(computedStyle.width);             //"100px"
```

### 12.2.2 操作样式表
`CSSStyleSheet`类型表示的是样式表
接口属性：
`disabled` 是否被禁用的布尔值，true为禁用样式表
`href` 如果样式表通过link包含的，则为样式表的URL，否则为null
`media`支持所有媒体类型的集合，为空表示适用于所有媒体
`ownerNode` 指向当前样式表的节点的指针，可能是通过link、style引入的，@important引入的属性值为null
`parentStyleSheet` 当前样式表通过important引入的，这个属性是一个指向导入它的样式表的指针
`title` ownerNode中title属性的值
`type` 样式表类型的字符串，CSS样式表的字符串为"type/css"
`cssRules` 样式表中包含的样式规则的集合
`ownerRule` 如果通过@import导入的，则为一个指针，指向表示导入的规则，否则值为null
`deleteRule(index)` 删除cssRules集合中指定位置的规则
`insertRule(rule,index)` 想cssRules集合中指定的位置插入rule字符串
所有样式表都是通过`document.styleSheets`集合来表示的,（在html里的样式标签集合）
同样通过`item()`或者`[]`来查询
```js
function outputStyleSheets(){
    var sheet = null;
    for (var i=0, len=document.styleSheets.length; i < len; i++){
        sheet = document.styleSheets[i];
        alert(sheet.href);
    }
}

function toggleStyleSheet(){
    document.styleSheets[0].disabled = !document.styleSheets[0].disabled;
}
```
IE没有这个属性，有个类似叫`sheet`
```js
//兼容模式
function getStyleSheet(element){
    return element.sheet || element.styleSheet;   //我觉得这个不太对，没有styleSheet，但是前边对的，后边我改写为document.styleSheet[0]
}


function outputStyleSheet(){            
    //get the style sheet for the first <link/> element
    var link = document.getElementsByTagName("link")[0];
    var sheet = getStyleSheet(link);
    alert(sheet.href);
}
```
#### 12.2.2.1 CSS规则
CSSRule对象表示样式表中的每一条规则。
它是供其他多种类型继承的基类，最常见的有`CSSStyleRule`类型
CSSStyleRule对象包含下列属性
`cssText` 返回整条规则对应的文本
`parentRule` 如果当前规则是导入的规则，这个属性引用的就是导入规则，否则为null
`parentStyleSheet` 当前规则所属的样式表
`selectorText` 返回当前规则的选择符文本
`style`一个CSSStyleDeclaration对象，可以设置或取得规则中特定的样式值
`type` 规则类型的常量值，值为1.
最常用的为cssText、selectorText、style
**cssText与style.cssText区别：前者包含选择符文本和花括号，后者只包含样式信息**
**并且前者是只读的，后者可以被重写**
```js
function getStyleInfo(){
    var sheet = document.styleSheets[0];         //获取样式表
    var rules = sheet.cssRules || sheet.rules;   //兼容IE
    var rule = rules[0];                     //获取样式表第一个样式
    alert(rule.selectorText);                 //"div box"
    alert(rule.style.cssText);                //完整的css代码，不含{}
    alert(rule.style.backgroundColor);
    alert(rule.style.width);
    alert(rule.style.height);
}

function changeStyleInfo(){        
    var sheet = document.styleSheets[0];
    var rules = sheet.cssRules || sheet.rules;
    var rule = rules[0];    

    rule.style.backgroundColor = "red";
}
```

#### 12.2.2.2 创建规则
`insertRule`向样式表里添加新规则
两个参数：规则文本+在哪里插入的索引
```js
function insertRule(sheet, selectorText, cssText, position){
    if (sheet.insertRule){                     //兼容判断
        sheet.insertRule(selectorText + "{" + cssText + "}", position);  //调用方式
    } else if (sheet.addRule){
        sheet.addRule(selectorText, cssText, position);
    }
}
        
function addNewRule(){        
    var sheet = document.styleSheets[0];
    insertRule(sheet, "body", "background-color: silver;", 0);      //函数调用方式   
    //Note: Opera < 9.5 doesn't add the rule in the correct location     
}
```

#### 12.2.2.3 删除规则
`deleteRule` 删除规则
```js
 function deleteRule(sheet, index){
    if (sheet.deleteRule){
        sheet.deleteRule(index);
    } else if (sheet.removeRule){
        sheet.removeRule(index);
    }
}

function removeFirstRule(){
    var sheet = document.styleSheets[0];
    deleteRule(sheet, 0);           
}
```

### 12.2.3 元素大小
#### 12.2.3.1 偏移量
**可见**空间
`offsetHeight` 包括边框
`offsetWidth` 包括边框
`offsetLeft`
`offsetTop`

`offsetParent`(包含元素的引用保存在这里)和`parentNode`的值不一定相等
![](/images/offset.png)
#### 12.2.3.2 客户区大小
`clientHeight`  不包括边框
`clientWidth`   不包括边框
```js
//混杂模式 document.compatMode == "BackCompat"
document.body.clientWidth;
//标准模式
document.documentElement.clientWidth
```
![](/images/client.png)
#### 12.2.3.3 滚动大小
`scrollHeight` 不含滚动条的高
`scrollWidth`
`scrollLeft`  
`scrollTop` 隐藏部分的高
![](/images/scroll.png)
#### 12.2.3.4 确定元素大小
`getBoundingClientRect()`返回一个矩形对象
4个属性：`left` `top` `right` `bottom`
给出的是**相对于视口的位置**
IE8及之前版本认为左上角坐标为(2,2)
```js
element.getBoundingClientRect().left;
```
#### 12.2.3.4 补充
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

![](/images/54586e9b0001838b05000495.jpg)

![](/images/图解.jpg)

jQuery取鼠标高度用

$('body,html').scrollTop();和$(document.body).scrollTop()     火狐不兼容
$(window).scrollTop();       这个火狐和chrome都兼容
例：
```js
$(function(){
  $(window).scroll(function(){
      var offsetTop =$(document.body).scrollTop();  /*$('body,html').scrollTop();也可以*/
      console.log(offsetTop);
  })
})
```
js用：
完美的获取scrollTop 赋值短语 ：
```js
var scrollTop = document.documentElement.scrollTop || window.pageYOffset || document.body.scrollTop;
```
例子：
```js
window.onload = function () {
    window.onscroll = function () {
        var mouseH = document.body.scrollTop;
        console.log(mouseH);
        }
    };
```

先总结下区别：

**event.clientX、event.clientY**

鼠标相对于浏览器窗口可视区域的X，Y坐标（窗口坐标），可视区域不包括工具栏和滚动条。IE事件和标准事件都定义了这2个属性

**event.pageX、event.pageY**

类似于event.clientX、event.clientY，但它们使用的是文档坐标而非窗口坐标。这2个属性不是标准属性，但得到了广泛支持。IE事件中没有这2个属性。

**event.offsetX、event.offsetY**

鼠标相对于事件源元素（srcElement）的X,Y坐标，只有IE事件有这2个属性，标准事件没有对应的属性。

**event.screenX、event.screenY**

鼠标相对于用户显示器屏幕左上角的X,Y坐标。标准事件和IE事件都定义了这2个属性

上图！！！！
![](/images/2014091409260873.png)


## 12.3 遍历
### 12.3.1 NodeIterator
`document.createNodeIterator()`方法创建它的新实例。
四个参数：
`root` 搜索起点的节点
`whatToShow` 要访问哪些节点的数字代码
`filter` 一个NodeFilter对象，或者一个应该接收还是拒绝某种特定的函数
`entityReferenceExpansion` 布尔值，是否扩展实体引用。这个参数在HTML页面中没有用，因为其中的实体引用不能扩展

whatToShow参数是一个位掩码，通过一个或多个过滤器来确定要访问哪些节点。
`NodeFilter.SHOW_ALL` 显示所有类型的节点
`NodeFilter.SHOW_ELEMENT`显示元素节点
`NodeFilter.SHOW_ATTRIBUTE`显示特性节点
`NodeFilter.SHOW_TEXT`显示文本节点
`NodeFilter.SHOW_CDATA_SECTION`显示CDATA节点
`NodeFilter.SHOW_ENTITY_REFERENCE`显示实体引用节点
`NodeFilter.SHOW_ENTITYE`显示实体节点
`NodeFilter.SHOW_PROCESSING_INSTRUCTION`显示处理指令节点
`NodeFilter.SHOW_COMMENT`显示注释节点
`NodeFilter.SHOW_DOCUMENT`显示文档节点
`NodeFilter.SHOW_DOCUMENT_TYPE`显示文档类型节点
`NodeFilter.SHOW_DOCUMENT_FRAGMENT`显示文档片段节点
`NodeFilter.SHOW_NOTATION`显示符号节点

通过filter来指定自定义的NodeFilter对象。
每个NodeFilter对象只有一个方法，即acceptNode();
应该访问给定的节点，返回`NodeFilter.FILTER_ACCEPT`
如果不应该访问，则返回`NodeFilter.FILTER_SKIP`

NodeIterator类型的两个主要方法
`nextNode()`向子节点方向前进
`previousNode()`向根节点方向前进

```js
<head>
    <title>NodeIterator Example</title>
    <script type="text/javascript">

       function makeList() {
            var div = document.getElementById("div1");
            var filter = function(node){                 //过滤器
                return (node.tagName.toLowerCase() == "li") ? 
                    NodeFilter.FILTER_ACCEPT :       
                    NodeFilter.FILTER_SKIP;
            };

            var iterator = document.createNodeIterator(div, NodeFilter.SHOW_ELEMENT, filter, false);    //遍历所有div元素+显示元素节点+过滤器（li元素）+不扩张实体
            //For Firefox: iterator = document.createTreeWalker(div, NodeFilter.SHOW_ELEMENT, filter, false);
           
            var output = document.getElementById("text1");
            var node = iterator.nextNode();     //开始遍历符合上边规则的节点
            while (node !== null) {             //当当前遍历的节点不是最后一个节点的时候
                output.value += node.tagName + "\n";
                node = iterator.nextNode();
            }

       }

    </script>
</head>
<body>
    <p><strong>Note:</strong> The <code>NodeIterator</code> object has only been implemented in Internet Explorer 9, Chrome, Firefox (version 3.5 and higher), Opera (version 7.6 and higher) and Safari (version 1.3 and higher). It has not been implemented in Internet Explorer or Firefox (so this example won't work).</p>
    <div id="div1">
        <p><b>Hello</b> world!</p>
        <ul>
            <li>List item 1</li>
            <li>List item 2</li>
            <li>List item 3</li>
        </ul>
    </div>
    <textarea rows="10" cols="40" id="text1"></textarea><br />
    <input type="button" value="Make List" onclick="makeList()" />
</body>
```

### 12.3.2 TreeWalker
更高级版
`document.createTreeWalker()`创建TreeWalker对象
除了`nextNode()`和`previousNode()`以外
`parentNode()`遍历当前节点的父节点
`firstChild()`遍历当前节点的第一个子节点
`lastChild()`遍历当前节点的最后一个子节点
`nextSibling()`遍历当前节点的下一个同辈节点
`previousSibling`遍历当前节点的的上一个同辈节点

TreeWalker的`NodeFilter.FILTER_SKIP`和`NodeFilter.FILTER_REJECT`的区别是：
前者会跳过相应节点继续前进到子树中的下一个节点
后者会跳过相应节点及该节点的**整个子树**
```js
<head>
    <title>TreeWalker Example</title>
    <script type="text/javascript">

       function makeList() {
           var div = document.getElementById("div1");
           var walker = document.createTreeWalker(div, NodeFilter.SHOW_ELEMENT, null, false);

           var output = document.getElementById("text1");
           
           walker.firstChild();   //go to <p>
           walker.nextSibling();  //go to <ul>
           var node = walker.firstChild();  //go to <li>
           while (node !== null) {
               output.value += node.tagName + "\n";                   
               node = walker.nextSibling();
           }

       }

    </script>
</head>
<body>
    <p><strong>Note:</strong> The <code>TreeWalker</code> object has only been implemented in Internet Explorer 9, Chrome, Opera (version 7.6 and higher), Safari (version 1.3 and higher), and Firefox (version 1.0 and higher). It has not been implemented in Internet Explorer 8 or earlier (so this example won't work).</p>

    <div id="div1">
        <p>Hello <b>World!</b></p>
        <ul>
            <li>List item 1</li>
            <li>List item 2</li>
            <li>List item 3</li>
        </ul>
    </div>
    <textarea rows="10" cols="40" id="text1"></textarea><br />
    <input type="button" value="Make List" onclick="makeList()" />
</body>
```
TreeWalker还有一个属性，叫`currentNode`,表示任何遍历方法在上一次遍历中返回的节点。
通常用来**修改遍历起点**
```js
walker.currentNode == document.body
```
## 12.4 范围
### 12.4.1 DOM中的范围
`createRange()`方法属于document对象。
创建DOM范围
```js
var range = document.createRange();
```
每个范围都是Range的实例，实例的属性有
`startContainer`包含范围起点的节点（第一个节点的父节点）
`startOffset`起点的偏移量
`endContainer`最后一个节点的父节点
`endOffset`终点的偏移量
`commonAncestorContainer`startContainer和endContainer共同的祖先节点在文档树中位置最深的那个

#### 12.4.1.1 用DOM范围实现简单选择
使用范围来选择文档中的一部分，最简单的方式就是使用`selectNode()`或`selectNodeContents`
`selectNode()`选择整个节点-包括父节点
`selectNodeContents`只选择子节点
```js
var range1 = document.createRange();
var range2 = document.createRange();
var p1 = document.getElementById("p1");
range1.selectNode(p1);
range2.selectNodeContents(p1);
```
![](/images/range1.png)
为了更精细的控制哪些节点包含在范围中，还有以下方法
`setStartBefore(refNode)`将范围起点设置在refNode之前。
`setStartAfter(refNode)`将范围起点设置在refNode之后。
`setEndBefore(refNode)`将范围终点设置在refNode之前。
`setEndAfter(refNode)`将范围终点设置在refNode之后。

#### 12.4.1.2 用DOM范围实现复杂选择
创建复杂的范围就得使用`setStart()`和`setEnd()`方法。
参数：参照节点+偏移量值
`setStart()`的参照节点会变成startContainer，而偏移量会变成startOffset
`setEnd()`的参照节点会变成endContainer，而偏移量会变成endOffset
```js
//模仿selectNode()和selectNodeContents()
var range1 = document.createRange(),
    range2 = document.createRange(),
    p1 = document.getElementById("p1"),                
    p1Index = -1,
    i, len;
    
for (i=0, len=p1.parentNode.childNodes.length; i < len; i++) {
    if (p1.parentNode.childNodes[i] == p1) {
        p1Index = i;
        break;
    }
}
        
range1.setStart(p1.parentNode, p1Index);
range1.setEnd(p1.parentNode, p1Index + 1);
range2.setStart(p1, 0);
range2.setEnd(p1, p1.childNodes.length);
```
取从hello的llo到world的o
```js
var p1 = document.getElementById("p1"),
    helloNode = p1.firstChild.firstChild,
    worldNode = p1.lastChild,
    range = document.createRange();

range.setStart(helloNode, 2);    //这里操作偏移量来选择
range.setEnd(worldNode, 3);      //这里操作偏移量来选择
```

#### 12.4.1.3操作DOM范围中的内容
`deleteContents()`从文档中删除范围所包含的内容
```js
var p1 = document.getElementById("p1"),
    helloNode = p1.firstChild.firstChild,
    worldNode = p1.lastChild,
    range = document.createRange();    //要先创建范围


range.setStart(helloNode, 2);
range.setEnd(worldNode, 3);
range.deleteContents();
```
`extractContents()`同样是移除范围选区，区别是这个方法**返回范围的文档片段**
利用这个可以将范围的内容插入到文档中的其他地方
```js
var p1 = document.getElementById("p1"),
    helloNode = p1.firstChild.firstChild,
    worldNode = p1.lastChild,
    range = document.createRange();

range.setStart(helloNode, 2);
range.setEnd(worldNode, 3);
var fragment = range.extractContents();
p1.parentNode.appendChild(fragment);
```
`cloneContents()`创建范围对象的一个副本
```js
var p1 = document.getElementById("p1"),
    helloNode = p1.firstChild.firstChild,
    worldNode = p1.lastChild,
    range = document.createRange();


range.setStart(helloNode, 2);
range.setEnd(worldNode, 3);
var fragment = range.cloneContents();
p1.parentNode.appendChild(fragment);
```
#### 12.4.1.4 插入DOM范围中的内容
`insertNode()`向范围选区的开始处插入一个节点。
```js
var p1 = document.getElementById("p1"),
    helloNode = p1.firstChild.firstChild,
    worldNode = p1.lastChild,
    range = document.createRange(),
    span = document.createElement("span");
    
span.style.color = "red";
span.appendChild(document.createTextNode("Inserted text"));

range.setStart(helloNode, 2);
range.setEnd(worldNode, 3);
range.insertNode(span);
```
`surroundContents()`环绕范围插入内容
```js
var p1 = document.getElementById("p1"),
    helloNode = p1.firstChild.firstChild,
    worldNode = p1.lastChild,
    range = document.createRange();

range.selectNode(helloNode);    //就这有点区别，其他没看出来

var span = document.createElement("span");
span.style.backgroundColor = "yellow";
range.surroundContents(span);
```
#### 12.4.1.5 折叠DOM范围
折叠范围，就是指范围中未选择文档的任何部分。
`collapse()`方法来折叠范围。
接收一个布尔值做参数，表示折叠的范围是哪一端。
true为起点，false为终点。
两个节点之间**没有节点**就说明这两个节点折叠的
![](/images/zhedie.png)
#### 12.4.1.6 比较DOM的范围
`compareBoundaryPoints()`方法来确定这些范围是否有公共的起点和终点
参数：比较方式的常量值+比较的范围
比较方式常量值有：
`Range.START_TO_START(0)`比较第一个范围和第二个范围的起点；
`Range.START_TO_END(1)`1起点2终点
`Range.END_TO_END(2)`1和2的终点
`Range.END_TO_START(3)`1终点2起点
```js
var range1 = document.createRange(),
    range2 = document.createRange(),
    p1 = document.getElementById("p1");

range1.selectNodeContents(p1);
range2.selectNodeContents(p1);
range2.setEndBefore(p1.lastChild);

alert(range1.compareBoundaryPoints(Range.START_TO_START, range2));  //outputs 0  相同
alert(range1.compareBoundaryPoints(Range.END_TO_END, range2));      //outputs 1  不同
```
#### 12.4.1.7 赋值DOM范围
`cloneRange()`
```js
var newRange = range.cloneRange();
```

#### 12.4.1.8 清理DOM范围
使用完范围最好清理一下！！
`detach()`从创建范围的文档中分离出该范围
```js
range.detach();  //从文档中分离
range = null;    //解除引用
```
### 12.4.2 IE8及更早版本中的范围
不再讨论老版本范围，如需要请看P340
# 13.事件
### 13.1 事件流
### 13.1.1 事件冒泡
IE的事件流叫做事件冒泡，即嵌套层最深的那个节点接收，向上传播
![](/images/maopao.png)

### 13.1.2 事件捕获
沿DOM树依次向下
![](/images/buhuo.png)

### 13.1.3 DOM事件流
三个阶段：**事件捕获阶段，处于目标阶段，事件冒泡阶段**
![](/images/sanjieduan.png)

## 13.2 事件处理程序
### 13.2.1 HTML事件处理程序
写在html中的事件，需要添加转义字符，单引号不需要转义
缺点：
需要改动两个地方（耦合度高）
在没加载完底部js就点击按钮，会报错

### 13.2.2 DOM0级事件处理程序
```js
var btn = document.getElementById("myBtn");
btn.onclick = function(){    //DOM0的方式
alert(this.id); //"myBtn"
};
```
**删除事件**
```js
btn.onclick = null;    //★
```

### 13.2.3 DOM2级事件处理
`addEventListener()`  监听事件
`removeEventListener()`   移除监听事件
3个参数：事件名+事件函数+布尔值true(捕获)false(冒泡)
优势：**添加多个事件**
缺点：无法移除匿名函数事件，解决方法：匿名函数在外边定义一下变成函数表达式
```js
var btn = document.getElementById("myBtn");
var handler = function(){             //这里是重点，定义了一个函数名
alert(this.id);                //DOM0的this指向当前元素
};
btn.addEventListener("click", handler, false);
//这里省略了其他代码
btn.removeEventListener("click", handler, false); //有效！
```
### 13.2.4 IE事件处理程序
`attachEvent()`
`detachEvent()`
2个参数：事件名+事件函数
**默认为冒泡**
*DOM0级方法事件处理程序在其所属元素的作用域内运行，DOM2方法会在全局作用域中运行*，因此this指向window。
```js
var btn = document.getElementById("myBtn");
btn.attachEvent("onclick", function(){
alert(this === window);     //true    DOM2的this指向window
});
```
添加多个事件的时候，执行顺序为**后添加的先执行**

### 13.2.5 跨浏览器的事件处理程序
```js
var EventUtil = {
    addHandler: function(element, type, handler){
        if (element.addEventListener){
            element.addEventListener(type, handler, false);
        } else if (element.attachEvent){
            element.attachEvent("on" + type, handler);
        } else {
            element["on" + type] = handler;
        }
    },
    removeHandler: function(element, type, handler){
        if (element.removeEventListener){
            element.removeEventListener(type, handler, false);
        } else if (element.detachEvent){
            element.detachEvent("on" + type, handler);
        } else {
            element["on" + type] = null;    //DOM0移除事件方法
        }
    }
};
//使用
EventUtil.addHandler(btn, "click", handler);
//这里省略了其他代码
EventUtil.removeHandler(btn, "click", handler);
```
## 13.3 事件对象
`event`触发DOM上的某个事件时，就会产生这个对象

### 13.3.1 DOM中的事件对象
`event.type` 查看事件类型
属性和方法
`bubbles` Boolean 只读表明事件是否冒泡
`cancelable` Boolean 只读表明是否可以取消事件的默认行为
`currentTarget` Element 只读其事件处理程序当前正在处理事件的那个元素
`defaultPrevented` Boolean 只读为 true 表示已经调用了preventDefault()（DOM3级事件中新增）
`detail` Integer 只读与事件相关的细节信息
`eventPhase` Integer 只读调用事件处理程序的阶段：1表示捕获阶段，2表示“处于目标”，3表示冒泡阶段
`preventDefault()` Function 只读取 消 事件的默认行为。如果cancelable是true，则可以使用这个方法
`stopImmediatePropagation()` Function 只读取消事件的进一步捕获或冒泡，同时阻止任何事件处理程序被调用（DOM3级事件中新增）
`stopPropagation()` Function 只读取消事件的进一步捕获或冒泡。如果bubbles为true，则可以使用这个方法
`target Element` 只读事件的目标
`trusted` Boolean 只读为true表示事件是浏览器生成的。为false表示事件是由开发人员通过JavaScript 创建的（DOM3级事件中新增）
`type` String 只读被触发的事件的类型
`view` AbstractView 只读 与事件关联的抽象视图。等同于发生事件的window对象

事件处理程序内部，`this`始终等于`currentTarget`(事件处理程序当前正在处理事件的那个元素)的值，而target则**只包含事件的实际目标**
```js
document.body.onclick = function(event){
    alert(event.currentTarget === document.body); //true  父节点
    alert(this === document.body); //true
    alert(event.target === document.getElementById("myBtn")); //true
};
```
处理多个事件可以通过`event.type`
```js
var btn = document.getElementById("myBtn");
var handler = function(event){
    switch(event.type){          //根据事件类型来选择操作
        case "click":
            alert("Clicked");
            break;
            
        case "mouseover":
            event.target.style.backgroundColor = "red";
            break;
            
        case "mouseout":
            event.target.style.backgroundColor = "";
            break;                        
    }
};

btn.onclick = handler;
btn.onmouseover = handler;
btn.onmouseout = handler;
```
**阻止默认行为**：`event.preventDefault()`
*注意：*只有`cancelable`属性设置为true时，才能使用这个方法
**阻止捕获/冒泡**：`event.stopPropagation()`
`eventPhase`确定时间正在处于**哪个阶段**
捕获：1，目标：2，冒泡：3
*注意：*尽管"处于目标"发生在冒泡阶段，但是eventPhase仍然一直等于2
```js
var btn = document.getElementById("myBtn");
btn.onclick = function(event){    //按钮上已经到了处于目标了
    alert(event.eventPhase);   //2
};

document.body.addEventListener("click", function(event){
    alert(event.eventPhase);   //1  捕获从body开始
}, true);

document.body.onclick = function(event){
    alert(event.eventPhase);   //3   冒泡阶段
};
```

### 13.3.2 IE中的事件对象
event对象作为window对象的一个属性存在
`event = window.event`
属性方法：
`cancelBubble` Boolean 读/写默认值为false，但将其设置为true就可以取消事件冒泡（与DOM中的stopPropagation()方法的作用相同）
`returnValue` Boolean 读/写默认值为true，但将其设置为false就可以取消事件的默认行为（与DOM中的preventDefault()方法的作用相同）
`srcElement` Element 只读事件的目标（与DOM中的target属性相同）
`type` String 只读被触发的事件的类型

`window.event.srcElement`和DOM的`event.target`效果相同
`returnValue`设置为`false`的话和DOM的`preventDefault()`方法相同
`cancelBubble`设置为`true`阻止冒泡，但是DOM的`stopPropagatioin`即可以阻止冒泡又可以阻止捕获

### 13.3.3 跨浏览器的事件对象
```js
var EventUtil = {
    addHandler: function (element, type, handler) {
//省略的代码
    },
    getEvent: function (event) {          //兼容event
        return event ? event : window.event;
    },
    getTarget: function (event) {          //兼容event.target
        return event.target || event.srcElement;
    },
    preventDefault: function (event) {       //兼容preventDefault()
        if (event.preventDefault) {
            event.preventDefault();
        } else {
            event.returnValue = false;
        }
    },
    removeHandler: function (element, type, handler) {
//省略的代码
    },
    stopPropagation: function (event) {    //兼容stopPropagation()
        if (event.stopPropagation) {
            event.stopPropagation();
        } else {
            event.cancelBubble = true;
        }
    }
};
```

## 13.4 事件类型
### 13.4.1 UI事件
不一定与用户操作有关的事件
`DOMActivate`元素已经被用户激活---被废弃，不建议使用
`load`当页面完全加载后再window上面触发
`unload`当页面完全卸载后在window上触发
`abort`用户停止下载过程时，如果嵌入的内容没有加载完，则在`<object>`元素上面触发
`error`当发生js错误时，在window上面触发
`select`选中1或多个字符时触发
`resize`当窗口或框架的大小变化是window上触发
`scroll`当用户滚动带滚动条的元素中的内容时，在该元素上面触发
除了DOMActivate都为HTML事件

### 13.4.1.1 load事件
当页面完全加载后**(包括所有图片，js，css等外部资源)**就会触发window上面的load事件
event.target 指向document
规范是在document上触发load，但是所有浏览器都在window上实现了该事件，确保向后兼容
*注意：*新图像元素**不一定要添加到文档后**才开始下载，**只要设置了src属性就会开始下载**。
但是`<script>` `<link>`的src和href必须**插入页面后**，才开始下载
创建图像有两种方法：
```js
//方法一
var image = document.createElement("img");
//方法二--有的浏览器并非会把Image对象实现为<img>元素
var image = new Image();
```
**通过load**可以验证已经加载完

#### 13.4.1.2 unload事件
从一个页面切换到另一个页面就会发生unload事件
和load事件用法相同

#### 13.4.1.3 resize事件
当浏览器窗口的大小被调整的时候，触发
与发生在window上的事件类似，target属性对象document

#### 13.4.1.4 scroll事件
也是在window上发生的，可以通过body元素的scrollLeft和scrollTop来监控这个变化

### 13.4.2 焦点事件
`blur` 在元素失去焦点时触发。不会冒泡
`focus`在元素获得焦点时触发。不会冒泡
`focusin`在元素获得焦点时触发，会冒泡
`focusout`在元素失去焦点时触发，会冒泡
`DOMFocusIn`在元素获得焦点时触发，与focus等价，但它会冒泡--DOM3废弃
`DOMFocusOut`在元素失去焦点时触发--DOM3废弃
focus和blur不冒泡，也可以在**捕获阶段**监听到他们

### 13.4.3 鼠标与滚轮事件
`click`  单击鼠标主键/回车
`dblclick` 双击鼠标主键
`mousedown` 按下任意鼠标键触发
`mouseenter` 移入元素范围触发
`mousemove` 范围内移动触发
`mouseleave` 移除元素范围触发

`mouseout` 同移出，但是它移到子元素也算移除
`mouseover` 首次移入触发
`mouseup` 按钮抬起时触发
除了mouseenter和mouseleave，所有鼠标事件**都会冒泡**，也可以取消
相继触发mousedown和mouseup事件，才会触发click事件；其中一个被取消就不会触发！
顺序：mousedown-mouseup-click-mousedown-mouseup-click-dblclick
IE8:mousedown-mouseup-click-无-mouseup-click-dblclick

#### 13.4.3.1 客户区坐标位置
浏览器视口位置信息保存在`clientX` `clientY`属性中
```js
var x = event.clientX;
var y = event.clientY;
```
#### 13.4.3.2 页面坐标位置
页面（文档）坐标位置信息保存在`pageX` `pageY`属性中
没有滚动的情况与client的值相等
#### 13.4.3.3 屏幕坐标位置
整个电脑屏幕的位置保存在`screenX` `screenY`属性中
![](/images/screen.png)

#### 13.4.3.4 修改键
Shift、Ctrl、Alt、Meta
DOM规定了4个属性，表示这些修改键的状态
`shiftKey` `ctrlKey` `altKey` `metaKey`包含的是布尔值
被按下值为true，否则为false
**下边为当按下某键+鼠标点击的时候触发**
```js
var div = document.getElementById("myDiv");
EventUtil.addHandler(div, "click", function(event){
    event = EventUtil.getEvent(event);
    var keys = new Array();

    if (event.shiftKey){
        keys.push("shift");
    }

    if (event.ctrlKey){
        keys.push("ctrl");
    }

    if (event.altKey){
        keys.push("alt");
    }

    if (event.metaKey){
        keys.push("meta");
    }

    alert("Keys: " + keys.join(","));

}); 
```
#### 13.4.3.5 相关元素
mouseover主要目标：获得光标的元素 相关元素：失去光标的元素
mouseout主要目标：失去光标的元素  相关元素：获得光标的元素
`event.relatedTarget`获得**相关元素的信息**，这个属性只对mouseover和mouseout事件才有值，其他事件值为null。
`toElement` IE专用同上
```js
var EventUtil = {
//省略了其他代码
    getRelatedTarget: function(event){
        if (event.relatedTarget){
            return event.relatedTarget;
        } else if (event.toElement){
            return event.toElement;
        } else if (event.fromElement){
            return event.fromElement;
        } else {
            return null;
        }
    },
//省略了其他代码
};
```

#### 13.4.3.6 鼠标按钮
对于`mousedown`和`mouseup`事件,其event对象存在一个button属性，表示按下或释放按钮。
button属性为0：鼠标主按钮 1：鼠标中间按钮 2：鼠标副按钮
IE8存在很多属性，下边做的兼容模式
```js
var EventUtil = {
//省略了其他代码
    getButton: function(event){
        if (document.implementation.hasFeature("MouseEvents", "2.0")){
            return event.button;
        } else {
            switch(event.button){
                case 0:
                case 1:
                case 3:
                case 5:
                case 7:
                    return 0;
                case 2:
                case 6:
                    return 2;
                case 4:
                    return 1;
            }
        }
    },
//省略了其他代码
};
```
可以通过上边的代码**得知是按下了哪个按钮**

#### 13.4.3.7 更多事件信息
`event.detail`属性，DOM2级给出有关事件的更多信息
对于鼠标事件，这个表示发生了多少次**单击**
这个属性从1开始计数
mousedown和mouseup各一次计数1次，如果这两个动作之间**移动**，重置为**0**

#### 13.4.3.8 鼠标滚轮事件
IE：`mousewheel`事件，冒泡到顶层为document/window
`event.wheelDelta`这个属性，当滚动滚轮时候，是**120**的倍数
![](/images/wheeldelta.png)
Firefox:`DOMMouseScroll`事件。会冒泡到window
`event.detail`这个属性，当滚动滚轮时候，是**3**的倍数
![](/images/detail.png)
兼容模式
```js
var EventUtil = {
//省略了其他代码
    getWheelDelta: function(event){
        if (event.wheelDelta){
            return (client.engine.opera && client.engine.opera < 9.5 ?
                -event.wheelDelta : event.wheelDelta);
        } else {
            return -event.detail * 40;
        }
    },
//省略了其他代码
};
```

#### 13.4.3.9 触摸设备
注意：
1.不支持dblclick事件，双击是放大
2.轻击会触发mousemove，如果有变化，将不再发生其他事件，如果没有变化，一次触发mousedown-mouseup-click。
3.mousemove事件也会触发mouseover和mouseout事件
4.两个手指放在屏幕上且页面随手指滚动的会触发mousewheel和scroll事件

#### 13.4.3.10 无障碍性问题
不建议使用click之外的其他鼠标事件！！！
1.屏幕阅读器中，无法触发mousedown事件，所以不要用这个
2.不要使用onmouseover，同样无法触发这个事件
3.不要使用dblclick,同样无法触发这个事件

### 13.4.4 键盘与文本事件
3个键盘事件--一般都是在用户输入的时候才用到
`keydown`按下**任意键**时触发，按住不放，会连续触发
`keypress`按下**字符键**时触发，按住不放，会连续触发
`keyup`释放按键的时候触发

`textInput`唯一的文本事件，其实就是keypress的引申，为了在显示之前拦截文本
按下一个**字符键**的时候执行顺序：
keydown-keypress-keyup
前两个动作在文本**发生变化之前**触发
后一个在文本发生变化后触发

#### 13.4.4.1 键码
发生keydown和keyup事件时，`event.keyCode`获得键码
keyCode属性的值与ASCII码中对应小写字母或数字的编码相同。
具体的keyCode的值查看P380
```js
var textbox = document.getElementById("myText");
EventUtil.addHandler(textbox, "keyup", function(event){
    event = EventUtil.getEvent(event);
    alert(event.keyCode);     
});
```
#### 13.4.4.2 字符编码
`event.charCode`这个属性只有只有在发生keypress事件时才包含值。
值是那个键所代表字符的ASCII编码，此时的keyCode通常等于0或者也可能等于所按键的键码
兼容模式
```js
var EventUtil = {
//省略的代码
    getCharCode: function(event){
        if (typeof event.charCode == "number"){
            return event.charCode;
        } else {
            return event.keyCode;
        }
    },
//省略的代码
};
```

#### 13.4.4.3 DOM3级变化
DOM3不再包含charCode，而包含两个新属性：`key` `char`
`key` 取代keyCode而新增的，它的值是一个字符串，获得的值是**相应的字符**(k)，按下非字符键时，值是相应的键名（Shift）
`char`按下字符的时候和key相同，但是非字符键的时候值为`null`
chrome支持`keyIdentifier`属性
存在严重的跨浏览器问题，所以**不推荐**用key、char、keyIdentifier
DOM3还添加了`location`属性
1：左侧位置 2：右侧位置 3:小键盘 4：移动设备键盘（虚拟键盘） 5：手柄
chrome支持名为`keyLocation`的等价属性
`getModifierState()`方法，指定的修改键是被按下的返回true，否则返回false

#### 13.4.4.4 textInput事件
当用户在**可编辑区域中**输入字符时，就会触发这个事件。
这个属性和keypress区别，后者只有有焦点就触发，但是前者必须可编辑

他有一个`event.data`属性，这个属性值**就是用户输入的字符**
event对象上还有一个属性，`inputMethod`，表示把文本输入到文本框的方式
 0，表示浏览器不确定是怎么输入的。
 1，表示是使用键盘输入的。
 2，表示文本是粘贴进来的。
 3，表示文本是拖放进来的。
 4，表示文本是使用IME 输入的。
 5，表示文本是通过在表单中选择某一项输入的。
 6，表示文本是通过手写输入的（比如使用手写笔）。
 7，表示文本是通过语音输入的。
 8，表示文本是通过几种方法组合输入的。
 9，表示文本是通过脚本输入的。

#### 13.4.4.5 设备中的键盘事件
任天堂的Wii遥控器
都是通过**键码**来操作的

### 13.4.5 复合事件
用于处理IME的输入序列，IME可以让用户输入在物理键盘上找不到的字符
IME通常需要同时按住多个键，但最终只输入一个字符，复合事件就是针对这种输入而设计的。
三种复合事件：
 compositionstart：在IME 的文本复合系统打开时触发，表示要开始输入了。
 compositionupdate：在向输入字段中插入新字符时触发。
 compositionend：在IME 的文本复合系统关闭时触发，表示返回正常键盘输入状态。
比文本事件多一个`data`属性
```js
var textbox = document.getElementById("myText");
if (document.implementation.hasFeature("CompositionEvent", "3.0")){
    EventUtil.addHandler(textbox, "compositionstart", function(event){
        event = EventUtil.getEvent(event);
        alert(event.data);     
    });
    EventUtil.addHandler(textbox, "compositionupdate", function(event){
        event = EventUtil.getEvent(event);
        alert(event.data);     
    });
    EventUtil.addHandler(textbox, "compositionend", function(event){
        event = EventUtil.getEvent(event);
        alert(event.data);     
    });
} else {
    document.write("<p>Your browser does not support composition events.</p>");
}
```

### 13.4.6 变动事件
DOM2级的变动事件能在DOM中某一部分发生变化时给出提示
 DOMSubtreeModified：在DOM 结构中发生任何变化时触发。这个事件在其他任何事件触发后都会触发。
 DOMNodeInserted：在一个节点作为子节点被插入到另一个节点中时触发。
 DOMNodeRemoved：在节点从其父节点中被移除时触发。
 DOMNodeInsertedIntoDocument：在一个节点被直接插入文档或通过子树间接插入文档之后触发。这个事件在DOMNodeInserted 之后触发。
 DOMNodeRemovedFromDocument：在一个节点被直接从文档中移除或通过子树间接从文档中移除之前触发。这个事件在DOMNodeRemoved 之后触发。
 DOMAttrModified：在特性被修改之后触发。
 DOMCharacterDataModified：在文本节点的值发生变化时触发。

#### 13.4.6.1 删除节点
使用removeChild()或replaceChild(),**首先**会触发`DOMNodeRemoved`事件，**会冒泡**
这个事件的目标(event.target)是被删除的节点，而`event.relateNode`属性中包含着目标节点父节点的引用

如果这个节点**包含子节点**，那么在其**所有子节点及这个被移除的节点上**会触发`DOMNodeRemovedFromDocument`事件，但**不会冒泡**
**紧随其后触发**`DOMSubtreeModified`事件，目标是被移除节点的父节点
```js
<! DOCTYPE html>
<html>
<head>
    <title>Node Removal Events Example</title>
</head>
<body>
<ul id="myList">
    <li>Item 1</li>
    <li>Item 2</li>
    <li>Item 3</li>
</ul>
</body>
</html>

```
在这个例子中，我们假设要移除<ul>元素。此时，就会依次触发以下事件。
(1) 在<ul>元素上触发DOMNodeRemoved 事件。relatedNode 属性等于document.body。
(2) 在<ul>元素上触发DOMNodeRemovedFromDocument 事件。
(3) 在身为<ul>元素子节点的每个<li>元素及文本节点上触发DOMNodeRemovedFromDocument
事件。
(4) 在document.body 上触发DOMSubtreeModified 事件，因为<ul>元素是document.body
的直接子元素。

#### 13.4.6.2 插入节点
appendChild()/replaceChild()/inserBefore()向DOM中插入节点时，首先会触发`DOMNodeInserted`事件。
`event.relatedNode`属性中包含一个对父节点的引用（新父节点），**冒泡的**
紧接着会在新插入的节点上触发`DOMNodeInsertedIntoDocument`事件。**不冒泡**
最后触发`DOMSubtreeModified`事件，触发于新插入节点的父节点
```js
EventUtil.addHandler(window, "load", function(event){
    var list = document.getElementById("myList");
    var item = document.createElement("li");
    item.appendChild(document.createTextNode("Item 4"));
    EventUtil.addHandler(document, "DOMSubtreeModified", function(event){
        alert(event.type);
        alert(event.target);
    });
    EventUtil.addHandler(document, "DOMNodeInserted", function(event){
        alert(event.type);
        alert(event.target);
        alert(event.relatedNode);
    });
    EventUtil.addHandler(item, "DOMNodeInsertedIntoDocument", function(event){
        alert(event.type);
        alert(event.target);
    });
    list.appendChild(item);
});
```

### 13.4.7 HTML5事件
#### 13.4.7.1 contextmenu事件
**单击右键调出上下文菜单**
这个时间是**冒泡**
因为它是鼠标事件，所以它包含与光标位置有关的所有属性
通常用contextmenu来**显示**菜单，用onclick来**隐藏**该菜单
```js
<div id="myDiv">Right click or Ctrl+click me to get a custom context menu. Click anywhere else to get the default context menu.</div>
    <ul id="myMenu" style="position:absolute;visibility:hidden;background-color:silver">
        <li><a href="http://www.nczonline.net">Nicholas' site</a></li>
        <li><a href="http://www.wrox.com">Wrox site</a></li>
        <li><a href="http://www.yahoo.com">Yahoo!</a></li>
    </ul>
    <script type="text/javascript">
        EventUtil.addHandler(window, "load", function(event){
            var div = document.getElementById("myDiv");
                        
            EventUtil.addHandler(div, "contextmenu", function(event){
                event = EventUtil.getEvent(event);
                EventUtil.preventDefault(event);
                
                var menu = document.getElementById("myMenu");
                menu.style.left = event.clientX + "px";
                menu.style.top = event.clientY + "px";
                menu.style.visibility = "visible";
            });
            
            EventUtil.addHandler(document, "click", function(event){
                document.getElementById("myMenu").style.visibility = "hidden";
            });
        });

    </script>
```

#### 13.4.7.2 beforeunload事件
目的：在页面卸载前阻止这一操作，弹出对话框，让用户选择
`event.returnVaule`这个值**必须**设置为显示给用户的字符串
```js
EventUtil.addHandler(window, "beforeunload", function(event){
    event = EventUtil.getEvent(event);
    var message = "I'm really going to miss you if you go.";
    event.returnValue = message;
    return message;
});
```

#### 13.4.7.3DOMContentLoaded事件
DOMContentLoaded事件在形成**完整的DOM树之后**就会触发，不理会图像，js，css或其他外部资源是否下载完成。
这个事件会**冒泡**到window，但是目标实际上是document

#### 13.4.7.4readystatechange事件
提供与文档或元素加载状态有关的信息，但是这个时间行为有时候很难预料！
这个事件的每个对象都有`readyState`属性：
 uninitialized（未初始化）：对象存在但尚未初始化。
 loading（正在加载）：对象正在加载数据。
 loaded（加载完毕）：对象加载数据完成。
 interactive（交互）：可以操作对象了，但还没有完全加载。
 complete（完成）：对象已经加载完毕。
**并不一定执行所有阶段**
当进入interactive阶段时与DOMContentLoaded大致相同的时刻触发readystatechange事件。
此时DOM树已经加载完
无法判断和load事件触发的先后顺序。
交互阶段有可能早于也有可能晚于完成阶段出现，无法确保顺序，所以要**同时检测这两个状态**
```js
EventUtil.addHandler(document, "readystatechange", function(event){
    if (document.readyState == "interactive" || document.readyState == "complete"){
        EventUtil.removeHandler(document, "readystatechange", arguments.callee);   //这里通过arguments.callee来删匿名函数
        alert("Content loaded");
    }
});
```
`script` `link`也会触发这个事件，**来确定外部的js和css是否加载完成**
这两个标签和上边代码一样，只是对象变了，不是document而是script和link节点了
#### 13.4.7.5 pageshow和pagehide事件
往返缓存：在用户使用浏览器的**后退和前进**按钮时加快页面的转换速度。
不仅保存着页面数据，还保存了DOM和javascript的状态；实际上是将整个页面都保存在了内存中。
如果页面位于`bfcache`中,再次打开就**不会触发load**事件
`pageshow`页面显示时触发，无论该页面是否来自bfcache。
但重新加载页面中，pageshow会在load事件触发后触发
必须将程序添加到window
其实就是点后退触发的事件（个人理解）
还包含一个`persisted`的布尔值属性
如果被保存在了bfcache中，值为true，否则为false
```js
(function(){
        var showCount = 0;
        EventUtil.addHandler(window, "load", function(){
            alert("Load fired");            
        });
        EventUtil.addHandler(window, "pageshow", function(event){
            showCount++;
            alert("Show has been fired " + showCount + " times. Persisted? " + event.persisted);            
        });
        EventUtil.addHandler(window, "pagehide", function(event){
            alert("Hiding. Persisted? " + event.persisted);            
        });
    })();
```
`pagehide`会在浏览器卸载页面的时候触发，而且是在unload事件之前触发。
如果页面在卸载之后会被保存在bfcache中，那么`persisted`的值为true。
**当第一次触发pageshow 时，persisted 的值一定是false，而在第一次触发pagehide 时，persisted 就会变成true（除非页面不会被保存在bfcache 中）**

#### 13.4.7.6 hashchange事件
以便在URL参数列表（及URL中#号后面的所有字符串）发生变化时通知开发人员。在Ajax应用中，开发人员经常要利用URL参数列表来保存状态或导航信息。
`oldURL` `newURL`分别代表变化前后的**完整URL**
最好使用location来确定当前的参数列表
```js
EventUtil.addHandler(window, "hashchange", function(event){
    alert("Old URL: " + event.oldURL + "\nNew URL: " + event.newURL);
});

EventUtil.addHandler(window, "hashchange", function(event){
    alert("Current hash: " + location.hash);   //利用location
});
```
检查是否支持这个属性：
```js
var isSupported = ("onhashchange" in window) && (document.documentMode ===
undefined || document.documentMode > 7);
```
### 13.4.8 设备事件
#### 13.4.8.1 orientationchange事件
Safari添加的事件`orientationchange`事件，确认是否横向查看
`window.orientation`属性：
`0`正着
`90`左旋转横向，iphone的圆扭在右侧
`-90`右旋转
每次改变模式都会触发这个事件。

#### 13.4.8.2 MozOrientation事件
Firefox添加的事件`MozOrientation`事件
该事件只提供**一个平面方向变化**
`event`对象包含三个属性： x 、 y 和 z 。
这几个属性的值都介于 1 到-1 之间，表示不同坐标轴上的方向。
在静止状态下， x 值为 0， y 值为 0， z 值为 1（表示设备处于竖直状态） 。
如果设备向右倾斜， x 值会减小；反之，向左倾斜， x 值会增大。
如果设备向远离用户的方向倾斜， y 值会减小，向接近用户的方向倾斜， y 值会增大。
z轴检测垂直加速度度，1 表示静止不动，在设备移动时值会减小。**失重状态下值为0**

#### 13.4.8.3 deviceorientation事件
这个事件和MozOrientation事件差不多，区别在于这个事件**意图告诉开发人员设备在空间中朝向哪**而不是**如何移动**
x轴方向是从左往右，y 轴方向是从下往上，z 轴方向是从后往前
5个属性
 alpha：在围绕 z轴旋转时（即左右旋转时），y 轴的度数差；是一个介于 0 到 360 之间的浮点数。
 beta： 在围绕 x轴旋转时 （即前后旋转时），z轴的度数差； 是一个介于-180到 180之间的浮点数。
 gamma：在围绕 y轴旋转时（即扭转设备时），z轴的度数差；是一个介于-90到 90之间的浮点数。
 absolute：布尔值，表示设备是否返回一个绝对值。
 compassCalibrated：布尔值，表示设备的指南针是否校准过。
![](/images/deviceorientation.png)
```js
EventUtil.addHandler(window, "deviceorientation", function(event){
    var output = document.getElementById("output");
    var arrow = document.getElementById("arrow");
    arrow.style.webkitTransform = "rotate(" + Math.round(event.alpha) + "deg)";
    output.innerHTML = "Alpha=" + event.alpha + ", Beta=" + event.beta + ", Gamma=" + event.gamma + "<br>";
});
```

#### 13.4.8.4 devicemotion事件
这个事件告诉开发人员设备**什么时候移动**，而**不仅仅是设备方向如何改变**，如检测设备是不是在往下掉。
属性：
 acceleration ：一个包含 x 、 y 和 z 属性的对象，在不考虑重力的情况下，告诉你在每个方向上的加速度。
 accelerationIncludingGravity ：一个包含 x 、 y 和 z 属性的对象，在考虑 z 轴自然重力加速度的情况下，告诉你在每个方向上的加速度。
 interval ：以毫秒表示的时间值，必须在另一个 devicemotion 事件触发前传入。这个值在每个事件中应该是一个常量。
 rotationRate ：一个包含表示方向的 alpha 、 beta 和 gamma 属性的对象。
在使用之前要检测 acceleration 、 accelerationIncludingGravity 和 rotationRate 值是不是为`null`
```js
EventUtil.addHandler(window, "devicemotion", function(event){
    var output = document.getElementById("output");
    if (event.rotationRate !== null){
        output.innerHTML += "Alpha=" + event.rotationRate.alpha + ", Beta=" + 
                            event.rotationRate.beta + ", Gamma=" + 
                            event.rotationRate.gamma;        
    }
});
```

### 13.4.9 触摸与手势事件
#### 13.4.9.1 触摸事件
 touchstart ：当手指触摸屏幕时触发；**即使已经有一个手指放在了屏幕上也会触发**。
 touchmove ： 当手指在屏幕上**滑动时连续**地触发。 在这个事件发生期间， 调用 preventDefault()可以**阻止滚动**。
 touchend ：当手指从屏幕上移开时触发。
 touchcancel ：当系统停止跟踪触摸时触发。关于此事件的确切触发时间，文档中没有明确说明。
都会**冒泡**
每个触摸事件的`event`对象都提供了鼠标常见的属性：
bubbles 、 cancelable 、 view 、 clientX 、 clientY 、 screenX 、 screenY 、 detail 、 altKey 、 shiftKey 、
ctrlKey 和 metaKey 。
还包括以下三个用于跟踪触摸的属性
 touches ：表示当前跟踪的触摸操作的 Touch 对象的数组。
 targetTouchs ：特定于事件目标的 Touch 对象的数组。
 changeTouches ：表示自上次触摸以来发生了什么改变的 Touch 对象的数组。
**每个 Touch 对象包含下列属性**
 clientX ：触摸目标在视口中的 x 坐标。
 clientY ：触摸目标在视口中的 y 坐标。
 identifier ：标识触摸的唯一 ID。
 pageX ：触摸目标在页面中的 x 坐标。
 pageY ：触摸目标在页面中的 y 坐标。
 screenX ：触摸目标在屏幕中的 x 坐标。
 screenY ：触摸目标在屏幕中的 y 坐标。
 target ：触摸的 DOM 节点目标。
```js
function handleTouchEvent(event){
            
    //only for one touch
    if (event.touches.length == 1){

        var output = document.getElementById("output");
        switch(event.type){
            case "touchstart":
                output.innerHTML = "Touch started (" + event.touches[0].clientX + "," + event.touches[0].clientY + ")";   //这里的touches[0]纯粹为了简单起见，只记录一次触摸活动，多次可以去掉
                break;
            case "touchend":      //注意changedTouches的使用！！！
                output.innerHTML += "<br>Touch ended (" + event.changedTouches[0].clientX + "," + event.changedTouches[0].clientY + ")";
                break;
            case "touchmove":
                event.preventDefault();  //prevent scrolling★ 先取消滚动
                output.innerHTML += "<br>Touch moved (" + event.changedTouches[0].clientX + "," + event.changedTouches[0].clientY + ")";
                break;
        }
    }
}

document.addEventListener("touchstart", handleTouchEvent, false);
document.addEventListener("touchend", handleTouchEvent, false);
document.addEventListener("touchmove", handleTouchEvent, false);
```
事件执行顺序：
(1)  touchstart
(2)  mouseover
(3)  mousemove （一次）
(4)  mousedown
(5)  mouseup
(6)  click
(7)  touchend

#### 13.4.9.2 手势事件
**两个手指**触摸屏幕时产生手势，有三个手势
 gesturestart ：当一个手指已经按在屏幕上而另一个手指又触摸屏幕时触发。
 gesturechange ：当触摸屏幕的任何一个手指的位置发生变化时触发。
 gestureend ：当任何一个手指从屏幕上面移开时触发。
触发顺序：
1.当一个手指放在屏幕上时，会触发 touchstart 事件。
2.如果另一个手指又放在了屏幕上， 则会先触发 gesturestart 事件， 
3.随后触发基于该手指的 touchstart事件。
4.如果一个或两个手指在屏幕上滑动，将会触发 gesturechange 事件。
5.但只要有一个手指移开，就会触发 gestureend 事件，紧接着又会触发基于该手指的 touchend 事件。
还包括两个重要属性：
`rotation`旋转角度。负值为逆时针，正值为顺时针(**从0开始**)
`scale`两个手指间距离的变化。这个值**从1开始**，拉大变大，缩小减小
```js
function handleGestureEvent(event){        
    var output = document.getElementById("output");
    switch(event.type){
        case "gesturestart":
            output.innerHTML = "Gesture started (rotation=" + event.rotation + ",scale=" + event.scale + ")";
            break;
        case "gestureend":
            output.innerHTML += "<br>Gesture ended (rotation=" + event.rotation + ",scale=" + event.scale + ")";
            break;
        case "gesturechange":
            output.innerHTML += "<br>Gesture changed (rotation=" + event.rotation + ",scale=" + event.scale + ")";
            break;
    }
}

document.addEventListener("gesturestart", handleGestureEvent, false);
document.addEventListener("gestureend", handleGestureEvent, false);
document.addEventListener("gesturechange", handleGestureEvent, false);
```

## 13.5 内存和性能
### 13.5.1 事件委托
利用的是事件冒泡原理，一直会冒到document层
```js
(function(){
    var list = document.getElementById("myLinks");
    
    EventUtil.addHandler(list, "click", function(event){
        event = EventUtil.getEvent(event);
        var target = EventUtil.getTarget(event);
    
        switch(target.id){
            case "doSomething":
                document.title = "I changed the document's title";
                break;
    
            case "goSomewhere":
                location.href = "http://www.wrox.com";
                break;
    
            case "sayHi":
                alert("hi");
                break;
        }
    });

})();
```
最好绑定到docuemtn，优点：
1.document对象很快就可以访问
2.任何时间点上添加事件，无需等待load事件
3.设置事件处理程序所需时间更少。（引用DOM少）
4.整个页面占用内存空间更少

### 13.5.2 移除事件处理程序
不用的事件及时移除
事件残留的原因：
`removeChild`和`replaceChild`方法进行移除或替换所产生的
`innerHTML`进行替换删除掉的
解决方法：
1.手工移除
```js
btn.onclick = function(){
//先执行某些操作
    btn.onclick = null; // 移除事件处理程序★
    document.getElementById("myDiv").innerHTML = "Processing...";
};
```
**有些浏览器页面被卸载了，但是之前有没有清理的，却还滞留在内存中**
通过`onunload`事件来移除所有事件。
通过事件委托更容易移除页面所有事件。
**onunload事件处理程序，意味着页面不会被缓存在bfcache中**

## 13.6 模拟事件
事件自动触发，多用于测试。需要的话，回来补，o(^▽^)o  P405

# 14.表单脚本
## 14.1 表单的基础知识
表单对应的是HTMLFormElement类型，这个类型继承了HTMLElement，所以继承了HTML相同的属性。
独有属性：
 acceptCharset ：服务器能够处理的字符集；等价于 HTML 中的 accept-charset 特性。
 action ：接受请求的 URL；等价于 HTML 中的 action 特性。
 elements ：表单中所有控件的集合（ HTMLCollection ） 。
 enctype ：请求的编码类型；等价于 HTML 中的 enctype 特性。
 length ：表单中控件的数量。
 method ：要发送的 HTTP 请求类型，通常是 "get" 或 "post" ；等价于 HTML 的 method 特性。
 name ：表单的名称；等价于 HTML 的 name 特性。
 reset() ：将所有表单域重置为默认值。
 submit() ：提交表单。
 target ：用于发送请求和接收响应的窗口名称；等价于 HTML 的 target 特性。
`document.forms`获取页面所有表单
可以通过`name`访问表单
```js
var myForm = document.forms['form2'];  //form2为name
```
###14.1.1 提交表单
`input`或`button`，将其`type`值设置为`submit` 或者`image`都可以**提交**表单
`submit()`这个方法也可以提交表单，但是这个方法**不会触发submit**事件，所以提交之前要验证数据
解决多次点击方法：
1.禁用提交按钮
2.提交后取消后续提交操作（做一个标记flag = true时可以点击）

### 14.1.2 重置表单
type类型为`reset`
`reset()`这个方法会像单机重置按钮一样**触发reset事件**

### 14.1.3 表单字段
每个表单都有`elements`属性，可以通过**name和位置**来访问它们
```js
<form method="post" action="javascript:alert('Form submitted!')" id="myForm">
    <ul>
        <li><input type="radio" name="color" value="red">Red</li>
        <li><input type="radio" name="color" value="green">Green</li>
        <li><input type="radio" name="color" value="blue">Blue</li>
    </ul>
</form>     
<script type="text/javascript">
    (function(){
        var form = document.getElementById("myForm");
        
        var colorFields = form.elements["color"];   //通过name获取
        alert(colorFields.length);  //3
        
        var firstColorField = colorFields[0];
        var firstFormField = form.elements[0];       //通过位置获取
        alert(firstColorField === firstFormField);   //true

    })();

</script>
```

#### 14.1.3.1共有的表单字段属性
除了`fieldset`元素外，表单元素都有相同的一组属性
 disabled ：布尔值，表示当前字段是否被禁用。
 form ：指向当前字段所属表单的**指针**；只读。
 name ：当前字段的名称。
 readOnly ：布尔值，表示当前字段是否只读。
 tabIndex ：表示当前字段的切换（tab）序号。
 type ：当前字段的类型，如 "checkbox" 、 "radio" ，等等。
 value ：当前字段将被提交给服务器的值。对文件字段来说，这个属性是只读的，包含着文件在计算机中的路径。
除了`form`其他都可以通过js来动态修改属性
能用.获取最好用点，不要用DOM方法，例如getAttribute
下边是**单击后禁用按钮**
```js
(function(){
    var form = document.forms[0];
    
    //Code to prevent multiple form submissions
    EventUtil.addHandler(form, "submit", function(event){
        event = EventUtil.getEvent(event);
        var target = EventUtil.getTarget(event);
    
        //get the submit button
        var btn = target.elements["submit-btn"];
    
        //disable it
        btn.disabled = true;     //禁用按钮
        
    });

})();
```
**不能通过onclick事件实现这个功能**因为有的浏览器会在触发表单的click事件之前触发submit事件.

#### 14.1.3.2 共有的表单字段方法
每个表单字段都有两个方法`focus()`和`blur()`
**隐藏元素**使用者两个属性会报错
`autofocus`属性，为type属性，会自动聚焦
在没有`readonly`属性的时候，blur()可以实现这个只读的功能

#### 14.1.3.3 共有的表单字段事件
事件！
 blur ：当前字段失去焦点时触发。
 change ：对于`<input>`和 `<textarea>`元素，在它们**失去焦点**且**value值改变**时触发；对于`<select>`元素，在其选项改变时触发。
 focus ：当前字段获得焦点时触发。

## 14.2 文本框脚本
`input`和`textarea`
`size`特性，设置文本框中能够显示的字符数。
`value`特性，可以设置文本框的初始值
`maxlength`特性，指定文本框可以接受的最大字符数

`rows`指定文本框的字符行数
`cols`指定文本框的字符列数
**初始值**放在textarea区域之间就可以

### 14.2.1 选择文本
`select()`方法，选择文本框内**所有**文本。
**当获取焦点的时候，选中文本框内的内容**
```js
EventUtil.addHandler(window, "load", function(event){
    var textbox = document.forms[0].elements[0];
    
    EventUtil.addHandler(textbox, "focus", function(event){
        event = EventUtil.getEvent(event);
        var target = EventUtil.getTarget(event);
        
        target.select();    //善用target
    });

    textbox.focus();
});    
```
#### 14.2.1.1 选择事件
`select`当用户选中文本的时候，就会触发这个选中事件

#### 14.2.1.2 取得选择的文本
`selectionStart`
`selectionEnd`
这两个属性保存的是基于0的数值
```js
function getSelectedText(textbox){
    return textbox.value.substring(textbox.selectionStart, textbox.selectionEnd);   //借助的substring，这个方法是偏移量
}
```
要取得选择的文本还可以通过12章介绍的范围
```js
(function(){
        
    function getSelectedText(textbox){
        if (typeof textbox.selectionStart == "number"){
            return textbox.value.substring(textbox.selectionStart, 
                    textbox.selectionEnd);                
        } else if (document.selection){      //表示当前网页中的选中内容
            return document.selection.createRange().text;
        }
    }
                  
    EventUtil.addHandler(window, "load", function(event){
        var textbox = document.forms[0].elements[0];

        EventUtil.addHandler(textbox, "select", function(event){
            alert(getSelectedText(textbox));
        });

        textbox.focus();
    });               
})();
```
#### 14.2.1.3 选择部分文本
`setSelectionRange()`类似于substring()方法
```js
textbox.value = "Hello world!"
//选择所有文本
textbox.setSelectionRange(0, textbox.value.length); //"Hello world!"
//选择前 3 个字符
textbox.setSelectionRange(0, 3); //"Hel"
//选择第 4 到第 6 个字符
textbox.setSelectionRange(4, 7); //"o w"
```
IE8及更早版本就只能使用12章的范围来解决选择部分文本的效果了。
`createTextRange()` `moveStart()` `moveEnd` `collapse()`用到这些方法
```js
//兼容
(function(){
        
    function selectText(textbox, startIndex, stopIndex){
        if (textbox.setSelectionRange){
            textbox.setSelectionRange(startIndex, stopIndex);
        } else if (textbox.createTextRange){
            var range = textbox.createTextRange();
            range.collapse(true);
            range.moveStart("character", startIndex);
            range.moveEnd("character", stopIndex - startIndex);
            range.select();                    
        }
        textbox.focus();
    }
                  
    var btn = document.getElementById("select-btn");
    EventUtil.addHandler(btn, "click", function(event){
        var textbox = document.forms[0].elements[0];
        selectText(textbox, 4, 7);
    });
    
    
})();
```

### 14.2.2 过滤输入
#### 14.2.2.1 屏蔽字符
通过屏蔽`keypress`事件的按钮操作

#### 14.2.2.2 操作剪贴板
剪贴板事件
 beforecopy ：在发生复制操作前触发。
 copy ：在发生复制操作时触发。
 beforecut ：在发生剪切操作前触发。
 cut ：在发生剪切操作时触发。
 beforepaste ：在发生粘贴操作前触发。
 paste ：在发生粘贴操作时触发。
`window.clipboardData`访问剪贴板数据
有三个方法：
`getData()`从剪贴板中取得数据
`setData()`连个参数：数据类型+要放入剪贴板中的文本
`clearData()`
```js
var EventUtil = {
//省略的代码
    getClipboardText: function(event){
        var clipboardData = (event.clipboardData || window.clipboardData);
        return clipboardData.getData("text");
    },
//省略的代码
    setClipboardText: function(event, value){
        if (event.clipboardData){
            return event.clipboardData.setData("text/plain", value);
        } else if (window.clipboardData){
            return window.clipboardData.setData("text", value);
        }
    },
//省略的代码
};
```
### 14.2.3 自动切换焦点
用户填写完当前字段时，自动将焦点切换到下一个字段
```js
//主要通过判断来实现的
(function(){
       
    function tabForward(event){            
        event = EventUtil.getEvent(event);
        var target = EventUtil.getTarget(event);
        
        if (target.value.length == target.maxLength){  
            var form = target.form;
            
            for (var i=0, len=form.elements.length; i < len; i++) {
                if (form.elements[i] == target) {
                    if (form.elements[i+1]){
                        form.elements[i+1].focus();
                    }
                    return;
                }
            }
        }
    }
                
    var textbox1 = document.getElementById("txtTel1"),
        textbox2 = document.getElementById("txtTel2"),
        textbox3 = document.getElementById("txtTel3");
    
    EventUtil.addHandler(textbox1, "keyup", tabForward);        
    EventUtil.addHandler(textbox2, "keyup", tabForward);        
    EventUtil.addHandler(textbox3, "keyup", tabForward);        
                
})();
```

### 14.2.4 HTML5约束验证API
1.必填字段
`required`  
2.其他输入类型
`email`
`url`
3.数值范围
`number`
`range`
`datetime`
`datetime-local`
`date`
`month`
`week`
`time`
4.输入模式
`pattern` 正则 pattern="\d+"
5.检测有效性
`checkValidity()`方法可以检测表单中的某个字段是否有效，有效返回true
可以对整个表单最检测，也可以对单一的做检测
```js
if(document.forms[0].checkValidity()){
//表单有效，继续
} else {
//表单无效
}
```
`validity`属性**告诉你为什么有效或无效**
还是推荐用正则
6.禁用验证
`novalidate`告诉表单不进行验证--给input添加的
`formnovalidate`整个表单不进行验证--给提交按钮添加

## 14.3 选择框脚本
选择框是通过`select` `option`来创建的
除了表单共有的属性和方法，还有
 add(newOption, relOption) ：向控件中插入新 `<option>` 元素，其位置在相关项（ relOption ）之前。
 multiple ：布尔值，表示是否允许多项选择；等价于 HTML 中的 multiple 特性。
 options ：控件中所有 `<option>` 元素的 HTMLCollection 。
 remove(index) ：移除给定位置的选项。
 selectedIndex ：基于 0 的选中项的索引，如果没有选中项，则值为 -1 。对于支持多选的控件，只保存选中项中第一项的索引。
 size ：选择框中可见的行数；等价于 HTML 中的 size 特性。
value值得不同情况
1.没有选中项，为空字符串
2.一个选中，取value值，如果没有value值，取**文本**的值
3.多选中，取第一个选中的值

每个option都有一个`HTMLOptionElement`对象表示
有以下属性
 index ：当前选项在 options 集合中的索引。
 label ：当前选项的标签；等价于 HTML 中的 label 特性。
 selected ：布尔值，表示当前选项是否被选中。将这个属性设置为 true 可以选中当前选项。
 text ：选项的文本。
 value ：选项的值（等价于 HTML 中的 value 特性） 。
推荐访问方法
```js
var text = selectbox.options[0].text; // 选项的文本
var value = selectbox.options[0].value; // 选项的值
```
`change`事件，只要选中就会触发

### 14.3.1 选择选项
`selectedIndex`属性，**取得选中项**-单选
设置选中项(可以多选)
```js
selectbox.options[0].selected = true; //令selected 为true--多选的话，其他选项也为true就行了
```
下边是获取选中项
```js
function getSelectedOptions(selectbox){
    var result = new Array();
    var option = null;
    
    for (var i=0, len=selectbox.options.length; i < len; i++){
        option = selectbox.options[i];
        if (option.selected){
            result.push(option);
        }
    }
    
    return result;            
}
```

### 14.3.2 添加选项
1.DOM的appendChild方法
2.`Option`构造函数创建
```js
var newOption = new Option("Option text", "Option value");
selectbox.appendChild(newOption); //在 IE8 及之前版本中有问题
```
3.`add()`方法，两个参数：添加的新选项+位于新选项之后的选项，如果设置为最后一个，那么第二个参数为`null`
```js
//插入最后一项--最佳方案
var newOption = new Option("Option text", "Option value");
selectbox.add(newOption, undefined); //最佳方案
```
### 14.3.3 移除选项
1.DOM方法-removeChild
2.`remove()`方法，一个参数：要移除项的索引
```js
selectbox.remove(0); //移除第一个选项
```
3.将选项设置为`null`
```js
selectbox.options[0] = null; //移除第一个选项
```

### 14.3.4 移动和重排选项
1.appendChild  将一个选项框中的选项，移到另一个选项框中（appendChild会先移除，再插入特性）
```js
var selectbox1 = document.getElementById("selLocations1");
var selectbox2 = document.getElementById("selLocations2");
selectbox2.appendChild(selectbox1.options[0]);
```
移动和移除的共同之处是**每一个选项的index属性会被重置**
通过`insertBefore()`和`appendChild()`进行重排

## 14.4 表单序列化
  对表单字段的名称和值进行 URL 编码，使用和号（&）分隔。
  不发送禁用的表单字段。
  只发送勾选的复选框和单选按钮。
  不发送 type 为 "reset" 和 "button" 的按钮。
  多选选择框中的每个选中的值单独一个条目。
  在单击提交按钮提交表单的情况下，也会发送提交按钮；否则，不发送提交按钮。也包括 type为 "image" 的 `<input>` 元素。
 `<select>` 元素的值，就是选中的 `<option>` 元素的 value 特性的值。如果 `<option>` 元素没有value 特性，则是 `<option>` 元素的文本值。
```js
function serialize(form){        
    var parts = [],
        field = null,
        i,
        len,
        j,
        optLen,
        option,
        optValue;
    
    for (i=0, len=form.elements.length; i < len; i++){
        field = form.elements[i];
    
        switch(field.type){
            case "select-one":
            case "select-multiple":
            
                if (field.name.length){
                    for (j=0, optLen = field.options.length; j < optLen; j++){
                        option = field.options[j];
                        if (option.selected){
                            optValue = "";
                            if (option.hasAttribute){
                                optValue = (option.hasAttribute("value") ? option.value : option.text);
                            } else {
                                optValue = (option.attributes["value"].specified ? option.value : option.text);
                            }
                            parts.push(encodeURIComponent(field.name) + "=" + encodeURIComponent(optValue));
                        }
                    }
                }
                break;
                
            case undefined:     //fieldset
            case "file":        //file input
            case "submit":      //submit button
            case "reset":       //reset button
            case "button":      //custom button
                break;
                
            case "radio":       //radio button
            case "checkbox":    //checkbox
                if (!field.checked){
                    break;
                }
                /* falls through */
                            
            default:
                //don't include form fields without names
                if (field.name.length){
                    parts.push(encodeURIComponent(field.name) + "=" + encodeURIComponent(field.value));
                }
        }
    }        
    return parts.join("&");
}

var btn = document.getElementById("serialize-btn");
EventUtil.addHandler(btn, "click", function(event){
    var form = document.forms[0];
    alert(serialize(form));
});
```

## 14.5 富文本编辑
就是在页面中嵌入一个包含空HTML页面的iframe。
通过设置`designMode`属性，让空白的HTML页面可以被编辑，而编辑的对象则是该页面`body`元素的HTML代码
包含两个可能的值`on`和`off`

使用onload事件，设置`designMode`为`on`
```js
<iframe name="richedit" style="height:100px;width:100px;" src="blank.htm"></iframe>
    <script type="text/javascript">
    EventUtil.addHandler(window, "load", function(){
        frames["richedit"].document.designMode = "on";
    });
</script>
```

### 14.5.1 使用contenteditable属性-比上边方法更好使
`contenteditable`可以应用到任何元素，然后用户可以立即编辑该元素
```html
<div class="editable" id="richedit" contenteditable></div>
```
设置了这个属性，就好像这个元素变成了`textarea`元素
属性值：
`true`打开`false`关闭`inherit`从父元素那里继承
```js
//打开编辑模式
var div = document.getElementById("richedit");
div.contentEditable = "true";
```

### 14.5.2 操作富文本
`document.execCommand()`对文档执行预定义命令
三个参数：要执行的命令名称+浏览器是否应该为当前命令提供用户界面的一个布尔值+执行命令必须的一个值(如不需要，则传递null)
确保兼容性，第二个参数设为`false`
```js
//转换粗体文本
document.execCommand("bold", false, null);
//转换斜体文本
document.execCommand("italic", false, null);
//创建指向 www.wrox.com 的链接
document.execCommand("createlink", false,
"http://www.wrox.com");
//格式化为 1 级标题
document.execCommand("formatblock", false, "<h1>");
```
不同浏览器对这些命令解析出来的**标签**不同，所以不要指望产生一致的HTML

`queryCommandEnabled()`检测是否可以针对当前选择的文本，或者当前插入字符所在位置执行某个命令
一个参数：要检测的命令
允许执行传入命令，返回true
```js
var result = frames["richedit"].document.queryCommandEnabled("bold");  //能执行返回true
```
具体是否能执行，还是要看不同浏览器的默认设置

`queryCommandValue()`取得传入的值，就是前边execCommand传入的第三个参数
```js
var fontSize = frames["richedit"].document.queryCommandValue("fontsize");
```

### 14.5.3 富文本选区 -比上边更重要一些
编辑区内使用`getSelection()`方法，可以确定实际选择的文本
属性
 anchorNode ：选区起点所在的节点。
 anchorOffset ：在到达选区起点位置之前跳过的 anchorNode 中的字符数量。
 focusNode ：选区终点所在的节点。
 focusOffset ： focusNode 中包含在选区之内的字符数量。
 isCollapsed ：布尔值，表示选区的起点和终点是否重合。
 rangeCount ：选区中包含的 DOM 范围的数量。
方法：
 addRange(range) ：将指定的 DOM 范围添加到选区中。
 collapse(node, offset) ：将选区折叠到指定节点中的相应的文本偏移位置。
 collapseToEnd() ：将选区折叠到终点位置。
 collapseToStart() ：将选区折叠到起点位置。
 containsNode(node) ：确定指定的节点是否包含在选区中。
 deleteFromDocument() ： 从文档中删除选区中的文本， 与 document.execCommand("delete",false, null) 命令的结果相同。
 extend(node, offset) ：通过将 focusNode 和 focusOffset 移动到指定的值来扩展选区。
 getRangeAt(index) ：返回索引对应的选区中的 DOM 范围。
 removeAllRanges() ：从选区中移除所有 DOM 范围。实际上，这样会移除选区，因为选区中至少要有一个范围。
 reomveRange(range) ：从选区中移除指定的 DOM 范围。
 selectAllChildren(node) ：清除选区并选择指定节点的所有子节点。
 toString() ：返回选区所包含的文本内容。
通过上边的方法，比`execCommand()`更加细化
```js
var selection = frames["richedit"].getSelection();
//取得选择的文本
var selectedText = selection.toString();
//取得代表选区的范围
var range = selection.getRangeAt(0);
//突出显示选择的文本
var span = frames["richedit"].document.createElement("span");
span.style.backgroundColor = "yellow";
range.surroundContents(span);
```
IE8不支持DOM范围，但可以通过`document.createRange()`来进行操作
具体结合12.4.2 和P443页来解决兼容问题

### 14.5.4 表单与富文本
在提取表单之前，从iframe中提取出HTML，然后将其插入到表单字段中，然后提交这个表单。
```js
EventUtil.addHandler(form, "submit", function(event){
    event = EventUtil.getEvent(event);
    var target = EventUtil.getTarget(event);
    target.elements["comments"].value =
        document.getElementById("richedit").innerHTML;
});
```

# 20 JSON
## 转换
1. JSON字符串转换为JSON对象
```js
var obj = str.parseJSON(); //由JSON字符串转换为JSON对象
//或者
var obj = JSON.parse(str); //由JSON字符串转换为JSON对象
```
2. JSON对象转化为JSON字符串
```js
var last=obj.toJSONString(); //将JSON对象转化为JSON字符
//或者
var last=JSON.stringify(obj); //将JSON对象转化为JSON字符
```

# 21.Ajax与Comet
## 21.1 XMLHttpRequest对象
创建XHR对象
```js
var xhr = new XMLHttpRequest();
```
兼容版：
```js
function createXHR(){
    if (typeof XMLHttpRequest != "undefined"){
        return new XMLHttpRequest();
    } else if (typeof ActiveXObject != "undefined"){
        if (typeof arguments.callee.activeXString != "string"){
            var versions = ["MSXML2.XMLHttp.6.0", "MSXML2.XMLHttp.3.0",
                            "MSXML2.XMLHttp"],
                i, len;
    
            for (i=0,len=versions.length; i < len; i++){
                try {
                    new ActiveXObject(versions[i]);
                    arguments.callee.activeXString = versions[i];
                    break;
                } catch (ex){
                    //skip
                }
            }
        }
    
        return new ActiveXObject(arguments.callee.activeXString);
    } else {
        throw new Error("No XHR object available.");
    }
}

var xhr = createXHR();         //创建XHR对象
xhr.open("get", "example.txt", false);
xhr.send(null);

if ((xhr.status >= 200 && xhr.status < 300) || xhr.status == 304){
    alert(xhr.statusText);
    alert(xhr.responseText);
} else {
    alert("Request was unsuccessful: " + xhr.status);
}
        
```

### 21.1.1 XHR用法
1.调用`open()`方法，3个参数：请求类型+URL(相对当前页面)+是否异步
只是启动请求，以备发送并不发送
```js
xhr.open("get","example.php",false);
```
2.发送特定请求`send()`
```js
xhr.open("get", "example.txt", false);
xhr.send(null);
```
XHR对象属性
 responseText：作为响应主体被返回的文本。
 responseXML：如果响应的内容类型是"text/xml"或"application/xml"，这个属性中将保存包含着响应数据的XML DOM 文档。
 status：响应的HTTP 状态。
 statusText：HTTP 状态的说明。
接收响应过程：
3.检查`status`属性,确定成功返回（200）。
此时，responseText属性内容已经准备就绪，responseXML可以访问
状态码为304的时候，表示资源没有被修改，直接访问浏览器中的缓存版本
检查状态：
```js
xhr.open("get", "example.txt", false);
xhr.send(null);

if ((xhr.status >= 200 && xhr.status < 300) || xhr.status == 304){  //成功响应或调用缓存
    alert(xhr.statusText);
    alert(xhr.responseText);
} else {
    alert("Request was unsuccessful: " + xhr.status);
}
```
异步请求：
检查XHR对象的`readyState`属性，这个属性值有
 0：未初始化。尚未调用open()方法。
 1：启动。已经调用open()方法，但尚未调用send()方法。
 2：发送。已经调用send()方法，但尚未接收到响应。
 3：接收。已经接收到部分响应数据。
 4：完成。已经接收到全部响应数据，而且已经可以在客户端使用了。
触发`readystatechange`事件，来获取`readyState`的值
在open()之前指定onreadystatechange事件才能确保兼容性
```js
var xhr = createXHR();        
xhr.onreadystatechange = function(event){
    if (xhr.readyState == 4){
        if ((xhr.status >= 200 && xhr.status < 300) || xhr.status == 304){
            alert(xhr.responseText);
        } else {
            alert("Request was unsuccessful: " + xhr.status);
        }
    }
};
xhr.open("get", "example.txt", true);
xhr.send(null);
```
在接收到响应之前调用abort()方法来**取消异步**请求
```js
xhr.abort();
```
停止触发事件，也不再允许访问任何与响应有关的对象属性

### 21.1.2 HTTP头部信息
请求头信息：
 Accept：浏览器能够处理的内容类型。
 Accept-Charset：浏览器能够显示的字符集。
 Accept-Encoding：浏览器能够处理的压缩编码。
 Accept-Language：浏览器当前设置的语言。
 Connection：浏览器与服务器之间连接的类型。
 Cookie：当前页面设置的任何Cookie。
 Host：发出请求的页面所在的域。
 Referer：发出请求的页面的URI。注意，HTTP 规范将这个头部字段拼写错了，而为保证与规范一致，也只能将错就错了。（这个英文单词的正确拼法应该是referrer。）
 User-Agent：浏览器的用户代理字符串。
`setRequestHeader()`设置自定义的请求头信息
两个参数：头部字段名称+值
**必须在open()之后，send()之前调用这个属性**
```js
xhr.open("get", "example.php", true);
xhr.setRequestHeader("MyHeader", "MyValue");
xhr.send(null);
```
`getResponseHeader()`方法，取得相应的响应头部信息
`getAllResponseHeaders()`方法，取得一个包含所有头部信息的长字符串。
```js
var myHeader = xhr.getResponseHeader("MyHeader");
var allHeaders = xhr.getAllResponseHeaders();
```
getAllResponseHeaders()方法返回的多行文本内容通常为：
Date: Sun, 14 Nov 2004 18:04:03 GMT
Server: Apache/1.3.29 (Unix)
Vary: Accept
X-Powered-By: PHP/4.3.8
Connection: close
Content-Type: text/html; charset=iso-8859-1

### 21.1.3 GET请求
查询字符串中（键值字符串）中每个参数的名称和值都必须使用`encodeURIComponent()`进行编码，然后才能放到URL的末尾
```js
xhr.open("get","example.php?name1=value1&name2=value2",true)
//向URL末尾添加查询字符串参数
function addURLParam(url, name, value) {
    url += (url.indexOf("?") == -1 ? "?" : "&");
    url += encodeURIComponent(name) + "=" + encodeURIComponent(value);
    return url;
}
```
### 21.1.4 POST请求
服务器对POST和WEB表单的请求并不会一视同仁。
我们可以使用XHR来模仿表单提交：
1.首先将Content-Type头信息设置为application/x-www-form-urlencoded,也就是表单类型提交的内容类型
2.然后将页面中表单的数据进行**序列化**
3.最后再通过XHR发送到服务器
```js
function submitData(){
    var xhr = createXHR();        
    xhr.onreadystatechange = function(event){
        if (xhr.readyState == 4){
            if ((xhr.status >= 200 && xhr.status < 300) || xhr.status == 304){
                alert(xhr.responseText);
            } else {
                alert("Request was unsuccessful: " + xhr.status);
            }
        }
    };
    
    xhr.open("post", "postexample.php", true);
    xhr.setRequestHeader("Content-Type", "application/x-www-form-urlencoded"); //第一步
    var form = document.getElementById("user-info");            
    xhr.send(serialize(form));    //第二步+第三步
}
```
服务器设置：
设置Content-Type头部信息设置为text/plain
如果不设置，发送过来的数据就不会出现在$_POST超级全局的变量中

## 21.2 XMLHttpRequest 2级
### 21.2.1 FormData
`FormData`类型，为表单序列化提供便利
```js
var data = new FormData();
data.append("name", "Nicholas");
```
`append()`方法接收两个额参数：键和值
也可以**直接传入表单元素**
```js
var data = new FormData(document.forms[0]);
```
```js
xhr.open("post","postexample.php", true);
var form = document.getElementById("user-info");
xhr.send(new FormData(form));   //发送序列化后的数据
```

### 21.2.2 超时设定
`timeout`**属性**，触发`timeout`**事件**
```js
xhr.onreadystatechange = function(event){
    try {                 //如果在超时事件处理之后来判断status，则会报错，所以用try-catch
        if (xhr.readyState == 4){
            if ((xhr.status >= 200 && xhr.status < 300) || xhr.status == 304){
                alert(xhr.responseText);
            } else {
                alert("Request was unsuccessful: " + xhr.status);
            }
        }
    } catch (ex){
        //assume handled by ontimeout
    }
};

xhr.open("get", "timeout.php", true);
xhr.timeout = 1000;                 //将超时设置为1秒钟
xhr.ontimeout = function(){         //触发超时事件
    alert("Request did not return in a second.");
};        
xhr.send(null);
```
### 21.2.3 overrideMimeType() 方法
`overrideMimeType()`用于重写MIME类型
```js
var xhr = createXHR();
xhr.open("get", "text.php", true);
xhr.overrideMimeType("text/xml");
xhr.send(null);
```
这个例子强迫XHR 对象将响应当作XML 而非纯文本来处理。调用overrideMimeType()必须在send()方法之前，才能保证重写响应的MIME 类型。

## 21.3 进度事件
6个事件
 loadstart：在接收到响应数据的第一个字节时触发。
 progress：在接收响应期间持续不断地触发。
 error：在请求发生错误时触发。
 abort：在因为调用abort()方法而终止连接时触发。
 load：在接收到完整的响应数据时触发。
 loadend：在通信完成或者触发error、abort 或load 事件后触发。

### 21.3.1 load事件
`onload`事件可以取代`readystatechange`事件，但是有的浏览器还不支持load，所以要写兼容模式
```js
var xhr = createXHR();        
xhr.onload = function(event){
    if ((xhr.status >= 200 && xhr.status < 300) || 
            xhr.status == 304){
        alert(xhr.responseText);
    } else {
        alert("Request was unsuccessful: " + xhr.status);
    }
};

xhr.open("get", "altevents.php", true);

xhr.send(null);
```

### 21.3.2 progress事件
在接收新数据期间周期性的触发
包含三个额外属性
`lengthComputable`进度信息是否可用
`position`已经接受的字节数
`totalSize`根据Content-Length 响应头部确定的预期字节数
```js
var xhr = createXHR();        
xhr.onload = function(event){
    if ((xhr.status >= 200 && xhr.status < 300) || 
            xhr.status == 304){
        alert(xhr.responseText);
    } else {
        alert("Request was unsuccessful: " + xhr.status);
    }
};
xhr.onprogress = function(event){
    var divStatus = document.getElementById("status");
    if (event.lengthComputable){    //假如信息进度可用
        divStatus.innerHTML = "Received " + event.position + " of " + event.totalSize + " bytes";
    }
};
xhr.open("get", "altevents.php", true);

xhr.send(null);
```

## 21.4 跨源资源共享
XHR主要限制：跨域安全策略（同源策略）
CORS使用自定义的HTTP头部让浏览器与服务器进行沟通
主体内容为text/plain的情况下，附加一个额外的Origin头部，其中包含请求页面的源信息（协议、域名和端口）
示例：
Origin: http://www.nczonline.net
如果服务器认为这个请求可以接受，就在`Access-Control-Allow-Origin`头部中回发相同的源信息（如果是公共资源，可以回复"*"）
Access-Control-Allow-Origin: http://www.nczonline.net

### 21.4.1 IE对CORS的实现
IE8引入了XDR类型，与XHR类似，可以实现跨域
不同之处
 cookie 不会随请求发送，也不会随响应返回。
 只能设置请求头部信息中的Content-Type 字段。
 不能访问响应头部信息。
 只支持 GET 和POST 请求。
这些变化使得CSRF(跨站点请求伪造)和XSS(跨站点脚本)的问题得到了缓解
自行决定是否设置Access-Control-Allow-Origin头部
所有的XDR都是**异步**的
```js
var xdr = new XDomainRequest();
xdr.onload = function(){         //事件
    alert(xdr.responseText);
};
xdr.onerror = function(){       //事件
    alert("Error!");
};
xdr.timeout = 1000;             //超时设置
xdr.ontimeout = function(){     //超时事件
alert("Request took too long.");
};
//you'll need to replace this URL with something that works
xdr.open("get", "http://www.somewhere-else.com/xdr.php");
xdr.contentType = "application/x-www-form-urlencoded";   //设置发送数据的格式
xdr.send(null);    
```
**只能访问响应的原始文本不能确定响应的状态代码**，只要响应有效就会触发load事件
如果失败（包括响应中缺少Access-Control-Allow-Origin头部）就会触发error事件
`abort()`方法可以终止请求

### 21.4.2 其他浏览器对CORS的实现
原生支持
为了安全，也有一些限制
 不能使用 setRequestHeader()设置自定义头部。
 不能发送和接收cookie。
 调用 getAllResponseHeaders()方法总会返回空字符串。

本地最好使用相对URL，远程再使用绝对URL

### 21.4.3 Preflighted Requests
可以通过Preflighted Reqeusts这种透明服务器验证机制支持开发人员使用自定义的头部、GET或POST之外的方法、以及不同类型的主体内容
使用`OPTIONS`方法，发送下列头部
 Origin：与简单的请求相同。
 Access-Control-Request-Method：请求自身使用的方法。
 Access-Control-Request-Headers：（可选）自定义的头部信息，多个头部以逗号分隔。
例：浏览器请求
Origin: http://www.nczonline.net
Access-Control-Request-Method: POST
Access-Control-Request-Headers: NCZ
服务器响应
 Access-Control-Allow-Origin：与简单的请求相同。
 Access-Control-Allow-Methods：允许的方法，多个方法以逗号分隔。
 Access-Control-Allow-Headers：允许的头部，多个头部以逗号分隔。
 Access-Control-Max-Age：应该将这个Preflight 请求缓存多长时间（以秒表示）。
例：
Access-Control-Allow-Origin: http://www.nczonline.net
Access-Control-Allow-Methods: POST, GET
Access-Control-Allow-Headers: NCZ
Access-Control-Max-Age: 1728000

### 21.4.4 带凭据的请求
默认情况，跨域不提供凭据
`withCredentials`属性设置为true，可以指定某个请求应该发送凭证
HTTP响应头：
Access-Control-Allow-Credentials: true

### 21.4.5 跨浏览器的CORS
检查XHR是否支持CORS最简单的方法，就是检查是否存在`withCredentials`属性。
再结合检测`XDomainReques`（XDR）对象是否存在就可以了
```js
function createCORSRequest(method, url){
    var xhr = new XMLHttpRequest();
    if ("withCredentials" in xhr){
        xhr.open(method, url, true);
    } else if (typeof XDomainRequest != "undefined"){
        xhr = new XDomainRequest();
        xhr.open(method, url);
    } else {
        xhr = null;
    }
    return xhr;
}

var request = createCORSRequest("get", "http://www.somewhere-else.com/xdr.php");
if (request){
    request.onload = function(){
        //do something with request.responseText
    };
    request.send();
}
```
这两个对象的共同属性/方法如下：
 abort()：用于停止正在进行的请求。
 onerror：用于替代onreadystatechange 检测错误。
 onload：用于替代onreadystatechange 检测成功。
 responseText：用于取得响应内容。
 send()：用于发送请求。
以上成员都包含在createCORSRequest()函数返回的对象中，在所有浏览器中都能正常使用。

## 21.5 其他跨域技术
### 21.5.1 图像Ping
动态创建图片--简单、单向、只能发送GET、无法访问服务器的响应文本
```js
var img = new Image();
img.onload = img.onerror = function(){
    alert("Done!");
};
img.src = "http://www.example.com/test?name=Nicholas";   
```

### 21.5.2 JSONP
动态调用script元素
```js
var script = document.createElement("script");
script.src = "http://freegeoip.net/json/?callback=handleResponse";
document.body.insertBefore(script, document.body.firstChild);
```
优点：可以直接访问响应文本+支持浏览器和服务器之间**双向**通信
缺点：不安全+无法判断JSONP请求是否失败（用定时器来检测指定时间内是否收到响应）

### 21.5.3 Comet
一种服务器向页面推送数据的技术
两种方式：长轮询和流
短轮询：即浏览器定时向服务器发送请求，看有没有更新的数据
长轮询：页面发起一个服务器的请求，然后服务器一直保持连接打开，直到有数据可以发送，然后关闭，再发起一次新请求。
优势：所有浏览器都支持-**通过XHR和setTimeout()就可以实现**

HTTP流：它在页面的整个生命周期内只使用一个HTTP链接。
就是浏览器向服务器发送一个请求，而服务器保持连接打开，然后周期性的**向浏览器发送数据**
需要服务器端设置。
浏览器端通过监听`readystatechange`事件及检测`readyState`为3来实现HTTP流。
```js
function createStreamingClient(url, progress, finished){        
            
    var xhr = new XMLHttpRequest(),
        received = 0;     //记录已经处理了多少个字符
        
    xhr.open("get", url, true);
    xhr.onreadystatechange = function(){
        var result;
        
        if (xhr.readyState == 3){
        
            //get only the new data and adjust counter
            result = xhr.responseText.substring(received);
            received += result.length;
            
            //call the progress callback
            progress(result);
            
        } else if (xhr.readyState == 4){
            finished(xhr.responseText);
        }
    };
    xhr.send(null);
    return xhr;
}

var client = createStreamingClient("streaming.php", function(data){
                alert("Received: " + data);
             }, function(data){
                alert("Done!");
             });
```
createStreamingClient()函数接收三个参数：要连接的URL + 在接收到数据时调用的函
数 + 关闭连接时调用的函数。

### 21.5.4 服务器发送事件
SSE:服务器发送事件
用于创建服务器**单向链接**
服务器响应的MIME类型必须是text/event-stream
SSE支持：长轮询/短轮询/HTTP流

首先创建一个`EventSource`对象，并传入一个入口点
```js
var source = new EventSource("myevents.php");  //必须同源
```
这个实例有一个`readyState`属性
0：连接到服务器
1：打开了连接
2：关闭了连接
三个事件：
 open：在建立连接时触发。
 message：在从服务器接收到新事件时触发。
 error：在无法建立连接时触发。
```js
source.onmessage = function(event){
    var data = event.data;
    //处理数据
};
```
`event.data`保存服务器发回的数据
如果连接断开，还会重新连接，如不想不再重新连接，调用`source.close()`

事件流：
通过一个持久的HTTP响应发送，响应的MIME类型为text/eventstream
响应的格式是纯文本，最简单的情况是每个数据项都带有前缀data：
data: foo  //第一个message事件

data: bar  //第二个message事件

data: foo  //第三个message事件，或的关系
data: bar  //第三个message事件

**只有数据行后面有空行时，才会触发message事件**
通过id：前缀可以给特定的事件指定一个关联的ID，这个ID行位于data：行前面或者后面皆可
data: foo
id: 1
设置ID可以在连接断开，向服务器发送一个包含名为Last-Event-ID的特殊HTTP头部请求，确保下次触发哪个事件。
这种机制可以确保浏览器以正确顺序收到连接的数据段

### 21.5.5 Web Sockets
**全双工，双向通信**
连接创建Web Socket协议
链接形式：ws://    （加密格式）wss://
可以在服务器和客户端发送少量数据，所以非常适合移动应用
#### 21.5.5.1 API
首先创建一个WbeSocket对象并传入要链接的URL
```js
var socket = new WebSocket("ws://www.example.com/server.php");   //必须是绝对地址
```
同源策略不适用
实例化对象后，浏览器会马上尝试创建连接。
WebSocket的`readyState`属性
 WebSocket.OPENING (0)：正在建立连接。
 WebSocket.OPEN (1)：已经建立连接。
 WebSocket.CLOSING (2)：正在关闭连接。
 WebSocket.CLOSE (3)：已经关闭连接。

关闭WebSocket调用`socket.close()`;
#### 21.5.5.2 发送和接收数据
WebSockets只能发送纯文本数据，所以复杂数据需要序列化
发送数据：
```js
var socket = new WebSocket("ws://www.example.com/server.php");
var message = {
    time: new Date(),
    text: "Hello world!",
    clientId: "asdfp8734rew"
};
socket.send(JSON.stringify(message));   //发送数据-转字符串
```
接收数据：
```js
socket.onmessage = function(event){       //接收事件
    var data = event.data;   //返回数据
    //处理数据               //同样是字符串，需要手动解析
};
```

#### 21.5.5.3 其他事件
其他三个事件
 open：在成功建立连接时触发。
 error：在发生错误时触发，连接不能持续。
 close：在连接关闭时触发。
不支持DOM2事件监听，只能用DOM0事件
```js
var socket = new WebSocket("ws://www.example.com/server.php");
socket.onopen = function(){
    alert("Connection established.");
};
socket.onerror = function(){
    alert("Connection error.");
};
socket.onclose = function(){
    alert("Connection closed.");
};
```
这三个事件的额外属性
`wasClean` 布尔值，连接是否已经关闭
`code` 返回数值状态码
`reason` 服务器发回的消息
```js
socket.onclose = function(event){
    console.log("Was clean? " + event.wasClean + " Code=" + event.code + " Reason="
    + event.reason);
};
```

### 21.5.6 SSE与Web Sockets
需要考虑的问题：
1：是否有支持Web Sockets的服务器
2：是否一定要双向通信

## 21.6 安全性
CSRF: 跨站点伪造，未授权系统伪装自己，让处理请求的服务器认为它是合法的
XSS: 跨站点脚本
验证发送者是否有权限访问的几种方式：
 要求以 SSL 连接来访问可以通过XHR 请求的资源。
 要求每一次请求都要附带经过相应算法计算得到的验证码。

下列措施对防范CSRF 攻击不起作用。
 要求发送 POST 而不是GET 请求——很容易改变。
 检查来源 URL 以确定是否可信——来源记录很容易伪造。
 基于 cookie 信息进行验证——同样很容易伪造。

# 22 高级技巧
## 22.1 高级函数
### 22.1.1 安全的类型检测
typeof、instanceof等等判断都会有一些不可靠
在任何值上调用Object 原生的toString()方法，都会返回一个\[object NativeConstructorName]格式的字符串。
通过每个类的内部都有一个\[\[Class]]属性，这个属性就指定了上述字符串中的构造函数名。
例：
```js
function isArray(value){
    return Object.prototype.toString.call(value) == "[object Array]";
}
function isFunction(value){
    return Object.prototype.toString.call(value) == "[object Function]";
}
function isRegExp(value){
    return Object.prototype.toString.call(value) == "[object RegExp]";
}
var isNativeJSON = window.JSON && Object.prototype.toString.call(JSON) == "[object JSON]";   //判断是否是源生JSON
```

### 22.1.2 作用域安全的构造函数
就是当不用new调用构造函数的时候，this指向window，导致window原有属性被修改
解决办法
```js
function Polygon(sides){    //作用域安全
    if (this instanceof Polygon) {      //进行 作用域安全 处理
        this.sides = sides;
        this.getArea = function(){
            return 0;
        };
    } else {
        return new Polygon(sides);
    }
}

function Rectangle(width, height){   //作用域不安全
    Polygon.call(this, 2);        //本身作用域不安全，通过继承将导致访问不到继承父级
    this.width = width;
    this.height = height;
    this.getArea = function(){
        return this.width * this.height;
    };
}

Rectangle.prototype = new Polygon();    //解决继承访问不到父级

var rect = new Rectangle(5, 10);
alert(rect.sides);   //2

```

### 22.1.3 惰性载入函数
有两种方法，根本上都是赋值重写
方法一：重写函数
```js
function createXHR(){
    if (typeof XMLHttpRequest != "undefined"){
        createXHR = function(){           //重写
            return new XMLHttpRequest();
        };
    } else if (typeof ActiveXObject != "undefined"){
        createXHR = function(){                       //重写
            if (typeof arguments.callee.activeXString != "string"){
                var versions = ["MSXML2.XMLHttp.6.0", "MSXML2.XMLHttp.3.0",
                                "MSXML2.XMLHttp"],
                    i, len;
        
                for (i=0,len=versions.length; i < len; i++){
                    try {
                        new ActiveXObject(versions[i]);
                        arguments.callee.activeXString = versions[i];
                    } catch (ex){
                        //skip
                    }
                }
            }
        
            return new ActiveXObject(arguments.callee.activeXString);
        };
    } else {
        createXHR = function(){       //重写
            throw new Error("No XHR object available.");
        };
    }
    
    return createXHR();
}
```
方法2:赋值到一个变量里
```js
var createXHR = (function(){     //赋值到变量createXHR  后边是个自执行行函数
    if (typeof XMLHttpRequest != "undefined"){
        return function(){                   //返回情况1
            return new XMLHttpRequest();
        };
    } else if (typeof ActiveXObject != "undefined"){
        return function(){                    //返回情况2         
            if (typeof arguments.callee.activeXString != "string"){
                var versions = ["MSXML2.XMLHttp.6.0", "MSXML2.XMLHttp.3.0",
                                "MSXML2.XMLHttp"],
                    i, len;
        
                for (i=0,len=versions.length; i < len; i++){
                    try {
                        new ActiveXObject(versions[i]);
                        arguments.callee.activeXString = versions[i];
                        break;
                    } catch (ex){
                        //skip
                    }
                }
            }
        
            return new ActiveXObject(arguments.callee.activeXString);    //返回情况3
        };
    } else {
        return function(){
            throw new Error("No XHR object available.");
        };
    }
})();
```

### 22.1.4函数绑定
主要目的就是处理this丢失问题
```js
function bind(fn, context){      //bind方法--主要是通过闭包来完成的保护作用域
            return function(){
                return fn.apply(context, arguments);
            };
        }
    
        var handler = {
            message: "Event handled",
        
            handleClick: function(event){
                alert(this.message + ":" + event.type);    //如果不通过绑定的话，这个this就会指向btn，btn是没有message的，所以就是undefined了
            }
        };
        
        var btn = document.getElementById("my-btn");
        EventUtil.addHandler(btn, "click", bind(handler.handleClick, handler));
```
**HTML5出了bind()方法**
```js
//用法
EventUtil.addHandler(btn, "click", handler.handleClick.bind(handler));
```

### 22.1.5 函数柯里化
允许我们把函数与传递给它的参数相结合，产生出一个新的函数。
```js
//只是让curry第一个参数为方法，第二个为参数，然后再给curriedAdd设置各种参数，会自动添加到curry第二个参数后边
function curry(fn){
    var args = Array.prototype.slice.call(arguments, 1);    //5
    return function(){
        var innerArgs = Array.prototype.slice.call(arguments),  //3
            finalArgs = args.concat(innerArgs);
        return fn.apply(null, finalArgs);
    };
}

function add(num1, num2){
    return num1 + num2;
}

var curriedAdd = curry(add, 5);
alert(curriedAdd(3));   //8
```
```js
function bind(fn, context){
    var args = Array.prototype.slice.call(arguments, 2);
    return function(){
        var innerArgs = Array.prototype.slice.call(arguments),
            finalArgs = args.concat(innerArgs);
        return fn.apply(context, finalArgs);
    };
}

var handler = {
    message: "Event handled",

    handleClick: function(name, event){
        alert(this.message + ":" + name + ":" + event.type);
    }
};

var btn = document.getElementById("my-btn");
EventUtil.addHandler(btn, "click", bind(handler.handleClick, handler, "my-btn"));
```
HTML5的finde()也实现函数柯里化
```js
var handler = {
    message: "Event handled",

    handleClick: function(name, event){
        alert(this.message + ":" + name + ":" + event.type);
    }
};

var btn = document.getElementById("my-btn");
EventUtil.addHandler(btn, "click", handler.handleClick.bind(handler, "my-btn"));

```
**主要用于动态函数创建**，一般用于复杂的算法和功能
（我觉得可能是用在迭代里）

## 22.2 防篡改对象
方法一：可以通过第六章里讲的手工设置属性来设置
`[[Configurable]]` `[[Writable]]` `[[Enumerable]]` `[[Value]]` `Get` `Set`
方法二：ES5增加了几个方法
**对象定义为防篡改，就无法撤销了**

### 22.2.1 不可扩展对象
`Object.preventExtensions()` 不能再给对象添加属性和方法
`Object.istExtensible()`确定对象是否可以扩展
```js
var person = { name: "Nicholas" };
alert(Object.isExtensible(person)); //true    可扩展
Object.preventExtensions(person);              //禁用扩展
alert(Object.isExtensible(person)); //false    不可扩展
```

### 22.2.2 密封的对象
ES5定义的第二个保护级别是密封对象。
`Object.seal()`密封对象的方法
`Object.isSealed()`确定对象是否密封了
密封对象不可扩展，**且以后成员的Configurable将被设置为false**，所以不能再用`Object.defineProperty()`来修改属性
```js
var person = { name: "Nicholas" };
alert(Object.isExtensible(person)); //true  可扩展
alert(Object.isSealed(person)); //false     没有密封
Object.seal(person);                         //进行密封
alert(Object.isExtensible(person)); //false  不可扩展
alert(Object.isSealed(person)); //true       已密封
```

### 22.2.3 冻结的对象
**最严格**的防篡改级别是冻结对象。
`Object.freeze`冻结对象方法
`Object.ifFrozen`确定是否冻结
不可扩展，密封，而且\[\[Writable]]被设置为false
如果设置\[\[Set]]函数，访问其属性仍然是可写的
```js
var person = { name: "Nicholas" };
alert(Object.isExtensible(person)); //true   可扩展
alert(Object.isSealed(person)); //false    没有密封
alert(Object.isFrozen(person)); //false    没有冻结
Object.freeze(person);
alert(Object.isExtensible(person)); //false   不可扩展
alert(Object.isSealed(person)); //true        已密封
alert(Object.isFrozen(person)); //true        已冻结
```

## 22.3 高级定时器
`setTimeout()` `setInterval()`指定的事件间隔表示何时添加到队列，而不是何时执行代码

### 22.3.1 重复的定时器
`setInterval()`会在没有该定时器的任何其他代码实例时，才将定时器代码添加到队列中，这样可以避免还没有执行完，另一端定时器程序就运行了。
问题：
1.某些间隔会被跳过
2.多个定时器的代码执行之间的间隔可能比预期小
![](/images/chongfudsq.png)
解决这2个问题：
使用链式setTimeout()调用
```js
setTimeout(function(){
    //处理中
    setTimeout(arguments.callee, interval);
}, interval);
```
### 22.3.2 Yielding Processes
避免长时间脚本运行
长时间运行原因：
1.过长、过深的嵌套函数
2.大量处理的循环
当运用大量循环的时候应考虑：
1.是否必须同步完成
2.是否必须按序排列

如果上边的问题是“否”，可**使用定时器分割这个循环**，这种技术叫**数组分块**。
```js
var data = [12,123,1234,453,436,23,23,5,4123,45,346,5634,2234,345,342];

function chunk(array, process, context){    //★主要是这个函数
    setTimeout(function(){
        var item = array.shift();
        process.call(context, item);
        
        if (array.length > 0){
            setTimeout(arguments.callee, 100);         
        }
    }, 100);        
}

function printValue(item){
    var div = document.getElementById("myDiv");
    div.innerHTML += item + "<br>";        
}

chunk(data, printValue);
```
chunk()方法有三个参数：要处理的项目的数组（待办事宜）+处理项目的函数+可选的运行该函数的环境

### 22.3.3 函数节流
基本思想：某些代码不可以在**没有间断**的情况连续重复执行。（导致崩溃）
方法一：限制最小执行时间间隔
方法二：用调用次数做节流，但要考虑最后一次调用需要执行
方法三：第一次调用创建一个定时器，第二次调用该函数时，清除前一次定时器。
**setTimeout()中用到的函数的环境总是window**
```js
function throttle(method, scope) {
    clearTimeout(method.tId);
    method.tId= setTimeout(function(){
        method.call(scope);
    }, 100);
}
```
`throttle()`节流方法
用处：一般在resize事件的时候用
例：
```js
function throttle(method, scope) {
    clearTimeout(method.tId);
    method.tId= setTimeout(function(){
        method.call(scope);
    }, 100);
}

function resizeDiv(){    //执行函数
    var div = document.getElementById("myDiv");
    div.style.height = div.offsetWidth + "px";
}

window.onresize = function(){    //resize事件触发执行函数-通过节流来避免多次执行
    throttle(resizeDiv);
};
```
## 22.4 自定义事件
观察者模式由两类对象组成：主体和观察者。
自定义事件原理：创建一个管理事件的对象，让其他对象监听那些事件。
```js
function EventTarget(){
    this.handlers = {};    
}

EventTarget.prototype = {
    constructor: EventTarget,

    addHandler: function(type, handler){
        if (typeof this.handlers[type] == "undefined"){
            this.handlers[type] = [];
        }

        this.handlers[type].push(handler);
    },
    
    fire: function(event){
        if (!event.target){
            event.target = this;
        }
        if (this.handlers[event.type] instanceof Array){
            var handlers = this.handlers[event.type];
            for (var i=0, len=handlers.length; i < len; i++){
                handlers[i](event);
            }
        }            
    },

    removeHandler: function(type, handler){
        if (this.handlers[type] instanceof Array){
            var handlers = this.handlers[type];
            for (var i=0, len=handlers.length; i < len; i++){
                if (handlers[i] === handler){
                    break;
                }
            }
            
            handlers.splice(i, 1);
        }            
    }
};
```
使用方法：
```js
function handleMessage(event){
    alert("Message received: " + event.message);
}
//创建一个新对象
var target = new EventTarget();
//添加一个事件处理程序
target.addHandler("message", handleMessage);
//触发事件
target.fire({ type: "message", message: "Hello world!"});
//删除事件处理程序
target.removeHandler("message", handleMessage);
//再次，应没有处理程序
target.fire({ type: "message", message: "Hello world!"});
```

# 23 离线应用与客户端存储
## 23.1 离线检测
检测设备是否在线
`navigator.onLine`为true表示设备能上网，false表示设备离线
```js
if (navigator.onLine){
    //正常工作
    } else {
    //执行离线状态时的任务
}
```
离线在线切换两个事件：`online` `offline`

## 23.2 应用缓存
应用缓存appcache
描述文件（manifest file）
文件可分为三个部分：
CACHE- 在此标题下列出的文件将在首次下载后进行缓存
NETWORK – 在此标题下列出的文件需要与服务器的连接，且不会被缓存
FALLBACK – 在此标题下列出的文件规定当页面无法访问时的回退页面（比如 404 页面）
位置在apache/conf/mime.types
```js
CACHE MANIFEST
# 2012-02-21 v1.0.0

CACHE:        //加载后对theme.css,logo.gif,main.js进行离线缓存
/theme.css
/logo.gif
/main.js

NETWORK:      //对login.php文件不进行缓存，如果用*代替，就是所有文件都不缓存，都要走联网
login.php
*             //这个*表示所有文件除了上边定义缓存的文件

FALLBACK:     //如果无法建立网络连接，则跳转到offline.html这个网址，可以是404错误
/html/ /offline.html
```
页面引入：
```html
<html manifest="/manifest.appcache">
```
更新缓存方法：
可以给manifest文件加时间注释，如果时间**注释被改变**，则被重新加载更新，注释用#开头

这个配置文件的MIME类型必须是text/cache-manifest
核心是`applicationCache`对象，这个对象有一个status属性，属性值有：
 0：无缓存，即没有与页面相关的应用缓存。
 1：闲置，即应用缓存未得到更新。
 2：检查中，即正在下载描述文件并检查更新。
 3：下载中，即应用缓存正在下载描述文件中指定的资源。
 4：更新完成，即应用缓存已经更新了资源，而且所有资源都已下载完毕，可以通过swapCache()来使用了。
 5：废弃，即应用缓存的描述文件已经不存在了，因此页面无法再访问应用缓存。

相关事件：从上至下顺序执行
 checking：在浏览器为应用缓存查找更新时触发。
 error：在检查更新或下载资源期间发生错误时触发。
 noupdate：在检查描述文件发现文件无变化时触发。
 downloading：在开始下载应用缓存资源时触发。
 progress：在文件下载应用缓存的过程中持续不断地触发。
 updateready：在页面新的应用缓存下载完毕且可以通过swapCache()使用时触发。
 cached：在应用缓存完整可用时触发。
`update()`手工干预更新
`swapCache()`启用新应用缓存
```js
//手动检查更新，触发checking事件
applicationCache.update();

//updateready事件触发swapCache()
EventUtil.addHandler(applicationCache, "updateready", function(){
    applicationCache.swapCache();
});
```

## 23.3 数据存储
### 23.3.1 Cookie
服务器对任意HTTP请求发送Set-Cookie，其中包含会话信息
```js
//服务器响应头
HTTP/1.1 200 OK
Content-type: text/html
Set-Cookie: name=value
Other-header: other-header-value
```
```js
//浏览器请求头添加Cookie信息发回服务器
GET /index.html HTTP/1.1
Cookie: name=value
Other-header: other-header-value
```
可以用于验证客户来自于发送的哪个请求
### 23.3.1.1 限制
绑定在特定的域名下，设定一个cookie后，给创建它的域名发送请求的时候，会**一直带着**这个cookie，且无法被其他域访问
IE6及更低版本不会最多20个，超出的话，会清除之前创建的cookie（具体删哪个看浏览器）
cookie尺寸限制在4095B（含4095），超出的话会被丢掉整个cookie

### 23.3.1.2 cookie的构成
以下几块信息构成：
名称：不区分大小写，最好区分，因为cookie名称必须经过URL编码的
值：储存在cookie字符串值中，值必须被URL编码
域：如果是www.a.com就对这个域起作用，如果是a.com则对所有这个域的子域也有效
路径：你可以指定cookie 只有从http://www.wrox.com/books/ 中才能访问，那么http://www.wrox.com 的页面就不会发送cookie 信息，即使请求都是来自同一个域的。
失效时间：何时应该停止向服务器发送这个cookie，默认会话结束就删除，也可以设置GMT日期
安全标识：cookie只有使用SSL连接的时候才发送到服务器。只能通过https发送，不能通过http发送

Set-Cookie使用**分号加空格**分隔每一段
```js
HTTP/1.1 200 OK
Content-type: text/html
Set-Cookie: name=value; expires=Mon, 22-Jan-07 07:10:24 GMT; domain=.wrox.com
Other-header: other-header-value
```
`secure` 标志是cookie 中唯一一个非名值对儿的部分，直接包含一个secure 单词。
**因为设置了secure 标志，这个cookie 只能通过SSL 连接才能传输**
```js
HTTP/1.1 200 OK
Content-type: text/html
Set-Cookie: name=value; domain=.wrox.com; path=/; secure
Other-header: other-header-value
```

### 23.3.1.3 Javascript中的cookie
`document.cookie`返回当前页面可用的所有cookie的字符串
例：name1=value1;name2=value2;name3=value3
都是经过URL编码的，所以必须使用`decodeURIComponent()`来解码
`document.cookie`也可以设置cookie，设置的字符串会被解释并**添加**到cookie集合中，并不会覆盖，除非设置的名称已经存在。
例：
```js
document.cookie = encodeURIComponent("name") + "=" +
encodeURIComponent("Nicholas") + "; domain=.wrox.com; path=/";   //直接在后边添加就行了
```
封装cookie方法-读取/写入/删除：
```js
var CookieUtil = {

    get: function (name){
        var cookieName = encodeURIComponent(name) + "=",
            cookieStart = document.cookie.indexOf(cookieName),
            cookieValue = null,
            cookieEnd;
            
        if (cookieStart > -1){
            cookieEnd = document.cookie.indexOf(";", cookieStart);
            if (cookieEnd == -1){
                cookieEnd = document.cookie.length;
            }
            cookieValue = decodeURIComponent(document.cookie.substring(cookieStart + cookieName.length, cookieEnd));
        } 

        return cookieValue;
    },
    
    set: function (name, value, expires, path, domain, secure) {
        var cookieText = encodeURIComponent(name) + "=" + encodeURIComponent(value);
    
        if (expires instanceof Date) {
            cookieText += "; expires=" + expires.toGMTString();  //转化为GMT时间
        }
    
        if (path) {
            cookieText += "; path=" + path;
        }
    
        if (domain) {
            cookieText += "; domain=" + domain;
        }
    
        if (secure) {
            cookieText += "; secure";
        }
    
        document.cookie = cookieText;
    },
    
    unset: function (name, path, domain, secure){
        this.set(name, "", new Date(0), path, domain, secure);
    }

};
```
用法：
```js
//设置cookie
CookieUtil.set("name", "Nicholas");
CookieUtil.set("book", "Professional JavaScript");
//读取cookie 的值
alert(CookieUtil.get("name")); //"Nicholas"
alert(CookieUtil.get("book")); //"Professional JavaScript"
//删除cookie
CookieUtil.unset("name");
CookieUtil.unset("book");
//设置cookie，包括它的路径、域、失效日期
CookieUtil.set("name", "Nicholas", "/books/projs/", "www.wrox.com",
new Date("January 1, 2010"));
//删除刚刚设置的cookie
CookieUtil.unset("name", "/books/projs/", "www.wrox.com");
//设置安全的cookie
CookieUtil.set("name", "Nicholas", null, null, null, true);
```

### 23.3.1.4 子cookie
绕开浏览器的单域名下的cookie数限制，也就是利用cookie值来存储多个名值对儿。。
格式如下：
name=name1=value1&name2=value2&name3=value3&name4=value4&name5=value5

```js
var SubCookieUtil = {

    get: function (name, subName){
        var subCookies = this.getAll(name);
        if (subCookies){
            return subCookies[subName];
        } else {
            return null;
        }
    },
    
    getAll: function(name){
        var cookieName = encodeURIComponent(name) + "=",
            cookieStart = document.cookie.indexOf(cookieName),
            cookieValue = null,
            cookieEnd,
            subCookies,
            i,
            parts,
            result = {};
            
        if (cookieStart > -1){
            cookieEnd = document.cookie.indexOf(";", cookieStart)
            if (cookieEnd == -1){
                cookieEnd = document.cookie.length;
            }
            cookieValue = document.cookie.substring(cookieStart + cookieName.length, cookieEnd);
            
            if (cookieValue.length > 0){
                subCookies = cookieValue.split("&");
                
                for (i=0, len=subCookies.length; i < len; i++){
                    parts = subCookies[i].split("=");
                    result[decodeURIComponent(parts[0])] = decodeURIComponent(parts[1]);
                }
    
                return result;
            }  
        } 

        return null;
    },
    
    set: function (name, subName, value, expires, path, domain, secure) {
    
        var subcookies = this.getAll(name) || {};
        subcookies[subName] = value;
        this.setAll(name, subcookies, expires, path, domain, secure);

    },
    
    setAll: function(name, subcookies, expires, path, domain, secure){
    
        var cookieText = encodeURIComponent(name) + "=",
            subcookieParts = new Array(),
            subName;
        
        for (subName in subcookies){
            if (subName.length > 0 && subcookies.hasOwnProperty(subName)){
                subcookieParts.push(encodeURIComponent(subName) + "=" + encodeURIComponent(subcookies[subName]));
            }
        }
        
        if (subcookieParts.length > 0){
            cookieText += subcookieParts.join("&");
                
            if (expires instanceof Date) {
                cookieText += "; expires=" + expires.toGMTString();
            }
        
            if (path) {
                cookieText += "; path=" + path;
            }
        
            if (domain) {
                cookieText += "; domain=" + domain;
            }
        
            if (secure) {
                cookieText += "; secure";
            }
        } else {
            cookieText += "; expires=" + (new Date(0)).toGMTString();
        }
    
        document.cookie = cookieText;        
    
    },
    
    unset: function (name, subName, path, domain, secure){
        var subcookies = this.getAll(name);
        if (subcookies){
            delete subcookies[subName];
            this.setAll(name, subcookies, null, path, domain, secure);
        }
    },
    
    unsetAll: function(name, path, domain, secure){
        this.setAll(name, null, new Date(0), path, domain, secure);
    }

};
```
读取用法：
```js
//假设document.cookie=data=name=Nicholas&book=Professional%20JavaScript
//取得全部子cookie
var data = SubCookieUtil.getAll("data");
alert(data.name); //"Nicholas"
alert(data.book); //"Professional JavaScript"
//逐个获取子cookie
alert(SubCookieUtil.get("data", "name")); //"Nicholas"
alert(SubCookieUtil.get("data", "book")); //"Professional JavaScript"
```
设置用法：
```js
//假设document.cookie=data=name=Nicholas&book=Professional%20JavaScript
//设置两个cookie
SubCookieUtil.set("data", "name", "Nicholas");
SubCookieUtil.set("data", "book", "Professional JavaScript");
//设置全部子cookie 和失效日期
SubCookieUtil.setAll("data", { name: "Nicholas", book: "Professional JavaScript" },
new Date("January 1, 2010"));
//修改名字的值，并修改cookie 的失效日期
SubCookieUtil.set("data", "name", "Michael", new Date("February 1, 2010"));
```
删除用法：
```js
//仅删除名为name 的子cookie
SubCookieUtil.unset("data", "name");
//删除整个cookie
SubCookieUtil.unsetAll("data");
```
#### 23.3.1.5 关于cookie的思考
还有一类cookie成为"HTTP专有cookie"，可以从服务器和浏览器设置，但是只能服务器读取。
由于cookie作为请求头发送，如果存储大量数据，完成服务器请求时间也会变长，影响性能

### 23.3.2 IE用户数据
通过getAttribute和setAttribute来存储读取数据

### 23.3.3 Web存储机制
保存在客户端，无须持续的将数据发回服务器。
#### 23.3.3.1 Storage 类型
Storage类型提供最大的存储空间来存储名值对儿，方法有
 clear()： 删除所有值；Firefox 中没有实现。
 getItem(name)：根据指定的名字name 获取对应的值。
 key(index)：获得index 位置处的值的名字。
 removeItem(name)：删除由name 指定的名值对儿。
 setItem(name, value)：为指定的name 设置一个对应的值。
无法判断数据大小，但是可以使用`length`判断有多少

#### 23.3.3.2 sessionStorage对象
浏览器关闭后消失，可以跨页面刷新而存在
有的浏览器，在崩溃恢复的时候也存在
因为是绑定服务器的对话，所以在本地运行的时候是不可用的，且只能由最初页面访问，此时不能多页面访问
存储方法：
```js
//使用方法存储数据
sessionStorage.setItem("name", "Nicholas");
//使用属性存储数据
sessionStorage.book = "Professional JavaScript";
```
Firefox 和WebKit 实现了同步写入，IE是异步写入
读取方法：
```js
//使用方法读取数据
var name = sessionStorage.getItem("name");
//使用属性读取数据
var book = sessionStorage.book;
```
还可以迭代，通过`length`和`key()`方法
```js
for (i=0, len = sessionStorage.length; i < len; i++){
    key = sessionStorage.key(i);
    value = sessionStorage.getItem(key);
    alert(key + "=" + value);
} 
```
还可以通过`for-in`进行迭代
```js
for(key in sessionStorage){
    var value =  sessionStorage.getItem(key);
    alert(key + "=" value);
}
```
删除方法：
```js
//使用 delete 删除一个值——在 WebKit 中无效
delete sessionStorage.name;
//使用方法删除一个值
sessionStorage.removeItem("book");
```
#### 23.3.3.3 globalStorage 对象
一直保存在客户端，除非客户删除
跨越会话访问，**要指定哪些域可以访问(包括子域)**该数据。通过方括号来实现
globalStorage对象不是 Storage 的实例，而具体的 globalStorage\["wrox.com"] 才是，但是所有的属性却都是Storage实例。
```js
//保存数据
globalStorage["wrox.com"].name = "Nicholas";
//获取数据
var name = globalStorage["wrox.com"].name;
```
对globalStorage空间的访问，依据发起请求的页面的域名+协议+端口号来限制。
使用方法：
```js
globalStorage["www.wrox.com"].name = "Nicholas";
globalStorage["www.wrox.com"].book = "Professional JavaScript";
globalStorage["www.wrox.com"].removeItem("name");
var book = globalStorage["www.wrox.com"].getItem("book");
```
**如果你事先不能确定域名，那么使用 location.host 作为属性名比较安全**
```js
globalStorage[location.host].name = "Nicholas";
var book = globalStorage[location.host].getItem("book");
```

#### 23.3.3.4 localStorage对象
为了取代globalStorage。
区别：不能给localStorage指定访问规则。
必须同一个域名，子域名无效+同一个协议+同一个端口
localStorage 是 Storage 的实例
像使用 sessionStorage 一样来使用它
兼容globalStorage写法：
```js
function getLocalStorage(){
    if (typeof localStorage == "object"){
        return localStorage;
    } else if (typeof globalStorage == "object"){
        return globalStorage[location.host];
    } else {
        throw new Error("Local storage not available.");
    }
}
```
#### 23.3.3.5 storage事件
对`Storage`对象任何修改，都会在文档上触发`storage`事件
事件属性
 domain ：发生变化的存储空间的域名。
 key ：设置或者删除的键名。
 newValue ：如果是设置值，则是新值；如果是删除键，则是 null 。
 oldValue ：键被更改之前的值。
```js
EventUtil.addHandler(document, "storage", function(event){
    alert("Storage changed for " + event.domain);
});
```
#### 23.3.3.6 限制
每个来源（协议、域和端口）都有固定大小的空间用于保存自己的数据。
`localStorage` 而言，大多数桌面浏览器会设置每个来源 5MB 的限制。
Chrome 和 Safari 对每个来源的限制是 2.5MB。
iOS 版 Safari 和 Android 版 WebKit 的限制也是 2.5MB。
`sessionStorage` 有的浏览器对 sessionStorage 的大小没有限制，
Chrome、Safari、iOS 版 Safari 和 Android 版 WebKit 都有限制，也都是 2.5MB。
IE8+和 Opera 对sessionStorage 的限制是 5MB。

### 23.3.4 IndexedDB
通常没有大小限制，超过50M会提示框询问是否增加大小
P643

## 23.4 补充
### 23.4.1 浏览器缓存
按F5刷新浏览器和在地址栏里输入网址然后回车。 这两个行为是不一样的。
按F5刷新浏览器， 浏览器会去Web服务器验证缓存。
如果是在地址栏输入网址然后回车，浏览器会”直接使用有效的缓存”, 而不会发http request 去服务器验证缓存，这种情况叫做缓存命中
如果需要在html页面上设置不缓存，这在`<head>`标签中加入如下语句：
```html
<meta http-equiv="pragma" content="no-cache">
<meta http-equiv="cache-control" content="no-cache">
<meta http-equiv="expires" content="0"> 
```
Request:
Cache-Control: max-age=0	以秒为单位
If-Modified-Since: Mon, 19 Nov 2012 08:38:01 GMT	缓存文件的最后修改时间。
If-None-Match: “0693f67a67cc1:0”	缓存文件的Etag值
Cache-Control: no-cache	不使用缓存
Pragma: no-cache	不使用缓存
 
Response:
Cache-Control: public	响应被缓存，并且在多用户间共享，  （公有缓存和私有缓存的区别，请看另一节）
Cache-Control: private	响应只能作为私有缓存，不能在用户之间共享
Cache-Control:no-cache	提醒浏览器要从服务器提取文档进行验证
Cache-Control:no-store	绝对禁止缓存（用于机密，敏感文件）
Cache-Control: max-age=60	60秒之后缓存过期（相对时间）
Date: Mon, 19 Nov 2012 08:39:00 GMT	当前response发送的时间
Expires: Mon, 19 Nov 2012 08:40:01 GMT	缓存过期的时间（绝对时间）
Last-Modified: Mon, 19 Nov 2012 08:38:01 GMT	服务器端文件的最后修改时间
ETag: “20b1add7ec1cd1:0”	服务器端文件的Etag值
 
属性说明：
Cache-Control的主要参数 Cache-Control: private/public Public 响应会被缓存，并且在多用户间共享。 Private 响应只能够作为私有的缓存，不能再用户间共享。
Cache-Control: no-cache：不进行缓存
Cache-Control: max-age=x：缓存时间 以秒为单位
Cache-Control: must-revalidate：如果页面是过期的 则去服务器进行获取。
Expires：显示的设置页面过期时间
Last-Modified：请求对象最后一次的修改时间 用来判断缓存是否过期 通常由服务器上文件的时间信息产生。
If-Modified-Since ：客户端发送请求附带的信息 指浏览器缓存请求对象的最后修改日期 用来和服务器端的Last-Modified做比较。
Etag：ETag是一个可以 与Web资源关联的记号（token），和Last-Modified功能才不多，也是一个标识符，一般和Last-Modified一起使用，加强服务器判断的准确度。


浏览器缓存机制，其实主要就是HTTP协议定义的缓存机制（如： Expires； Cache-control等）。但是也有非HTTP协议定义的缓存机制，如使用HTML Meta 标签，Web开发者可以在HTML页面的`<head>`节点中加入`<meta>`标签，代码如下：
![](/images/0064cTs2jw1eyk0s2j3ktj30gg01bjr6.jpg)


上述代码的作用是告诉浏览器当前页面不被缓存，每次访问都需要去服务器拉取。使用上很简单，但只有部分浏览器可以支持，而且所有缓存代理服务器都不支持，因为代理不解析HTML内容本身。

下面我主要介绍HTTP协议定义的缓存机制。

**Expires策略**
Expires是Web服务器响应消息头字段，在响应http请求时告诉浏览器在过期时间前浏览器可以直接从浏览器缓存取数据，而无需再次请求。

下面是宝宝PK项目中，浏览器拉取jquery.js web服务器的响应头：
![](/images/0064cTs2jw1eyk0rf60znj309f09gwek.jpg)


注：Date头域表示消息发送的时间，时间的描述格式由rfc822定义。例如，Date: Mon,31 Dec 2001 04:25:57GMT。

Web服务器告诉浏览器在2012-11-28 03:30:01这个时间点之前，可以使用缓存文件。发送请求的时间是2012-11-28 03:25:01，即缓存5分钟。

不过Expires 是HTTP 1.0的东西，现在默认浏览器均默认使用HTTP 1.1，所以它的作用基本忽略。

**Cache-control策略（重点关注）**
Cache-Control与Expires的作用一致，都是指明当前资源的有效期，控制浏览器是否直接从浏览器缓存取数据还是重新发请求到服务器取数据。只不过Cache-Control的选择更多，设置更细致，如果同时设置的话，其优先级高于Expires。
![](/images/0064cTs2jw1eyk0s2vs8oj30gh08d3z5.jpg)


还是上面那个请求，web服务器返回的Cache-Control头的值为max-age=300，即5分钟（和上面的Expires时间一致，这个不是必须的）。
![](/images/0064cTs2jw1eyk0rficdhj308h05lwef.jpg)


1. Last-Modified/If-Modified-Since
Last-Modified/If-Modified-Since要配合Cache-Control使用。

Last-Modified：标示这个响应资源的最后修改时间。web服务器在响应请求时，告诉浏览器资源的最后修改时间。

If-Modified-Since：当资源过期时（使用Cache-Control标识的max-age），发现资源具有Last-Modified声明，则再次向web服务器请求时带上头 If-Modified-Since，表示请求时间。web服务器收到请求后发现有头If-Modified-Since 则与被请求资源的最后修改时间进行比对。若最后修改时间较新，说明资源又被改动过，则响应整片资源内容（写在响应消息包体内），HTTP 200；若最后修改时间较旧，说明资源无新修改，则响应HTTP 304 (无需包体，节省浏览)，告知浏览器继续使用所保存的cache。

2. Etag/If-None-Match
Etag/If-None-Match也要配合Cache-Control使用。

Etag：web服务器响应请求时，告诉浏览器当前资源在服务器的唯一标识（生成规则由服务器觉得）。Apache中，ETag的值，默认是对文件的**索引节（INode），大小（Size）和最后修改时间（MTime）**进行Hash后得到的。

If-None-Match：当资源过期时（使用Cache-Control标识的max-age），发现资源具有Etage声明，则再次向web服务器请求时带上头If-None-Match （Etag的值）。web服务器收到请求后发现有头If-None-Match 则与被请求资源的相应校验串进行比对，决定返回200或304。

3. 既生Last-Modified何生Etag？
你可能会觉得使用Last-Modified已经足以让浏览器知道本地的缓存副本是否足够新，为什么还需要Etag（实体标识）呢？
HTTP1.1中Etag的出现主要是为了解决几个Last-Modified比较难解决的问题：

Last-Modified标注的最后修改只能精确到秒级，如果某些文件在**1秒内，被修改多次**的话，它将不能准确标注文件的修改时间

如果某些文件会被**定期生成**，Last-Modified改变了，但**内容却没有变化**，导致文件没法使用缓存

有可能存在服务器没有准确获取文件修改时间，或者与代理服务器**时间不一致**等情形

Etag是服务器自动生成或者由开发者生成的对应资源在服务器端的唯一标识符，能够更加准确的控制缓存。
Last-Modified与ETag是可以一起使用的，服务器会**优先验证**ETag，一致的情况下，才会继续比对Last-Modified，最后才决定是否返回304。

用户行为与缓存
浏览器缓存行为还有用户的行为有关！！！
![](/images/0064cTs2jw1eyk0vbifjfj30ht04qmx5.jpg)

总结

浏览器第一次请求：
![](/images/0064cTs2jw1eyk0rfqki2j30bf0a9t8z.jpg)

浏览器再次请求时：
![](/images/0064cTs2jw1eyk0rg6jlgj30fe0eoq3s.jpg)

# 24.最佳实践
## 24.1可维护性
### 24.1.1什么是可维护的代码
 可理解性——其他人可以接手代码并理解它的意图和一般途径，而无需原开发人员的完整解释。
 直观性——代码中的东西一看就能明白，不管其操作过程多么复杂。
 可适应性——代码以一种数据上的变化不要求完全重写的方法撰写。
 可扩展性——在代码架构上已考虑到在未来允许对核心功能进行扩展。
 可调试性——当有地方出错时，代码可以给予你足够的信息来尽可能直接地确定问题所在。

### 24.1.2 代码约定
#### 24.1.2.1 可读性
1. 缩进
2. 注释-以下内容需要注释
 函数和方法
 大段代码
 复杂的算法
 Hack

#### 24.1.2.2 变量和函数名
 变量名应为名词如car 或person。
 函数名应该以动词开始，如getName()。返回布尔类型值的函数一般以is 开头，如isEnable()。
 变量和函数都应使用合乎逻辑的名字，不要担心长度。

#### 24.1.2.3 变量类型透明
避免忘记变量包含的数据类型

1. 初始化-最开始初始化为一个值
```js
//通过初始化指定变量类型
var found = false; //布尔型
var count = -1; //数字
var name = ""; //字符串
var person = null; //对象
```
2. 使用匈牙利标记法
"o"代表对象
"s"代表字符串
"i"代表整数
"f"代表浮点数
"b"代表布尔型
```js
//用于指定数据类型的匈牙利标记法
var bFound; //布尔型
var iCount; //整数
var sName; //字符串
var oPerson; //对象
```
3. 类型注释
```js
//用于指定类型的类型注释
var found /*:Boolean*/ = false;
var count /*:int*/ = 10;
var name /*:String*/ = "Nicholas";
var person /*:Object*/ = null;
```
缺点：块级注释会错误

### 24.1.3 松散耦合
只要应用的某个部分过分依赖于另一部分，代码就是耦合过紧，难于维护

1. 解耦HTML/JavaScript
事件/通过js插入html
2. 解耦CSS/JavaScript
避免用style，改用className
3. 解耦应用逻辑／事件处理程序
通过调用函数来进行分离
```js
//分离开，让a是a，不要写成一个函数
function a(){};
function b(){a()}
```
 勿将 event 对象传给其他方法；只传来自event 对象中所需的数据；
 任何可以在应用层面的动作都应该可以在不执行任何事件处理程序的情况下进行；
 任何事件处理程序都应该处理事件，然后将处理转交给应用逻辑。

### 24.1.4 编程实践
#### 24.1.4.1 尊重对象所有权
不要修改不属于你的对象
 不要为实例或原型添加属性；
 不要为实例或原型添加方法；
 不要重定义已存在的方法。

#### 24.1.4.2 避免全局变量
可以定义一个对象，扩充自己的属性和方法
```js
//创建全局对象
var Wrox = {};
//为 Professional JavaScript 创建命名空间
Wrox.ProJS = {};
//将书中用到的对象附加上去
Wrox.ProJS.EventUtil = { ... };
Wrox.ProJS.CookieUtil = { ... };
```
#### 24.1.4.3 避免与null比较
不要和null比较，改用其他的比较

#### 24.1.4.4 使用常量
将常量抽取出来，改为变量
```js
var Constants = {
    INVALID_VALUE_MSG: "Invalid value!",
    INVALID_VALUE_URL: "/errors/invalid.php"
};
function validate(value){
    if (!value){
        alert(Constants.INVALID_VALUE_MSG);
        location.href = Constants.INVALID_VALUE_URL;
    }
}
```
 重复值——任何在多处用到的值都应抽取为一个常量。这就限制了当一个值变了而另一个没变的时候会造成的错误。这也包含了CSS 类名。
 用户界面字符串—— 任何用于显示给用户的字符串，都应被抽取出来以方便国际化。
 URLs —— 在 Web 应用中，资源位置很容易变更，所以推荐用一个公共地方存放所有的URL。
 任意可能会更改的值—— 每当你在用到字面量值的时候，你都要问一下自己这个值在未来是不是会变化。如果答案是“是”，那么这个值就应该被提取出来作为一个常量。

## 24.2 性能
### 24.2.1 注意作用域
#### 24.2.1.1 避免全局查找
```js
function updateUI(){
    //将document存在doc变量中，避免反复查询全局变量
    var doc = document;
    var imgs = doc.getElementsByTagName("img");
    for (var i=0, len=imgs.length; i < len; i++){
        imgs[i].title = doc.title + " image " + i;
    }
    var msg = doc.getElementById("msg");
    msg.innerHTML = "Update complete.";
}
```

#### 24.2.1.2 避免with语句
with会修改作用域链的长度

### 24.2.2 选择正确方法
#### 24.2.2.1 避免不必要的属性查找
算法的复杂度是使用O 符号来表示的。最简单、最快捷的算法是常数值即O(1)。
![](/images/fuzadu.png)
![排序算法比较](img/sort-compare.png)
例如，请看以下代码：
```js
var query = window.location.href.substring(window.location.href.indexOf("?"));
```
在这段代码中，有6 次属性查找：
window.location.href.substring()有3 次，
window.location.href.indexOf()又有3 次。
只要**数一数代码中的点的数量**，就可以确定属性查找的次数了。
这段代码由于两次用到了window.location.href，同样的查找进行了两次，因此效率特别不好。
应该将其存储在局部变量中。第一次访问该值会是O(n)，然而后续的访问都会是O(1)，就会节省很多。

#### 24.2.2.2 优化循环
(1) 减值迭代——大多数循环使用一个从0 开始、增加到某个特定值的迭代器。在很多情况下，从最大值开始，在循环中不断减值的迭代器更加高效。
(2) 简化终止条件——由于每次循环过程都会计算终止条件，所以必须保证它尽可能快。也就是说避免属性查找或其他O(n)的操作。
(3) 简化循环体——循环体是执行最多的，所以要确保其被最大限度地优化。确保没有某些可以被很容易移出循环的密集计算。
(4) 使用后测试循环——最常用for 循环和while 循环都是前测试循环。而如do-while 这种后测试循环，可以避免最初终止条件的计算，因此运行更快。
```js
//原始
for (var i=0; i < values.length; i++){
    process(values[i]);
}
//优化一：减值迭代
for (var i=values.length -1; i >= 0; i--){
    process(values[i]);
}
//优化二：终止条件和自减操作组合，后测试
var i=values.length -1;
if (i > -1){
    do {
        process(values[i]);
    }while(--i >= 0);
}
```

#### 24.2.2.3 展开循环
当循环的次数是确定的，消除循环并使用多次函数调用往往更快。
```js
//消除循环--次数少所以代替for循环
process(values[0]);
process(values[1]);
process(values[2]);
```
Duff装置--8倍例子
```js
//更新前
//credit: Jeff Greenberg for JS implementation of Duff’s Device
//假设 values.length > 0
var iterations = Math.ceil(values.length / 8);
var startAt = values.length % 8;
var i = 0;
do {
    switch(startAt){
        case 0: process(values[i++]);
        case 7: process(values[i++]);
        case 6: process(values[i++]);
        case 5: process(values[i++]);
        case 4: process(values[i++]);
        case 3: process(values[i++]);    //后边没有return的话，会把下边两项也执行，不管case值
        case 2: process(values[i++]);
        case 1: process(values[i++]);
    }
    startAt = 0;
} while (--iterations > 0);
//更新后的-快40%
//credit: Speed Up Your Site (New Riders, 2003)
var iterations = Math.floor(values.length / 8);
var leftover = values.length % 8;
var i = 0;
if (leftover > 0){
    do {                                   //不管别的，先运行一次process()
        process(values[i++]);
    } while (--leftover > 0);              //为2和1时，上边又运行了两次
}
do {                                       //不管判断，先运行8次
    process(values[i++]);
    process(values[i++]);
    process(values[i++]);
    process(values[i++]);
    process(values[i++]);
    process(values[i++]);
    process(values[i++]);
    process(values[i++]);                  
} while (--iterations > 0);

```
#### 24.2.2.4 避免双重解释
代码在字符串内，js在启动时候，必须要再启动一个解析器来解析新的代码
例：
```js
//某些代码求值——避免!!
eval("alert('Hello world!')");
//创建新函数——避免!!
var sayHi = new Function("alert('Hello world!')");
//设置超时——避免!!
setTimeout("alert('Hello world!')", 500);
```
修改：
```js
//已修正
alert('Hello world!');
//创建新函数——已修正
var sayHi = function(){
alert('Hello world!');
};
//设置一个超时——已修正
setTimeout(function(){
alert('Hello world!');
}, 500);
```

#### 24.2.2.5 性能的其他注意事项
 原生方法较快
 Switch 语句较快
 位运算符较快

### 24.2.3 最小化语句块
#### 24.2.3.1 多个变量声明
用一个var定义
```js
//一个语句
var count = 5,
    color = "blue",
    values = [1,2,3],
    now = new Date();
```

#### 24.2.3.2 插入迭代值
当使用迭代值（也就是在不同的位置进行增加或减少的值）的时候，尽可能合并语句。
```js
//优化前
var name = values[i];
i++;
//优化后
var name = values[i++];
```
#### 24.2.3.3 使用数组和对象字面量
//只用一条语句创建和初始化数组/对象
```js
var values = \[123, 456, 789];
```
### 24.2.4 优化DOM交互
#### 24.2.4.1 最小化现场更新
方法一：先将列表从页面上移除，最后一并添加进去
缺点：有可能会出现闪烁现象
方法二：使用文档片段构造DOM结构，然后添加到List
```js
var list = document.getElementById("myList"),
    fragment = document.createDocumentFragment(),   //★创建文档片段
    item,
    i;
for (i=0; i < 10; i++) {
    item = document.createElement("li");
    fragment.appendChild(item);
    item.appendChild(document.createTextNode("Item " + i));
}
list.appendChild(fragment);
```

#### 24.2.4.2 使用innerHTML
前边的例子改写：
```js
var list = document.getElementById("myList"),
    html = "",
    i;
for (i=0; i < 10; i++) {
    html += "<li>Item " + i + "</li>";
}
list.innerHTML = html;
```

#### 24.2.4.3 使用事件代理
第13章 事件委托

#### 24.2.4.4 注意HTMLCollection
每次访问HTMLCollection都会消耗大量内存
解决：将返回来的数据**存到变量中**
以下情况时会返回HTMLCollection 对象：
 进行了对 getElementsByTagName() 的调用；
 获取了元素的childNodes 属性；
 获取了元素的attributes 属性；
 访问了特殊的集合，如document.forms、document.images 等。

## 24.3 部署
### 24.3.1 构建过程
合并文件
 知识产权问题—— 如果把带有完整注释的代码放到线上，那别人就更容易知道你的意图，对它再利用，并且可能找到安全漏洞。
 文件大小 —— 书写代码要保证容易阅读，才能更好地维护，但是这对于性能是不利的。浏览器并不能从额外的空白字符或者是冗长的函数名和变量名中获得什么好处。
 代码组织 —— 组织代码要考虑到可维护性并不一定是传送给浏览器的最好方式。基于这些原因，最好给JavaScript 文件定义一个构建过程。

### 24.3.2 验证
JSLint检查语法

### 24.3.3 压缩
1. 文件压缩
压缩器一般进行如下一些步骤：
 删除额外的空白（包括换行）；
 删除所有注释；
 缩短变量名。

2. HTTP压缩
gzip压缩