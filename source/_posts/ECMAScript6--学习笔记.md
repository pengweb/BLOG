---
title: ECMAScript6--学习笔记
date: 2016-04-11 09:58:05
tags: [js,javascript,es6,ecmascript6,note]

---
# 1.let、const和块级作用域
## 1.1 let 命令
1. 只在`let`命令所在的**代码块内**有效。
2. for循环内用let声明，类似于bind(),当前循环有效
```js
var a = [];
for (let i = 0; i < 10; i++) {
  a[i] = function () {
    console.log(i);
  };
}
a[6](); // 6
```
3. 不存在变量提升
4. 暂时性死区：在作用域内let声明，则不再受外部的影响(内部也不会提升的)
5. 暂时性死区的 `typeof` 有可能不存在，如果let在typeof之后
6. 函数参数默认值也存在**死区**
7. 不允许重复声明，重复声明会报错--因此不能在**函数内部**再次声明参数，除非再增加一个块级作用域{}

## 1.2 块级作用域
1. 一个`{}`代表一个块级作用域
2. if语句的{}也是一个块级作用域，所以它不再影响外部变量
3. 外层也访问不到内层作用域
4. 块级作用域就可以替代自执行函数
5. 块级作用域的外部不能调用块级作用域内部定义的**函数**，函数声明不再提升，不过可以通过下边这样处理
```js
let f;
{
  let a = 'secret';
  f = function () {
    return a;
  }
}
f() // "secret"
```
6. ES5在if这种语句内声明函数是会报错的，但是ES6就会将语句的{}视为块级作用域，所以内部再定义函数就不会报错了

## 1.3 const命令
1. const也用来声明变量，但是声明的是常量。
2. 一旦声明，常量的值就**不能改变**--后边不可以再进行赋值或改变指针（但可以改变属性）
3. 可以通过`Object.freeze()`方法来进行冻结，冻结后就不可以改变属性了-仅仅只是对象本身冻结

## 1.4 跨模块常量
```js
// constants.js 模块
export const A = 1;
export const B = 3;
export const C = 4;

// test1.js 模块
import * as constants from './constants';    //方法一
console.log(constants.A); // 1
console.log(constants.B); // 3

// test2.js 模块
import {A, B} from './constants';             //方法二
console.log(A); // 1
console.log(B); // 3
```

## 1.5 全局对象属性
1. var命令和function命令声明的全局变量，依旧是全局对象的属性；
2. let命令、const命令、class命令声明的全局变量，不属于全局对象的属性。
3. `window.` 和不带标识符的声明，仍是全局变量

# 2.变量的解构赋值
如果右边不是`undefined`则为右边的值，如果为undefined，就可以取到左边的赋值
## 2.1 数组和解构赋值
### 2.1.1 基本用法
```js
let [foo, [[bar], baz]] = [1, [[2], 3]];
foo // 1
bar // 2
baz // 3

let [ , , third] = ["foo", "bar", "baz"];
third // "baz"

let [x, , y] = [1, 2, 3];
x // 1
y // 3

let [head, ...tail] = [1, 2, 3, 4];
head // 1
tail // [2, 3, 4]

let [x, y, ...z] = ['a'];
x // "a"
y // undefined
z // []

var [foo] = []; 
foo // undefined

var [bar, foo] = [1];
foo // undefined

let [x, y] = [1, 2, 3];
x // 1
y // 2

let [a, [b], d] = [1, [2, 3], 4];
a // 1
b // 2
d // 4

let [x, y, z] = new Set(["a", "b", "c"])  //对于Set结构，也可以使用数组的解构赋值。
x // "a"

```
### 2.1.2 默认值
```js

[x, y = 'b'] = ['a'] // x='a', y='b'
[x, y = 'b'] = ['a', undefined] // x='a', y='b' 右边如果不是undefined的话随便是一个数的话，那结果就是这个数，而不是前边的赋值

var [x = 1] = [null];   //因为后边不是undefined，所以结果不是1，而是null
x // null

let [x = 1, y = x] = [];     // x=1; y=1   y=x的默认值x在前边已经声明过了，所以可以取到
let [x = y, y = 1] = [];     // ReferenceError   x=y的默认值y还没有被声明，所以报错

```
 
## 2.2 对象的解构赋值
数组按顺序，但对象不是
```js
var { bar, foo } = { foo: "aaa", bar: "bbb" };
foo // "aaa"
bar // "bbb"

var { baz } = { foo: "aaa", bar: "bbb" };
baz // undefined

var { foo: baz } = { foo: "aaa", bar: "bbb" };
baz // "aaa"

let obj = { first: 'hello', last: 'world' };
let { first: f, last: l } = obj;
f // 'hello'
l // 'world'

var { foo: baz } = { foo: "aaa", bar: "bbb" };   //真正被赋值的是变量baz，而不是模式foo。
baz // "aaa"
foo // error: foo is not defined

let foo;
let {foo} = {foo: 1}; // SyntaxError: Duplicate declaration "foo"   //声明过的不能再声明

let baz;
({bar: baz} = {bar: 1}); // 成功  没有let

var node = {
  loc: {
    start: {
      line: 1,
      column: 5
    }
  }
};

var { loc: { start: { line }} } = node;
line // 1        只有line是变量，loc和start都是模式
loc  // error: loc is undefined
start // error: start is undefined

let obj = {};
let arr = [];

({ foo: obj.prop, bar: arr[0] } = { foo: 123, bar: true });

obj // {prop:123}
arr // [true]

// 报错
var {foo: {bar}} = {baz: 'baz'}   //此时foo是undefined  所以foo.bar 就会报错了

// 错误的写法
var x;
{x} = {x: 1};    //前边没有声明，会认为{}是一个代码块，而发生错误
// SyntaxError: syntax error
// 正确的写法
({x} = {x: 1});          //必须全括起来，而不仅仅是前边

let { log, sin, cos } = Math;    //可以很方便地将现有对象的方法，赋值到某个变量。
```

## 2.3字符串的解构赋值
```js
const [a, b, c, d, e] = 'hello';
a // "h"
b // "e"
c // "l"
d // "l"
e // "o"

let {length : len} = 'hello';
len // 5
```

## 2.4 数值和布尔值的解构赋值
先转化为对象
```js
let {toString: s} = 123;
s === Number.prototype.toString // true

let {toString: s} = true;
s === Boolean.prototype.toString // true

//下边无法转化为对象，报错
let { prop: x } = undefined; // TypeError
let { prop: y } = null; // TypeError
```

## 2.5 函数参数为解构赋值
```js
function add([x, y]){
  return x + y;
}

add([1, 2]) // 3

function move({x = 0, y = 0} = {}) {
  return [x, y];
}

move({x: 3, y: 8}); // [3, 8]
move({x: 3}); // [3, 0]
move({}); // [0, 0]
move(); // [0, 0]

function move({x, y} = { x: 0, y: 0 }) {    //为参数指定默认值，而不是为x和y
  return [x, y];
}

move({x: 3, y: 8}); // [3, 8]
move({x: 3}); // [3, undefined]
move({}); // [undefined, undefined]
move(); // [0, 0]

[1, undefined, 3].map((x = 'yes') => x)
// [ 1, 'yes', 3 ]
```
## 2.6 圆括号问题
只要有可能导致解构的歧义，就不得使用圆括号，所以只要有可能，就不要在模式中放置圆括号。
非模式才不会报错**前边不要加声明var/let/conse**

## 2.7 用途
### 2.7.1 交换变量
```js
[x, y] = [y, x];
```
### 2.7.2 从函数返回多个值--一一对应
```js
// 返回一个数组

function example() {
  return [1, 2, 3];
}
var [a, b, c] = example();

// 返回一个对象

function example() {
  return {
    foo: 1,
    bar: 2
  };
}
var { foo, bar } = example();
```

### 2.7.3 函数参数的定义
```js
// 参数是一组有次序的值
function f([x, y, z]) { ... }
f([1, 2, 3])

// 参数是一组无次序的值
function f({x, y, z}) { ... }
f({z: 3, y: 2, x: 1})
```

### 2.7.4 提取JSON数据
```js
var jsonData = {
  id: 42,
  status: "OK",
  data: [867, 5309]
}

let { id, status, data: number } = jsonData;

console.log(id, status, number)
// 42, "OK", [867, 5309]
```

### 2.7.5 函数参数的默认值
```js
//避免了在函数体内部再写var foo = config.foo || 'default foo';这样的语句。
jQuery.ajax = function (url, {
  async = true,
  beforeSend = function () {},
  cache = true,
  complete = function () {},
  crossDomain = false,
  global = true,
  // ... more config
}) {
  // ... do stuff
};
```

### 2.7.6 遍历Map结构
```js
//任何部署了Iterator接口的对象，都可以用for...of循环遍历
var map = new Map();
map.set('first', 'hello');
map.set('second', 'world');

for (let [key, value] of map) {
  console.log(key + " is " + value);
}
// first is hello
// second is world

// 获取键名
for (let [key] of map) {
  // ...
}

// 获取键值
for (let [,value] of map) {
  // ...
}
```

### 2.7.7 输入模块的指定方法
```js
const { SourceMapConsumer, SourceNode } = require("source-map");
```

# 3. 字符串的扩展
## 3.1 字符的Unicode表示法
6中表示方法
```js
'\z' === 'z'  // true
'\172' === 'z' // true
'\x7A' === 'z' // true
'\u007A' === 'z' // true
'\u{7A}' === 'z' // true     ES6新方法
```

ES5 charAt()                //返回索引值：无法返回𠮷的值
ES5 charCodeAt()            //返回编码
ES5 String.fromCharCode()   //返回编码的实际字符

ES6 at()                    //返回索引值：可以返回𠮷的值
ES6 codePointAt()           //返回编码
ES6 String.fromCodePoint()  //返回编码的实际字符

for-of 遍历接口
```js
for (let codePoint of 'foo') {
  console.log(codePoint)
}
// "f"
// "o"
// "o"
```

## 3.6 normalize()
强调重音符号，两种方法，这两者是相等的，但是js识别
Ǒ（\u01D1）
O（\u004F）和ˇ（\u030C）合成Ǒ（\u004F\u030C）
```js
'\u01D1'.normalize() === '\u004F\u030C'.normalize()
// true
```
- NFC  合成
- NFD  分解
- NFKC
- NFKD
```js
'\u004F\u030C'.normalize('NFC').length // 1
'\u004F\u030C'.normalize('NFD').length // 2
```

## 3.7 includes(),startsWith(),endsWith()
`includes()`：返回布尔值，表示是否找到了参数字符串。
`startsWith()`：返回布尔值，表示参数字符串是否在源字符串的头部。
`endsWith()`：返回布尔值，表示参数字符串是否在源字符串的尾部。
```js
var s = 'Hello world!';

s.startsWith('Hello') // true
s.endsWith('!') // true
s.includes('o') // true
s.startsWith('world', 6) // true    第二个参数代表开始搜索的位置
```

## 3.8 repeat()
repeat方法返回一个新字符串，表示将原字符串重复n次。
```js
'x'.repeat(3)            // "xxx"
'hello'.repeat(2)        // "hellohello"
'na'.repeat(0)           // ""
'na'.repeat(2.9)         // "nana"   取整
'na'.repeat(Infinity)    // RangeError
'na'.repeat(-1)          // RangeError
'na'.repeat(-0.9)        // ""    0到-1之间的都取0
'na'.repeat(NaN)         // ""    NAN等同于0
'na'.repeat('na')        // ""     先转成数字
'na'.repeat('3')         // "nanana"     先转成数字

```

## 3.9 padStart()，padEnd()
ES7推出了字符串补全长度的功能。

```js
'x'.padStart(5, 'ab') // 'ababx'
'x'.padStart(4, 'ab') // 'abax'
'x'.padEnd(5, 'ab') // 'xabab'
'x'.padEnd(4, 'ab') // 'xaba'
'xxx'.padStart(2, 'ab') // 'xxx' 如果原字符串的长度，等于或大于指定的最小长度，则返回原字符串。
'xxx'.padEnd(2, 'ab') // 'xxx'   如果原字符串的长度，等于或大于指定的最小长度，则返回原字符串。
'abc'.padStart(10, '0123456789')   // '0123456abc'  超出从后边截取补全字符
'x'.padStart(4) // '   x'   如果省略第二个参数，则会用空格补全长度。
'x'.padEnd(4) // 'x   '     如果省略第二个参数，则会用空格补全长度。
```

## 3.10 模板字符串
原来模板写法
```js
$("#result").append(
  "There are <b>" + basket.count + "</b> " +
  "items in your basket, " +
  "<em>" + basket.onSale +
  "</em> are on sale!"
);
```
ES6写法
```js
$("#result").append(`     //这里有个反引号
  There are <b>${basket.count}</b> items
   in your basket, <em>${basket.onSale}</em>
  are on sale!
`);                  //这里也有个反引号
```
```js
// 普通字符串
`In JavaScript '\n' is a line-feed.`

// 多行字符串-- 所有的空格和缩进都会被保留在输出之中。
`In JavaScript this is
 not legal.`

//如果需要使用反引号，则前面要用反斜杠转义。
var greeting = `\`Yo\` World!`;

// ★字符串中嵌入变量--将变量名写在${}之中,括号内可以进行运算，同时也可以调用函数
//如果大括号内不是字符，通过toString来转换
var name = "Bob", time = "today";
`Hello ${name}, how are you ${time}?`

//如果需要引用模板字符串本身，可以像下面这样写。
// 写法一
let str = 'return ' + '`Hello ${name}!`';
let func = new Function('name', str);
func('Jack') // "Hello Jack!"

// 写法二
let str = '(name) => `Hello ${name}!`';
let func = eval.call(null, str);
func('Jack') // "Hello Jack!"
```

## 3.11 实例：模板编译
## 3.12 标签模板
```js
var a = 5;
var b = 10;
tag`Hello ${ a + b } world ${ a * b }`;
//tag函数的第一个参数是一个数组，该数组的成员是模板字符串中那些没有变量替换的部分
tag(['Hello ', ' world ', ''], 15, 50)
```

13. String.raw()
String.raw方法，往往用来充当模板字符串的处理函数，返回一个斜杠都被转义（即斜杠前面再加一个斜杠）的字符串，对应于替换变量后的模板字符串。
```js
String.raw`Hi\n${2+3}!`;
// "Hi\\n5!"

String.raw`Hi\u000A!`;
// 'Hi\\u000A!'

String.raw`Hi\\n`      //原式已经带了\就不会再添加了
// "Hi\\n"

//作为函数使用时---一般很少用于函数
String.raw({ raw: 'test' }, 0, 1, 2);
// 't0e1s2t'

// 等同于
String.raw({ raw: ['t','e','s','t'] }, 0, 1, 2);
```

# 5.正则的扩展
总结在正则表达式--学习笔记内

# 6.数值的扩展
## 6.1 二进制和八进制表示法
ES6提供了二进制和八进制数值的新的写法，分别用前缀0b（或0B）和0o（或0O）表示。
ES5的严格模式中，八进制就不再允许使用前缀0表示了。但是非严格模式还是可以的
转换为十进制用`Number()`方法
```js
Number('0b111')  // 7
Number('0o10')  // 8
```

## 6.2 Number.isFinite(), Number.isNaN()
`Number.isFinite()`检查是否**非无穷**
```js
Number.isFinite(15); // true
Number.isFinite(0.8); // true
Number.isFinite(NaN); // false
Number.isFinite(Infinity); // false
Number.isFinite(-Infinity); // false
Number.isFinite('foo'); // false
Number.isFinite('15'); // false
Number.isFinite(true); // false
```
`Number.isNaN()`用来检查一个值是否为NaN。
```js
Number.isNaN(NaN) // true
Number.isNaN(15) // false
Number.isNaN('15') // false
Number.isNaN(true) // false
Number.isNaN(9/NaN) // true
Number.isNaN('true'/0) // true
Number.isNaN('true'/'true') // true
```
它们与传统的全局方法`isFinite()`和`isNaN()`的区别在于他们**不转化**，只对数值判断
```js
isFinite(25) // true
isFinite("25") // true
Number.isFinite(25) // true
Number.isFinite("25") // false

isNaN(NaN) // true
isNaN("NaN") // true
Number.isNaN(NaN) // true
Number.isNaN("NaN") // false
```

## 6.3 Number.parseInt(), Number.parseFloat()
ES6将全局方法parseInt()和parseFloat()，移植到Number对象上面，行为**完全保持不变**。

## 6.4 Number.isInteger()
Number.isInteger()用来判断一个值是否为整数。
*注意：在JavaScript内部，整数和浮点数是同样的储存方法，所以3和3.0被视为同一个值*
```js
Number.isInteger(25) // true
Number.isInteger(25.0) // true
Number.isInteger(25.1) // false
Number.isInteger("15") // false
Number.isInteger(true) // false
```
## 6.5 Number.EPSILON
ES6在Number对象上面，新增一个极小的常量`Number.EPSILON`
Js浮点计算是不精确的，但是如果这个误差能够小于Number.EPSILON，我们就可以认为得到了正确结果。
```js
Number.EPSILON
// 2.220446049250313e-16
Number.EPSILON.toFixed(20)
// '0.00000000000000022204'
```

## 6.6 安全整数和Number.isSafeInteger()
JavaScript能够准确表示的整数范围在-2^53到2^53之间（不含两个端点），超过这个范围，无法精确表示这个值。
```js
Math.pow(2, 53) === Math.pow(2, 53) + 1           //超过这个值得值都会转化为这个值
// true
```
ES6引入了`Number.MAX_SAFE_INTEGER`和`Number.MIN_SAFE_INTEGER`这两个常量，用来表示这个范围的上下限。
```js
Number.MAX_SAFE_INTEGER === Math.pow(2, 53) - 1
// true
Number.MAX_SAFE_INTEGER === 9007199254740991     //超过这个值得值都会转化为这个值
// true
```
`Number.isSafeInteger()`则是用来判断一个整数是否落在这个范围之内。
```js
Number.isSafeInteger('a') // false
Number.isSafeInteger(null) // false
Number.isSafeInteger(NaN) // false
Number.isSafeInteger(Infinity) // false
Number.isSafeInteger(-Infinity) // false

Number.isSafeInteger(3) // true
Number.isSafeInteger(1.2) // false
Number.isSafeInteger(9007199254740990) // true
Number.isSafeInteger(9007199254740992) // false
```

## 6.7 Math扩展的方法
Math.trunc方法用于去除一个数的小数部分，返回整数部分。
Math.sign方法用来判断一个数到底是正数、负数、还是零。
Math.cbrt方法用于计算一个数的立方根。
Math.clz32方法返回一个数的32位无符号整数形式有多少个前导0。
Math.imul方法返回两个数以32位带符号整数形式相乘的结果，返回的也是一个32位的带符号整数。
Math.fround方法返回一个数的单精度浮点数形式。
Math.hypot方法返回所有参数的平方和相加的平方根。例：3的平方加上4的平方，等于5的平方。
对数方法：
Math.expm1(x)返回ex - 1，即Math.exp(x) - 1。
Math.log1p(x)方法返回1 + x的自然对数，即Math.log(1 + x)。如果x小于-1，返回NaN。
Math.log10(x)返回以10为底的x的对数。如果x小于0，则返回NaN。
Math.log2(x)返回以2为底的x的对数。如果x小于0，则返回NaN。
三角函数：
Math.sinh(x) 返回x的双曲正弦（hyperbolic sine）
Math.cosh(x) 返回x的双曲余弦（hyperbolic cosine）
Math.tanh(x) 返回x的双曲正切（hyperbolic tangent）
Math.asinh(x) 返回x的反双曲正弦（inverse hyperbolic sine）
Math.acosh(x) 返回x的反双曲余弦（inverse hyperbolic cosine）
Math.atanh(x) 返回x的反双曲正切（inverse hyperbolic tangent）

## 6.8 指数运算
ES7新增了一个指数运算符`**`
```js
2 ** 2 // 4
2 ** 3 // 8

let b = 3;
b **= 3;
// 等同于 b = b * b * b;
```

# 7.数组的扩展
## 7.1 Array.from()
Array.from方法用于将两类对象转为真正的数组：
**类数组**的对象（array-like object）和
**可遍历**（iterable）的对象（包括ES6新增的数据结构Set和Map）
```js
let arrayLike = {
    '0': 'a',
    '1': 'b',
    '2': 'c',
    length: 3
};
//ES5写法
var arr1 = [].slice.apply(arrayLike) // ['a', 'b', 'c']
// ES6的写法
let arr2 = Array.from(arrayLike); // ['a', 'b', 'c']
```
可以用在**NodeList对象**和**arguments对象**上
也可以用在**字符串**上和其他**Iterator**接口的数据结构上
`...`ye也有同样的效果--在函数对象有详细介绍
```js
// arguments对象
var args = [...arguments];
// NodeList对象
var nodeList = [...document.querySelectorAll('div')]
```
任何有`length`属性的对象，都可以通过Array.from方法转为数组
如果成员为定义，则为`undefined`
```js
Array.from({ length: 3 });
// [ undefined, undefined, undefinded ]
```
Array.from还可以接受第二个参数，作用类似于数组的`map`方法，用来对每个元素进行处理，将处理后的值放入返回的数组。
```js
Array.from(arrayLike, x => x * x);
// 等同于
Array.from(arrayLike).map(x => x * x);

Array.from([1, 2, 3], (x) => x * x)
// [1, 4, 9]
```
如果map函数里面用到了this关键字，还可以传入Array.from的**第三个参数**，用来绑定this。
Array.from()的另一个应用是，将**字符串转为数组**，然后返回字符串的长度。因为它能正确处理各Unicode字符，可以避免JavaScript将**大于\uFFFF的Unicode字符**，算作两个字符的bug。

## 7.2 Array.of()
Array.of方法用于将一组值，转换为数组。
**完全可以替代**Array()方法
```js
Array.of(3, 11, 8) // [3,11,8]
Array.of(3) // [3]

//老方法
Array(3) // [, , ,]     会有歧义不方便
Array(3, 11, 8) // [3, 11, 8]
```
## 7.3 数组实例的copyWithin()
数组实例的copyWithin方法，在当前数组内部，将指定位置的成员复制到其他位置（会覆盖原有成员），然后返回当前数组。
三个参数：copyWithin(target, start = 0, end = this.length)
target（必需）：从该位置开始替换数据。
start（可选）：从该位置开始读取数据，默认为0。如果为负值，表示倒数。
end（可选）：到该位置前停止读取数据，默认等于数组长度。如果为负值，表示倒数。
```js
[1, 2, 3, 4, 5].copyWithin(0, 3)
// [4, 5, 3, 4, 5]
```

## 7.4 数组实例的find()和findIndex()
数组实例的`find()`方法，用于找出第一个符合条件的数组成员。如果没有符合条件的成员，则返回`undefined`。
```js
[1, 4, -5, 10].find((n) => n < 0)
// -5
```
find()方法的回调函数可以接受三个参数，依次为**当前的值+当前的位置+原数组**。
```js
[1, 5, 10, 15].find(function(value, index, arr) {
  return value > 9;
}) // 10
```
`findIndex()`方法的用法与find方法非常类似，返回第一个符合条件的数组成员的**位置**，如果所有成员都不符合条件，则返回**-1**。
```js
[1, 5, 10, 15].findIndex(function(value, index, arr) {
  return value > 9;
}) // 2   只是位置
```
这两个方法都可以接受**第二个参数**，用来绑定回调函数的`this`对象。
弥补indexOf()方法不能发现`NAN`的不足，上边两个方法都可以发现
```js
[NaN].indexOf(NaN)
// -1

[NaN].findIndex(y => Object.is(NaN, y))
// 0
```

## 7.5 数组实例的fill()
fill方法使用给定值，填充一个数组。
但是**数组中已有的元素，会被全部抹去。**
```js
['a', 'b', 'c'].fill(7)
// [7, 7, 7]

new Array(3).fill(7)
// [7, 7, 7]
```
fill方法还可以接受第二个和第三个参数，用于指定填充的起始位置和结束位置。
```js
['a', 'b', 'c'].fill(7, 1, 2)
// ['a', 7, 'c']
```

## 7.6 数组实例的entries()，keys()和values()
ES6提供三个新的方法——entries()，keys()和values()——用于**遍历数组**。
同样可以用for...of循环进行遍历，唯一的区别是keys()是对**键名**的遍历、values()是对**键值**的遍历，entries()是对**键值对**的遍历。
```js
for (let index of ['a', 'b'].keys()) {
  console.log(index);
}
// 0
// 1

for (let elem of ['a', 'b'].values()) {
  console.log(elem);
}
// 'a'
// 'b'

for (let [index, elem] of ['a', 'b'].entries()) {
  console.log(index, elem);
}
// 0 "a"
// 1 "b"
```
如果不使用`for...of`循环，可以手动调用遍历器对象的`next`方法，进行遍历。
```js
let letter = ['a', 'b', 'c'];
let entries = letter.entries();
console.log(entries.next().value); // [0, 'a']
console.log(entries.next().value); // [1, 'b']
console.log(entries.next().value); // [2, 'c']
```

## 7.7 数组实例的includes()
Array.prototype.includes方法返回一个布尔值，表示某个数组是否包含给定的值，与字符串的includes方法类似。
```js
[1, 2, 3].includes(2);     // true
[1, 2, 3].includes(4);     // false
[1, 2, NaN].includes(NaN); // true
```
该方法的**第二个参数**表示搜索的起始位置，默认为0。
```js
[1, 2, 3].includes(3, 3);  // false
[1, 2, 3].includes(3, -1); // true 
//如果第二个参数大于总长度，则从0开始
```
indexOf内部使用严格相当运算符（===）进行判断，这会导致对NaN的误判。但是includes不会
**与Map和Set**的 `has`的区别
Map结构的has方法，是用来查找键名的
Set结构的has方法，是用来查找值的

## 7.8 数组的空位
数组的空位指，数组的某一个位置没有任何值。
空位**不是**`undefined`,空位没有任何值
```js
Array(3) // [, , ,]
0 in [undefined, undefined, undefined] // true  undefined代表有值
0 in [, , ,] // false    没有值的
```
ES5对空位的处理：
forEach(), filter(), every() 和some()都会跳过空位。
map()会跳过空位，但会保留这个值
join()和toString()会将空位视为undefined，而undefined和null会被处理成空字符串。
```js
// forEach方法
[,'a'].forEach((x,i) => log(i)); // 1

// filter方法
['a',,'b'].filter(x => true) // ['a','b']

// every方法
[,'a'].every(x => x==='a') // true

// some方法
[,'a'].some(x => x !== 'a') // false

// map方法
[,'a'].map(x => 1) // [,1]

// join方法
[,'a',undefined,null].join('#') // "#a##"

// toString方法
[,'a',undefined,null].toString() // ",a,,"
```
ES6则**明确将空位转为undefined**,所以在操作方法的时候，空位都**不会被忽略**
`Array.from`方法会**将数组的空位，转为undefined**
`entries()`、`keys()`、`values()`、`find()`和`findIndex()`会将空位处理成undefined。
由于空位的处理规则非常不统一，所以建议**避免出现空位**。

## 7.9 数组推导
数组推导（array comprehension）提供简洁写法，允许直接**通过现有数组生成新数组**。
```js
var a1 = [1, 2, 3, 4];
var a2 = [for (i of a1) i * 2];

a2 // [2, 4, 6, 8]
```
数组推导中，`for...of`结构总是写在**最前面**，返回的**表达式**写在最后面。
for...of后面还可以附加`if`语句，用来设定循环的限制条件。
**可以多个if连用**,if后可以加`{}`
```js
var years = [ 1954, 1974, 1990, 2006, 2010, 2014 ];
[for (year of years) if (year > 2000) if(year < 2010) year];
// [ 2006]
```
还可以使用多个`for-of`结构，构成多重循环
```js
var a1 = ['x1', 'y1'];
var a2 = ['x2', 'y2'];
var a3 = ['x3', 'y3'];

[for (s of a1) for (w of a2) for (r of a3) console.log(s + w + r)];
// x1x2x3
// x1x2y3
// x1y2x3
// x1y2y3
// y1x2x3
// y1x2y3
// y1y2x3
// y1y2y3
```
*数组推导的方括号构成了一个单独的作用域，在这个方括号中声明的变量类似于使用let语句声明的变量。*
**字符串**可以视为数组，因此字符串也可以直接用于数组推导。
*新数组会立即在内存中生成。这时，如果原数组是一个很大的数组，将会非常耗费内存。*

# 8.函数的扩展
## 8.1 函数参数的默认值
### 8.1.1 基本用法
ES6允许为函数的参数设置默认值，即直接写在参数定义的后面。
```js
function log(x, y = 'World') {
  console.log(x, y);
}

log('Hello') // Hello World
log('Hello', 'China') // Hello China
log('Hello', '') // Hello  如果不赋值，后边的空字符就被忽略了，结果为Hello World 
```
参数变量是**默认声明**的，所以不能用let或const再次声明。
```js
function foo(x = 5) {
  let x = 1; // error
  const x = 2; // error
}
```
### 8.1.2 与解构赋值默认值结合使用
```js
function foo({x, y = 5}) {
  console.log(x, y);
}

foo({}) // undefined, 5
foo({x: 1}) // 1, 5
foo() // 报错
//但是原式改为
function foo({x, y = 5} = {}) {
  console.log(x, y);
}
foo()   //这样就不会报错了，同样会取到默认值 y = 5
```
### 8.1.3 参数默认值的位置
如果非尾部的参数设置默认值，实际上这个参数是没法省略的。
```js
/ 例一
function f(x = 1, y) {
  return [x, y];
}
f(, 1) // 报错
f(undefined, 1) // [1, 1]
```

### 8.1.4 函数的length属性
函数的length属性，将返回**没有**指定默认值的参数个数。
rest参数也不会计入length属性
```js
(function(a = 5){}).length // 0
(function(a, b, c = 5){}).length // 2
```

### 8.1.5 作用域
如果参数默认值是一个**变量**，则该变量所处的作用域，与其他变量的作用域规则是一样的，即先是当前函数的作用域，然后才是全局作用域。
```js
var x = 1;     //x为全局变量

function f(x, y = x) {     //x为局部变量
  console.log(y);
}

f(2) // 2
```
函数的作用域是其声明时所在的作用域
```js
let foo = 'outer';

function bar(func = x => foo) {
  let foo = 'inner';
  console.log(func()); // outer
}

bar();
```

### 8.1.6 应用
将参数默认值设为undefined，表明这个参数是可以**省略**的
```js
function foo(optional = undefined) { ··· }
```

## 8.2 rest参考
ES6引入rest参数（形式为“...变量名”），用于获取函数的多余参数，这样就不需要使用arguments对象了。
rest参数是一个**数组**
rest参数只能最后一个参数
函数的length属性，**不包括**rest参数。
```js
function add(...values) {
  let sum = 0;

  for (var val of values) {
    sum += val;
  }

  return sum;
}

add(2, 5, 3) // 10
```
我的理解是  ...变量名 = arguments 
```js
// arguments变量的写法
const sortNumbers = () =>
  Array.prototype.slice.call(arguments).sort();

// rest参数的写法
const sortNumbers = (...numbers) => numbers.sort();
```

## 8.3 扩展运算符
### 8.3.1 含义
扩展运算符（spread）是三个点`...`(在数组里见到过，转化为一个数组，相当于Array.from)。
它好比rest参数的逆运算，将一个数组转为用逗号分隔的**参数序列**。
```js
console.log(1, ...[2, 3, 4], 5)
// 1 2 3 4 5

[...document.querySelectorAll('div')]
// [<div>, <div>, <div>]
```
主要用于函数调用：
```js
function push(array, ...items) {
  array.push(...items);
}

function add(x, y) {
  return x + y;
}

var numbers = [4, 38];    //直接在下边把这个输入当参数引入
add(...numbers) // 42
```

### 8.3.2 替代数组的apply方法
由于扩展运算符可以展开数组，所以不再需要apply方法，将数组转为函数的参数了。
```js
// ES5的写法
function f(x, y, z) {
  // ...
}
var args = [0, 1, 2];
f.apply(null, args);

// ES6的写法
function f(x, y, z) {
  // ...
}
var args = [0, 1, 2];
f(...args);
```

### 8.3.3 扩展运算符的应用
#### 8.3.3.1 合并数组
扩展运算符提供了数组合并的新写法
```js
// ES5的合并数组
arr1.concat(arr2, arr3);
// [ 'a', 'b', 'c', 'd', 'e' ]

// ES6的合并数组
[...arr1, ...arr2, ...arr3]
// [ 'a', 'b', 'c', 'd', 'e' ]
```
#### 8.3.3.2 与解构赋值结合
```js
// ES5
a = list[0], rest = list.slice(1)
// ES6
[a, ...rest] = list

const [first, ...rest] = [1, 2, 3, 4, 5];
first // 1
rest  // [2, 3, 4, 5]
```
#### 8.3.3.3 函数的返回值
JavaScript的函数只能返回一个值，如果需要返回多个值，只能返回数组或对象。
```js
var dateFields = readDateFields(database);
var d = new Date(...dateFields);
```
#### 8.3.3.4 字符串
扩展运算符还可以将字符串转为真正的数组。
有一个重要的好处，那就是**能够正确识别**32位的Unicode字符。

```js
[...'hello']
// [ "h", "e", "l", "l", "o" ]
```
#### 8.3.3.5 实现了Iterator接口的对象
任何Iterator接口的对象，都可以用扩展运算符转为真正的**数组**。
```js
var nodeList = document.querySelectorAll('div');
var array = [...nodeList];
```
#### 8.3.3.6 Map和Set结构，Generator函数
只要具**有Iterator接口**的对象，都可以使用扩展运算符，比如Map结构
```js
let map = new Map([
  [1, 'one'],
  [2, 'two'],
  [3, 'three'],
]);

let arr = [...map.keys()]; // [1, 2, 3]
```
Generator函数运行后，返回一个遍历器对象，因此也可以使用扩展运算符。
```js
var go = function*(){
  yield 1;
  yield 2;
  yield 3;
};

[...go()] // [1, 2, 3]
```
下边没有Iterator接口,报错
```js
var obj = {a: 1, b: 2};
let arr = [...obj]; // TypeError: Cannot spread non-iterable object
```
## 8.4 name属性
函数的name属性，返回该函数的函数名。
```js
function foo() {}
foo.name // "foo"
```
ES5和ES6区别
```js
var func1 = function () {};

// ES5
func1.name // ""   无法获取匿名函数的名字

// ES6
func1.name // "func1"
```
Function构造函数返回的函数实例，name属性的值为“anonymous”。
```js
(new Function).name // "anonymous"
```
bind返回的函数，name属性值会加上“bound ”前缀。
```js
function foo() {};
foo.bind({}).name // "bound foo"

(function(){}).bind({}).name // "bound "
```

## 8.5 箭头函数
### 8.5.1 基本用法
ES6允许使用“箭头”（=>）定义函数。
```js
var f = v => v;
//等同于
var f = function(v) {
  return v;
};
```
**不需要**或者需要**多个**参数，就使用一个圆括号代表参数部分
```js
var f = () => 5;
// 等同于
var f = function (){ return 5 };

var sum = (num1, num2) => num1 + num2;
// 等同于
var sum = function(num1, num2) {
  return num1 + num2;
};
```
如果箭头函数的代码块部分**多于一条语句**，就要使用**大括号**将它们括起来，并且使用`return`语句返回。
```js
var sum = (num1, num2) => { return num1 + num2; }
```
由于大括号被解释为**代码块**，所以如果箭头函数直接返回一个**对象**，必须在对象外面加上**括号**。
```js
var getTempItem = id => ({ id: id, name: "Temp" });
```
用处1：简化回调函数
```js
// 正常函数写法
[1,2,3].map(function (x) {
  return x * x;
});

// 箭头函数写法
[1,2,3].map(x => x * x);
```
### 8.5.2 使用注意点：
（1）函数体内的this对象，就是定义时所在的对象，而不是使用时所在的对象。

（2）不可以当作构造函数，也就是说，不可以使用new命令，否则会抛出一个错误。

（3）不可以使用arguments对象，该对象在函数体内不存在。如果要用，可以用Rest参数代替。

（4）不可以使用yield命令，因此箭头函数不能用作Generator函数。

第一点说明下：this对象的指向是可变的，但是在箭头函数中，**它是固定**的。
```js
function foo() {
  setTimeout( () => {
    console.log("id:", this.id);
  },100);
}

var id = 21;

foo.call( { id: 42 } );
// id: 42
```
由于箭头函数**没有自己的this**，所以当然也就**不能用**call()、apply()、bind()这些方法去改变this的指向。

### 8.5.3 嵌套的箭头函数
箭头函数内部，还可以再使用箭头函数。下面是一个ES5语法的多重嵌套函数。
```js
//ES5
function insert(value) {
  return {into: function (array) {
    return {after: function (afterValue) {
      array.splice(array.indexOf(afterValue) + 1, 0, value);
      return array;
    }};
  }};
}

insert(2).into([1, 3]).after(1); //[1, 2, 3]
//箭头函数改写
let insert = (value) => ({into: (array) => ({after: (afterValue) => {
  array.splice(array.indexOf(afterValue) + 1, 0, value);
  return array;
}})});

insert(2).into([1, 3]).after(1); //[1, 2, 3]

```
**管道机制（pipeline）**的例子
```js
const pipeline = (...funcs) =>
  val => funcs.reduce((a, b) => b(a), val);

const plus1 = a => a + 1;
const mult2 = a => a * 2;
const addThenMult = pipeline(plus1, mult2);

addThenMult(5)
// 12
//可读性更高一些的
const plus1 = a => a + 1;
const mult2 = a => a * 2;

mult2(plus1(5))
// 12
```
λ演算
```js
// λ演算的写法
fix = λf.(λx.f(λv.x(x)(v)))(λx.f(λv.x(x)(v)))

// ES6的写法
var fix = f => (x => f(v => x(x)(v)))
               (x => f(v => x(x)(v)));
```

## 8.6 函数绑定
箭头函数可以绑定this对象，但并不适用于所有场合，所以ES7提出了“函数绑定”（function bind）运算符，用来取代call、apply、bind调用。
函数绑定运算符是并排的两个双冒号（::），双冒号左边是一个对象，右边是一个函数。
该运算符会自动将**左边**的对象，作为上下文环境（即this对象），绑定到右边的函数上面。
```js
foo::bar;
// 等同于
bar.bind(foo);

foo::bar(...arguments);
// 等同于
bar.apply(foo, arguments);
```
**如果双冒号左边为空，右边是一个对象的方法，则等于将该方法绑定在该对象上面**
```js
var method = ::obj.foo;
// 等同于
var method = obj::obj.foo;
```
因此可以采用**链式写法**
```js
// 例一
import { map, takeWhile, forEach } from "iterlib";

getPlayers()
::map(x => x.character())
::takeWhile(x => x.strength > 100)
::forEach(x => console.log(x));
```

## 8.7 尾调用优化
### 8.7.1 什么是尾调用
指某个函数的**最后一步**是调用另一个函数。
```js
//是尾调用
function f(x){
  return g(x);
}
//不是尾调用
// 情况一
function f(x){
  let y = g(x);
  return y;
}

// 情况二
function f(x){
  return g(x) + 1;
}

// 情况三
function f(x){
  g(x);
}
```
### 8.7.2 尾调用优化
函数调用会在内存形成一个“调用记录”，又称“调用帧”（call frame），保存调用位置和内部变量等信息。
“尾调用优化”（Tail call optimization），即只保留内层函数的调用帧。
执行到最后，完全可以**删除**f(x)的调用帧，指保留g()的调用帧
如果所有函数都是尾调用，那么完全可以做到每次执行时，调用帧**只有一项**，这将大大节省内存。
尾调用优化：
```js
function addOne(a){
  var one = 1;
  function inner(b){
    return b + one;
  }
  return inner(a);
}
```
### 8.7.3 尾递归
如果尾调用自身，就称为尾递归。
由于只存在一个调用帧，所以永远不会发生“栈溢出”错误。
```js
//优化前--计算n的阶乘，最多需要保存n个调用记录，复杂度 O(n) 
function factorial(n) {
  if (n === 1) return 1;
  return n * factorial(n - 1);
}

factorial(5) // 120
//优化后--只保留一个调用记录，复杂度 O(1)
//方法思路：把所有用到的内部变量改写成函数的参数。
function factorial(n, total) {
  if (n === 1) return total;
  return factorial(n - 1, n * total);
}

factorial(5, 1) // 120
```

### 8.7.4 递归函数的改写---需要好好看看
柯里化（currying），意思是将多参数的函数转换成单参数的形式。

### 8.7.5 严格模式
**ES6的尾调用优化只在严格模式下开启，正常模式是无效的。**
因为：在正常模式下，函数内部有两个变量，可以跟踪函数的调用栈。 
   `func.arguments`：返回调用时函数的参数。
   `func.caller`：返回调用当前函数的那个函数。
严格模式禁用这两个变量，所以尾调用模式仅在严格模式下生效。

### 8.7.6 尾递归优化的实现
就是在正常模式下，实现尾递归优化

## 8.8 函数参数的尾逗号
ES7有一个提案，允许函数的**最后一个参数**有尾逗号（trailing comma），**目前还不允许**

# 9.对象的扩展
## 9.1 属性的简洁表示法
ES6允许直接写入变量和函数，作为对象的属性和方法。这样的书写更加简洁。
```js
//属性
var foo = 'bar';
var baz = {foo};
baz // {foo: "bar"}

// 等同于
var baz = {foo: foo};

//参数
function f(x, y) {
  return {x, y};
}

// 等同于

function f(x, y) {
  return {x: x, y: y};
}

f(1, 2) // Object {x: 1, y: 2}
//方法
var o = {
  method() {
    return "Hello!";
  }
};

// 等同于

var o = {
  method: function() {
    return "Hello!";
  }
};
```
CommonJS模块输出变量，就非常合适使用简洁写法。
```js
var ms = {};

function getItem (key) {
  return key in ms ? ms[key] : null;
}

function setItem (key, value) {
  ms[key] = value;
}

function clear () {
  ms = {};
}

module.exports = { getItem, setItem, clear };   //简写的
// 等同于
module.exports = {
  getItem: getItem,
  setItem: setItem,
  clear: clear
};
```
如果某个方法的值是一个Generator函数，前面需要加上**星号**。
```js
var obj = {
  * m(){
    yield 'hello world';
  }
}
```

## 9.2 属性名表达式
允许字面量定义对象时，用方法二（表达式）作为对象的属性名，即把表达式放在方括号内。
```js
let obj = {
  [propKey]: true,
  ['a' + 'bc']: 123      //前边那个算式是表达式
};
```
注意，属性名表达式与简洁表示法，不能同时使用，会报错。
```js
// 报错
var foo = 'bar';
var bar = 'abc';
var baz = { [foo] };

// 正确
var foo = 'bar';
var baz = { [foo]: 'abc'};
```

## 9.3 方法的name属性
```js
var person = {
  sayName() {
    console.log(this.name);
  },
  get firstName() {
    return "Nicholas"
  }
}

person.sayName.name   // "sayName"
person.firstName.name // "get firstName"    前边有个get
```
*注意*有两种特殊情况：bind方法创造的函数，name属性返回“bound”加上原函数的名字；Function构造函数创造的函数，name属性返回“anonymous”。
如果对象的方法是一个`Symbol`值，那么name属性返回的是这个Symbol值的**描述**。
```js
const key1 = Symbol('description');
const key2 = Symbol();
let obj = {
  [key1]() {},
  [key2]() {},
};
obj[key1].name // "[description]"
obj[key2].name // ""
```

## 9.4 Object.is()
表示是否相等，相当于`===`
```js
+0 === -0 //true
NaN === NaN // false

Object.is(+0, -0) // false
Object.is(NaN, NaN) // true
```

## 9.5 Object.assign()
### 9.5.1 基本方法
Object.assign方法用于对象的合并，将源对象（source）的所有**可枚举**属性，复制到目标对象（target）。
Object.assign方法的第一个参数是目标对象，后面的参数都是源对象。
```js
var target = { a: 1, b: 1 };

var source1 = { b: 2, c: 2 };
var source2 = { c: 3 };

Object.assign(target, source1, source2);
target // {a:1, b:2, c:3}
```
如果该参数不是对象，则会**先转成对象**，然后返回。
```js
typeof Object.assign(2) // "object"
```
由于undefined和null**无法转成对象**，所以如果它们作为参数，就会报错。
**但是**如果undefined和null和其他不能转为对象的值**不在首参数**，就不会报错。
```js
let obj = {a: 1};
Object.assign(obj, undefined) === obj // true
Object.assign(obj, null) === obj // true
```
布尔值、数值、字符串分别转成对应的包装对象，他们的原始值在内部属性`[[PrimitiveValue]]`上面,
但是只有字符串的包装对象上有可枚举的属性，所以只有字符串支持这个方法。
Object.assign拷贝的属性是有限制的，只拷贝源对象的自身属性**（不拷贝继承属性）**，也不拷贝**不可枚举**的属性（enumerable: false）。
属性名为`Symbol`值的属性，也会被Object.assign拷贝。
```js
Object.assign({ a: 'b' }, { [Symbol('c')]: 'd' })
// { a: 'b', Symbol(c): 'd' }
```
### 9.5.2 注意点
Object.assign方法实行的是浅拷贝，而不是深拷贝。
所以这个对象的任何变化，都会反映到目标对象上面。
对于这种嵌套的对象，一旦遇到**同名**属性，Object.assign的处理方法是**替换**，而不是添加。
Object.assign可以用来**处理数组**，但是会把数组**视为对象**。
```js
Object.assign([1, 2, 3], [4, 5])
// [4, 5, 3]
```
### 9.5.3 常见用途
#### 9.5.3.1 为对象添加属性
```js
class Point {
  constructor(x, y) {
    Object.assign(this, {x, y});
  }
}
```

#### 9.5.3.2 为对象添加方法
```js
Object.assign(SomeClass.prototype, {
  someMethod(arg1, arg2) {
    ···
  },
  anotherMethod() {
    ···
  }
});
//添加了两个方法;
SomeClass.prototype.someMethod
SomeClass.prototype.anotherMethod
```

#### 9.5.3.3 克隆对象
```js
function clone(origin) {
  return Object.assign({}, origin);
}
```
不能克隆它**继承**的值。

#### 9.5.3.4 合并多个对象
```js
const merge = (target, ...sources) => Object.assign(target, ...sources);
```

#### 9.5.3.5 为属性指定默认值
```js
//利用同名属性覆盖原理
const DEFAULTS = {
  logLevel: 0,
  outputFormat: 'html'
};

function processContent(options) {
  let options = Object.assign({}, DEFAULTS, options);
}
```

## 9.6 属性的可枚举型
`Object.getOwnPropertyDescriptor()`方法可以获取该**属性**的描述对象
`enumerable`属性，称为**可枚举性**，如果该属性为false,表示某些操作会忽略当前属性。
忽略enumerable为false的属性的的值的**操作**有：
ES5:
for...in 循环：只遍历对象自身的和继承的可枚举的属性
Object.keys()：返回对象自身的所有可枚举的属性的键名
JSON.stringify()：只串行化对象自身的可枚举的属性
ES6:
Object.assign()：只拷贝对象自身的可枚举的属性
Reflect.enumerate()：返回所有for...in循环会遍历的属性
只有for...in和Reflect.enumerate()会返回**继承**的属性。
因为继承的关系，尽量不要用for...in循环，而用Object.keys()代替

## 9.7 属性的遍历
（1）for...in

for...in循环遍历对象自身的和继承的可枚举属性（不含Symbol属性）。

（2）Object.keys(obj)

Object.keys返回一个数组，包括对象自身的（不含继承的）所有可枚举属性（不含Symbol属性）。

（3）Object.getOwnPropertyNames(obj)

Object.getOwnPropertyNames返回一个数组，包含对象自身的所有属性（不含Symbol属性，但是包括不可枚举属性）。

（4）Object.getOwnPropertySymbols(obj)

Object.getOwnPropertySymbols返回一个数组，包含对象自身的所有Symbol属性。

（5）Reflect.ownKeys(obj)

Reflect.ownKeys返回一个数组，包含对象自身的所有属性，不管是属性名是Symbol或字符串，也不管是否可枚举。

（6）Reflect.enumerate(obj)

Reflect.enumerate返回一个Iterator对象，遍历对象自身的和继承的所有可枚举属性（不含Symbol属性），与for...in循环相同。

以上的6种方法遍历对象的属性，都遵守同样的属性遍历的**次序**规则。

首先遍历所有属性名为**数值**的属性，按照数字排序。
其次遍历所有属性名为**字符串**的属性，按照生成时间排序。
最后遍历所有属性名为**Symbol**值的属性，按照生成时间排序。

## 9.8 __proto__属性，Object.setPrototypeOf()，Object.getPrototypeOf() 
### 9.8.1 __proto__属性
`__proto__`属性（前后各两个下划线），用来读取或设置当前对象的prototype对象。
无论从语义的角度，还是从兼容性的角度，都不要使用这个属性，而是使用下面的`Object.setPrototypeOf()`（写操作）、`Object.getPrototypeOf()`（读操作）、`Object.create()`（生成操作）代替。

### 9.8.2 Object.setPrototypeOf()
Object.setPrototypeOf方法的作用与`__proto__`相同，用来设置一个对象的prototype对象。它是ES6**正式推荐**的设置原型对象的方法。
```js
let proto = {};
let obj = { x: 10 };
Object.setPrototypeOf(obj, proto);

proto.y = 20;
proto.z = 40;

obj.x // 10
obj.y // 20
obj.z // 40
```

### 9.8.3 Object.getPrototypeOf()
该方法与setPrototypeOf方法配套，用于读取一个对象的prototype对象。
```js
Object.getPrototypeOf(obj);
```

## 9.9 Object.values()，Object.entries();
ES5的`Object.keys`方法，返回一个数组，成员是参数对象自身的（**不含继承的**）所有可遍历（enumerable）属性的**键名**。
```js
var obj = { foo: "bar", baz: 42 };
Object.keys(obj)
// ["foo", "baz"]
```
ES6的`Object.values`方法返回一个数组，成员是参数对象自身的（**不含继承的**）且所有可遍历（enumerable）属性的**键值**。
```js
var obj = { foo: "bar", baz: 42 };
Object.values(obj)
// ["bar", 42]
```
**注意：**
排序按照上边说的那个顺序走
Object.values会过滤属性名为Symbol值的属性。
Object.values方法的参数是一个字符串，会返回各个字符组成的一个数组。
Object.values会先将其转为对象--数值和布尔值的包装对象，都不会为实例添加非继承的属性。所以，Object.values会返回空数组。
```js
Object.values({ [Symbol()]: 123, foo: 'abc' });
// ['abc']
Object.values('foo')
// ['f', 'o', 'o']
Object.values(42) // []
Object.values(true) // []
```
ES6的`Object.entries`方法返回一个数组，成员是参数对象自身的（不含继承的）所有可遍历（enumerable）属性的键值对**数组**。
```js
var obj = { foo: 'bar', baz: 42 };
Object.entries(obj)
// [ ["foo", "bar"], ["baz", 42] ]
```

## 9.10 对象的扩展运算符
将Rest解构赋值/扩展运算符`...`引入对象
### 9.10.1 Rest解构赋值
对象的Rest解构赋值用于从一个对象取值，相当于将所有可遍历的、但尚未被读取的属性，分配到指定的对象上面。
由于Rest解构赋值要求等号右边是一个对象，所以如果等号右边是undefined或null，就会报错，因为它们无法转为对象。
Rest解构赋值的拷贝是**浅拷贝**
```js
let { x, y, ...z } = { x: 1, y: 2, a: 3, b: 4 };
x // 1
y // 2
z // { a: 3, b: 4 }

let { x, y, ...z } = null; // 运行时错误
let { x, y, ...z } = undefined; // 运行时错误
//浅拷贝
let o1 = { a: 1 };
let o2 = { b: 2 };
o2.__proto__ = o1;
let o3 = { ...o2 };
o3 // { b: 2 }
```
用处：扩展某个函数的参数，引入其他操作。
```js
function baseFunction({ a, b }) {
  // ...
}
function wrapperFunction({ x, y, ...restConfig }) {
  // 使用x和y参数进行操作
  // 其余参数传给原始函数
  return baseFunction(restConfig);
}
```

### 9.10.2 扩展运算符
扩展运算符`...`，用于取出参数对象的所有可遍历属性，拷贝到当前对象之中
等同于使用`Object.assign`方法
**同名覆盖**，可以修改部分属性
如果扩展运算符的参数是null或undefined，这个两个值会被忽略，不会报错。
```js
let z = { a: 3, b: 4 };
let n = { ...z };
n // { a: 3, b: 4 }
//合并两个对象
let ab = { ...a, ...b };
// 等同于
let ab = Object.assign({}, a, b);

let emptyObject = { ...null, ...undefined }; // 忽略，不报错
```
扩展运算符的参数对象之中，如果有取值函数get，这个函数是会**执行**的。
```js
// 并不会抛出错误，因为x属性只是被定义，但没执行
let aWithXGetter = {
  ...a,
  get x() {
    throws new Error('not thrown yet');
  }
};

// 会抛出错误，因为x属性被执行了
let runtimeError = {
  ...a,
  ...{
    get x() {
      throws new Error('thrown now');
    }
  }
};
```

## 9.11 Object.getOwnPropertyDescriptors()
ES5有一个`Object.getOwnPropertyDescriptor`方法，返回**某个**对象属性的描述对象（descriptor）。
ES7有一个`Object.getOwnPropertyDescriptors`方法，返回指定对象**所有自身**属性（非继承属性）的描述对象。
该方法的提出目的，**主要是为了解决**Object.assign()无法正确拷贝get属性和set属性的问题。
Object.getOwnPropertyDescriptors方法**配合**Object.defineProperties方法，就可以实现正确拷贝。
```js
const source = {
  set foo(value) {
    console.log(value);
  }
};

const target2 = {};
Object.defineProperties(target2, Object.getOwnPropertyDescriptors(source));   //添加这个属性，用的只有这句
Object.getOwnPropertyDescriptor(target2, 'foo')
// { get: undefined,
//   set: [Function: foo],
//   enumerable: true,
//   configurable: true }
```
Object.getOwnPropertyDescriptors方法的另一个用处，是配合Object.create方法，将对象属性**克隆**到一个新对象。这属于**浅拷贝**。
```js
const clone = Object.create(Object.getPrototypeOf(obj),
  Object.getOwnPropertyDescriptors(obj));

// 或者

const shallowClone = (obj) => Object.create(
  Object.getPrototypeOf(obj),
  Object.getOwnPropertyDescriptors(obj)
);
```
Object.getOwnPropertyDescriptors方法的另一个用处，一个对象继承另一个对象。
```js
const obj = Object.create(
  prot,
  Object.getOwnPropertyDescriptors({
    foo: 123,
  })
);
```
Object.getOwnPropertyDescriptors也可以用来实现Mixin（混入）模式。
```js
//对象a和b被混入了对象c
let mix = (object) => ({
  with: (...mixins) => mixins.reduce(
    (c, mixin) => Object.create(
      c, Object.getOwnPropertyDescriptors(mixin)
    ), object)
});

// multiple mixins example
let a = {a: 'a'};
let b = {b: 'b'};
let c = {c: 'c'};
let d = mix(c).with(a, b);
```
# 10.Symbol
# 10.1 概述
ES6引入了一种新的原始数据类型Symbol，表示独一无二的值。
它是JavaScript语言的第七种数据类型，前六种是：Undefined、Null、布尔值（Boolean）、字符串（String）、数值（Number）、对象（Object）。
Symbol值通过Symbol函数生成。
Symbol函数可以接受一个字符串作为**参数**，表示对Symbol实例的**描述**，主要是为了在控制台显示，或者转为字符串时，比较容易区分。
```js
let s = Symbol();
typeof s   // "symbol"
```
Symbol函数的参数只是表示对当前Symbol值的描述，因此相同参数的Symbol函数的返回值是**不相等**的。
Symbol值不能与其他类型的值进行运算，会报错。
```js
var sym = Symbol('My symbol');

"your symbol is " + sym  // TypeError: can't convert symbol to string
`your symbol is ${sym}`  // TypeError: can't convert symbol to string
```
Symbol值可以显式转为字符串。
Symbol值也可以转为布尔值，但是不能转为数值。
```js
var sym = Symbol();
Boolean(sym) // true
!sym  // false

if (sym) {
  // ...
}

Number(sym) // TypeError
sym + 2 // TypeError
```
## 10.2 作为属性名的Symbol
```js
var mySymbol = Symbol();

// 第一种写法
var a = {};
a[mySymbol] = 'Hello!';

// 第二种写法
var a = {
  [mySymbol]: 'Hello!'
};

// 第三种写法 --不推荐
var a = {};
Object.defineProperty(a, mySymbol, { value: 'Hello!' });

// 以上写法都得到同样结果
a[mySymbol] // "Hello!"
```
Symbol值作为对象属性名时，**不能用点运算符**，且必须放在`[]`中。
```js
var mySymbol = Symbol();
var a = {};

a.mySymbol = 'Hello!';       //这个用点赋值的只是一个字符串
a[mySymbol] // undefined
a['mySymbol'] // "Hello!"     //证明只是一个字符串
```
常量使用Symbol值最大的好处，就是**其他任何值**都不可能有相同的值。

## 10.3 实例： 消除魔术字符串
魔术字符串指的是，在代码之中多次出现、与代码形成强耦合的某一个具体的字符串或者数值。
**其实就是将字符串改为一个变量，以后好修改**
```js
//头部定义
var shapeType = {
  triangle: 'Triangle'
};
//下边引用的时候用
shapeType.triangle

//头部改写
const shapeType = {
  triangle: Symbol()    //等于哪个值并不重要，只要确保不会跟其他shapeType属性的值冲突即可
};
```

## 10.4 属性名的遍历
`Object.getOwnPropertySymbols` **可以**获取指定对象的所有Symbol属性名。
for...in、for...of、Object.keys()、Object.getOwnPropertyNames()这些都**不可以**获取。
但Symbol仍然不是私有属性
Object.getOwnPropertySymbols方法返回一个**数组**，成员是当前对象的所有用作属性名的Symbol值（键值）。

```js
var obj = {};

var foo = Symbol("foo");

Object.defineProperty(obj, foo, {
  value: "foobar",
});
 
for (var i in obj) {          //for-in无法获取
  console.log(i); // 无输出
}

Object.getOwnPropertyNames(obj)
// []

Object.getOwnPropertySymbols(obj)
// [Symbol(foo)]
```
`Reflect.ownKeys`方法**可以**返回所有类型的键名，包括常规键名和Symbol键名。
```js
let obj = {
  [Symbol('my_key')]: 1,
  enum: 2,
  nonEnum: 3
};

Reflect.ownKeys(obj)
// [Symbol(my_key), 'enum', 'nonEnum']
```
**由于以Symbol值作为名称的属性，不会被常规方法遍历得到。我们可以利用这个特性，为对象定义一些非私有的、但又希望只用于内部的方法。**

## 10.5 Symbol.for()，Symbol.keyFor()
`Symbol.for`表示重新使用同一个Symbol值
它接受一个字符串作为参数，然后搜索有没有以该参数作为名称的Symbol值。如果有，就返回这个Symbol值，否则就**新建**并返回一个以该字符串为名称的Symbol值。
```js
var s1 = Symbol.for('foo');
var s2 = Symbol.for('foo');

s1 === s2 // true
```
Symbol.for()与Symbol()这两种写法，都会生成新的Symbol。
它们的区别是，前者会被登记在**全局环境**中供搜索，后者不会。
因为全局环境的，所以可以在不同的`iframe`或`service worker`中取到同一个值。
`Symbol.keyFor`方法返回一个已登记的Symbol类型值的key。
```js
var s1 = Symbol.for("foo");
Symbol.keyFor(s1) // "foo"

var s2 = Symbol("foo");                  //未登记
Symbol.keyFor(s2) // undefined
```

## 10.6 内置的Symbol值
### 10.6.1 Symbol.hasInstance
当其他对象使用instanceof运算符，判断是否为该对象的实例时，会调用这个方法。
比如，`foo instanceof Foo`在语言内部，实际调用的是`Foo[Symbol.hasInstance](foo)`。
```js
class MyClass {
  [Symbol.hasInstance](foo) {
    return foo instanceof Array;
  }
}

[1, 2, 3] instanceof MyClass() // true
```
### 10.6.2 Symbol.isConcatSpreadable
表示该对象使用`Array.prototype.concat()`时，是否可以展开（时候有`[]`）。
数组，默认是可以展开的(true)
类数组，默认是不可以展开的(false),必须手动展开
```js
let obj = {length: 2, 0: 'c', 1: 'd'};
['a', 'b'].concat(obj, 'e') // ['a', 'b', obj, 'e']

obj[Symbol.isConcatSpreadable] = true;
['a', 'b'].concat(obj, 'e') // ['a', 'b', 'c', 'd', 'e']
```
类A1是可扩展的，类A2是不可扩展的，所以使用concat时有不一样的结果。
```js
class A1 extends Array {
  [Symbol.isConcatSpreadable]() {
    return true;
  }
}
class A2 extends Array {
  [Symbol.isConcatSpreadable]() {
    return false;
  }
}
let a1 = new A1();
a1[0] = 3;
a1[1] = 4;
let a2 = new A2();
a2[0] = 5;
a2[1] = 6;
[1, 2].concat(a1).concat(a2)
// [1, 2, 3, 4, [5, 6]]
```

### 10.6.3 Symbol.species
该对象作为构造函数创造实例时，会调用这个方法。
即如果`this.constructor[Symbol.species]`存在，就会使用这个属性作为构造函数，来创造新的实例对象。
```js
static get [Symbol.species]() {
  return this;
}
```

### 10.6.4 Symbol.match
当执行`str.match(myObject)`时，如果该属性存在，会调用它，返回该方法的返回值。
```js
String.prototype.match(regexp)
// 等同于
regexp[Symbol.match](this)

class MyMatcher {
  [Symbol.match](string) {
    return 'hello world'.indexOf(string);
  }
}

'e'.match(new MyMatcher()) // 1
```

### 10.6.5 Symbol.replace
当该对象被`String.prototype.replace`方法调用时，会返回该方法的返回值。
```js
String.prototype.replace(searchValue, replaceValue)
// 等同于
searchValue[Symbol.replace](this, replaceValue)
```

### 10.6.6 Symbol.search
当该对象被`String.prototype.search`方法调用时，会返回该方法的返回值。

### 10.6.7 Symbol.split
当该对象被`String.prototype.split`方法调用时，会返回该方法的返回值。

### 10.6.8 Symbol.iterator
指向该对象的默认遍历器方法，即该对象进行`for...of`循环时，会调用这个方法，返回该对象的默认遍历器
```js
class Collection {
  *[Symbol.iterator]() {
    let i = 0;
    while(this[i] !== undefined) {
      yield this[i];
      ++i;
    }
  }
}

let myCollection = new Collection();
myCollection[0] = 1;
myCollection[1] = 2;

for(let value of myCollection) {
  console.log(value);
}
// 1
// 2
```

### 10.6.9 Symbol.toPrimitive
该对象被转为原始类型的值时，会调用这个方法，返回该对象对应的原始类型值。
`Symbol.toPrimitive`被调用时，会接受**一个字符串参数**，表示当前运算的模式，一共有**三种模式**。
Number：该场合需要转成数值
String：该场合需要转成字符串
Default：该场合可以转成数值，也可以转成字符串

### 10.6.10 Symbol.toStringTag
在该对象上面调用`Object.prototype.toString`方法时，如果这个属性存在，它的返回值会出现在toString方法返回的字符串之中，表示对象的类型。
```js
({[Symbol.toStringTag]: 'Foo'}.toString())
// "[object Foo]"

class Collection {
  get [Symbol.toStringTag]() {
    return 'xxx';
  }
}
var x = new Collection();
Object.prototype.toString.call(x) // "[object xxx]"
```

### 10.6.11 Symbol.unscopables
该对象指定了使用with关键字时，哪些属性会被with环境排除。


# 11.Proxy和Reflect
## 11.1 Proxy概述
可以译为“代理器”。
Proxy可以理解成，在目标对象之前架设一层**拦截**，外界对该对象的访问，都必须先通过这层拦截，因此提供了一种机制，可以对外界的访问进行**过滤**和**改写**。
```js
var obj = new Proxy({}, {
  get: function (target, key, receiver) {
    console.log(`getting ${key}!`);
    return Reflect.get(target, key, receiver);
  },
  set: function (target, key, value, receiver) {
    console.log(`setting ${key}!`);
    return Reflect.set(target, key, value, receiver);
  }
});
//结果
obj.count = 1
//  setting count!
++obj.count
//  getting count!
//  setting count!
//  2
```
ES6原生提供`Proxy`构造函数，用来**生成**Proxy**实例**。
```js
var proxy = new Proxy(target, handler)
```
Proxy对象的所有用法，**都是**上面这种形式，不同的只是handler参数的写法。
`target`参数表示所要拦截的目标对象，
`handler`参数也是一个对象，用来定制拦截行为。
```js
var proxy = new Proxy({}, {
  get: function(target, property) {    //对get进行拦截，让返回值都是35
    return 35;
  }
});

proxy.time // 35
proxy.name // 35
proxy.title // 35
```
一个**技巧**是将Proxy对象，设置到object.proxy属性，从而可以在object对象上调用。
```js
var object = { proxy: new Proxy(target, handler) }
```
Proxy实例也可以作为其他对象的**原型**对象，如果访问原型，就要经过过滤，而对象本身不需要
下面是Proxy**支持的拦截操作**一览。
（1）get(target, propKey, receiver)

拦截对象属性的读取，比如proxy.foo和proxy['foo']，返回类型不限。最后一个参数receiver可选，当target对象设置了propKey属性的get函数时，receiver对象会绑定get函数的this对象。

（2）set(target, propKey, value, receiver)

拦截对象属性的设置，比如proxy.foo = v或proxy['foo'] = v，返回一个布尔值。

（3）has(target, propKey)

拦截propKey in proxy的操作，返回一个布尔值。

（4）deleteProperty(target, propKey)

拦截delete proxy[propKey]的操作，返回一个布尔值。

（5）enumerate(target)

拦截for (var x in proxy)，返回一个遍历器。

（6）ownKeys(target)

拦截Object.getOwnPropertyNames(proxy)、Object.getOwnPropertySymbols(proxy)、Object.keys(proxy)，返回一个数组。该方法返回对象所有自身的属性，而Object.keys()仅返回对象可遍历的属性。

（7）getOwnPropertyDescriptor(target, propKey)

拦截Object.getOwnPropertyDescriptor(proxy, propKey)，返回属性的描述对象。

（8）defineProperty(target, propKey, propDesc)

拦截Object.defineProperty(proxy, propKey, propDesc）、Object.defineProperties(proxy, propDescs)，返回一个布尔值。

（9）preventExtensions(target)

拦截Object.preventExtensions(proxy)，返回一个布尔值。

（10）getPrototypeOf(target)

拦截Object.getPrototypeOf(proxy)，返回一个对象。

（11）isExtensible(target)

拦截Object.isExtensible(proxy)，返回一个布尔值。

（12）setPrototypeOf(target, proto)

拦截Object.setPrototypeOf(proxy, proto)，返回一个布尔值。

如果目标对象是函数，那么还有两种额外操作可以拦截。

（13）apply(target, object, args)

拦截Proxy实例作为函数调用的操作，比如proxy(...args)、proxy.call(object, ...args)、proxy.apply(...)。

（14）construct(target, args, proxy)

拦截Proxy实例作为构造函数调用的操作，比如new proxy(...args)。
用法：例如
```js
var handler = {
  get: function(target, name) {                               //get
    if (name === 'prototype') return Object.prototype;  
    return 'Hello, '+ name;
  },
  apply: function(target, thisBinding, args) { return args[0]; }, //apply
  construct: function(target, args) { return args[1]; }        //construct
};

var fproxy = new Proxy(function(x,y) {
  return x+y;
},  handler);

fproxy(1,2); // 1
new fproxy(1,2); // 2
fproxy.prototype; // Object.prototype
fproxy.foo; // 'Hello, foo'
```

## 11.2 Proxy实例的方法
上边提供所有方法的用法：

## 11.3 Proxy.revocable()
`Proxy.revocable`方法返回一个**可取消**的Proxy实例。
```js
let target = {};
let handler = {};

let {proxy, revoke} = Proxy.revocable(target, handler);

proxy.foo = 123;
proxy.foo // 123

revoke();
proxy.foo // TypeError: Revoked
```
`Proxy.revocable`方法返回一个对象，该对象的`proxy`属性是Proxy实例，`revoke`属性是一个函数，可以取消Proxy实例。
上面代码中，当**执行**revoke函数之后，**再访问**Proxy实例，就会抛出一个错误。

## 11.4 Reflect概述
Reflect对象的设计目的有这样几个。
（1） 将Object对象的一些明显属于语言内部的方法（比如Object.defineProperty），**放到Reflect对象上**。现阶段，某些方法**同时**在Object和Reflect对象上部署，**未来的新方法**将只部署在Reflect对象上。

（2） 修改某些Object方法的返回结果，让其变得更合理。比如，`Object.defineProperty(obj, name, desc)`在无法定义属性时，会抛出一个错误，而`Reflect.defineProperty(obj, name, desc)`则会返回false。
```js
// 老写法
try {
  Object.defineProperty(target, property, attributes);
  // success
} catch (e) {
  // failure
}

// 新写法
if (Reflect.defineProperty(target, property, attributes)) {
  // success
} else {
  // failure
}
```
（3） 让Object操作都变成**函数**行为。某些Object操作是命令式，比如`name in obj`和`delete obj[name]`，而`Reflect.has(obj, name)`和`Reflect.deleteProperty(obj, name)`让它们变成了函数行为。
```js
// 老写法
'assign' in Object // true

// 新写法
Reflect.has(Object, 'assign') // true
```
（4）Reflect对象的方法与Proxy对象的方法**一一对应**，只要是Proxy对象的方法，就能在Reflect对象上找到对应的方法。这就让Proxy对象可以方便地调用对应的Reflect方法，完成默认行为，作为修改行为的基础。也就是说，不管Proxy怎么修改默认行为，**你总可以在Reflect上获取默认行为**。
```js
var loggedObj = new Proxy(obj, {
  get(target, name) {
    console.log('get', target, name);
    return Reflect.get(target, name);
  },
  deleteProperty(target, name) {
    console.log('delete' + name);
    return Reflect.deleteProperty(target, name);
  },
  has(target, name) {
    console.log('has' + name);
    return Reflect.has(target, name);
  }
});
```
每一个Proxy对象的拦截操作（get、delete、has），内部都调用对应的Reflect方法，保证原生行为能够正常执行。添加的工作，就是将每一个操作输出一行日志。
有了Reflect对象以后，很多操作会**更易读**。
```js
// 老写法
Function.prototype.apply.call(Math.floor, undefined, [1.75]) // 1

// 新写法
Reflect.apply(Math.floor, undefined, [1.75]) // 1
```
## 11.5 Reflect对象的方法
Reflect对象的方法清单如下，共14个。

Reflect.apply(target,thisArg,args)
Reflect.construct(target,args)
Reflect.get(target,name,receiver)
Reflect.set(target,name,value,receiver)
Reflect.defineProperty(target,name,desc)
Reflect.deleteProperty(target,name)
Reflect.has(target,name)
Reflect.ownKeys(target)
Reflect.enumerate(target)
Reflect.isExtensible(target)
Reflect.preventExtensions(target)
Reflect.getOwnPropertyDescriptor(target, name)
Reflect.getPrototypeOf(target)
Reflect.setPrototypeOf(target, prototype)
大部分与Object对象的同名方法的**作用都是相同**的，而且它与Proxy对象的方法是**一一对应**的。
（1）Reflect.get(target, name, receiver)
**查找并返回**target对象的name属性，如果没有该属性，则返回undefined。
如果name属性部署了读取函数，则读取函数的this绑定receiver。
```js
var obj = {
  get foo() { return this.bar(); },
  bar: function() { ... }
}

// 下面语句会让 this.bar()
// 变成调用 wrapper.bar()
Reflect.get(obj, "foo", wrapper);
```
（2）Reflect.set(target, name, value, receiver)

设置target对象的name属性等于value。如果name属性设置了赋值函数，则赋值函数的this绑定receiver。

（3）Reflect.has(obj, name)

等同于name in obj。

（4）Reflect.deleteProperty(obj, name)

等同于delete obj[name]。

（5）Reflect.construct(target, args)

等同于new target(...args)，这提供了一种不使用new，来调用构造函数的方法。

（6）Reflect.getPrototypeOf(obj)

读取对象的__proto__属性，对应Object.getPrototypeOf(obj)。

（7）Reflect.setPrototypeOf(obj, newProto)

设置对象的__proto__属性，对应Object.setPrototypeOf(obj, newProto)。

（8）Reflect.apply(fun,thisArg,args)

等同于Function.prototype.apply.call(fun,thisArg,args)。一般来说，如果要绑定一个函数的this对象，可以这样写fn.apply(obj, args)，但是如果函数定义了自己的apply方法，就只能写成Function.prototype.apply.call(fn, obj, args)，采用Reflect对象可以简化这种操作。

注意：
Reflect.set()、Reflect.defineProperty()、Reflect.freeze()、Reflect.seal()和Reflect.preventExtensions()返回一个布尔值，表示操作是否成功。它们对应的`Object`方法，**失败时都会抛出错误**。

# 12.二进制数组
二进制数组（ArrayBuffer对象、TypedArray视图和DataView视图）是JavaScript操作二进制数据的一个接口。
这个接口的原始设计目的，与WebGL项目有关。所谓WebGL，就是指浏览器与显卡之间的通信接口，为了满足JavaScript与显卡之间大量的、实时的数据交换，它们之间的数据通信必须是二进制的，而不能是传统的文本格式。
这时要是存在一种机制，可以像C语言那样，直接操作字节，将4个字节的32位整数，以二进制形式原封不动地送入显卡，脚本的性能就会大幅提升。
二进制数组由**三类对象**组成。
（1）ArrayBuffer对象：代表内存之中的一段二进制数据，可以通过“视图”进行操作。“视图”部署了数组接口，这意味着，可以用数组的方法操作内存。

（2）TypedArray视图：共包括9种类型的视图，比如Uint8Array（无符号8位整数）数组视图, Int16Array（16位整数）数组视图, Float32Array（32位浮点数）数组视图等等。

（3）DataView视图：可以自定义复合格式的视图，比如第一个字节是Uint8（无符号8位整数）、第二、三个字节是Int16（16位整数）、第四个字节开始是Float32（32位浮点数）等等，此外还可以自定义字节序。

**简单说，ArrayBuffer对象代表原始的二进制数据，TypedArray视图用来读写简单类型的二进制数据，DataView视图用来读写复杂类型的二进制数据。**

# 13.Set和Map数据结构
## 13.1 Set
### 13.1.1 基本用法
ES6提供了新的数据结构Set。
它**类似于数组**，但是成员的值都是**唯一**的，**没有重复**的值。
Set本身是一个**构造函数**，用来生成Set数据结构。
```js
var s = new Set();

[2,3,5,4,5,2,2].map(x => s.add(x))

for (let i of s) {console.log(i)}
// 2 3 5 4
```
上面代码通过add方法向Set结构加入成员，结果表明Set结构**不会添加重复的值**。

Set函数可以接受一个数组（或类似数组的对象）作为**参数**，用来初始化。
```js
var set = new Set([1, 2, 3, 4, 4])
[...set]
// [1, 2, 3, 4]

var items = new Set([1, 2, 3, 4, 5, 5, 5, 5]);
items.size // 5

function divs () {
  return [...document.querySelectorAll('div')]
}

var set = new Set(divs())
set.size // 56

// 类似于
divs().forEach(div => set.add(div))
set.size // 56
```
向Set加入值的时候，**不会发生类型转换**，所以5和"5"是两个不同的值。
Set内部判断两个值**是否不同**，使用的算法叫做“Same-value equality”，它类似于精确相等运算符（===），主要的区别是**NaN等于自身**，而精确相等运算符认为NaN不等于自身。
```js
let set = new Set();
let a = NaN;
let b = NaN;
set.add(a);
set.add(b);
set // Set {NaN}   同一个值，所以只有一个
```
另外，两个**对象**总是不相等的。
```js
let set = new Set();

set.add({})
set.size // 1

set.add({})
set.size // 2
```
### 13.1.2 Set实例的属性和方法
Set结构的实例有以下属性。

`Set.prototype.constructor`：构造函数，默认就是Set函数。
`Set.prototype.size`：返回Set实例的成员总数。
Set实例的方法分为两大类：操作方法（用于操作数据）和遍历方法（用于遍历成员）。下面先介绍四个操作方法。

`add(value)`：添加某个值，返回Set结构本身。
`delete(value)`：删除某个值，返回一个布尔值，表示删除是否成功。
`has(value)`：返回一个布尔值，表示该值是否为Set的成员。
`clear()`：清除所有成员，没有返回值。
```js
// 对象的写法
var properties = {
  "width": 1,
  "height": 1
};

if (properties[someName]) {
  // do something
}

// Set的写法
var properties = new Set();

properties.add("width");
properties.add("height");

if (properties.has(someName)) {
  // do something
}
```
`Array.from`方法可以将Set结构`转为数组`。
**可以有效的通过这个方法来去重**
```js
var items = new Set([1, 2, 3, 4, 5]);
var array = Array.from(items);
```
### 13.1.3 遍历操作
Set结构的实例有四个遍历方法，可以用于遍历成员。

`keys()`：返回一个键名的遍历器
`values()`：返回一个键值的遍历器
`entries()`：返回一个键值对的遍历器
`forEach()`：使用回调函数遍历每个成员

由于Set结构**没有键名**，只有键值（或者说键名和键值是同一个值），所以key方法和value方法的行为完全一致。
```js
let set = new Set(['red', 'green', 'blue']);

for ( let item of set.values() ){
  console.log(item);
}
// red
// green
// blue

for ( let item of set.entries() ){
  console.log(item);
}
// ["red", "red"]
// ["green", "green"]
// ["blue", "blue"]
```
Set结构的实例默认可遍历，它的**默认**遍历器生成函数就是它的values方法。
```js
Set.prototype[Symbol.iterator] === Set.prototype.values
// true
```
这意味着，可以**省略values**方法，直接用for...of循环遍历Set。
```js
let set = new Set(['red', 'green', 'blue']);

for (let x of set) {           //省略value
  console.log(x);
}
// red
// green
// blue
```
由于**扩展运算符（...）内部使用for...of循环**，所以也可以用于Set结构。
```js
let set = new Set(['red', 'green', 'blue']);
let arr = [...set];
// ['red', 'green', 'blue']
```
这就提供了另一种便捷的**去除数组重复元素**的方法。
```js
let arr = [3, 5, 2, 2, 5, 5];
let unique = [...new Set(arr)];
// [3, 5, 2]
```
而且，数组的map和filter方法也可以用于Set了。
```js
let set = new Set([1, 2, 3]);
set = new Set([...set].map(x => x * 2));
// 返回Set结构：{2, 4, 6}

let set = new Set([1, 2, 3, 4, 5]);
set = new Set([...set].filter(x => (x % 2) == 0));
// 返回Set结构：{2, 4}
```
因此使用Set，可以很容易地实现**并集（Union）、交集（Intersect）和差集（Difference）**。
```js
let a = new Set([1, 2, 3]);
let b = new Set([4, 3, 2]);

// 并集
let union = new Set([...a, ...b]);
// [1, 2, 3, 4]

// 交集
let intersect = new Set([...a].filter(x => b.has(x)));
// [2, 3]

// 差集
let difference = new Set([...a].filter(x => !b.has(x)));
// [1]
```
Set结构的实例的forEach方法，用于对每个成员执行某种操作，没有返回值。
```js
let set = new Set([1, 2, 3]);
set.forEach((value, key) => console.log(value * 2) )
// 2
// 4
// 6
```
上面代码说明,forEach方法的参数就是一个处理函数。该函数的参数依次为键值、键名、集合本身（上例省略了该参数）。另外，forEach方法还可以有第二个参数，表示绑定的this对象。
如果想在遍历操作中，同步改变原来的Set结构，目前没有直接的方法，但有两种变通方法。一种是利用原Set结构映射出一个新的结构，然后赋值给原来的Set结构；另一种是利用Array.from方法。
```js
// 方法一
let set = new Set([1, 2, 3]);
set = new Set([...set].map(val => val * 2));
// set的值是2, 4, 6

// 方法二
let set = new Set([1, 2, 3]);
set = new Set(Array.from(set, val => val * 2));
// set的值是2, 4, 6
```
## 13.2 WeakSet
WeakSet结构与Set类似，也是**不重复**的值的集合。但是，它与Set有两个区别。

1. WeakSet的成员**只能是对象**，而不能是其他类型的值。
2. WeakSet中的对象都是弱引用，即垃圾回收机制不考虑WeakSet对该对象的引用，也就是说，如果其他对象都不再引用该对象，那么垃圾回收机制会自动回收该对象所占用的内存，不考虑该对象还存在于WeakSet之中。这个特点意味着，无法引用WeakSet的成员，因此WeakSet是**不可遍历**的。
```js
var ws = new WeakSet();
ws.add(1)           //只能放置对象，所以报错
// TypeError: Invalid value used in weak set
ws.add(Symbol())    //Symbol()是新的数据类型也不是对象
// TypeError: invalid value used in weak set
```
WeakSet是一个**构造函数**，可以使用new命令，创建WeakSet数据结构。
```js
var ws = new WeakSet();
```
```js
var a = [[1,2], [3,4]];
var ws = new WeakSet(a);
```
上面代码中，a是一个数组，它有两个成员，也都是数组。将a作为WeakSet构造函数的参数，a的成员会**自动成为WeakSet的成员**。
**是a数组的成员成为WeakSet的成员，而不是a数组本身。**
这意味着，数组的**成员只能是对象**。
WeakSet结构有以下三个方法。

`WeakSet.prototype.add(value)`：向WeakSet实例添加一个新成员。
`WeakSet.prototype.delete(value)`：清除WeakSet实例的指定成员。
`WeakSet.prototype.has(value)`：返回一个布尔值，表示某个值是否在WeakSet实例之中。

WeakSet**没有** `size`属性，没有办法遍历它的成员。
WeakSet不能遍历，是因为成员都是**弱引用，随时可能消失**，遍历机制无法保证成员的存在，很可能刚刚遍历结束，成员就取不到了。
WeakSet的一个用处，是储存DOM节点，而不用担心这些节点从文档移除时，会引发内存泄漏。
```js
const foos = new WeakSet()
class Foo {
  constructor() {
    foos.add(this)
  }
  method () {
    if (!foos.has(this)) {
      throw new TypeError('Foo.prototype.method 只能在Foo的实例上调用！')
    }
  }
}
```
上面代码保证了Foo的实例方法，只能在Foo的实例上调用。这里使用WeakSet的好处是，foos对实例的引用，不会被计入内存回收机制，所以删除实例的时候，不用考虑foos，也不会出现内存泄漏。

## 13.3 Map
### 13.3.1 Map结构的目的和基本用法
JavaScript的对象（Object），本质上是键值对的集合（Hash结构），但是只能用字符串当作键。这给它的使用带来了很大的限制。
ES6提供了Map数据结构。它类似于对象，也是键值对的集合，但是“键”的范围**不限于字符串**，各种类型的值（包括对象）都可以当作键。
```js
var m = new Map();
var o = {p: "Hello World"};

m.set(o, "content")
m.get(o) // "content"

m.has(o) // true
m.delete(o) // true
m.has(o) // false
//数组
var map = new Map([["name", "张三"], ["title", "Author"]]);

map.size // 2
map.has("name") // true
map.get("name") // "张三"
map.has("title") // true
map.get("title") // "Author"
```
如果对同一个键多次赋值，后面的值将**覆盖**前面的值。
如果读取一个**未知的键**（没有定义过的），则返回`undefined`。
只有对同一个对象的引用，Map结构才将其视为同一个键。
同样的值的两个实例，在Map结构中被视为两个键。
```js
var map = new Map();

map.set(['a'], 555);
map.get(['a']) // undefined     这两个['a']内存地址是不同的？

var k1 = ['a'];
var k2 = ['a'];

map
.set(k1, 111)
.set(k2, 222);

map.get(k1) // 111
map.get(k2) // 222
```
**由此可知Map的键实际上是跟内存地址绑定的，只要内存地址不一样，就视为两个键。**
```js
let map = new Map();

map.set(NaN, 123);
map.get(NaN) // 123

map.set(-0, 123);
map.get(+0) // 123
```
### 13.3.2 实例的属性和操作方法
（1）size属性
size属性返回Map结构的成员总数。

（2）set(key, value)
set方法设置key所对应的键值，然后返回整个Map结构。如果key已经有值，则键值会被更新，否则就新生成该键。
set方法返回的是Map本身，因此可以采用**链式**写法。

（3）get(key)
get方法读取key对应的键值，如果找不到key，返回undefined。

（4）has(key)
has方法返回一个布尔值，表示某个键是否在Map数据结构中。

（5）delete(key)
delete方法删除某个键，返回true。如果删除失败，返回false。

（6）clear()
clear方法清除所有成员，没有返回值。

### 13.3.3 遍历方法
Map原生提供三个遍历器生成函数和一个遍历方法。

`keys()`：返回键名的遍历器。
`values()`：返回键值的遍历器。
`entries()`：返回所有成员的遍历器。
`forEach()`：遍历Map的所有成员。

```js
let map = new Map([
  ['F', 'no'],
  ['T',  'yes'],
]);

for (let key of map.keys()) {
  console.log(key);
}
// "F"
// "T"

for (let value of map.values()) {
  console.log(value);
}
// "no"
// "yes"

for (let item of map.entries()) {
  console.log(item[0], item[1]);
}
// "F" "no"
// "T" "yes"

// 或者
for (let [key, value] of map.entries()) {
  console.log(key, value);
}

// 等同于使用map.entries()
for (let [key, value] of map) {
  console.log(key, value);
}
```
上面代码最后的那个例子，表示Map结构的默认遍历器接口（Symbol.iterator属性），就是entries方法。
```js
map[Symbol.iterator] === map.entries
// true
```
Map结构**转为数组**结构，比较快速的方法是结合使用**扩展运算符**（...）。
```js
let map = new Map([
  [1, 'one'],
  [2, 'two'],
  [3, 'three'],
]);

[...map.keys()]
// [1, 2, 3]
```
结合数组的map方法、filter方法，可以实现Map的遍历和过滤（**Map本身没有map和filter方法**）
```js
let map0 = new Map()
  .set(1, 'a')
  .set(2, 'b')
  .set(3, 'c');

let map1 = new Map(
  [...map0].filter(([k, v]) => k < 3)
);
// 产生Map结构 {1 => 'a', 2 => 'b'}

let map2 = new Map(
  [...map0].map(([k, v]) => [k * 2, '_' + v])
    );
// 产生Map结构 {2 => '_a', 4 => '_b', 6 => '_c'}
```
Map还有一个forEach方法，与数组的forEach方法类似，也可以实现遍历。
forEach方法还可以接受**第二个参数**，用来绑定`this`。

### 13.3.4 与其他数据结构的互相转换
（1）Map转为数组
前面已经提过，Map转为数组最方便的方法，就是使用扩展运算符（...）。
```js
let myMap = new Map().set(true, 7).set({foo: 3}, ['abc']);
[...myMap]
// [ [ true, 7 ], [ { foo: 3 }, [ 'abc' ] ] ]
```
（2）数组转为Map
将数组转入Map构造函数，就可以转为Map。
```js
new Map([[true, 7], [{foo: 3}, ['abc']]])
// Map {true => 7, Object {foo: 3} => ['abc']}
```
（3）Map转为对象
如果所有Map的键都是字符串，它可以转为对象。
```js
function strMapToObj(strMap) {
  let obj = Object.create(null);
  for (let [k,v] of strMap) {
    obj[k] = v;
  }
  return obj;
}

let myMap = new Map().set('yes', true).set('no', false);
strMapToObj(myMap)
// { yes: true, no: false }
```
（4）对象转为Map
```js
function objToStrMap(obj) {
  let strMap = new Map();
  for (let k of Object.keys(obj)) {
    strMap.set(k, obj[k]);
  }
  return strMap;
}

objToStrMap({yes: true, no: false})
// [ [ 'yes', true ], [ 'no', false ] ]
```
（5）Map转为JSON
Map转为JSON要区分两种情况。一种情况是，Map的键名都是字符串，这时可以选择转为对象JSON。
```js
function strMapToJson(strMap) {
  return JSON.stringify(strMapToObj(strMap));
}

let myMap = new Map().set('yes', true).set('no', false);
strMapToJson(myMap)
// '{"yes":true,"no":false}'
```
另一种情况是，Map的键名有非字符串，这时可以选择转为数组JSON。
```js
function mapToArrayJson(map) {
  return JSON.stringify([...map]);
}

let myMap = new Map().set(true, 7).set({foo: 3}, ['abc']);
mapToArrayJson(myMap)
// '[[true,7],[{"foo":3},["abc"]]]'
```
（6）JSON转为Map
JSON转为Map，正常情况下，所有键名都是字符串。
```js
function jsonToStrMap(jsonStr) {
  return objToStrMap(JSON.parse(jsonStr));
}

jsonToStrMap('{"yes":true,"no":false}')
// Map {'yes' => true, 'no' => false}
```
但是，有一种特殊情况，整个JSON就是一个数组，且每个数组成员本身，又是一个有两个成员的数组。这时，它可以一一对应地转为Map。这往往是数组转为JSON的逆操作。
```js
function jsonToMap(jsonStr) {
  return new Map(JSON.parse(jsonStr));
}

jsonToMap('[[true,7],[{"foo":3},["abc"]]]')
// Map {true => 7, Object {foo: 3} => ['abc']}
```

## 13.4 WeakMap
WeakMap结构与Map结构基本类似，唯一的区别是它只接受**对象**作为键名（null除外），不接受其他类型的值作为键名，而且键名所指向的对象，不计入垃圾回收机制。
典型应用是，一个对应DOM元素的WeakMap结构，当某个DOM元素被清除，其所对应的WeakMap记录就会自动被移除。
```js
var map = new WeakMap()
map.set(1, 2)
// TypeError: 1 is not an object!
map.set(Symbol(), 2)
// TypeError: Invalid value used as weak map key
```
WeakMap与Map在API上的区别主要是两个:
一是没有遍历操作（即没有key()、values()和entries()方法），也没有size属性；
二是无法清空，即不支持clear方法。
因此，WeakMap只有四个方法可用：get()、set()、has()、delete()。

前文说过，WeakMap应用的典型场合就是DOM节点作为键名。下面是一个例子。
```js
let myElement = document.getElementById('logo');
let myWeakmap = new WeakMap();

myWeakmap.set(myElement, {timesClicked: 0});

myElement.addEventListener('click', function() {
  let logoData = myWeakmap.get(myElement);
  logoData.timesClicked++;
  myWeakmap.set(myElement, logoData);
}, false);
```
上面代码中，myElement是一个DOM节点，每当发生click事件，就更新一下状态。我们将这个状态作为键值放在WeakMap里，对应的键名就是myElement。一旦这个DOM节点删除，该状态就会自动消失，不存在内存泄漏风险。

WeakMap的另一个用处是部署私有属性。
```js
let _counter = new WeakMap();
let _action = new WeakMap();

class Countdown {
  constructor(counter, action) {
    _counter.set(this, counter);
    _action.set(this, action);
  }
  dec() {
    let counter = _counter.get(this);
    if (counter < 1) return;
    counter--;
    _counter.set(this, counter);
    if (counter === 0) {
      _action.get(this)();
    }
  }
}

let c = new Countdown(2, () => console.log('DONE'));

c.dec()
c.dec()
// DONE
```

# 14. Iterator和for...of循环
## 14.1 Iterator（遍历器）的概念
JavaScript原有的表示“集合”的数据结构，主要是**数组（Array）**和**对象（Object）**，ES6又添加了**Map**和**Set**。
Iterator的作用有三个：
一是为各种数据结构，提供一个统一的、简便的访问接口；
二是使得数据结构的成员能够按某种次序排列；
三是ES6创造了一种新的遍历命令for...of循环，Iterator接口主要供for...of消费。
Iterator的遍历过程:
（1）创建一个指针对象，指向当前数据结构的起始位置。也就是说，遍历器对象本质上，就是一个指针对象。

（2）第一次调用指针对象的`next`方法，可以将指针指向数据结构的第一个成员。

（3）第二次调用指针对象的`next`方法，指针就指向数据结构的第二个成员。

（4）不断调用指针对象的`next`方法，直到它指向数据结构的结束位置。
每一次调用`next`方法，都会返回数据结构的当前成员的信息。
具体来说，就是返回一个包含`value`和`done`两个属性的对象。
value属性返回当前位置的成员，done属性是一个布尔值，表示遍历是否结束，即是否还有必要**再一次**调用next方法。
`done`为true是为末位
对于遍历器对象来说，done: false和value: undefined属性都是可以**省略**的，因此上面的makeIterator函数可以简写成下面的形式。
```js
function makeIterator(array){
  var nextIndex = 0;
  return {
    next: function(){
      return nextIndex < array.length ?
        {value: array[nextIndex++]} :
        {done: true};
    }
  }
}
```
## 14.2 数据结构的默认Iterator接口
Iterator接口的目的，就是为所有数据结构，提供了一种统一的访问机制，即for...of循环.
一个数据结构只要具有`Symbol.iterator`属性，就可以认为是“可遍历的”（iterable）。
在ES6中，有三类数据结构**原生具备**Iterator接口：**数组、某些类似数组的对象、Set和Map结构**
除此之外，其他数据结构（主要是对象）的Iterator接口，都需要自己在Symbol.iterator属性上面z**部署**，这样才会被for...of循环遍历。
方法一：一个类部署Iterator接口的写法，Symbol.iterator属性对应一个函数，执行后返回当前对象的遍历器对象。
```js
class RangeIterator {
  constructor(start, stop) {
    this.value = start;
    this.stop = stop;
  }

  [Symbol.iterator]() { return this; }

  next() {
    var value = this.value;
    if (value < this.stop) {
      this.value++;
      return {done: false, value: value};
    } else {
      return {done: true, value: undefined};
    }
  }
}

function range(start, stop) {
  return new RangeIterator(start, stop);
}

for (var value of range(0, 3)) {
  console.log(value);
}
```
方法二：为**对象**添加Iterator接口的例子
```js
let obj = {
  data: [ 'hello', 'world' ],
  [Symbol.iterator]() {
    const self = this;
    let index = 0;
    return {
      next() {
        if (index < self.data.length) {
          return {
            value: self.data[index++],
            done: false
          };
        } else {
          return { value: undefined, done: true };
        }
      }
    };
  }
};
```
方法三：对于**类似数组**的对象（存在数值键名和length属性），部署Iterator接口，有一个简便方法，就是Symbol.iterator方法**直接引用数组**的Iterator接口。
```js
NodeList.prototype[Symbol.iterator] = Array.prototype[Symbol.iterator];
// 或者
NodeList.prototype[Symbol.iterator] = [][Symbol.iterator];

[...document.querySelectorAll('div')] // 可以执行了
```
例子：下面是类似数组的对象调用数组的Symbol.iterator方法的例子。
```js
let iterable = {
  0: 'a',
  1: 'b',
  2: 'c',
  length: 3,
  [Symbol.iterator]: Array.prototype[Symbol.iterator]
};
for (let item of iterable) {
  console.log(item); // 'a', 'b', 'c'
}
```
注意，普通对象部署数组的Symbol.iterator方法，并无效果。
```js
let iterable = {
  a: 'a',         //键必须是0123456
  b: 'b',
  c: 'c',
  length: 3,
  [Symbol.iterator]: Array.prototype[Symbol.iterator]
};
for (let item of iterable) {
  console.log(item); // undefined, undefined, undefined
}
```

## 14.3 调用Iterator接口的场合
（1）解构赋值
对数组和Set结构进行解构赋值时，会默认调用Symbol.iterator方法
```js
let set = new Set().add('a').add('b').add('c');

let [x,y] = set;
// x='a'; y='b'

let [first, ...rest] = set;
// first='a'; rest=['b','c'];
```
（2）扩展运算符
扩展运算符（...）也会调用默认的iterator接口。
（3）yield*
yield*后面跟的是一个可遍历的结构，它会调用该结构的遍历器接口。
（4）其他场合

由于数组的遍历会调用遍历器接口，所以任何接受**数组作为参数**的场合，其实**都调用**了遍历器接口。下面是一些例子。

## 14.4 字符串的Iterator接口
字符串是一个类似数组的对象，也原生具有Iterator接口。
```js
var someString = "hi";
typeof someString[Symbol.iterator]
// "function"

var iterator = someString[Symbol.iterator]();

iterator.next()  // { value: "h", done: false }
iterator.next()  // { value: "i", done: false }
iterator.next()  // { value: undefined, done: true }
```

## 14.5 Iterator接口与Generator函数
Symbol.iterator方法的**最简单实现**，还是使用下一章要介绍的`Generator`函数。
```js
var myIterable = {};

myIterable[Symbol.iterator] = function* () {
  yield 1;
  yield 2;
  yield 3;
};
[...myIterable] // [1, 2, 3]

// 或者采用下面的简洁写法

let obj = {
  * [Symbol.iterator]() {
    yield 'hello';
    yield 'world';
  }
};

for (let x of obj) {
  console.log(x);
}
// hello
// world
```
上面代码中，Symbol.iterator方法几乎不用部署任何代码，只要用yield命令给出每一步的返回值即可。

## 14.6 遍历器对象的return()，throw()
遍历器对象除了具有next方法，还可以具有return方法和throw方法。
如果for...of循环**提前退出**（通常是因为出错，或者有break语句或continue语句），就会调用`return`方法。
```js
function readLinesSync(file) {
  return {
    next() {
      if (file.isAtEndOfFile()) {
        file.close();
        return { done: true };
      }
    },
    return() {
      file.close();
      return { done: true };
    },
  };
}
```
`throw`方法主要是配合Generator函数使用，一般的遍历器对象用不到这个方法。

## 14.7 for...of循环
作为遍历**所有**数据结构的统一的方法。
只要部署了`Symbol.iterator`属性，就可以用`for...of`循环遍历它的成员。
**for...of循环可以使用的范围包括数组、Set和Map结构、某些类似数组的对象（比如arguments对象、DOM NodeList对象）、后文的Generator对象，以及字符串。**
### 14.7.1 数组
数组原生具备iterator接口，for...of循环本质上就是调用这个接口产生的遍历器，可以用下面的代码证明。
```js
//下面代码的for...of循环的两种写法是等价的。
const arr = ['red', 'green', 'blue'];
let iterator  = arr[Symbol.iterator]();

for(let v of arr) {
  console.log(v); // red green blue
}

for(let v of iterator) {
  console.log(v); // red green blue
}
```
for...of循环可以代替数组实例的`forEach`方法。
```js
const arr = ['red', 'green', 'blue'];

arr.forEach(function (element, index) {
  console.log(element); // red green blue
  console.log(index);   // 0 1 2
});
```
原有的for...in循环，只能获得对象的**键名**，不能直接获取键值。ES6提供for...of循环，允许遍历获得**键值**。
```js
var arr = ['a', 'b', 'c', 'd'];

for (let a in arr) {
  console.log(a); // 0 1 2 3
}

for (let a of arr) {
  console.log(a); // a b c d
}
```
如果要通过for...of循环，获取数组的索引，可以借助数组实例的`entries`方法和`keys`方法，参见《数组的扩展》章节。
for...of循环调用**遍历器接口**，数组的遍历器接口只返回具有数字索引的属性。这一点跟for...in循环也不一样。
```js
let arr = [3, 5, 7];
arr.foo = 'hello';

for (let i in arr) {
  console.log(i); // "0", "1", "2", "foo"
}

for (let i of arr) {
  console.log(i); //  "3", "5", "7"
}
```
上面代码中，for...of循环**不会返回**数组arr的foo属性。

### 14.7.2 Set和Map结构
Set和Map结构也原生具有Iterator接口，可以直接使用for...of循环。
```js
var engines = new Set(["Gecko", "Trident", "Webkit", "Webkit"]);
for (var e of engines) {
  console.log(e);
}
// Gecko
// Trident
// Webkit

var es6 = new Map();
es6.set("edition", 6);
es6.set("committee", "TC39");
es6.set("standard", "ECMA-262");
for (var [name, value] of es6) {
  console.log(name + ": " + value);
}
// edition: 6
// committee: TC39
// standard: ECMA-262
```
注意的地方有**两个**
首先，遍历的**顺序**是按照各个成员被添加进数据结构的顺序。
其次，Set结构遍历时，返回的是一个**值**，而Map结构遍历时，返回的是一个数组，该数组的两个成员分别为当前Map成员的**键名和键值**。
```js
let map = new Map().set('a', 1).set('b', 2);
for (let pair of map) {
  console.log(pair);
}
// ['a', 1]
// ['b', 2]

for (let [key, value] of map) {
  console.log(key + ' : ' + value);
}
// a : 1
// b : 2
```
### 14.7.3 计算生成的数据结构
ES6的数组、Set、Map都部署了以下三个方法，配合for-of调用后都返回遍历器对象。
`entries()` 返回一个遍历器对象，用来遍历\[键名, 键值]组成的数组。对于数组，键名就是索引值；对于Set，键名与键值相同。Map结构的iterator接口，默认就是调用entries方法。
`keys()` 返回一个遍历器对象，用来遍历所有的键名。
`values()` 返回一个遍历器对象，用来遍历所有的键值。
这三个方法调用后生成的遍历器对象，所遍历的都是计算生成的数据结构。

### 14.7.4 类似数组的对象
类似数组的对象包括好几类。
下面是for...of循环用于`字符串`、`DOM NodeList`对象、`arguments`对象的例子。
对于字符串来说，for...of循环还有一个特点，就是会**正确识别**32位UTF-16字符。
使用Array.from方法将类数组**转为**数组。
```js
// 字符串
let str = "hello";

for (let s of str) {
  console.log(s); // h e l l o
}

// DOM NodeList对象
let paras = document.querySelectorAll("p");

for (let p of paras) {
  p.classList.add("test");
}

// arguments对象
function printArgs() {
  for (let x of arguments) {
    console.log(x);
  }
}
printArgs('a', 'b');
// 'a'
// 'b'
```
### 14.7.5 对象
对于普通的对象，for...of结构**不能直接使用**，会报错，必须**部署**了iterator**接口**后才能使用。
一种解决方法是，使用Object.keys方法将对象的键名生成一个数组，然后遍历这个数组。**不推荐**
```js
for (var key of Object.keys(someObject)) {
  console.log(key + ": " + someObject[key]);
}
```
第二种方法：一个方便的方法是将数组的Symbol.iterator属性，直接赋值给其他对象的Symbol.iterator属性。
比如，想要让for...of环遍历jQuery对象，只要加上下面这一行就可以了。
```js
jQuery.prototype[Symbol.iterator] =
  Array.prototype[Symbol.iterator];
```
第三种方法：使用Generator函数将对象重新包装一下。
```js
function* entries(obj) {
  for (let key of Object.keys(obj)) {
    yield [key, obj[key]];
  }
}

for (let [key, value] of entries(obj)) {
  console.log(key, "->", value);
}
// a -> 1
// b -> 2
// c -> 3
```
### 14.7.6 与其他遍历语法的比较
以数组为例，JavaScript提供多种遍历语法。最原始的写法就是for循环。
for...in循环的缺点：

1. 数组的键名是数字，但是for...in循环是以字符串作为键名“0”、“1”、“2”等等。
2. for...in循环不仅遍历数字键名，还会遍历手动添加的其他键，甚至包括原型链上的键。
3. 某些情况下，for...in循环会以任意顺序遍历键名。

for...of循环的**优点**：

1. 有着同for...in一样的简洁语法，但是没有for...in那些缺点。
2. 不同用于forEach方法，它可以与break、continue和return配合使用。
3. 提供了遍历所有数据结构的统一操作接口。

下面是一个使用`break`语句，跳出for...of循环的例子。
```js
for (var n of fibonacci) {
  if (n > 1000)
    break;
  console.log(n);
}
```
上面的例子，会输出斐波纳契数列小于等于1000的项。如果当前项大于1000，就会使用break语句跳出for...of循环。

# 15 Generator函数
## 15.1 简介
### 15.1.1 基本概念
Generator函数是ES6提供的一种异步编程解决方案，语法行为与传统函数完全不同。它的异步编程应用请看《异步操作》一章。
Generator函数除了状态机，还是一个**遍历器对象**生成函数。返回的遍历器对象，可以依次遍历Generator函数内部的每一个**状态**。
两个特征：
一是，function关键字与函数名之间有一个**星号**；二是，函数体内部使用yield语句，定义不同的**内部状态**
调用Generator函数后，该函数并**不执行**，返回的也**不是**函数**运行结果**，而是一个指向内部状态的**指针对象**，也就是上一章介绍的**遍历器对象**（Iterator Object）。
下一步，必须调用遍历器对象的`next`方法，使得指针移向下一个状态。
Generator函数是分段执行的，`yield`语句是暂停执行的标记，而`next`方法可以恢复执行。
每次调用遍历器对象的next方法，就会返回一个有着value和done两个属性的对象。
```js
function* helloWorldGenerator() {
  yield 'hello';
  yield 'world';
  return 'ending';
}

var hw = helloWorldGenerator();
hw.next()       // { value: 'hello', done: false }
hw.next()       // { value: 'world', done: false }
hw.next()       // { value: 'ending', done: true }
hw.next()       // { value: undefined, done: true }
```
写法：推荐
```js
function* foo(x, y) { ··· }
```
### 15.1.2 yield语句
yield语句就是暂停标志。
如果没有再遇到新的yield语句，就一直运行到函数结束，直到`return`语句**为止**，并将return语句**后面的表达式的值**，作为返回的对象的value属性值。
**注意**：yield语句后面的表达式，只有当调用next方法、内部指针指向该语句时才会执行，因此等于为JavaScript提供了手动的“惰性求值”（Lazy Evaluation）的语法功能。
yield语句与return语句既有相似之处，也有区别。
相似之处在于，都能**返回**紧跟在语句后面的那个表达式的**值**。
区别在于每次遇到yield，函数暂停执行，下一次再从该位置继续向后执行，而`return`语句**不具备位置记忆**的功能。
Generator函数可以不用yield语句，这时就变成了一个单纯的暂缓执行函数。
```js
function* f() {
  console.log('执行了！')
}

var generator = f();

setTimeout(function () {
  generator.next()
}, 2000);
```
yield语句如果用在一个表达式之中，必须放在**圆括号**里面。
```js
console.log('Hello' + yield); // SyntaxError
console.log('Hello' + yield 123); // SyntaxError

console.log('Hello' + (yield)); // OK
console.log('Hello' + (yield 123)); // OK
```
yield语句用作函数**参数**或**赋值表达式的右边**，可以不加括号。
```js
foo(yield 'a', yield 'b'); // OK
let input = yield; // OK
```
### 15.1.3 与Iterator接口的关系
任意一个对象的Symbol.iterator方法，**等于**该对象的遍历器对象生成函数，调用该函数会返回该对象的一个遍历器对象。
```js
function* gen(){
  // some code
}

var g = gen();

g[Symbol.iterator]() === g
// true
```
上面代码中，gen是一个Generator函数，调用它会生成一个遍历器对象g。
它的Symbol.iterator属性，也是一个遍历器对象生成函数，执行后返回它自己。

## 15.2 next方法的参数
yield句本身没有返回值，或者说总是返回`undefined`。
`next`方法可以带一个**参数**，该参数就会被当作**上一个yield语句的返回值**。
```js
function* f() {
  for(var i=0; true; i++) {
    var reset = yield i;        //执行语句结果是i值
    if(reset) { i = -1; }
  }
}

var g = f();

g.next() // { value: 0, done: false }
g.next() // { value: 1, done: false }
g.next(true) // { value: 0, done: false }
```
上面代码先定义了一个可以无限运行的Generator函数f，如果next方法没有参数，每次运行到yield语句，变量reset的值总是undefined。当next方法带一个参数true时，当前的变量reset就被重置为这个参数（即true），因此i会等于-1，下一轮循环就会从-1开始递增。
如果想要第一次调用next方法时，就能够输入值，可以在Generator函数外面**再包一层**。
```js
function wrapper(generatorFunction) {
  return function (...args) {
    let generatorObject = generatorFunction(...args);    //在eneratorFunction(...args)里先定义一个yield
    generatorObject.next();
    return generatorObject;
  };
}

const wrapped = wrapper(function* () {
  console.log(`First input: ${yield}`);     //这个yield里存的是下一个next的参数，就是hello
  return 'DONE';
});

wrapped().next('hello!')
// First input: hello!

```

## 15.3 for...of循环
for...of循环可以自动遍历Generator函数，且此时不再需要调用next方法。
```js
function *foo() {
  yield 1;
  yield 2;
  yield 3;
  yield 4;
  yield 5;
  return 6;    //return不包含在for···of循环内
}

for (let v of foo()) {
  console.log(v);
}
// 1 2 3 4 5
```
一旦next方法的返回对象的`done`属性为true，for...of循环就会**中止**，且**不包含该返回对象**，所以上面代码的return语句返回的6，不包括在for...of循环之中。
for...of循环、扩展运算符（...）、解构赋值和Array.from方法内部调用的，**都是遍历器接口**。这意味着，它们可以将Generator函数返回的Iterator对象，作为**参数**。
```js
function* numbers () {
  yield 1
  yield 2
  return 3
  yield 4
}

[...numbers()] // [1, 2]

Array.from(numbers()) // [1, 2]

let [x, y] = numbers();
x // 1
y // 2

for (let n of numbers()) {
  console.log(n)
}
// 1
// 2
```
**原生**的JavaScript**对象没有**遍历接口，无法使用for...of循环，通过Generator函数为它加上这个接口，就可以用了。
方法一：通过Generator函数objectEntries为它加上遍历器接口
```js
function* objectEntries(obj) {
  let propKeys = Reflect.ownKeys(obj);

  for (let propKey of propKeys) {
    yield [propKey, obj[propKey]];
  }
}

let jane = { first: 'Jane', last: 'Doe' };

for (let [key, value] of objectEntries(jane)) {
  console.log(`${key}: ${value}`);
}
// first: Jane
// last: Doe
```
方法二：将Generator函数加到对象的Symbol.iterator属性上面。
```js
function* objectEntries() {
  let propKeys = Object.keys(this);

  for (let propKey of propKeys) {
    yield [propKey, this[propKey]];
  }
}

let jane = { first: 'Jane', last: 'Doe' };

jane[Symbol.iterator] = objectEntries;

for (let [key, value] of jane) {
  console.log(`${key}: ${value}`);
}
// first: Jane
// last: Doe
```

## 15.4 Generator.prototype.throw()
Generator函数返回的遍历器对象，都有一个`throw`方法，可以在函数体外抛出错误，然后在Generator函数体内捕获。

## 15.5 Generator.prototype.return()
Generator函数返回的遍历器对象，还有一个`return`方法，可以返回给定的值，并且终结遍历Generator函数。
```js
function* gen() {
  yield 1;
  yield 2;
  yield 3;
}

var g = gen();

g.next()        // { value: 1, done: false }
g.return('foo') // { value: "foo", done: true }
g.next()        // { value: undefined, done: true }
```
遍历器对象g调用return方法后，返回值的value属性就是return方法的参数`foo`。
如果return方法调用时，**不提供参数**，则返回值的value属性为`undefined`。
并且，Generator函数的遍历就**终止**了，返回值的done属性为true，以后再调用next方法，`done`属性总是返回`true`。
如果Generator函数内部有try...finally代码块，那么return方法会推迟到finally代码块执行完再执行。

## 15.6 yield*语句

如果在Generater函数内部，调用**另一个**Generator函数，默认情况下是**没有效果**的。
```js
function* foo() {
  yield 'a';
  yield 'b';
}

function* bar() {
  yield 'x';
  foo();             //无效果
  yield 'y';
}

for (let v of bar()){
  console.log(v);
}
// "x"
// "y"
```
这个就需要用到`yield*`语句，用来在一个Generator函数里面执行另一个Generator函数。
```js
function* bar() {
  yield 'x';
  yield* foo();
  yield 'y';
}

// 等同于
function* bar() {
  yield 'x';
  yield 'a';
  yield 'b';
  yield 'y';
}

// 等同于
function* bar() {
  yield 'x';
  for (let v of foo()) {
    yield v;
  }
  yield 'y';
}

for (let v of bar()){
  console.log(v);
}
// "x"
// "a"
// "b"
// "y"
```
如果yield命令后面跟的是一个遍历器对象，需要在yield命令后面加上**星号**，表明它**返回的是一个遍历器对象**。这被称为`yield*`语句。
`yield*`语句**等同于**在Generator函数内部，部署一个for...of循环。
任何数据结构只要有`Iterator`接口，就可以被`yield*`遍历。
```js
function* concat(iter1, iter2) {
  yield* iter1;
  yield* iter2;
}

// 等同于

function* concat(iter1, iter2) {
  for (var value of iter1) {
    yield value;
  }
  for (var value of iter2) {
    yield value;
  }
}
```
如果被代理的Generator函数有return语句，那么就可以向代理它的Generator函数返回数据。
```js
function *foo() {
  yield 2;
  yield 3;
  return "foo";
}

function *bar() {
  yield 1;
  var v = yield *foo();        //return foo   所以下句是v：foo
  console.log( "v: " + v );
  yield 4;
}

var it = bar();

it.next()
// {value: 1, done: false}
it.next()
// {value: 2, done: false}
it.next()
// {value: 3, done: false}
it.next();
// "v: foo"
// {value: 4, done: false}
it.next()
// {value: undefined, done: true}
```

**yield*命令可以很方便地取出嵌套数组的所有成员。**
```js
function* iterTree(tree) {
  if (Array.isArray(tree)) {
    for(let i=0; i < tree.length; i++) {
      yield* iterTree(tree[i]);
    }
  } else {
    yield tree;
  }
}

const tree = [ 'a', ['b', 'c'], ['d', 'e'] ];

for(let x of iterTree(tree)) {
  console.log(x);
}
// a
// b
// c
// d
// e
```

## 15.7 作为对象属性的Generator函数
如果一个对象的属性是Generator函数，可以简写成下面的形式。
```js
let obj = {
  * myGeneratorMethod() {
    ···
  }
};
//完整形式
let obj = {
  myGeneratorMethod: function* () {
    // ···
  }
};
```

## 15.8 Generator函数的this
ES6规定这个遍历器是Generator函数的实例，也继承了Generator函数的prototype对象上的方法。
```js
function* g() {
  this.a = 11;
}

let obj = g();
obj.a // undefined
```
函数F是一个构造函数，又是一个Generator函数。这时，使用new命令就无法生成F的实例了，因为F返回的是一个内部指针。
```js
function* F(){
  yield this.x = 2;
  yield this.y = 3;
}
var obj = {};
var f = F.bind(obj)();

f.next();  // Object {value: 2, done: false}
f.next();  // Object {value: 3, done: false}
f.next();  // Object {value: undefined, done: true}

obj // { x: 2, y: 3 }
```
## 15.9 Generator函数推导
ES7在数组推导的基础上，提出了Generator函数推导（Generator comprehension）。
Generator函数推导是对数组结构的一种模拟，它的最大优点是惰性求值，即直到真正用到时才会求值，这样可以保证效率。
```js
let bigArray = new Array(100000);
for (let i = 0; i < 100000; i++) {
  bigArray[i] = i;
}

let first = bigArray.map(n => n * n)[0];
console.log(first);
```
上面例子遍历一个大数组，但是在真正遍历之前，这个数组已经生成了，占用了系统资源。如果改用Generator函数推导，就能避免这一点。
下面代码**只在用到时，才会生成一个大数组**。
```js
let bigGenerator = function* () {
  for (let i = 0; i < 100000; i++) {
    yield i;
  }
}

let squared = ( for (n of bigGenerator()) n * n );

console.log(squared.next());
```

## 15.10 含义
### 15.10.1 Generator与状态机
Generator是实现状态机的最佳结构。比如，下面的clock函数就是一个状态机。
```js
var ticking = true;
var clock = function() {
  if (ticking)
    console.log('Tick!');
  else
    console.log('Tock!');
  ticking = !ticking;
}
//用Generator实现
var clock = function*() {
  while (true) {
    console.log('Tick!');
    yield;
    console.log('Tock!');
    yield;
  }
};
```
### 15.10.2 Generator与协程
协程（coroutine）是一种程序运行的方式，可以理解成“协作的线程”或“协作的函数”
（1）协程与子例程的差异
传统的“子例程”（subroutine）采用堆栈式**后进先出**的执行方式，只有当调用的子函数完全**执行完毕**，才会结束执行父函数。
协程与其不同，多个线程（单线程情况下，即**多个函数**）可以并行执行，但是只有一个线程（或函数）处于正在运行的状态，其他线程（或函数）都处于暂停态（suspended），线程（或函数）之间可以**交换执行权**。也就是说，一个线程（或函数）执行到一半，可以**暂停执行**，将执行权**交给另一个线程**（或函数），等到稍后收回执行权的时候，**再恢复**执行。这种可以并行执行、交换执行权的线程（或函数），就称为协程。

从实现上看，在内存中，子例程只使用一个栈（stack），而协程是同时存在多个栈，但只有一个栈是在运行状态，也就是说，协程是以多占用内存为代价，实现多任务的并行。

（2）协程与普通线程的差异

不难看出，协程适合用于多任务运行的环境。在这个意义上，它与普通的线程很相似，都有自己的执行上下文、可以分享全局变量。它们的不同之处在于，同一时间可以**有多个线程处于运行状态，但是运行的协程只能有一个**，其他协程都处于暂停状态。此外，普通的线程是抢先式的，到底哪个线程优先得到资源，必须由运行环境决定，但是协程是合作式的，执行权由协程自己分配。

由于ECMAScript是单线程语言，只能保持一个调用栈。引入协程以后，每个任务可以保持自己的调用栈。这样做的最大好处，就是**抛出错误的时候，可以找到原始的调用栈**。不至于像异步操作的回调函数那样，一旦出错，原始的调用栈早就结束。

Generator函数是ECMAScript 6对协程的实现，但属于不完全实现。Generator函数被称为**半协程**（semi-coroutine），意思是只有Generator函数的调用者，才能将程序的执行权还给Generator函数。如果是完全执行的协程，任何函数都可以让暂停的协程继续执行。

如果将Generator函数当作协程，完全可以将多个需要互相协作的任务写成Generator函数，它们之间使用yield语句交换控制权。

## 15.11 应用
Generator可以**暂停函数执行**，返回任意表达式的值。这种特点使得Generator有多种应用场景。
### 15.11.1 异步操作的同步化表达
Generator函数的暂停执行的效果，意味着**可以把异步操作写在yield语句里面**，等到调用next方法时再往后执行。
这实际上**等同于不需要写回调函数**了，因为异步操作的后续操作可以放在yield语句下面，**反正要等到调用next方法时再执行**。
所以，Generator函数的一个重要实际意义就是用来处理异步操作，**改写回调函数**
```js
function* loadUI() {
  showLoadingScreen();
  yield loadUIDataAsynchronously();
  hideLoadingScreen();
}
var loader = loadUI();
// 加载UI
loader.next()     //执行showLoadingScreen();并且加载loadUIDataAsynchronously();

// 卸载UI
loader.next()     //执行hideLoadingScreen();
```
部署Ajax操作，用**同步**的方式表达。
```js
function* main() {
  var result = yield request("http://some.url");
  var resp = JSON.parse(result);
    console.log(resp.value);
}

function request(url) {
  makeAjaxCall(url, function(response){
    it.next(response);
  });
}

var it = main();
it.next();
```
上面代码的main函数，就是通过Ajax操作获取数据。可以看到，除了多了一个yield，它几乎与同步操作的写法完全一样。注意，makeAjaxCall函数中的next方法，必须加上response参数，因为yield语句构成的表达式，本身是没有值的，总是等于undefined。

### 15.11.2 控制流管理
如果有一个多步操作非常耗时，采用回调函数，可能会写成下面这样。
```js
step1(function (value1) {
  step2(value1, function(value2) {
    step3(value2, function(value3) {
      step4(value3, function(value4) {
        // Do something with value4
      });
    });
  });
});
```
采用`Promise`改写上面的代码。
```js
Q.fcall(step1)
  .then(step2)
  .then(step3)
  .then(step4)
  .then(function (value4) {
    // Do something with value4
  }, function (error) {
    // Handle any error from step1 through step4
  })
  .done();
```
上面代码已经把回调函数，改成了直线执行的形式，但是加入了大量Promise的语法。Generator函数可以**进一步改善**代码运行流程。
```js
function* longRunningTask() {
  try {
    var value1 = yield step1();
    var value2 = yield step2(value1);
    var value3 = yield step3(value2);
    var value4 = yield step4(value3);
    // Do something with value4
  } catch (e) {
    // Handle any error from step1 through step4
  }
}
//然后，使用一个函数，按次序自动执行所有步骤
scheduler(longRunningTask());

function scheduler(task) {
  setTimeout(function() {
    var taskObj = task.next(task.value);
    // 如果Generator函数未结束，就继续调用
    if (!taskObj.done) {
      task.value = taskObj.value
      scheduler(task);
    }
  }, 0);
}
```
注意，yield语句**是同步**运行，不是异步运行（否则就失去了取代回调函数的设计目的了）。实际操作中，一般让yield语句返回Promise对象。
```js
var Q = require('q');

function delay(milliseconds) {
  var deferred = Q.defer();
  setTimeout(deferred.resolve, milliseconds);
  return deferred.promise;
}

function* f(){
  yield delay(100);
};
```
上面代码使用Promise的函数库Q，yield语句返回的就是一个Promise对象。
多个任务按顺序一个接一个执行时，yield语句可以按顺序排列。多个任务需要并列执行时（比如只有A任务和B任务都执行完，才能执行C任务），可以采用数组的写法。
```js
function* parallelDownloads() {
  let [text1,text2] = yield [
    taskA(),
    taskB()
  ];
  console.log(text1, text2);
}
```
上面代码中，yield语句的参数是一个数组，成员就是两个任务taskA和taskB，只有等这两个任务都完成了，才会接着执行下面的语句。
### 15.11.3 部署iterator接口
利用Generator函数，可以在任意对象上**部署iterator接口**。
```js
function* iterEntries(obj) {
  let keys = Object.keys(obj);
  for (let i=0; i < keys.length; i++) {
    let key = keys[i];
    yield [key, obj[key]];
  }
}

let myObj = { foo: 3, bar: 7 };

for (let [key, value] of iterEntries(myObj)) {
  console.log(key, value);
}

// foo 3
// bar 7
```
这个是给对象添加iterator接口，已经说过很多次了

### 15.11.4 作为数据结构
Generator可以看作是数据结构，更确切地说，可以看作是一个数组结构，因为Generator函数可以返回一系列的值，这意味着它可以对任意表达式，**提供类似数组的接口**。
```js
function *doStuff() {
  yield fs.readFile.bind(null, 'hello.txt');
  yield fs.readFile.bind(null, 'world.txt');
  yield fs.readFile.bind(null, 'and-such.txt');
}
//处理这三个返回的函数
for (task of doStuff()) {
  // task是一个函数，可以像回调函数那样使用它
}
```

# 16 Promise对象
## 16.1 Promise的含义
Promise是异步编程的一种解决方案，比传统的解决方案——**回调函数和事件**——更合理和更强大。
所谓Promise，简单说就是一个容器，里面保存着**某个未来才会结束的事件**（通常是一个异步操作）的结果。

Promise对象有以下两个特点。
（1）对象的状态**不受外界影响**。Promise对象代表一个异步操作，有**三种状态**：Pending（进行中）、Resolved（已完成，又称Fulfilled）和Rejected（已失败）。
只有异步操作的结果，可以决定当前是哪一种状态，**任何其他操作都无法改变这个状态**。这也是Promise这个名字的由来，它的英语意思就是“承诺”，表示其他手段无法改变。
（2）一旦状态改变，**就不会再变**，任何时候都可以得到这个结果。
Promise对象的状态改变，只有**两种可能**：从`Pending`变为`Resolved`和从`Pending`变为`Rejected`。

Promise也有一些**缺点**。
首先，**无法取消**Promise，一旦新建它就会**立即执行**，无法中途取消。
其次，如果**不设置回调函数**，Promise内部抛出的错误，不会反应到外部。
第三，当处于Pending状态时，无法得知目前进展到哪一个阶段（刚刚开始还是即将完成）。

**如果某些事件不断地反复发生，一般来说，使用stream模式是比部署Promise更好的选择。**

## 16.2 基本用法
ES6规定，Promise对象是一个构造函数，用来生成Promise实例。

下面代码创造了一个Promise实例。
```js
var promise = new Promise(function(resolve, reject) {
  // ... some code

  if (/* 异步操作成功 */){
    resolve(value);
  } else {
    reject(error);
  }
});
```
Promise实例生成以后，可以用`then`方法分别指定Resolved状态和Reject状态的**回调函数**。
then方法可以接受两个回调函数作为**参数**。第一个回调函数是Promise对象的状态变为Resolved时调用，第二个回调函数是Promise对象的状态变为Reject时调用。
```js
promise.then(function(value) {
  // success
}, function(value) {
  // failure
});
```
一个Promise对象的简单例子。
```js
function timeout(ms) {
  return new Promise((resolve, reject) => {
    setTimeout(resolve, ms, 'done');
  });
}

timeout(100).then((value) => {
  console.log(value);
});
```
上面代码中，timeout方法返回一个Promise实例，表示一段时间以后才会发生的结果。过了指定的时间（ms参数）以后，Promise实例的状态变为Resolved，就会触发**then方法绑定的回调函数**。
Promise新建后就会**立即执行**。
Promise实例的状态变为Resolved，**就会触发then方法绑定的回调函数**。
```js
let promise = new Promise(function(resolve, reject) {
  console.log('Promise');
  resolve();
});

promise.then(function() {         //异步执行的
  console.log('Resolved.');
});

console.log('Hi!');

// Promise
// Hi!
// Resolved
```
下面是异步加载图片的例子。
```js
function loadImageAsync(url) {
  return new Promise(function(resolve, reject) {
    var image = new Image();

    image.onload = function() {
      resolve(image);
    };

    image.onerror = function() {
      reject(new Error('Could not load image at ' + url));
    };

    image.src = url;
  });
}
```
下面是一个用Promise对象实现的Ajax操作的例子。
```js
var getJSON = function(url) {
  var promise = new Promise(function(resolve, reject){
    var client = new XMLHttpRequest();
    client.open("GET", url);
    client.onreadystatechange = handler;
    client.responseType = "json";
    client.setRequestHeader("Accept", "application/json");
    client.send();

    function handler() {
      if ( this.readyState !== 4 ) {
        return;
      }
      if (this.status === 200) {
        resolve(this.response);
      } else {
        reject(new Error(this.statusText));
      }
    };
  });

  return promise;
};

getJSON("/posts.json").then(function(json) {
  console.log('Contents: ' + json);
}, function(error) {
  console.error('出错了', error);
});
```
异步操作的结果有可能是一个值，也有可能是**另一个异步操作**，比如像下面这样。
```js
var p1 = new Promise(function(resolve, reject){
  // ...
});

var p2 = new Promise(function(resolve, reject){
  // ...
  resolve(p1);
})
```
注意，这时p1的状态就会传递给p2，也就是说，p1的状态决定了p2的状态。如果p1的状态是Pending，那么p2的回调函数就会等待p1的状态改变；如果p1的状态已经是Resolved或者Rejected，那么p2的回调函数将会立刻执行。
```js
var p1 = new Promise(function (resolve, reject) {
  setTimeout(() => reject(new Error('fail')), 3000)
})
var p2 = new Promise(function (resolve, reject) {
  setTimeout(() => resolve(p1), 1000)
})
p2.then(result => console.log(result))
p2.catch(error => console.log(error))
// Error: fail
```
上面代码中，p1是一个Promise，3秒之后变为rejected。p2的状态由p1决定，1秒之后，p2调用resolve方法，但是此时p1的状态还没有改变，因此p2的状态也不会变。又过了2秒，p1变为rejected，p2也跟着变为rejected。

## 16.3 Promise.prototype.then() 
它的作用是为Promise实例添加状态改变时的回调函数。
then方法返回的是一个**新的**Promise实例（注意，**不是原来那个Promise实例**）。因此可以采用**链式**写法，即then方法后面再调用另一个then方法。
```js
getJSON("/posts.json").then(function(json) {
  return json.post;
}).then(function(post) {
  // ...
});
```
上面的代码使用then方法，依次指定了两个回调函数。第一个回调函数完成以后，会将返回结果作为参数，传入第二个回调函数。
采用链式的then，可以指定一组按照次序调用的回调函数。这时，前一个回调函数，有可能返回的还是一个Promise对象（即有异步操作），这时后一个回调函数，就会等待该Promise对象的状态发生变化，才会被调用。
```js
getJSON("/post/1.json").then(function(post) {
  return getJSON(post.commentURL);
}).then(function funcA(comments) {
  console.log("Resolved: ", comments);
}, function funcB(err){
  console.log("Rejected: ", err);
});
```
上面代码中，第一个then方法指定的回调函数，返回的是另一个Promise对象。这时，第二个then方法指定的回调函数，就会等待这个新的Promise对象状态发生变化。如果变为Resolved，就调用funcA，如果状态变为Rejected，就调用funcB。

### 16.4 Promise.prototype.catch()
Promise.prototype.catch方法是.then(null, rejection)的别名，用于指定**发生错误**时的回调函数。
一般来说，**不要在**then方法里面定义Reject状态的回调函数（即then的第二个参数），总是使用catch方法。
需要注意的是，catch方法返回的还是一个Promise对象，因此后面还可以接着调用then方法。
```js
getJSON("/posts.json").then(function(posts) {
  // ...
}).catch(function(error) {
  // 处理 getJSON 和 前一个回调函数运行时发生的错误
  console.log('发生错误！', error);
});
```
Promise对象的错误具有**“冒泡”**性质，会一直向后传递，**直到被捕获为止**。也就是说，错误总是会被下一个catch语句捕获。
```js
getJSON("/post/1.json").then(function(post) {
  return getJSON(post.commentURL);
}).then(function(comments) {
  // some code
}).catch(function(error) {
  // 处理前面三个Promise产生的错误
});
```
上面代码中，一共有三个Promise对象：一个由getJSON产生，两个由then产生。它们之中任何一个抛出的错误，都会被最后一个catch捕获。
一般来说，不要在then方法里面定义Reject状态的回调函数（即then的第二个参数），总是使用catch方法。
```js
// bad
promise
  .then(function(data) {
    // success
  }, function(err) {
    // error
  });

// good
promise
  .then(function(data) { //cb
    // success
  })
  .catch(function(err) {
    // error
  });
```
Node.js有一个`unhandledRejection`事件，专门监听未捕获的reject错误。
```js
process.on('unhandledRejection', function (err, p) {
  console.error(err.stack)
});
```
上面代码中，unhandledRejection事件的监听函数有两个参数，第一个是错误对象，第二个是报错的Promise实例，它可以用来了解发生错误的环境信息。

## 16.5 Promise.all()
romise.all方法用于将多个Promise实例，包装成一个新的Promise实例。
Promise.all方法的参数**可以不是数组**，但**必须具有Iterator接口**，且返回的每个成员**都是Promise实例**。
```js
var p = Promise.all([p1, p2, p3]);
```
（1）只有p1、p2、p3的状态都变成fulfilled，p的状态才会变成fulfilled
（2）只要p1、p2、p3之中有一个被rejected，p的状态就变成rejected
```js
// 生成一个Promise对象的数组
var promises = [2, 3, 5, 7, 11, 13].map(function (id) {
  return getJSON("/post/" + id + ".json");
});

Promise.all(promises).then(function (posts) {
  // ...
}).catch(function(reason){
  // ...
});
```

## 16.6 Promise.race()
Promise.race方法同样是将多个Promise实例，包装成一个新的Promise实例。
```js
var p = Promise.race([p1,p2,p3]);
```
上面代码中，只要p1、p2、p3之中**有一个实例率先改变状态**，**p的状态就跟着改变**。那个率先改变的Promise实例的返回值，就传递给p的回调函数。

## 16.7 Promise.resolve()
有时需要将现有对象转为Promise对象，Promise.resolve方法就起到这个作用。
```js
var jsPromise = Promise.resolve($.ajax('/whatever.json'));
```
```js
Promise.resolve('foo')
// 等价于
new Promise(resolve => resolve('foo'))
```
Promise.resolve方法的参数分成**四种**情况
（1）参数是一个Promise实例
如果参数是Promise实例，那么Promise.resolve将不做任何修改、原封不动地返回这个实例。
（2）参数是一个thenable对象
thenable对象指的是具有then方法的对象，比如下面这个对象。
```js
let thenable = {
  then: function(resolve, reject) {
    resolve(42);
  }
};
```
Promise.resolve方法会将这个对象**转为Promise对象**，然后就**立即执行thenable对象**的then方法。
（3）参数不是具有then方法的对象，或根本就不是对象
如果参数是一个原始值，或者是一个不具有then方法的对象，则Promise.resolve方法返回一个新的Promise对象，状态为Resolved。
```js
var p = Promise.resolve('Hello');

p.then(function (s){
  console.log(s)
});
// Hello
```
（4）不带有任何参数
Promise.resolve方法允许调用时不带参数，直接返回一个Resolved状态的Promise对象。
```js
var p = Promise.resolve();

p.then(function () {
  // ...
});
```

## 16.8 Promise.reject()
Promise.reject(reason)方法也会返回一个新的Promise实例，该实例的状态为rejected
```js
var p = Promise.reject('出错了');
// 等同于
var p = new Promise((resolve, reject) => reject('出错了'))

p.then(null, function (s){
  console.log(s)
});
// 出错了
```

## 16.9 两个有用的附加方法
下面介绍如何部署两个不在ES6之中、但很有用的方法。
### 16.9.1 done()
Promise对象的回调链，不管以then方法或catch方法结尾，要是最后一个方法抛出错误，都有可能无法捕捉到（因为Promise内部的错误不会冒泡到全局）。因此，我们可以提供一个done方法，总是处于回调链的尾端，保证抛出任何可能出现的错误。
```js
asyncFunc()
  .then(f1)
  .catch(r1)
  .then(f2)
  .done();
```
实现代码：
```js
Promise.prototype.done = function (onFulfilled, onRejected) {
  this.then(onFulfilled, onRejected)
    .catch(function (reason) {
      // 抛出一个全局错误
      setTimeout(() => { throw reason }, 0);
    });
};
```

### 16.9.2 finally()
finally方法用于指定不管Promise对象最后状态如何，都会执行的操作。
```js
server.listen(0)
  .then(function () {
    // run test
  })
  .finally(server.stop);
```
实现代码：
```js
Promise.prototype.finally = function (callback) {
  let P = this.constructor;
  return this.then(
    value  => P.resolve(callback()).then(() => value),
    reason => P.resolve(callback()).then(() => { throw reason })
  );
};
```

## 16.10 应用
### 16.10.1 加载图片
我们可以将图片的加载写成一个Promise，一旦加载完成，Promise的状态就发生变化。
```js
const preloadImage = function (path) {
  return new Promise(function (resolve, reject) {
    var image = new Image();
    image.onload  = resolve;
    image.onerror = reject;
    image.src = path;
  });
};
```
### 16.10.2 Generator函数与Promise的结合
使用Generator函数**管理流程**，遇到异步操作的时候，通常返回一个Promise对象。
```js
function getFoo () {
  return new Promise(function (resolve, reject){
    resolve('foo');
  });
}

var g = function* () {
  try {
    var foo = yield getFoo();
    console.log(foo);
  } catch (e) {
    console.log(e);
  }
};

function run (generator) {
  var it = generator();

  function go(result) {
    if (result.done) return result.value;

    return result.value.then(function (value) {
      return go(it.next(value));
    }, function (error) {
      return go(it.throw(error));
    });
  }

  go(it.next());
}

run(g);
```

## 16.11 async函数
async函数与Promise、Generator函数一样，是用来取代回调函数、解决异步操作的一种方法。它本质上是Generator函数的**语法糖**。async函数并不属于ES6，而是被列入了ES7，但是traceur、Babel.js、regenerator等转码器已经支持这个功能，转码后立刻就能使用。

# 17 异步操作和Async函数
Javascript语言的执行环境是“单线程”的，如果没有异步编程，根本没法用，非卡死不可。
ES6诞生以前，异步编程的方法，大概有下面四种。

1. 回调函数
2. 事件监听
3. 发布/订阅
4. Promise 对象

## 17.1 基本概念
### 17.1.1 异步
所谓"异步"，简单说就是一个任务分成两段，先执行第一段，然后转而执行其他任务，等做好了准备，再回过头执行第二段。
相应地，连续的执行就叫做同步。由于是连续执行，不能插入其他任务，所以操作系统从硬盘读取文件的这段时间，程序只能干等着。

### 17.1.2 回调函数
JavaScript语言对异步编程的实现，就是回调函数。所谓回调函数，就是把任务的第二段单独写在一个函数里面，等到重新执行这个任务的时候，就直接调用这个函数。它的英语名字callback，直译过来就是"重新调用"。
一个有趣的问题是，为什么Node.js约定，回调函数的第一个参数，必须是错误对象err（如果没有错误，该参数就是null）？原因是执行分成两段，在这两段之间抛出的错误，程序无法捕捉，只能当作参数，传入第二段。

### 17.1.3 Promise
```js
var readFile = require('fs-readfile-promise');

readFile(fileA)
.then(function(data){
  console.log(data.toString());
})
.then(function(){
  return readFile(fileB);
})
.then(function(data){
  console.log(data.toString());
})
.catch(function(err) {
  console.log(err);
});
```
可以看到，Promise 的写法只是回调函数的改进，使用then方法以后，异步任务的两段执行看得更清楚了，除此以外，**并无新意**。
Promise 的最大问题是**代码冗余**，原来的任务被Promise 包装了一下，不管什么操作，一眼看去都是一堆 then，原来的语义变得很不清楚。

## 17.2 Generator函数
### 17.2.1 协程
传统的编程语言，早有异步编程的解决方案（其实是多任务的解决方案）。其中有一种叫做"协程"（coroutine），意思是多个线程互相协作，完成异步任务。

协程有点像函数，又有点像线程。它的运行流程大致如下。

第一步，协程A开始执行。
第二步，协程A执行到一半，进入暂停，执行权转移到协程B。
第三步，（一段时间后）协程B交还执行权。
第四步，协程A恢复执行。

```js
function *asnycJob() {
  // ...其他代码
  var f = yield readFile(fileA);
  // ...其他代码
}
```
它表示执行到此处，执行权将交给其他协程。也就是说，yield命令是异步两个阶段的分界线。

### 17.2.2 Generator函数的概念

```js
function* gen(x){
  var y = yield x + 2;
  return y;
}

var g = gen(1);
g.next() // { value: 3, done: false }
g.next() // { value: undefined, done: true }
```

### 17.2.3 Generator函数的数据交换和错误处理
```js
function* gen(x){
  try {
    var y = yield x + 2;
  } catch (e){
    console.log(e);
  }
  return y;
}

var g = gen(1);
g.next();
g.throw('出错了');
// 出错了
```
上面代码的最后一行，Generator函数体外，使用指针对象的throw方法抛出的错误，可以被函数体内的try ...catch代码块捕获。这意味着，出错的代码与处理错误的代码，实现了时间和空间上的分离，这对于异步编程无疑是很重要的。

### 17.2.4 异步任务的封装--使用 Generator 函数
```js
var fetch = require('node-fetch');

function* gen(){
  var url = 'https://api.github.com/users/github';
  var result = yield fetch(url);
  console.log(result.bio);
}
//执行
var g = gen();
var result = g.next();

result.value.then(function(data){
  return data.json();
}).then(function(data){
  g.next(data);
});
```
## 17.3 Thunk函数
### 17.3.1 参数的求值策略
传名调用

### 17.3.2 Thunk函数的含义
编译器的"传名调用"实现，往往是将参数放到一个临时函数之中，再将这个临时函数传入函数体。这个临时函数就叫做Thunk函数。
```js
function f(m){
  return m * 2;
}

f(x + 5);

// 等同于

var thunk = function () {
  return x + 5;
};

function f(thunk){
  return thunk() * 2;
}
```

### 17.3.3 JavaScript语言的Thunk函数
任何函数，只要参数有回调函数，就能写成Thunk函数的形式。下面是一个简单的Thunk函数转换器。
```js
var Thunk = function(fn){
  return function (){
    var args = Array.prototype.slice.call(arguments);
    return function (callback){
      args.push(callback);
      return fn.apply(this, args);
    }
  };
};
//使用上面的转换器，生成fs.readFile的Thunk函数。
var readFileThunk = Thunk(fs.readFile);
readFileThunk(fileA)(callback);
```

### 17.3.4 Thunkify模块
生产环境的转换器，建议使用Thunkify模块。

首先是安装
```js
$ npm install thunkify
```
使用方式如下
```js
var thunkify = require('thunkify');
var fs = require('fs');

var read = thunkify(fs.readFile);
read('package.json')(function(err, str){
  // ...
});
```

### 17.3.5 Generator 函数的流程管理
yield命令用于将程序的执行权移出Generator函数，那么就需要一种方法，将执行权再交还给Generator函数。
这种方法就是Thunk函数，因为它可以在回调函数里，将执行权交还给Generator函数。
Thunk函数**其实就是一个执行器**来运行Generator 函数的

### 17.3.6 Thunk函数的自动流程管理
Thunk函数真正的威力，在于可以**自动执行Generator函数**。下面就是一个基于Thunk函数的Generator执行器。
```js
function run(fn) {
  var gen = fn();

  function next(err, data) {
    var result = gen.next(data);
    if (result.done) return;
    result.value(next);
  }

  next();
}

run(gen);
```
用法：
```js
var gen = function* (){
  var f1 = yield readFile('fileA');
  var f2 = yield readFile('fileB');
  // ...
  var fn = yield readFile('fileN');
};

run(gen);
```
## 17.4 co模块
### 17.4.1 基本用法
co模块用于Generator函数的自动执行。
有一个Generator函数，用于依次读取两个文件
```js
var gen = function* (){
  var f1 = yield readFile('/etc/fstab');
  var f2 = yield readFile('/etc/shells');
  console.log(f1.toString());
  console.log(f2.toString());
};
```
co模块可以让你**不用**编写Generator函数的执行器。
```js
var co = require('co');
co(gen);
```
**co函数返回一个Promise对象，因此可以用then方法添加回调函数。**
```js
co(gen).then(function (){
  console.log('Generator 函数执行完成');
})
```

### 17.4.2 co模块的原理
为什么co可以自动执行Generator函数？

前面说过，Generator就是一个异步操作的容器。它的自动执行需要一种机制，当异步操作有了结果，能够自动交回执行权。

两种方法可以做到这一点。

（1）回调函数。将异步操作包装成Thunk函数，**在回调函数里面交回执行权(执行器)**。

（2）Promise 对象。将异步操作包装成Promise对象，**用then方法交回执行权(then)**。

co模块其实就是将两种自动执行器（Thunk函数和Promise对象），包装成一个模块。使用co的前提条件是，**Generator函数的yield命令后面，只能是Thunk函数或Promise对象**。

### 17.4.3 基于Promise对象的自动执行
Generator函数手动执行**其实就是用then方法，层层添加回调函数**。
**then实现的一个自动执行器**。
```js
function run(gen){
  var g = gen();

  function next(data){
    var result = g.next(data);
    if (result.done) return result.value;
    result.value.then(function(data){
      next(data);
    });
  }

  next();
}

run(gen);
```
### 17.4.4 co模块的源码
### 17.4.5 处理并发的异步操作
```js
// 数组的写法
co(function* () {
  var res = yield [
    Promise.resolve(1),
    Promise.resolve(2)
  ];
  console.log(res);
}).catch(onerror);

// 对象的写法
co(function* () {
  var res = yield {
    1: Promise.resolve(1),
    2: Promise.resolve(2),
  };
  console.log(res);
}).catch(onerror);
//下面是另一个例子。
co(function* () {
  var values = [n1, n2, n3];
  yield values.map(somethingAsync);
});

function* somethingAsync(x) {
  // do something async
  return y
}
//上面的代码允许并发三个somethingAsync异步操作，等到它们全部完成，才会进行下一步。
```

## 17.5 async函数
### 17.5.1 含义
ES7提供了async函数，使得异步操作变得更加方便。
async函数就是Generator函数的**语法糖**
用法：
```js
var asyncReadFile = async function (){
  var f1 = await readFile('/etc/fstab');
  var f2 = await readFile('/etc/shells');
  console.log(f1.toString());
  console.log(f2.toString());
};
```
async函数对 Generator 函数的改进，体现在以下**四点**:
（1）**内置执行器**。Generator函数的执行必须靠执行器，所以才有了co模块，而async函数自带执行器。也就是说，async函数的执行，与普通函数一模一样，只要一行。
```js
var result = asyncReadFile();
```
（2）更好的语义。async和await，比起星号和yield，语义更清楚了。async表示函数里有异步操作，await表示紧跟在后面的表达式需要等待结果。

（3）更广的适用性。 co模块约定，yield命令后面只能是Thunk函数或Promise对象，而async函数的await命令后面，可以是**Promise对象和原始类型的值**（数值、字符串和布尔值，但这时等同于同步操作）。

（4）返回值是Promise。async函数的返回值是Promise对象，这比Generator函数的返回值是Iterator对象方便多了。你**可以用then**方法指定下一步的操作。

进一步说，async函数完全可以看作多个异步操作，包装成的一个Promise对象，而await命令就是内部then命令的语法糖。
正常情况下，await命令后面是一个Promise对象，否则会被转成Promise。

### 17.5.2 async函数的实现
### 17.5.3 async 函数的用法
下面是一个例子
```js
async function getStockPriceByName(name) {
  var symbol = await getStockSymbol(name);
  var stockPrice = await getStockPrice(symbol);
  return stockPrice;
}

getStockPriceByName('goog').then(function (result) {
  console.log(result);
});
```
指定多少毫秒后输出一个值
```js
function timeout(ms) {
  return new Promise((resolve) => {
    setTimeout(resolve, ms);
  });
}

async function asyncPrint(value, ms) {
  await timeout(ms);
  console.log(value)
}

asyncPrint('hello world', 50);
```
Async函数有多种使用形式。
```js
// 函数声明
async function foo() {}

// 函数表达式
const foo = async function () {};

// 对象的方法
let obj = { async foo() {} }

// 箭头函数
const foo = async () => {};
```

### 17.5.4 注意点
第一点，await命令后面的Promise对象，运行结果可能是rejected，所以最好把await命令放在try...catch代码块中。
```js
async function myFunction() {
  try {
    await somethingThatReturnsAPromise();
  } catch (err) {
    console.log(err);
  }
}

```
第二点，多个await命令后面的异步操作，如果不存在继发(同步)关系，最好让它们同时触发。
```js
// 写法一
let [foo, bar] = await Promise.all([getFoo(), getBar()]);

// 写法二
let fooPromise = getFoo();
let barPromise = getBar();
let foo = await fooPromise;
let bar = await barPromise;
```
上面两种写法，getFoo和getBar都是**同时触发**，这样就会缩短程序的执行时间。
第三点，await命令只能用在async函数之中，如果用在普通函数，就会报错。
如果确实希望多个请求并发执行，可以使用Promise.all方法。
```js
async function dbFuc(db) {
  let docs = [{}, {}, {}];
  let promises = docs.map((doc) => db.post(doc));

  let results = await Promise.all(promises);
  console.log(results);
}

// 或者使用下面的写法

async function dbFuc(db) {
  let docs = [{}, {}, {}];
  let promises = docs.map((doc) => db.post(doc));

  let results = [];
  for (let promise of promises) {
    results.push(await promise);
  }
  console.log(results);
}
```

### 17.5.5 与Promise、Generator的比较
假定某个DOM元素上面，部署了一系列的动画，前一个动画结束，才能开始后一个。如果当中有一个动画出错，就不再往下执行，返回上一个成功执行的动画的返回值。
首先是Promise的写法。
```js
function chainAnimationsPromise(elem, animations) {

  // 变量ret用来保存上一个动画的返回值
  var ret = null;

  // 新建一个空的Promise
  var p = Promise.resolve();

  // 使用then方法，添加所有动画
  for(var anim in animations) {
    p = p.then(function(val) {
      ret = val;
      return anim(elem);
    })
  }

  // 返回一个部署了错误捕捉机制的Promise
  return p.catch(function(e) {
    /* 忽略错误，继续执行 */
  }).then(function() {
    return ret;
  });

}
```
虽然Promise的写法比回调函数的写法大大改进，但是一眼看上去，代码完全都是Promise的API（then、catch等等），操作本身的语义反而不容易看出来。

接着是Generator函数的写法。
```js
function chainAnimationsGenerator(elem, animations) {

  return spawn(function*() {
    var ret = null;
    try {
      for(var anim of animations) {
        ret = yield anim(elem);
      }
    } catch(e) {
      /* 忽略错误，继续执行 */
    }
      return ret;
  });

}
```
上面代码使用Generator函数遍历了每个动画，语义比Promise写法更清晰，用户定义的操作全部都出现在spawn函数的内部。这个写法的问题在于，必须有一个任务运行器，自动执行Generator函数，上面代码的spawn函数就是自动执行器，它返回一个Promise对象，而且必须保证yield语句后面的表达式，必须返回一个Promise。

最后是Async函数的写法。
```js
async function chainAnimationsAsync(elem, animations) {
  var ret = null;
  try {
    for(var anim of animations) {
      ret = await anim(elem);
    }
  } catch(e) {
    /* 忽略错误，继续执行 */
  }
  return ret;
}
```
可以看到Async函数的实现最简洁，最符合语义，几乎没有语义不相关的代码。它将Generator写法中的自动执行器，改在语言层面提供，不暴露给用户，因此代码量最少。如果使用Generator写法，自动执行器需要用户自己提供。

# 18 Class
先看下边这文章 http://keenwon.com/1524.html
## 18.1 Class基本语法
### 18.1.1 概述
JavaScript语言的传统方法是通过**构造函数**，定义并生成新对象。
ES6提供了更接近传统语言的写法，引入了Class（类）这个概念，作为对象的模板。
通过class关键字，可以定义类。
```js
//构造函数
function Point(x,y){
  this.x = x;
  this.y = y;
}

Point.prototype.toString = function () {
  return '(' + this.x + ', ' + this.y + ')';
}
//类 改写
class Point {

  constructor(x, y) {
    this.x = x;
    this.y = y;
  }
                       //这里没有逗号
  toString() {
    return '(' + this.x + ', ' + this.y + ')';
  }

}
```
方法之间**不需要逗号**分隔，加了会报错。
构造函数的prototype属性，在ES6的“类”上面继续存在。
事实上，类的所有方法**都定义在类的prototype属性上面**。
```js
class Point {
  constructor(){
    // ...
  }

  toString(){
    // ...
  }

  toValue(){
    // ...
  }
}

// 等同于

Point.prototype = {
  toString(){},
  toValue(){}
}
```
**类的实例上面调用方法，其实就是调用原型上的方法**
```js
class B {}
let b = new B();

b.constructor === B.prototype.constructor // true
```
b是B类的实例，它的constructor方法就是B类原型的constructor方法。

`Object.assign`方法可以很方便地一次向类**添加多个方法**。
```js
class Point {
  constructor(){
    // ...
  }
}

Object.assign(Point.prototype, {
  toString(){},
  toValue(){}
})
```
prototype对象的constructor属性，直接指向“类”的本身，这与ES5的行为是一致的。
```js
Point.prototype.constructor === Point // true
```
类的内部所有定义的方法，都是**不可枚举**的
类的**属性**名，可以采用表达式。
```js
let methodName = "getArea";
class Square{
  constructor(length) {
    // ...
  }

  [methodName]() {
    // ...
  }
}
```
上面代码中，Square类的**方法**名getArea，是从表达式得到的。

### 18.1.2 constructor方法
constructor方法是类的默认方法，通过`new`命令**生成**对象实例时，自动调用该方法。
一个类必须有constructor方法，如果没有显式定义，一个空的constructor方法会被**默认添加**。
constructor方法默认返回实例对象（即this），完全可以指定**返回另外一个对象**。
```js
class Foo {
  constructor() {
    return Object.create(null);
  }
}

new Foo() instanceof Foo
// false
```
上面代码中，constructor函数返回一个全新的对象，结果导致实例对象不是Foo类的实例。

### 18.1.3 实例对象
生成实例对象的写法，与ES5完全一样，也是使用`new`命令。
如果忘记加上new，像函数那样调用Class，将会报错。
与ES5一样，实例的属性除非显式定义在其本身（即定义在this对象上），否则都是定义在原型上（即定义在class上）。
```js
//定义类
class Point {

  constructor(x, y) {
    this.x = x;
    this.y = y;
  }

  toString() {
    return '('+this.x+', '+this.y+')';
  }

}

var point = new Point(2, 3);

point.toString() // (2, 3)

point.hasOwnProperty('x') // true
point.hasOwnProperty('y') // true
point.hasOwnProperty('toString') // false
point.__proto__.hasOwnProperty('toString') // true
```
可以通过实例的__proto__属性为Class添加方法

### 18.1.4 name属性
ES6的Class只是ES5的构造函数的一层**包装**，所以函数的许多特性都被Class继承，包括name属性。
```js
class Point {}
Point.name // "Point"
```

### 18.1.5 Class表达式
与函数一样，Class也可以**使用表达式的形式定义**。
```js
const MyClass = class Me {
  getClassName() {
    return Me.name;
  }
};
```
上面代码使用表达式定义了一个类。
需要**注意**的是，这个类的名字是`MyClass` **而不是** `Me`，Me只在Class的内部代码可用，指代当前类。
```js
let inst = new MyClass();
inst.getClassName() // Me 必须通过内部调用
Me.name // ReferenceError: Me is not defined
```
如果Class**内部没用到**的话，可以省略Me，也就是可以写成下面的形式。
采用Class表达式，可以写出**立即执行**的Class。
```js
let person = new class {
  constructor(name) {
    this.name = name;
  }

  sayName() {
    console.log(this.name);
  }
}("张三");

person.sayName(); // "张三"
```
上面代码中，`person`是一个立即执行的Class的实例

### 18.1.6 不存在变量提升
Class**不存在变量提升**（hoist），这一点与ES5完全不同。

### 18.1.7 严格模式
类和模块的内部，**默认**就是严格模式，所以不需要使用use strict指定运行模式。

## 18.2 Class的继承
### 18.2.1 基本用法
Class之间可以通过`extends`关键字实现继承，这比ES5的通过修改原型链实现继承，要清晰和方便很多。
```js
class ColorPoint extends Point {}
```
上面代码定义了一个ColorPoint类，该类通过`extends`关键字，继承了Point类的所有属性和方法。
但是由于没有部署任何代码，所以这两个类完全一样，等于**复制**了一个Point类。下面，我们在ColorPoint内部加上代码。
```js
class ColorPoint extends Point {

  constructor(x, y, color) {
    super(x, y); // 调用父类的constructor(x, y)
    this.color = color;
  }

  toString() {
    return this.color + ' ' + super.toString(); // 调用父类的toString()
  }

}
```
上面代码中，constructor方法和toString方法之中，都出现了super关键字，它指代父类的实例（即父类的this对象）。
子类必须在constructor方法中调用super方法，**否则新建实例时会报错**。这是因为**子类没有自己的this对象**，而是继承父类的this对象，然后对其进行加工。**如果不调用super方法，子类就得不到this对象**。

```js
class Point { /* ... */ }

class ColorPoint extends Point {
  constructor() {
  }
}

let cp = new ColorPoint(); // ReferenceError 
```
上面代码中，ColorPoint继承了父类Point，但是它的构造函数**没有调用super方法**，导致新建实例时报错。
ES5的继承，实质是先创造子类的实例对象this，然后再将父类的方法添加到this上面（Parent.apply(this)）。ES6的继承机制完全不同，实质是先创造父类的实例对象this（所以必须先调用super方法），然后再用子类的构造函数修改this。
如果子类没有定义constructor方法，这个方法会被默认添加，代码如下。也就是说，不管有没有显式定义，**任何一个子类都有constructor方法**。
另一个需要注意的地方是，在子类的构造函数中，**只有调用super之后**，才可以使用this关键字，否则会报错。
这是因为子类实例的构建，是基于对父类实例加工，只有super方法才能返回父类实例。
```js
class Point {
  constructor(x, y) {
    this.x = x;
    this.y = y;
  }
}

class ColorPoint extends Point {
  constructor(x, y, color) {
    this.color = color; // ReferenceError
    super(x, y);    //引入super
    this.color = color; // 正确
  }
}
```
上面代码中，子类的constructor方法没有调用super之前，就使用this关键字，结果报错，而放在super方法之后就是正确的。

下面是生成子类实例的代码。
```js
let cp = new ColorPoint(25, 8, 'green');

cp instanceof ColorPoint // true
cp instanceof Point // true
```

### 18.2.2 类的prototype属性和__proto__属性
大多数浏览器的ES5实现之中，每一个对象都有__proto__属性，指向对应的构造函数的prototype属性。
Class作为构造函数的语法糖，同时有prototype属性和__proto__属性，因此**同时存在两条继承链**。

**类的继承**是按照下面的模式实现的。
```js
class A {
}

class B {
}

// B的实例继承A的实例
Object.setPrototypeOf(B.prototype, A.prototype);

// B继承A的静态属性
Object.setPrototypeOf(B, A);
```
《对象的扩展》一章给出过`Object.setPrototypeOf`方法的实现。
```js
Object.setPrototypeOf(B.prototype, A.prototype);
// 等同于
B.prototype.__proto__ = A.prototype;

Object.setPrototypeOf(B, A);
// 等同于
B.__proto__ = A;
```
这两条继承链，可以这样理解：作为一个对象，子类（B）的原型（__proto__属性）是父类（A）；作为一个构造函数，子类（B）的原型（prototype属性）是父类的实例。
```js
B.prototype = new A();
// 等同于
B.prototype.__proto__ = A.prototype;
```

### 18.2.3 Extends 的继承目标
extends关键字后面可以跟多种类型的值
上面代码的A，只要是一个有prototype属性的函数，就能被B继承。由于函数都有prototype属性，因此A可以是任意函数。

下面，讨论三种特殊情况。

第一种特殊情况，子类继承Object类。
```js
class A extends Object {
}

A.__proto__ === Object // true
A.prototype.__proto__ === Object.prototype // true
```
这种情况下，A其实就是构造函数Object的复制，A的实例就是Object的实例。

第二种特殊情况，不存在任何继承。
```js
class A {
}

A.__proto__ === Function.prototype // true
A.prototype.__proto__ === Object.prototype // true
```
这种情况下，A作为一个基类（即不存在任何继承），就是一个普通函数，所以直接继承Funciton.prototype。但是，A调用后返回一个空对象（即Object实例），所以A.prototype.__proto__指向构造函数（Object）的prototype属性。

第三种特殊情况，子类继承null。
```js
class A extends null {
}

A.__proto__ === Function.prototype // true
A.prototype.__proto__ === undefined // true
```
这种情况与第二种情况非常像。A也是一个普通函数，所以直接继承Funciton.prototype。但是，A调用后返回的对象不继承任何方法，所以它的__proto__指向Function.prototype，即实质上执行了下面的代码。
```js
class C extends null {
  constructor() { return Object.create(null); }
}
```

### 18.2.4 Object.getPrototypeOf() 
Object.getPrototypeOf方法可以用来从子类上获取父类。
```js
Object.getPrototypeOf(ColorPoint) === Point
// true
```
因此，可以使用这个方法**判断**，一个类是否继承了另一个类。

### 18.2.5 super关键字
上面讲过，在子类中，**super关键字代表父类实例**。
```js
class B extends A {
  get m() {
    return this._p * super._p;
  }
  set m() {
    throw new Error('该属性只读');
  }
}
```
上面代码中，子类**通过super关键字，调用父类的实例**。

由于，对象总是继承其他对象的，所以可以在任意一个对象中，使用super关键字。
```js
var obj = {
  toString() {
    return "MyObject: " + super.toString();
  }
}

obj.toString(); // MyObject: [object Object]
```

### 18.2.6 实例的__proto__属性
子类实例的__proto__属性的__proto__属性，指向父类实例的__proto__属性。也就是说，**子类的原型的原型，是父类的原型**。
```js
var p1 = new Point(2, 3);
var p2 = new ColorPoint(2, 3, 'red');

p2.__proto__ === p1.__proto__ // false
p2.__proto__.__proto__ === p1.__proto__ // true
```
上面代码中，ColorPoint继承了Point，导致前者原型的原型是后者的原型。

因此，通过子类实例的__proto__.__proto__属性，可以修改父类实例的行为。

## 18.3 原生构造函数的继承
原生构造函数是指语言内置的构造函数，通常用来生成数据结构。ECMAScript的原生构造函数大致有下面这些。

Boolean()
Number()
String()
Array()
Date()
Function()
RegExp()
Error()
Object()
以前，这些原生构造函数是无法继承的，比如，不能自己定义一个Array的子类。
ES6是先新建父类的实例对象this，然后再用子类的构造函数修饰this，使得父类的所有行为都可以继承。下面是一个继承Array的例子。
```js
class MyArray extends Array {
  constructor(...args) {
    super(...args);
  }
}

var arr = new MyArray();
arr[0] = 12;
arr.length // 1

arr.length = 0;
arr[0] // undefined
```
注意，继承Object的子类，有一个行为差异。
```js
class NewObj extends Object{
  constructor(){
    super(...arguments);
  }
}
var o = new NewObj({attr: true});
console.log(o.attr === true);  // false
```
上面代码中，NewObj继承了Object，但是无法通过super方法向父类Object传参。这是因为ES6改变了Object构造函数的行为，一旦发现Object方法**不是通过new Object()这种形式调用**，ES6规定Object构造函数会**忽略参数**。

## 18.4 Class的取值函数（getter）和存值函数（setter）
与ES5一样，在Class内部可以使用get和set关键字，对某个属性设置存值函数和取值函数，拦截该属性的存取行为。
```js
class MyClass {
  constructor() {
    // ...
  }
  get prop() {
    return 'getter';
  }
  set prop(value) {
    console.log('setter: '+value);
  }
}

let inst = new MyClass();

inst.prop = 123;
// setter: 123

inst.prop
// 'getter'
```

## 18.5 Class的Generator方法
如果某个方法之前加上星号（*），就表示该方法是一个Generator函数。
```js
class Foo {
  constructor(...args) {
    this.args = args;
  }
  * [Symbol.iterator]() {
    for (let arg of this.args) {
      yield arg;
    }
  }
}

for (let x of new Foo('hello', 'world')) {
  console.log(x);
}
// hello
// world
```

## 18.6 Class的静态方法
类相当于实例的原型，所有在类中定义的方法，都会被实例继承。如果在一个方法前，加上`static`关键字，就表示该方法**不会被实例继承**，而是直接通过类来调用，这就称为“静态方法”。
```js
class Foo {
  static classMethod() {
    return 'hello';
  }
}

Foo.classMethod() // 'hello'

var foo = new Foo();
foo.classMethod()
// TypeError: undefined is not a function
```
上面代码中，Foo类的classMethod方法前有static关键字，表明该方法是一个静态方法，可以直接在Foo类上调用（Foo.classMethod()），**而不是在Foo类的实例上调用**。
父类的静态方法，可以被**子类继承**（而不是实例）。
```js
class Foo {
  static classMethod() {
    return 'hello';
  }
}

class Bar extends Foo {
}

Bar.classMethod(); // 'hello'
```
上面代码中，父类Foo有一个静态方法，子类Bar可以调用这个方法。

静态方法也是可以从super对象上调用的。

## 18.7 Class的静态属性和实例属性
静态属性指的是Class**本身的属性**，即`Class.propname`，而不是定义在实例对象（this）上的属性。
```js
class Foo {
}

Foo.prop = 1;
Foo.prop // 1
```
上面的写法为Foo类定义了一个静态属性prop。
目前，只有这种写法可行，因为ES6明确规定，Class内部只有**静态方法**，没有**静态属性**。
ES7有一个静态属性的提案，目前Babel转码器支持。
这个提案对**实例属性和静态属性**，都规定了新的写法。
（1）类的实例属性

类的实例属性可以用等式，写入类的定义之中。
```js
class MyClass {
  myProp = 42;

  constructor() {
    console.log(this.myProp); // 42
  }
}
```
以前，我们定义实例属性，只能写在类的constructor方法里面。
有了新的写法以后，**可以不在constructor方法里面定义**。
```js
class ReactCounter extends React.Component {
  state = {
    count: 0
  };
}
```
为了可读性的目的，对于那些在constructor里面已经定义的实例属性，新写法允许直接列出。
```js
class ReactCounter extends React.Component {
  constructor(props) {
    super(props);
    this.state = {
      count: 0
    };
  }
  state;
}
```
（2）类的静态属性

类的静态属性只要在上面的实例属性写法前面，加上`static`关键字就可以了。
```js
class MyClass {
  static myStaticProp = 42;

  constructor() {
    console.log(MyClass.myProp); // 42
  }
}
```
同样的，这个新写法大大方便了静态属性的表达。
```js
// 老写法
class Foo {
}
Foo.prop = 1;

// 新写法
class Foo {
  static prop = 1;
}
```
## 18.8 new.target属性
new是从构造函数生成实例的命令。ES6为new命令引入了一个`new.target`属性，（在构造函数中）返回new命令作用于的**那个构造函数**。如果构造函数不是通过new命令调用的，new.target会返回`undefined`，因此这个属性可以用来确定构造函数是怎么调用的。
```js
function Person(name) {
  if (new.target !== undefined) {
    this.name = name;
  } else {
    throw new Error('必须使用new生成实例');
  }
}

// 另一种写法
function Person(name) {
  if (new.target === Person) {
    this.name = name;
  } else {
    throw new Error('必须使用new生成实例');
  }
}

var person = new Person('张三'); // 正确
var notAPerson = Person.call(person, '张三');  // 报错
```
上面代码**确保构造函数只能通过new命令调用**。
Class内部调用new.target，**返回当前Class**。
```js
class Rectangle {
  constructor(length, width) {
    console.log(new.target === Rectangle);
    this.length = length;
    this.width = width;
  }
}

var obj = new Rectangle(3, 4); // 输出 true
```
**子类继承父类时，new.target会返回子类**。
利用这个特点，可以写出不能独立使用、**必须继承后才能使用的类**。
```js
class Shape {
  constructor() {
    if (new.target === Shape) {
      throw new Error('本类不能实例化');
    }
  }
}

class Rectangle extends Shape {
  constructor(length, width) {
    super();
    // ...
  }
}

var x = new Shape();  // 报错
var y = new Rectangle(3, 4);  // 正确
```
上面代码中，Shape类不能被实例化，只能用于继承。

注意，**在函数外部**，使用new.target会报错。

## 18.9 Mixin模式的实现
Mixin模式指的是，将多个类的接口“混入”（mix in）另一个类。它在ES6的实现如下。
```js
function mix(...mixins) {
  class Mix {}

  for (let mixin of mixins) {
    copyProperties(Mix, mixin);
    copyProperties(Mix.prototype, mixin.prototype);
  }

  return Mix;
}

function copyProperties(target, source) {
  for (let key of Reflect.ownKeys(source)) {
    if ( key !== "constructor"
      && key !== "prototype"
      && key !== "name"
    ) {
      let desc = Object.getOwnPropertyDescriptor(source, key);
      Object.defineProperty(target, key, desc);
    }
  }
}
```
上面代码的mix函数，可以将多个对象合成为一个类。使用的时候，只要继承这个类即可。
```js
class DistributedEdit extends mix(Loggable, Serializable) {
  // ...
}
```
# 19 Decorator修饰器
//下边内容自己搜的是python的描述
装饰器是一个很著名的设计模式，经常被用于有切面需求的场景，较为经典的有插入日志、性能测试、事务处理, Web权限校验, Cache等。
很有名的例子，就是咖啡，加糖的咖啡，加牛奶的咖啡。本质上，还是咖啡，只是在原有的东西上，做了“装饰”，使之附加一些功能或特性。
例如记录日志，需要对某些函数进行记录
笨的办法，每个函数加入代码，如果代码变了，就悲催了
装饰器的办法，定义一个专门日志记录的装饰器，对需要的函数进行装饰，搞定

装饰器是一个函数,一个用来包装函数的函数，装饰器在函数申明完成的时候被调用，调用之后返回一个修改之后的函数对象，将其重新赋值原来的标识符，并永久丧失对原始函数对象的访问(申明的函数被换成一个被装饰器装饰过后的函数)
当我们对某个方法应用了装饰方法后， 其实就改变了被装饰函数名称所引用的函数代码块入口点，使其重新指向了由装饰方法所返回的函数入口点。
由此我们可以用decorator改变某个原有函数的功能，添加各种操作，或者完全改变原有实现
## 19.1 类的修饰
修饰器（Decorator）是一个函数，用来修改**类的行为**。
修饰器对类的行为的改变，是**代码编译时**发生的，而不是在运行时。
```js
function testable(target) {
  target.isTestable = true;
}

@testable
class MyTestableClass {}

console.log(MyTestableClass.isTestable) // true
```
上面代码中，**@testable就是一个修饰器**。它修改了MyTestableClass这个类的行为，为它**加上了**静态属性isTestable。
**修饰器的行为就是下面这样**
```js
@decorator
class A {}

// 等同于

class A {}
A = decorator(A) || A;
```
也就是说，修饰器**本质**就是编译时**执行的函数**。
修饰器函数的**第一个参数**，就是所要修饰的目标类。
```js
function testable(target) {
  // ...
}
```
上面代码中，testable函数的参数`target`，就是**会被修饰**的类。
如果觉得**一个参数不够用**，可以在修饰器外面**再封装一层函数**。
```js
function testable(isTestable) {
  return function(target) {
    target.isTestable = isTestable;
  }
}

@testable(true)
class MyTestableClass {}
MyTestableClass.isTestable // true

@testable(false)
class MyClass {}
MyClass.isTestable // false
```
上面代码中，修饰器testable可以接受参数，这就**等于**可以修改修饰器的行为。
前面的例子是为类添加一个静态属性，如果想添加实例属性，可以通过目标类的prototype对象操作。
```js
function testable(target) {
  target.prototype.isTestable = true;    //在prototype上定义就可以在实例上调用
}

@testable
class MyTestableClass {}

let obj = new MyTestableClass();
obj.isTestable // true
```
上面代码中，修饰器函数testable是在目标类的prototype对象上添加属性，因此就可以在实例上调用。
## 19.2 方法的修饰
修饰器不仅可以**修饰类**，还可以修饰类的**属性**。
修饰器函数一共可以接受**三个参数**，第一个参数是所要修饰的**目标对象**，第二个参数是所要修饰的**属性名**，第三个参数是该属性的**描述对象**。
```js
function readonly(target, name, descriptor){
  // descriptor对象原来的值如下
  // {
  //   value: specifiedFunction,
  //   enumerable: false,
  //   configurable: true,
  //   writable: true
  // };
  descriptor.writable = false;
  return descriptor;
}

readonly(Person.prototype, 'name', descriptor);
// 类似于
Object.defineProperty(Person.prototype, 'name', descriptor);
```
上面代码说明，修饰器（readonly）会修改属性的描述对象（descriptor），**然后**被修改的描述对象再用来定义属性。
下面是另一个例子，修改属性描述对象的enumerable属性，**使得该属性不可遍历**。
```js
class Person {
  @nonenumerable
  get kidCount() { return this.children.length; }
}

function nonenumerable(target, name, descriptor) {
  descriptor.enumerable = false;
  return descriptor;
}
```
修饰器有**注释的作用**。
```js
@testable
class Person {
  @readonly
  @nonenumerable
  name() { return `${this.first} ${this.last}` }
}
```
从上面代码中，我们一眼就能看出，Person类是可测试的，而name方法是只读和不可枚举的。
如果同一个方法有多个修饰器，会**像剥洋葱一样，先从外到内进入，然后由内向外执行**。
```js
function dec(id){
    console.log('evaluated', id);
    return (target, property, descriptor) => console.log('executed', id);
}

class Example {
    @dec(1)
    @dec(2)
    method(){}
}
// evaluated 1
// evaluated 2
// executed 2
// executed 1
```
## 19.3 为什么修饰器不能用于函数？
修饰器只能用于类和类的方法，不能用于函数，**因为存在函数提升**。

## 19.4 core-decorators.js
core-decorators.js是一个第三方模块，提供了几个常见的修饰器，通过它可以更好地理解修饰器。
### 19.4.1 @autobind
autobind修饰器使得方法中的this对象，绑定原始对象。
```js
import { autobind } from 'core-decorators';

class Person {
  @autobind
  getPerson() {
    return this;
  }
}

let person = new Person();
let getPerson = person.getPerson;

getPerson() === person;
// true
```
### 19.4.2 @readonly
readonly修饰器使得属性或方法不可写。
```js
import { readonly } from 'core-decorators';

class Meal {
  @readonly
  entree = 'steak';
}

var dinner = new Meal();
dinner.entree = 'salmon';
// Cannot assign to read only property 'entree' of [object Object]
```
### 19.4.3 override
override修饰器检查子类的方法，是否正确覆盖了父类的同名方法，如果不正确会报错。
```js
import { override } from 'core-decorators';

class Parent {
  speak(first, second) {}
}

class Child extends Parent {
  @override
  speak() {}
  // SyntaxError: Child#speak() does not properly override Parent#speak(first, second)
}

// or

class Child extends Parent {
  @override
  speaks() {}
  // SyntaxError: No descriptor matching Child#speaks() was found on the prototype chain.
  //
  //   Did you mean "speak"?
}
```
### 19.4.4 @deprecate (别名@deprecated)
deprecate或deprecated修饰器在控制台显示一条警告，表示该方法将废除。

### 19.4.5 @suppressWarnings
suppressWarnings修饰器抑制decorated修饰器导致的console.warn()调用。但是，异步代码发出的调用除外。

## 19.5 使用修饰器实现自动发布事件
我们可以使用修饰器，使得对象的方法被调用时，自动发出一个事件。
```js
import postal from "postal/lib/postal.lodash";

export default function publish(topic, channel) {
  return function(target, name, descriptor) {
    const fn = descriptor.value;

    descriptor.value = function() {
      let value = fn.apply(this, arguments);
      postal.channel(channel || target.channel || "/").publish(topic, value);
    };
  };
}
```
上面代码定义了一个名为publish的修饰器，它通过改写descriptor.value，使得原方法被调用时，会自动发出一个事件。它使用的事件“发布/订阅”库是Postal.js。

用法如下：
```js
import publish from "path/to/decorators/publish";

class FooComponent {
  @publish("foo.some.message", "component")
  someMethod() {
    return {
      my: "data"
    };
  }
  @publish("foo.some.other")
  anotherMethod() {
    // ...
  }
}
```
以后，只要调用someMethod或者anotherMethod，就会自动发出一个事件。
```js
let foo = new FooComponent();

foo.someMethod() // 在"component"频道发布"foo.some.message"事件，附带的数据是{ my: "data" }
foo.anotherMethod() // 在"/"频道发布"foo.some.other"事件，不附带数据
```

## 19.6 Mixin
在修饰器的基础上，可以实现Mixin模式。所谓Mixin模式，就是对象继承的一种替代方案，中文译为“混入”（mix in），意为在一个对象之中混入另外一个对象的方法。
请看下面的例子。
```js
const Foo = {
  foo() { console.log('foo') }
};

class MyClass {}

Object.assign(MyClass.prototype, Foo);

let obj = new MyClass();
obj.foo() // 'foo'
```
上面代码之中，对象Foo有一个foo方法，通过Object.assign方法，可以将foo方法“混入”MyClass类，导致MyClass的实例obj对象都具有foo方法。这就是“混入”模式的一个简单实现。

## 19.7 Trait
Trait也是一种修饰器，效果与Mixin类似，但是提供更多功能，比如防止同名方法的冲突、排除混入某些方法、为混入的方法起别名等等。

## 19.8 Babel转码器的支持
目前，Babel转码器已经支持Decorator。
配置方法省略

# 20 Module
ES6的Class只是面向对象编程的语法糖，升级了ES5的构造函数的原型链继承的写法，并没有解决模块化问题。Module功能就是为了解决这个问题而提出的。

历史上，JavaScript一直没有模块（module）体系，无法将一个大程序拆分成互相依赖的小文件，再用简单的方法拼装起来。其他语言都有这项功能，比如Ruby的require、Python的import，甚至就连CSS都有@import，但是JavaScript任何这方面的支持都没有，这对开发大型的、复杂的项目形成了巨大障碍。

在ES6之前，社区制定了一些模块加载方案，最主要的有CommonJS和AMD两种。**前者用于服务器，后者用于浏览器**。ES6在语言规格的层面上，实现了模块功能，而且实现得相当简单，完全可以取代现有的CommonJS和AMD规范，成为浏览器和服务器通用的模块解决方案。

ES6模块的设计思想，是尽量的静态化，使得编译时就能确定模块的依赖关系，以及输入和输出的变量。CommonJS和AMD模块，都只能在运行时确定这些东西。比如，CommonJS**模块就是对象**，输入时必须查找对象属性。
```js
// CommonJS模块
let { stat, exists, readFile } = require('fs');

// 等同于
let _fs = require('fs');
let stat = _fs.stat, exists = _fs.exists, readfile = _fs.readfile;
```
上面代码的实质是整体加载fs模块（即加载fs的所有方法），生成一个对象（_fs），然后再从这个对象上面读取3个方法。这种加载称为“运行时加载”，因为**只有运行时才能得到这个对象**，导致完全没办法在编译时做“静态优化”。

ES6模块**不是对象**，而是通过`export`命令显式指定输出的代码，输入时也采用静态命令的形式。
```js
// ES6模块
import { stat, exists, readFile } from 'fs';
```
上面代码的实质是从fs模块加载3个方法，**其他方法不加载**。这种加载称为“编译时加载”，即ES6可以在编译时就完成模块加载，效率要比CommonJS模块的加载方式高。当然，这也导致了没法引用ES6模块本身，因为它不是对象。

由于ES6模块是编译时加载，使得静态分析成为可能。有了它，就能进一步拓宽JavaScript的语法，比如引入宏（macro）和类型检验（type system）这些只能靠静态分析实现的功能。

除了静态加载带来的各种好处，ES6模块还有以下好处。

不再需要UMD模块格式了，将来服务器和浏览器都会支持ES6模块格式。目前，通过各种工具库，其实已经做到了这一点。
将来浏览器的新API就能用模块格式提供，不再必要做成全局变量或者navigator对象的属性。
不再需要对象作为命名空间（比如Math对象），未来这些功能可以通过模块提供。
## 20.1 严格模式
ES6的模块自动采用严格模式，不管你有没有在模块头部加上`"use strict"`;。

严格模式主要有以下限制。

变量必须声明后再使用
函数的参数不能有同名属性，否则报错
不能使用with语句
不能对只读属性赋值，否则报错
不能使用前缀0表示八进制数，否则报错
不能删除不可删除的属性，否则报错
不能删除变量delete prop，会报错，只能删除属性delete global\[prop]
eval不会在它的外层作用域引入变量
eval和arguments不能被重新赋值
arguments不会自动反映函数参数的变化
不能使用arguments.callee
不能使用arguments.caller
禁止this指向全局对象
不能使用fn.caller和fn.arguments获取函数调用的堆栈
增加了保留字（比如protected、static和interface）

# 20.2 export命令
模块功能主要由两个命令构成：`export`和`import`。
`export`命令用于**规定模块**的对外接口，`import`命令用于输入**其他模块**提供的功能。
一个模块就是一个独立的文件。该文件内部的所有变量，外部无法获取。如果你希望外部能够读取模块内部的某个变量，就必须使用export关键字输出该变量。
```js
// profile.js
export var firstName = 'Michael';
export var lastName = 'Jackson';
export var year = 1958;
```
export的**写法**，除了像上面这样，还有另外一种。**优先考虑使用这种写法。**
```js
// profile.js
var firstName = 'Michael';
var lastName = 'Jackson';
var year = 1958;

export {firstName, lastName, year};        //注意大括号
```
通常情况下，export输出的变量就是本来的名字，但是可以使用`as`关键字**重命名**。
```js
function v1() { ... }
function v2() { ... }

export {
  v1 as streamV1,
  v2 as streamV2,
  v2 as streamLatestVersion
};
```
注意的是，export命令规定的是对外的接口，必须与模块内部的**变量**建立一一对应关系。
```js
// 报错
export 1;

// 报错
var m = 1;
export m;
```
上面两种写法都会报错，因为没有提供对外的接口。第一种写法直接输出1，第二种写法通过变量m，还是直接输出1。1只是一个值，不是接口。**正确的写法**是下面这样。
```js
// 写法一
export var m = 1;

// 写法二
var m = 1;
export {m};         //注意大括号

// 写法三
var n = 1;
export {n as m};
```
同样的，`function`和`class`的输出，也必须遵守这样的写法。
```js
// 报错
function f() {}
export f;

// 正确
export function f() {};

// 正确
function f() {}
export {f};                //推荐
```
最后，export命令可以出现在模块的**任何位置**，只要处于模块**顶层**就可以。

## 20.3 import命令
使用export命令定义了模块的对外接口以后，其他JS文件就可以通过`import`命令**加载**这个模块（文件）。
```js
// main.js

import {firstName, lastName, year} from './profile';

function setName(element) {
  element.textContent = firstName + ' ' + lastName;
}
```
如果想为输入的变量重新取一个名字，import命令要使用as关键字，将输入的**变量重命名**。
注意，import命令具有**提升**效果，会提升到整个模块的**头部**，**首先执行**。
```js
foo();         //不会报错，因为import会提升foo
 
import { foo } from 'my_module'; 
```
如果在一个模块之中，**先输入后输出**同一个模块，import语句可以与export语句写在一起。
```js
export { es6 as default } from './someModule';

// 等同于
import { es6 } from './someModule';
export default es6;
```
另外，ES7有一个提案，简化先输入后输出的写法，**拿掉输出时的大括号**。
```js
// 提案的写法
export v from 'mod';

// 现行的写法
export {v} from 'mod';
```
## 20.4 模块的整体加载
除了指定加载某个输出值，还可以使用整体加载，即用星号`*`指定一个对象，所有输出值都加载在这个对象上面。
下面是一个circle.js文件，它输出两个方法area和circumference。
```js
// circle.js

export function area(radius) {
  return Math.PI * radius * radius;
}

export function circumference(radius) {
  return 2 * Math.PI * radius;
}
```
加载这个模块
```js
// main.js
//逐一指定要加载的方法
import { area, circumference } from './circle';
//整体加载的写法
import * as circle from './circle';
```

## 20.5 export default命令
不知道模块有哪些属性和方法，可以用到`export default`命令，为模块指定默认输出。
```js
// export-default.js
export default function () {
  console.log('foo');
}
```
上面代码是一个模块文件export-default.js，它的默认输出是一个函数。

其他模块加载该模块时，import命令可以为该匿名函数**指定任意名字**
```js
// import-default.js
import customName from './export-default';
customName(); // 'foo'
```
需要注意的是，这时import命令后面，**不使用大括号**。
export default命令用在**非匿名函数**前，也是可以的。
```js
// export-default.js
export default function foo() {
  console.log('foo');
}

// 或者写成

function foo() {
  console.log('foo');
}

export default foo;   //非匿名函数
```
**常用输入输出格式**
有了export default命令，输入模块时就非常直观了，以输入jQuery模块为例。
```js
import $ from 'jquery';
```
如果想在一条import语句中，**同时输入默认方法和其他变量**，可以写成下面这样。
```js
import customName, { otherMethod } from './export-default';
```
如果要输出默认的**值**，只需将值跟在export default之后即可。
```js
export default 42;
```
export default也可以用来输出类。
```js
// MyClass.js
export default class { ... }

// main.js
import MyClass from 'MyClass'
let o = new MyClass();
```

## 20.6 模块的继承
模块之间也可以继承。

假设有一个circleplus模块，继承了circle模块。
```js
// circleplus.js

export * from 'circle';
export var e = 2.71828182846;
export default function(x) {
  return Math.exp(x);
}
```
上面代码中的`export *`，表示再输出circle模块的所有属性和方法。
**注意**，`export *`命令会**忽略**circle模块的`default`方法。
加载上面模块的写法如下。
```js
// main.js

import * as math from 'circleplus';
import exp from 'circleplus';
console.log(exp(math.e));
```

## 20.7 ES6模块加载的实质
ES6模块加载的机制，与CommonJS模块完全不同。
CommonJS模块输出的是一个值的**拷贝**，而ES6模块输出的是值的**引用**。
CommonJS模块输出的是被输出值的**拷贝**，也就是说，一旦输出一个值，模块内部的变化就**影响不到**这个值。
ES6模块的运行机制与CommonJS不一样，它遇到模块加载命令import时，**不会去执行模块**，而是只生成一个**动态的只读引用**。等到真的**需要用到时**，再到模块里面去取值，换句话说，ES6的输入有点像Unix系统的”符号连接“，原始值变了，import输入的值也会跟着变。
因此，**ES6模块是动态引用，并且不会缓存值**，模块里面的变量绑定其所在的模块。

## 20.8 循环加载
“循环加载”（circular dependency）指的是，a脚本的执行依赖b脚本，而b脚本的执行又依赖a脚本。
```js
// a.js
var b = require('b');

// b.js
var a = require('a');
```
通常，“循环加载”表示存在**强耦合**，如果处理不好，还可能导致递归加载，使得程序无法执行，因此应该避免出现。
但是实际上，这是很难避免的，尤其是依赖关系复杂的大项目
目前最常见的两种模块格式CommonJS和ES6，**处理“循环加载”的方法是不一样**的，返回的**结果也不一样**。

### 20.8.1 CommonJS模块的加载原理
CommonJS的一个模块，就是一个脚本文件。require命令**第一次加载该脚本**，就会**执行整个脚本**，然后在**内存生成**一个对象。
CommonJS模块无论加载多少次，都只会在第一次加载时运行一次，以后再加载，就**返回第一次运行的结果**，**除非手动清除系统缓存**。

### 20.8.2 CommonJS模块的循环加载
CommonJS模块的重要特性是加载时执行，即脚本代码在require的时候，就会全部执行。
一旦出现某个模块被"循环加载"，就只输出已经执行的部分，**还未执行的部分不会输出**。
让我们来看，Node官方文档里面的例子。脚本文件a.js代码如下。
```js
exports.done = false;
var b = require('./b.js');
console.log('在 a.js 之中，b.done = %j', b.done);
exports.done = true;
console.log('a.js 执行完毕');
```
上面代码之中，a.js脚本先输出一个done变量，然后加载另一个脚本文件b.js。注意，此时a.js代码就停在这里，等待b.js执行完毕，再往下执行。

再看b.js的代码。
```js
exports.done = false;
var a = require('./a.js');
console.log('在 b.js 之中，a.done = %j', a.done);
exports.done = true;
console.log('b.js 执行完毕');
```
上面代码之中，b.js执行到第二行，就会去加载a.js，这时，就发生了“循环加载”。系统会去a.js模块对应对象的exports属性取值，可是因为a.js还没有执行完，从exports属性只能取回已经执行的部分，而不是最后的值。

a.js已经执行的部分，只有一行。
```js
exports.done = false;
```
因此，对于b.js来说，它从a.js只输入一个变量done，值为false。
因此，对于b.js来说，它从a.js只输入一个变量done，值为false。

然后，b.js**接着往下执行**(a只运行一行，所以就执行这一行之后，继续向下运行)，等到全部执行完毕，再把执行权交还给a.js。于是，a.js接着往下执行，直到执行完毕。我们写一个脚本main.js，验证这个过程。
```js
var a = require('./a.js');
var b = require('./b.js');
console.log('在 main.js 之中, a.done=%j, b.done=%j', a.done, b.done);
```
执行main.js，运行结果如下。
```js
$ node main.js

在 b.js 之中，a.done = false
b.js 执行完毕
在 a.js 之中，b.done = true
a.js 执行完毕
在 main.js 之中, a.done=true, b.done=true
```
上面的代码证明了两件事。一是，在b.js之中，a.js没有执行完毕，只执行了第一行。二是，main.js执行到第二行时，不会再次执行b.js，而是输出缓存的b.js的执行结果，即它的第四行。
```js
exports.done = true;
```
总之，CommonJS输入的是被输出值的拷贝，不是引用。

另外，由于CommonJS模块遇到循环加载时，返回的是当前已经执行的部分的值，而不是代码全部执行后的值，两者可能会有差异。所以，输入变量的时候，必须非常小心。
```js
var a = require('a'); // 安全的写法
var foo = require('a').foo; // 危险的写法

exports.good = function (arg) {
  return a.foo('good', arg); // 使用的是 a.foo 的最新值
};

exports.bad = function (arg) {
  return foo('bad', arg); // 使用的是一个部分加载时的值
};
```
上面代码中，如果发生循环加载，require('a').foo的值很可能后面会被改写，改用require('a')会更保险一点。

### 20.8.3 ES6模块的循环加载
ES6处理“循环加载”与CommonJS有本质的不同。ES6模块是动态引用，遇到模块加载命令import时，不会去执行模块，只是生成一个指向被加载模块的引用，需要开发者自己保证，真正取值的时候能够取到值。
```js
// a.js
import {bar} from './b.js';
export function foo() {
  bar();
  console.log('执行完毕');
}
foo();

// b.js
import {foo} from './a.js';
export function bar() {
  if (Math.random() > 0.5) {
    foo();
  }
}
```
按照CommonJS规范，上面的代码是没法执行的。a先加载b，然后b又加载a，这时a还没有任何执行结果，所以输出结果为null，即对于b.js来说，变量foo的值等于null，后面的foo()就会报错。

但是，ES6可以执行上面的代码。
```js
$ babel-node a.js

执行完毕
```
a.js之所以能够执行，原因就在于ES6加载的变量，都是动态引用其所在的模块。只要引用是存在的，代码就能执行。

# 21 编程风格
