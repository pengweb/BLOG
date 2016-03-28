---
title: javascript高级程序设计---笔记
date: 2016-03-20 14:12:30
tags: [javascript,笔记,note,js]

---
3.4.1 typeof没总结

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
typeof(正则表达式)   //function  因为内部实现[[Call]]方法的对象都返回function

instanceof判断引用类型，返回值为`true`和`false`
person instanceof Object  //判断是不是对象
Array
RegExp
Function

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

`splice`可以实现`插入``删除``替换`
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
每个函数都含有两个非继承而来的的方法`apply()``call()`.
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
`charAt()``charCodeAt()`访问字符串中特定字符的方法.
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
`indexOf()``lastIndexOf()` 查找字符串位置，只能得到**第一个**出现的位置
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
`undefined``NaN``Infinity``Object``Array``Function``Boolean``String``Number``Date``RegExp``Error``EvalError``RangeError``ReferenceError``SyntaxError``TypeError``URIError`

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
>工厂模式虽然解决了创建多个相似对象的问题，但却没有解决对象识别的问题（即怎么知道一个对象的类型）。

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
    SuperType.call(this, name);              //借用构造函数-继承       第二次调用SuperType()，创建实例
    
    this.age = age;
}

SubType.prototype = new SuperType();         //原型链-继承             第一次调用SuperType()，创建实例
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

//原型式继承--浅复制
function object(o){
    function F(){}
    F.prototype = o;
    return new F();
}

//原型链继承--下边这个和SubType.prototype = new SuperType();是一个意思，下边这么写的意思是为了避免多次创建SuperType()的实例
function inheritPrototype(subType, superType){
    var prototype = object(superType.prototype);   //create object
    prototype.constructor = subType;               //augment object
    subType.prototype = prototype;                 //assign object
}
                        
function SuperType(name){
    this.name = name;
    this.colors = ["red", "blue", "green"];
}

SuperType.prototype.sayName = function(){
    alert(this.name);
};

//借用构造函数
function SubType(name, age){  
    SuperType.call(this, name);
    
    this.age = age;
}

inheritPrototype(SubType, SuperType);

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
