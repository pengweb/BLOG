---
title: Nodejs--学习笔记
date: 2016-04-07 15:41:44
tags: [nodejs,笔记,note]

---
<strong>创建Nodejs应用</strong>
步骤一、引入 required 模块
```js var http = require("http");```
步骤一、创建服务器
使用 http.createServer() 方法创建服务器，并使用 listen 方法绑定 8888 端口。 函数通过 request, response 参数来接收和响应数据。
创建一个叫 server.js 的文件
```js var http = require('http');

http.createServer(function (request, response) {

// 发送 HTTP 头部
// HTTP 状态值: 200 : OK
// 内容类型: text/plain
response.writeHead(200, {'Content-Type': 'text/plain'});

// 发送响应数据 "Hello World"
response.end('Hello World\n');
}).listen(8888);

// 终端打印如下信息
console.log('Server running at http://127.0.0.1:8888/');```
二、运行服务器
```js node server.js```
<strong>NPM使用介绍：</strong>
升级npm
```js npm install npm -g```
全局安装和局部安装：
```js npm install express # 本地安装
npm install express -g # 全局安装```
本地安装
1. 将安装包放在 ./node_modules 下（运行 npm 命令时所在的目录），如果没有 node_modules 目录，会在当前执行 npm 命令的目录下生成 node_modules 目录。
2. 可以通过 require() 来引入本地安装的包。
全局安装
1. 将安装包放在 /usr/local 下。
2. 可以直接在命令行里使用。
3. 不能通过 require() 来引入本地安装的包。

Package.json 属性说明
name - 包名。
version - 包的版本号。
description - 包的描述。
homepage - 包的官网 url 。
author - 包的作者姓名。
contributors - 包的其他贡献者姓名。
dependencies - 依赖包列表。如果依赖包没有安装，npm 会自动将依赖包安装在 node_module 目录下。
repository - 包代码存放的地方的类型，可以是 git 或 svn，git 可在 Github 上。
main - main 字段是一个模块ID，它是一个指向你程序的主要项目。就是说，如果你包的名字叫 express，然后用户安装它，然后require("express")。
keywords - 关键字

卸载模块
我们可以使用以下命令来卸载 Node.js 模块。
$ npm uninstall express
卸载后，你可以到 /node_modules/ 目录下查看包是否还存在，或者使用以下命令查看：
$ npm ls

更新模块
我们可以使用以下命令更新模块：
$ npm update express
搜索模块
使用以下来搜索模块：
$ npm search express

版本号
使用NPM下载和发布代码时都会接触到版本号。NPM使用语义版本号来管理代码，这里简单介绍一下。
语义版本号分为X.Y.Z三位，分别代表主版本号、次版本号和补丁版本号。当代码变更时，版本号按以下原则更新。
如果只是修复bug，需要更新Z位。
如果是新增了功能，但是向下兼容，需要更新Y位。
如果有大变动，向下不兼容，需要更新X位。

<strong>Node.js REPL(交互式解释器)</strong>

REPL 命令
ctrl + c - 退出当前终端。
ctrl + c 按下两次 - 退出 Node REPL。
ctrl + d - 退出 Node REPL.
向上/向下 键 - 查看输入的历史命令
tab 键 - 列出当前命令
.help - 列出使用命令
.break - 退出多行表达式
.clear - 退出多行表达式
.save filename - 保存当前的 Node REPL 会话到指定文件
.load filename - 载入当前 Node REPL 会话的文件内容。

<strong>Node.js 回调函数</strong>

Node.js 异步编程的直接体现就是回调。
异步编程依托于回调来实现，但不能说使用了回调后程序就异步化了。
回调函数在完成任务后就会被调用，Node 使用了大量的回调函数，Node 所有 API 都支持回调函数。
例如，我们可以一边读取文件，一边执行其他命令，在文件读取完成后，我们将文件内容作为回调函数的参数返回。这样在执行代码时就没有阻塞或等待文件 I/O 操作。这就大大提高了 Node.js 的性能，可以处理大量的并发请求
```js Node.js 事件循环```
Node.js 是单进程单线程应用程序，但是通过事件和回调支持并发，所以性能非常高。
Node.js 的每一个 API 都是异步的，并作为一个独立线程运行，使用异步函数调用，并处理并发。
Node.js 基本上所有的事件机制都是用设计模式中观察者模式实现。
Node.js 单线程类似进入一个while(true)的事件循环，直到没有事件观察者退出，每个异步事件都生成一个事件观察者，如果有事件发生就调用该回调函数.
```js // 引入 events 模块
var events = require('events');
// 创建 eventEmitter 对象
var eventEmitter = new events.EventEmitter();

// 创建事件处理程序
var connectHandler = function connected() {
console.log('连接成功。');

// 触发 data_received 事件
eventEmitter.emit('data_received');
}

// 绑定 connection 事件处理程序
eventEmitter.on('connection', connectHandler);

// 使用匿名函数绑定 data_received 事件
eventEmitter.on('data_received', function(){
console.log('数据接收成功。');
});

// 触发 connection 事件
eventEmitter.emit('connection');

console.log("程序执行完毕。");```
连接成功。
数据接收成功。
程序执行完毕。

Node 应用程序是如何工作的？
```js var fs = require("fs"); //fs是用来读取的

fs.readFile('input.txt', function (err, data) {
if (err){
console.log(err.stack);
return;
}
console.log(data.toString());
});
console.log("程序执行完毕");```
```js Node.js EventEmitter```
Node.js 所有的异步 I/O 操作在完成时都会发送一个事件到事件队列。
Node.js里面的许多对象都会分发事件：一个net.Server对象会在每次有新连接时分发一个事件， 一个fs.readStream对象会在文件被打开的时候发出一个事件。 所有这些产生事件的对象都是 events.EventEmitter 的实例。

EventEmitter 类
events 模块只提供了一个对象： events.EventEmitter。EventEmitter 的核心就是事件触发与事件监听器功能的封装。
你可以通过require("events");来访问该模块。
```js // 引入 events 模块
var events = require('events');
// 创建 eventEmitter 对象
var eventEmitter = new events.EventEmitter();```
EventEmitter 对象如果在实例化时发生错误，会触发 'error' 事件。当添加新的监听器时，'newListener' 事件会触发，当监听器被移除时，'removeListener' 事件被触发。
下面我们用一个简单的例子说明 EventEmitter 的用法：
```js //event.js 文件
var EventEmitter = require('events').EventEmitter;
var event = new EventEmitter();
event.on('some_event', function() {
console.log('some_event 事件触发');
});
setTimeout(function() {
event.emit('some_event');
}, 1000);```
$ node event.js
some_event 事件触发

EventEmitter 的每个事件由一个事件名和若干个参数组成，事件名是一个字符串，通常表达一定的语义。对于每个事件，EventEmitter 支持 若干个事件监听器。
当事件触发时，注册到这个事件的事件监听器被依次调用，事件参数作为回调函数参数传递。

让我们以下面的例子解释这个过程：
```js //event.js 文件
var events = require('events');
var emitter = new events.EventEmitter();
emitter.on('someEvent', function(arg1, arg2) {
console.log('listener1', arg1, arg2);
});
emitter.on('someEvent', function(arg1, arg2) {
console.log('listener2', arg1, arg2);
});
emitter.emit('someEvent', 'arg1 参数', 'arg2 参数');```
执行以上代码，运行的结果如下：/p&gt;
```js $ node event.js
listener1 arg1 参数 arg2 参数
listener2 arg1 参数 arg2 参数```
以上例子中，emitter 为事件 someEvent 注册了两个事件监听器，然后触发了 someEvent 事件。
运行结果中可以看到两个事件监听器回调函数被先后调用。 这就是EventEmitter最简单的用法。
EventEmitter 提供了多个属性，如 on 和 emit。on 函数用于绑定事件函数，emit 属性用于触发一个事件。接下来我们来具体看下 EventEmitter 的属性介绍。

实例
```js var events = require('events');
var eventEmitter = new events.EventEmitter();

// 监听器 #1
var listner1 = function listner1() {
console.log('监听器 listner1 执行。');
}

// 监听器 #2
var listner2 = function listner2() {
console.log('监听器 listner2 执行。');
}

// 绑定 connection 事件，处理函数为 listner1
eventEmitter.addListener('connection', listner1);

// 绑定 connection 事件，处理函数为 listner2
eventEmitter.on('connection', listner2);

var eventListeners = require('events').EventEmitter.listenerCount(eventEmitter,'connection');
console.log(eventListeners + " 监听器监听连接事件。");

// 处理 connection 事件
eventEmitter.emit('connection');

// 移除监绑定的 listner1 函数
eventEmitter.removeListener('connection', listner1);
console.log("listner1 不再受监听。");

// 触发连接事件
eventEmitter.emit('connection');

eventListeners = require('events').EventEmitter.listenerCount(eventEmitter,'connection');
console.log(eventListeners + " 监听器监听连接事件。");

console.log("程序执行完毕。");```
error 事件
```js var events = require('events');
var emitter = new events.EventEmitter();
emitter.emit('error');```
继承 EventEmitter
大多数时候我们不会直接使用 EventEmitter，而是在对象中继承它。包括 fs、net、 http 在内的，只要是支持事件响应的核心模块都是 EventEmitter 的子类。
为什么要这样做呢？原因有两点：
首先，具有某个实体功能的对象实现事件符合语义， 事件的监听和发射应该是一个对象的方法。
其次 JavaScript 的对象机制是基于原型的，支持 部分多重继承，继承 EventEmitter 不会打乱对象原有的继承关系。

<strong>Node.js Buffer(缓冲区)
</strong>

JavaScript 语言自身只有字符串数据类型，没有二进制数据类型。
但在处理像TCP流或文件流时，必须使用到二进制数据。因此在 Node.js中，定义了一个 Buffer 类，该类用来创建一个专门存放二进制数据的缓存区。
在 Node.js 中，Buffer 类是随 Node 内核一起发布的核心库。Buffer 库为 Node.js 带来了一种存储原始数据的方法，可以让 Node.js 处理二进制数据，每当需要在 Node.js 中处理I/O操作中移动的数据时，就有可能使用 Buffer 库。原始数据存储在 Buffer 类的实例中。一个 Buffer 类似于一个整数数组，但它对应于 V8 堆内存之外的一块原始内存。

创建 Buffer 类
Node Buffer 类可以通过多种方式来创建。
方法 1
创建长度为 10 字节的 Buffer 实例：
```js var buf = new Buffer(10);```
方法 2
通过给定的数组创建 Buffer 实例：
```js var buf = new Buffer([10, 20, 30, 40, 50]);```
方法 3
通过一个字符串来创建 Buffer 实例：
```js var buf = new Buffer("www.runoob.com", "utf-8")```
写入缓冲区

写入 Node 缓冲区的语法如下所示：
```js buf.write(string[, offset][, length][, encoding])```
参数
参数描述如下：
string - 写入缓冲区的字符串。
offset - 缓冲区开始写入的索引值，默认为 0 。
length - 写入的字节数，默认为 buffer.length
encoding - 使用的编码。默认为 'utf8' 。
返回值
返回实际写入的大小。如果 buffer 空间不足， 则只会写入部分字符串。
实例
```js buf = new Buffer(256); //最长为256字节
len = buf.write("www.runoob.com"); ////存入的是二进制
console.log("写入字节数 : "+ len);```
执行以上代码，输出结果为：
```js $node main.js```
写入字节数 : 14

从缓冲区读取数据
读取 Node 缓冲区数据的语法如下所示：
```js buf.toString([encoding][, start][, end]) //先将二进制转化成字符串，再将字符串转化成要输出的格式，例如ascii```
参数
参数描述如下：
encoding - 使用的编码。默认为 'utf8' 。
start - 指定开始读取的索引位置，默认为 0。
end - 结束位置，默认为缓冲区的末尾。

将 Buffer 转换为 JSON 对象
将 Node Buffer 转换为 JSON 对象的函数语法格式如下：
```js buf.toJSON() //输出的就是二进制，不进行转换```
缓冲区合并
语法
Node 缓冲区合并的语法如下所示：
```js Buffer.concat(list[, totalLength])```
参数
参数描述如下：
list - 用于合并的 Buffer 对象数组列表。
totalLength - 指定合并后Buffer对象的总长度。
返回值
返回一个多个成员合并的新 Buffer 对象。
实例
```js var buffer1 = new Buffer('Pengweb ');
var buffer2 = new Buffer('www.pengweb.com');
var buffer3 = Buffer.concat([buffer1,buffer2]); //主要是这里合并
console.log("buffer3 内容: " + buffer3.toString());```
执行以上代码，输出结果为：
buffer3 内容: Pengweb www.pengweb.com

下边是自己写的：
```js var buf1=new Buffer(10); //要从新new一个才行
len1 =buf1.write("我自己的网站");
con=Buffer.concat([buf1,buf]); //合并的时候一定要是buf1，不能是len1
console.log(con.toString()); //一定要读取出来才行```
缓冲区比较
语法
Node Buffer 比较的函数语法如下所示：
```js buf.compare(otherBuffer);```
参数
参数描述如下：
otherBuffer - 与 buf 对象比较的另外一个 Buffer 对象。
返回值
返回一个数字，表示 buf 在 otherBuffer 之前，之后或相同。
实例
```js var buffer1 = new Buffer('ABC');
var buffer2 = new Buffer('ABCD');
var result = buffer1.compare(buffer2);

if(result &lt; 0) {
console.log(buffer1 + " 在 " + buffer2 + "之前");
}else if(result == 0){
console.log(buffer1 + " 与 " + buffer2 + "相同");
}else {
console.log(buffer1 + " 在 " + buffer2 + "之后");
}```
执行以上代码，输出结果为：
ABC在ABCD之前

拷贝缓冲区
语法
Node 缓冲区拷贝语法如下所示：
```js buf.copy(targetBuffer[, targetStart][, sourceStart][, sourceEnd])```
参数
参数描述如下：
targetBuffer - 要拷贝的 Buffer 对象。
targetStart - 数字, 可选, 默认: 0
sourceStart - 数字, 可选, 默认: 0
sourceEnd - 数字, 可选, 默认: buffer.length
返回值
没有返回值。
实例
```js var buffer1 = new Buffer('ABC');
// 拷贝一个缓冲区
var buffer2 = new Buffer(3);
buffer1.copy(buffer2); //将buffer1拷贝给buffer3
console.log("buffer2 content: " + buffer2.toString());```
执行以上代码，输出结果为：
buffer2 content: ABC

缓冲区裁剪
Node 缓冲区裁剪语法如下所示：
```js buf.slice([start][, end])```
参数
参数描述如下：
start - 数字, 可选, 默认: 0
end - 数字, 可选, 默认: buffer.length
返回值
返回一个新的缓冲区，它和旧缓冲区指向同一块内存，但是从索引 start 到 end 的位置剪切。
实例
```js var buffer1 = new Buffer('runoob');
// 剪切缓冲区
var buffer2 = buffer1.slice(0,2); //这里是剪掉保留2位
console.log("buffer2 content: " + buffer2.toString());```
执行以上代码，输出结果为：
buffer2 content: ru

缓冲区长度
语法
Node 缓冲区长度计算语法如下所示：
```js buf.length;```
返回值
返回 Buffer 对象所占据的内存长度。
实例
```js var buffer = new Buffer('www.runoob.com');
// 缓冲区长度
console.log("buffer length: " + buffer.length);```
执行以上代码，输出结果为：
buffer length: 14

Node.js Stream(流)

Stream 是一个抽象接口，Node 中有很多对象实现了这个接口。例如，对http 服务器发起请求的request 对象就是一个 Stream，还有stdout（标准输出）。
Node.js，Stream 有四种流类型：
Readable - 可读操作。
Writable - 可写操作。
Duplex - 可读可写操作.
Transform - 操作被写入数据，然后读出结果。
所有的 Stream 对象都是 EventEmitter 的实例。常用的事件有：
data - 当有数据可读时触发。
end - 没有更多的数据可读时触发。
error - 在接收和写入过程中发生错误时触发。
finish - 所有数据已被写入到底层系统时触发。

从流中读取数据
```js var fs = require("fs");
var data = '';

// 创建可读流
var readerStream = fs.createReadStream('input.txt');

// 设置编码为 utf8。
readerStream.setEncoding('UTF8');

// 处理流事件 --&gt; data, end, and error
readerStream.on('data', function(chunk) {
data += chunk;
});

readerStream.on('end',function(){ //结束时触发
console.log(data);
});

readerStream.on('error', function(err){
console.log(err.stack); //错误时，触发原因
});

console.log("程序执行完毕");```
写入流
```js var fs = require("fs");
var data = '我的地址：www.pengweb.com';

// 创建一个可以写入的流，写入到文件 output.txt 中
var writerStream = fs.createWriteStream('output.txt');

// 使用 utf8 编码写入数据
writerStream.write(data,'UTF8');

// 标记文件末尾
writerStream.end();

// 处理流事件 --&gt; data, end, and error
writerStream.on('finish', function() {
console.log("写入完成。");
});

writerStream.on('error', function(err){
console.log(err.stack);
});

console.log("程序执行完毕");```
以上程序会将 data 变量的数据写入到 output.txt 文件中。代码执行结果如下：
$ node main.js
程序执行完毕
写入完成。
查看 output.txt 文件的内容：
$ cat output.txt
我的地址：www.pengweb.com

管道流
管道提供了一个输出流到输入流的机制。通常我们用于从一个流中获取数据并将数据传递到另外一个流中。
我们把文件比作装水的桶，而水就是文件里的内容，我们用一根管子(pipe)连接两个桶使得水从一个桶流入另一个桶，这样就慢慢的实现了大文件的复制过程。
以下实例我们通过读取一个文件内容并将内容写入到另外一个文件中。
```js var fs = require("fs");

// 创建一个可读流
var readerStream = fs.createReadStream('input.txt');

// 创建一个可写流
var writerStream = fs.createWriteStream('output.txt');

// 管道读写操作
// 读取 input.txt 文件内容，并将内容写入到 output.txt 文件中
readerStream.pipe(writerStream); //会先清空目标文件

console.log("程序执行完毕");```
链式流
链式是通过连接输出流到另外一个流并创建多个对个流操作链的机制。链式流一般用于管道操作。
接下来我们就是用管道和链式来压缩和解压文件。
```js var fs = require("fs");
var zlib = require('zlib');

// 压缩 input.txt 文件为 input.txt.gz
fs.createReadStream('input.txt')
.pipe(zlib.createGzip())
.pipe(fs.createWriteStream('input.txt.gz'));

console.log("文件压缩完成。");```
接下来，让我们来解压该文件，创建 decompress.js 文件，代码如下：
```js var fs = require("fs");
var zlib = require('zlib');

// 解压 input.txt.gz 文件为 input.txt
fs.createReadStream('input.txt.gz')
.pipe(zlib.createGunzip())
.pipe(fs.createWriteStream('input.txt'));

console.log("文件解压完成。");```
<strong>Node.js模块系统</strong>
为了让Node.js的文件可以相互调用，Node.js提供了一个简单的模块系统。
模块是Node.js 应用程序的基本组成部分，文件和模块是一一对应的。换言之，一个 Node.js 文件就是一个模块，这个文件可能是JavaScript 代码、JSON 或者编译过的C/C++ 扩展。

创建模块
有时候我们只是想把一个对象封装到模块中，格式如下：
//hello.js
```js function Hello() {
var name;
this.setName = function(thyName) {
name = thyName;
};
this.sayHello = function() {
console.log('Hello ' + name);
};
};
module.exports = Hello;```
这样就可以直接获得这个对象了：
//main.js
```js var Hello = require('./hello');
hello = new Hello(); //这里一定要new出来 才能引用
hello.setName('BYVoid');
hello.sayHello();```
模块接口的唯一变化是使用 module.exports = Hello 代替了exports.world = function(){}。 在外部引用该模块时，其接口对象就是要输出的 Hello 对象本身，而不是原先的 exports。

服务端的模块放在哪里
也许你已经注意到，我们已经在代码中使用了模块了。像这样：
```js var http = require("http");

...

http.createServer(...);```
Node.js中自带了一个叫做"http"的模块，我们在我们的代码中请求它并把返回值赋给一个本地变量。
这把我们的本地变量变成了一个拥有所有 http 模块所提供的公共方法的对象。
Node.js 的 require方法中的文件查找策略如下：
由于Node.js中存在4类模块（原生模块和3种文件模块），尽管require方法极其简单，但是内部的加载却是十分复杂的，其加载优先级也各自不同。如下图所示：

<img class="alignnone size-full wp-image-6555" src="http://www.runoob.com/wp-content/uploads/2014/03/nodejs-require.jpg" alt="nodejs-require" width="479" height="601" />

从文件模块缓存中加载
尽管原生模块与文件模块的优先级不同，但是都不会优先于从文件模块的缓存中加载已经存在的模块。
从原生模块加载
原生模块的优先级仅次于文件模块缓存的优先级。require方法在解析文件名之后，优先检查模块是否在原生模块列表中。以http模块为例，尽管在目录下存在一个http/http.js/http.node/http.json文件，require("http")都不会从这些文件中加载，而是从原生模块中加载。
原生模块也有一个缓存区，同样也是优先从缓存区加载。如果缓存区没有被加载过，则调用原生模块的加载方式进行加载和执行。
从文件加载

require方法接受以下几种参数的传递：
http、fs、path等，原生模块。
./mod或../mod，相对路径的文件模块。
/pathtomodule/mod，绝对路径的文件模块。
mod，非原生模块的文件模块。

<strong>Node.js 函数</strong>

Node.js中函数的使用与Javascript类似，举例来说，你可以这样做：
```js function say(word) {
console.log(word);
}

function execute(someFunction, value) { //say的变量是通过value来传的，而不能通过someFunction(value)来传！！
someFunction(value);
}

execute(say, "Hello");```
以上代码中，我们把 say 函数作为execute函数的第一个变量进行了传递。这里返回的不是 say 的返回值，而是 say 本身！
这样一来， say 就变成了execute 中的本地变量 someFunction ，execute可以通过调用 someFunction() （带括号的形式）来使用 say 函数。
当然，因为 say 有一个变量， execute 在调用 someFunction 时可以传递这样一个变量。

匿名函数：
function execute(someFunction, value) {
someFunction(value);
}

execute(function(word){ console.log(word) }, "Hello"); //Hello 传递的变量还是在后边定义

函数传递是如何让HTTP服务器工作的
```js var http = require("http");

http.createServer(function(request, response) {
response.writeHead(200, {"Content-Type": "text/plain"});
response.write("Hello World");
response.end();
}).listen(8888);```
<strong>Node.js 路由</strong>
http://localhost:8888/start?foo=bar&amp;hello=world
start 是url.parse(string).pathname
foo=bar&amp;hello=world是url.parse(string).query
bar 是querystring(string)["foo"]
world 是querystring(string)["hello"]

//server.js
```js var http = require("http");
var url = require("url");

function start(route) {
function onRequest(request, response) {
var pathname = url.parse(request.url).pathname;
console.log("Request for " + pathname + " received.");

route(pathname);

response.writeHead(200, {"Content-Type": "text/plain"});
response.write("Hello World");
response.end();
}

http.createServer(onRequest).listen(8888);
console.log("Server has started.");
}
exports.start = start;```
//router.js
```js function route(pathname) {
console.log("About to route a request for " + pathname);
}
module.exports = route; //我这里用的是封装形式，所以下边start(router)而不是start(router.route)```
//index.js
```js var server = require("./server");
var router = require("./router");
server.start(router);```
<strong>Node.js 全局对象</strong>
JavaScript 中有一个特殊的对象，称为全局对象（Global Object），它及其所有属性都可以在程序的任何地方访问，即全局变量。
在浏览器 JavaScript 中，通常 window 是全局对象， 而 Node.js 中的全局对象是 global，所有全局变量（除了 global 本身以外）都是 global 对象的属性。
global 最根本的作用是作为全局变量的宿主。按照 ECMAScript 的定义，满足以下条 件的变量是全局变量：
在最外层定义的变量；
全局对象的属性；

全局对象与全局变量
隐式定义的变量（未定义直接赋值的变量）。
当你定义一个全局变量时，这个变量同时也会成为全局对象的属性，反之亦然。需要注 意的是，在 Node.js 中你不可能在最外层定义变量，因为所有用户代码都是属于当前模块的， 而模块本身不是最外层上下文。
注意： 永远使用 var 定义变量以避免引入全局变量，因为全局变量会污染 命名空间，提高代码的耦合风险。

__filename
__filename 表示当前正在执行的脚本的文件名。它将输出文件所在位置的绝对路径，且和命令行参数所指定的文件名不一定相同。 如果在模块中，返回的值是模块文件的路径。

__dirname
__dirname 表示当前执行脚本所在的目录。

setTimeout(cb, ms)
setTimeout(cb, ms) 全局函数在指定的毫秒(ms)数后执行指定函数(cb)。：setTimeout() 只执行一次指定函数。
返回一个代表定时器的句柄值。

clearTimeout(t)
clearTimeout( t ) 全局函数用于停止一个之前通过 setTimeout() 创建的定时器。 参数 t 是通过 setTimeout() 函数创建的计算器。
```js function printHello(){
console.log("hello world")
}
var t = setTimeout(printHello,2000);
clearTimeout(t); //彻底清除t，不管t放在clear上还是下，都不在显示hello world```
setInterval(cb, ms)
setInterval(cb, ms) 全局函数在指定的毫秒(ms)数后执行指定函数(cb)。
返回一个代表定时器的句柄值。可以使用 clearInterval(t) 函数来清除定时器。
setInterval() 方法会不停地调用函数，直到 clearInterval() 被调用或窗口被关闭。

console
console 用于提供控制台标准输出，它是由 Internet Explorer 的 JScript 引擎提供的调试工具，后来逐渐成为浏览器的事实标准。
Node.js 沿用了这个标准，提供与习惯行为一致的 console 对象，用于向标准输出流（stdout）或标准错误流（stderr）输出字符。
```js var counter = 10;
console.log("计数: %d", counter); //计数: 10```
process
process 是一个全局变量，即 global 对象的属性。
它用于描述当前Node.js 进程状态的对象，提供了一个与操作系统的简单接口。通常在你写本地命令行程序的时候，少不了要 和它打交道。下面将会介绍 process 对象的一些最常用的成员方法。
```js process.on('exit', function(code) { //当进程准备退出时触发，所以放在最后显示

// 以下代码永远不会执行
setTimeout(function() {
console.log("该代码不会执行");
}, 0);

console.log('退出码为:', code);
});
console.log("程序执行结束");```
执行代码如下所示:
```js 程序执行结束
退出码为: 0```
属性：
```js // 输出到终端
process.stdout.write("Hello World!" + "\n");

// 通过参数读取
//argv它的第一个成员总是node，第二个成员是脚本文件名，其余成员是脚本文件的参数。
process.argv.forEach(function(val, index, array) {
console.log(index + ': ' + val);
});

// 获取执行路局
console.log(process.execPath);

// 平台信息
console.log(process.platform);```
$ node main.js
```js Hello World!
0: node
1: /web/www/node/main.js
/usr/local/node/0.10.36/bin/node
darwin```
方法：
```js // 输出当前目录
console.log('当前目录: ' + process.cwd());

// 输出当前版本
console.log('当前版本: ' + process.version);

// 输出内存使用情况
console.log(process.memoryUsage());```
$ node main.js
```js 当前目录: /web/com/runoob/nodejs
当前版本: v0.10.36
{ rss: 12541952, heapTotal: 4083456, heapUsed: 2157056 }```
<strong>Node.js 常用工具</strong>
util 是一个Node.js 核心模块，提供常用函数的集合，用于弥补核心JavaScript 的功能 过于精简的不足。

util.inherits
util.inherits(constructor, superConstructor)是一个实现对象间原型继承 的函数。
JavaScript 的面向对象特性是基于原型的，与常见的基于类的不同。JavaScript 没有 提供对象继承的语言级别特性，而是通过原型复制来实现的。

util.inherits
util.inherits(constructor, superConstructor)是一个实现对象间原型继承 的函数。
JavaScript 的面向对象特性是基于原型的，与常见的基于类的不同。JavaScript 没有 提供对象继承的语言级别特性，而是通过原型复制来实现的。
```js util.inherits(Sub, Base);```
Sub 仅仅继承了Base 在原型中定义的函数，而构造函数内部创造的 base 属 性和 sayHello 函数都没有被 Sub 继承。
同时，在原型中定义的属性不会被console.log 作为对象的属性输出。

util.inspect
util.inspect(object,[showHidden],[depth],[colors])是一个将任意对象转换 为字符串的方法，通常用于调试和错误输出。它至少接受一个参数 object，即要转换的对象。
showHidden 是一个可选参数，如果值为 true，将会输出更多隐藏信息。
depth 表示最大递归的层数，如果对象很复杂，你可以指定层数以控制输出信息的多 少。如果不指定depth，默认会递归2层，指定为 null 表示将不限递归层数完整遍历对象。 如果color 值为 true，输出格式将会以ANSI 颜色编码，通常用于在终端显示更漂亮 的效果。
特别要指出的是，util.inspect 并不会简单地直接把对象转换为字符串，即使该对 象定义了toString 方法也不会调用。
```js var util = require('util');
function Person() {
this.name = 'byvoid';
this.toString = function() {
return this.name;
};
}
var obj = new Person();
console.log(util.inspect(obj));
console.log(util.inspect(obj, true));```
```js { name: 'byvoid', toString: [Function] }
{ toString:
{ [Function]
[prototype]: { [constructor]: [Circular] },
[caller]: null,
[length]: 0,
[name]: '',
[arguments]: null },
name: 'byvoid' }```
util.isArray(object)
如果给定的参数 "object" 是一个数组返回true，否则返回false。
```js var util = require('util');

util.isArray([])
// true
util.isArray(new Array)
// true
util.isArray({})
// false```
util.isRegExp(object)
如果给定的参数 "object" 是一个正则表达式返回true，否则返回false。
```js var util = require('util');

util.isRegExp(/some regexp/)
// true
util.isRegExp(new RegExp('another regexp'))
// true
util.isRegExp({})
// false```
util.isDate(object)
如果给定的参数 "object" 是一个日期返回true，否则返回false。
```js var util = require('util');

util.isDate(new Date())
// true
util.isDate(Date())
// false (without 'new' returns a String)
util.isDate({})
// false```
util.isError(object)
如果给定的参数 "object" 是一个错误对象返回true，否则返回false。
```js var util = require('util');

util.isError(new Error())
// true
util.isError(new TypeError())
// true
util.isError({ name: 'Error', message: 'an error occurred' })
// false```
<strong>Node.js 文件系统</strong>
Node.js 提供一组类似 UNIX（POSIX）标准的文件操作API。 Node 导入文件系统模块(fs)语法如下所示：
var fs = require("fs")
异步和同步
Node.js 文件系统（fs 模块）模块中的方法均有异步和同步版本，例如读取文件内容的函数有异步的 fs.readFile() 和同步的 fs.readFileSync()。
异步的方法函数最后一个参数为回调函数，回调函数的第一个参数包含了错误信息(error)。
建议大家是用异步方法，比起同步，异步方法性能更高，速度更快，而且没有阻塞。
```js //异步读取
fs.readFile('input.txt',function(err,data){
if(err){
return console.error(err);
}
console.log("异步读取："+data.toString());
})

//同步读取
var data=fs.readFileSync('input.txt');
console.log("同步都去："+data.toString());
console.log("程序执行完毕");```
打开文件
语法
以下为在异步模式下打开文件的语法格式：
```js fs.open(path, flags[, mode], callback)```
参数
参数使用说明如下：
path - 文件的路径。
flags - 文件打开的行为。具体值详见下文。
mode - 设置文件模式(权限)，文件创建默认权限为 0666(可读，可写)。
callback - 回调函数，带有两个参数如：callback(err, fd)。

获取文件信息
语法
以下为通过异步模式获取文件信息的语法格式：
```js fs.stat(path, callback)```
参数
参数使用说明如下：
path - 文件路径。
callback - 回调函数，带有两个参数如：(err, stats), stats 是 fs.Stats 对象。
fs.stat(path)执行后，会将stats类的实例返回给其回调函数。可以通过stats类中的提供方法判断文件的相关属性。例如判断是否为文件：
stats类中的方法有：
方法 描述
stats.isFile() 如果是文件返回 true，否则返回 false。
stats.isDirectory() 如果是目录返回 true，否则返回 false。
stats.isBlockDevice() 如果是块设备返回 true，否则返回 false。
stats.isCharacterDevice() 如果是字符设备返回 true，否则返回 false。
stats.isSymbolicLink() 如果是软链接返回 true，否则返回 false。
stats.isFIFO() 如果是FIFO，返回true，否则返回 false。FIFO是UNIX中的一种特殊类型的命令管道。
stats.isSocket() 如果是 Socket 返回 true，否则返回 false。

写入文件
语法
以下为异步模式下写入文件的语法格式：
```js fs.writeFile(filename, data[, options], callback)```
如果文件存在，该方法写入的内容会覆盖旧的文件内容。
参数
参数使用说明如下：
path - 文件路径。
data - 要写入文件的数据，可以是 String(字符串) 或 Buffer(流) 对象。
options - 该参数是一个对象，包含 {encoding, mode, flag}。默认编码为 utf8, 模式为 0666 ， flag 为 'w'
callback - 回调函数，回调函数只包含错误信息参数(err)，在写入失败时返回。

读取文件
语法
以下为异步模式下读取文件的语法格式：
```js fs.read(fd, buffer, offset, length, position, callback)```
该方法使用了文件描述符来读取文件。
参数
参数使用说明如下：
fd - 通过 fs.open() 方法返回的文件描述符。
buffer - 数据写入的缓冲区。
offset - 缓冲区写入的写入偏移量。
length - 要从文件中读取的字节数。
position - 文件读取的起始位置，如果 position 的值为 null，则会从当前文件指针的位置读取。
callback - 回调函数，有三个参数err, bytesRead, buffer，err 为错误信息， bytesRead 表示读取的字节数，buffer 为缓冲区对象。

关闭文件
语法
以下为异步模式下关闭文件的语法格式：
```js fs.close(fd, callback)```
该方法使用了文件描述符来读取文件。
参数
参数使用说明如下：
fd - 通过 fs.open() 方法返回的文件描述符。
callback - 回调函数，没有参数。

截取文件
语法
以下为异步模式下截取文件的语法格式：
```js fs.ftruncate(fd, len, callback)```
该方法使用了文件描述符来读取文件。
参数
参数使用说明如下：
fd - 通过 fs.open() 方法返回的文件描述符。
len - 文件内容截取的长度。
callback - 回调函数，没有参数。

先打开，后截取，再读取，最后关闭

删除文件
语法
以下为删除文件的语法格式：
```js fs.unlink(path, callback)```
参数
参数使用说明如下：
path - 文件路径。
callback - 回调函数，没有参数。

创建目录
语法
以下为创建目录的语法格式：
```js fs.mkdir(path[, mode], callback)```
参数
参数使用说明如下：
path - 文件路径。
mode - 设置目录权限，默认为 0777。
callback - 回调函数，没有参数。

读取目录
语法
以下为读取目录的语法格式：
```js fs.readdir(path, callback)```
参数
参数使用说明如下：
path - 文件路径。
callback - 回调函数，回调函数带有两个参数err, files，err 为错误信息，files 为 目录下的文件数组列表。

只能读取下边一层目录

删除目录
语法
以下为删除目录的语法格式：
```js fs.rmdir(path, callback)```
参数
参数使用说明如下：
path - 文件路径。
callback - 回调函数，没有参数。

注意：必须为空文件夹在能删除！！！

fs的实例代码：
```js var fs = require('fs');

//异步读取
fs.readFile('input.txt',function(err,data){
if(err){
return console.error(err);
}
console.log("异步读取："+data.toString());
})

//同步读取
var data=fs.readFileSync('input.txt');
console.log("同步读取："+data.toString());
console.log("程序执行完毕");

//异步打开文件
console.log('准备打开文件');
fs.open('input.txt','r+',function(err,fd){
if(err){
return console.error(err); //没有return也可以,也可以写成err.stack
}
console.log('打开文件成功');
})

//获取文件信息
fs.stat('input.txt',function(err,stats){
console.log(stats);
console.log(stats.isFile()); //true 判断是不是文件
console.log(stats.isDirectory()) //false 判断是否为目录
});

//写入文件
console.log("准备写入文件");
fs.writeFile('input.txt','这是写入的内容',function(err){ //写入数据会覆盖掉原数据
if(err){
return console.error(err);
}
console.log('数据写入成功');
console.log('读取写入数据');
fs.readFile('input.txt',function(err,data){
if(err){
console.log(err);
}
console.log('读取数据：'+data.toString());
})
});

//读取文件

var buf = new Buffer(1024);
console.log('读取文件开始');
fs.open('input.txt','r+',function(err,fd){
if(err){
return console.error(err);
}
console.log('打开文件成功');
console.log('准备读取文件');
fs.read(fd,buf,0,buf.length,0,function(err,bytes){
if(err){
console.log(err);
}
console.log(bytes+'字节被读取');
if(bytes&gt;0){
console.log(buf.slice(0,bytes).toString());
}
})
});

//关闭文件（接着上边那个写）

var buf = new Buffer(1024);
console.log('读取文件开始');
fs.open('input.txt','r+',function(err,fd){
if(err){
return console.error(err);
}
console.log('打开文件成功');
console.log('准备读取文件');
fs.read(fd,buf,0,buf.length,0,function(err,bytes){
if(err){
console.log(err);
}
console.log(bytes+'字节被读取');
if(bytes&gt;0){
console.log(buf.slice(0,bytes).toString());
}

fs.close(fd,function(err){
if(err){
console.log(err);
}
console.log("文件关闭成功")
})
})
});

//截取文件 先打开，后截取，再读取，最后关闭
fs.open('input.txt','r+',function(err,fd){
if(err){
return console.error(err);
}
console.log('打开文件成功');
console.log('准备读取文件');
fs.ftruncate(fd,10,function(err){
if(err){
console.log(err);
}
console.log("截取成功")
console.log('再读取相同文件');
fs.read(fd,buf,0,buf.length,0,function(err,bytes){
if(err){
console.log(err);
}
if(bytes&gt;0){
console.log(buf.slice(0,bytes).toString());
}

//关闭文件
fs.close(fd,function(err){
if(err){
console.log(err);
}
console.log("文件已经关闭")
})
})
})
});

//删除文件

//console.log("准备删除文件");
//fs.unlink('in.txt',function(err){
// if(err){
// console.log(err);
// }
// console.log('删除成功');
//})

//创建目录
//console.log("test");
//fs.mkdir('test1',function(err){ //不知道为什么在这个文件里只能创建一级目录，单放到一个文件内就可以创建二级的
// if (err) {
// return console.error(err);
// }
// console.log("目录创建成功。");
//});

//读取目录
//console.log("查看 /test 目录");
//fs.readdir("test1",function(err, files){ //只能读取下边一层目录，也可以读取这一层的文件名
// if (err) {
// return console.error(err);
// }
// files.forEach( function (file){
// console.log( file );
// });
//});

//删除目录
console.log("准备删除目录");
fs.rmdir("./test1/1",function(err){ //可以指定删除第二层目录的,但是必须为空文件夹
if (err) {
return console.error(err);
}
console.log("读取test 目录");
fs.readdir("./test1",function(err, files){
if (err) {
return console.error(err);
}
files.forEach( function (file){
console.log( file );
});
});
});```
Node.js GET/POST请求
在很多场景中，我们的服务器都需要跟用户的浏览器打交道，如表单提交。
表单提交到服务器一般都使用GET/POST请求。
本章节我们将为大家介绍 Node.js GET/POST请求。

获取GET请求内容
由于GET请求直接被嵌入在路径中，URL是完整的请求路径，包括了?后面的部分，因此你可以手动解析后面的内容作为GET请求的参数。
node.js中url模块中的parse函数提供了这个功能。
```js var http = require('http');
var url = require('url');
var util = require('util');

http.createServer(function(req, res){
res.writeHead(200, {'Content-Type': 'text/plain'});
res.end(util.inspect(url.parse(req.url, true)));
}).listen(3000);```
在浏览器中访问http://localhost:3000/user?name=w3c&amp;email=w3c@w3cschool.cc 然后查看返回结果:

<img class="alignnone size-full wp-image-8041" src="http://www.runoob.com/wp-content/uploads/2014/06/w3cnodejs.jpg" alt="w3cnodejs" width="462" height="265" />

获取POST请求内容
POST请求的内容全部的都在请求体中，http.ServerRequest并没有一个属性内容为请求体，原因是等待请求体传输可能是一件耗时的工作。
比如上传文件，而很多时候我们可能并不需要理会请求体的内容，恶意的POST请求会大大消耗服务器的资源，所有node.js默认是不会解析请求体的， 当你需要的时候，需要手动来做。
```js var http = require('http');
var querystring = require('querystring');
var util = require('util');

http.createServer(function(req, res){
var post = ''; //定义了一个post变量，用于暂存请求体的信息

req.on('data', function(chunk){ //通过req的data事件监听函数，每当接受到请求体的数据，就累加到post变量中
post += chunk;
});

req.on('end', function(){ //在end事件触发后，通过querystring.parse将post解析为真正的POST请求格式，然后向客户端返回。
post = querystring.parse(post);
res.end(util.inspect(post));
});
}).listen(3000);```
Node.js Web 模块
什么是 Web 服务器？
Web服务器一般指网站服务器，是指驻留于因特网上某种类型计算机的程序，Web服务器的基本功能就是提供Web信息浏览服务。它只需支持HTTP协议、HTML文档格式及URL，与客户端的网络浏览器配合。
大多数 web 服务器都支持服务端的脚本语言（php、python、ruby）等，并通过脚本语言从数据库获取数据，将结果返回给客户端浏览器。
目前最主流的三个Web服务器是Apache、Nginx、IIS。

Web 应用架构

<img title="Web 应用架构" src="http://www.runoob.com/wp-content/uploads/2015/09/web_architecture.jpg" alt="" />

Client - 客户端，一般指浏览器，浏览器可以通过 HTTP 协议向服务器请求数据。
Server - 服务端，一般指 Web 服务器，可以接收客户端请求，并向客户端发送响应数据。
Business - 业务层， 通过 Web 服务器处理应用程序，如与数据库交互，逻辑运算，调用外部程序等。
Data - 数据层，一般由数据库组成。

使用 Node 创建 Web 服务器
Node.js 提供了 http 模块，http 模块主要用于搭建 HTTP 服务端和客户端，使用 HTTP 服务器或客户端功能必须调用 http 模块，代码如下：


```js var http = require('http');```


以下是演示一个最基本的 HTTP 服务器架构(使用8081端口)，创建 server.js 文件，代码如下所示：


```js var http = require('http');
var fs = require('fs');
var url = require('url');


// 创建服务器
http.createServer( function (request, response) {  
   // 解析请求，包括文件名
   var pathname = url.parse(request.url).pathname;
   
   // 输出请求的文件名
   console.log("Request for " + pathname + " received.");
   
   // 从文件系统中读取请求的文件内容
   fs.readFile(pathname.substr(1), function (err, data) {
      if (err) {
         console.log(err);
         // HTTP 状态码: 404 : NOT FOUND
         // Content Type: text/plain
         response.writeHead(404, {'Content-Type': 'text/html'});
      }else{	         
         // HTTP 状态码: 200 : OK
         // Content Type: text/plain
         response.writeHead(200, {'Content-Type': 'text/html'});	
         
         // 响应文件内容
         response.write(data.toString());		
      }
      //  发送响应数据
      response.end();
   });   
}).listen(8081);

// 控制台会输出以下信息
console.log('Server running at http://127.0.0.1:8081/');```

使用 Node 创建 Web 客户端
Node 创建 Web 客户端需要引入 http 模块，创建 client.js 文件，代码如下所示：



```js var http = require('http');

// 用于请求的选项
var options = {
   host: 'localhost',
   port: '8081',
   path: '/index.htm'  
};

// 处理响应的回调函数
var callback = function(response){
   // 不断更新数据
   var body = '';
   response.on('data', function(data) {
      body += data;
   });
   
   response.on('end', function() {
      // 数据接收完成
      console.log(body);
   });
}
// 向服务端发送请求
var req = http.request(options, callback);
req.end();```


新开一个终端，执行 client.js 文件，输出结果如下：


```js $ node client.js
<html>
<head>
<title>Sample Page</title>
</head>
<body>
Hello World!
</body>
</html>```


执行 server.js 的控制台输出信息如下：


```js Server running at http://127.0.0.1:8081/
Request for /index.htm received.   # 客户端请求信息```

<strong>Node.js 工具模块</strong>
Node.js OS 模块
Node.js os 模块提供了一些基本的系统操作函数。我们可以通过以下方式引入该模块：
var os = require("os")



```js var os = require("os");

// CPU 的字节序
console.log('endianness : ' + os.endianness());

// 操作系统名
console.log('type : ' + os.type());

// 操作系统名
console.log('platform : ' + os.platform());

// 系统内存总量
console.log('total memory : ' + os.totalmem() + " bytes.");

// 操作系统空闲内存量
console.log('free memory : ' + os.freemem() + " bytes.");```



```js endianness : LE
type : Linux
platform : linux
total memory : 25103400960 bytes.
free memory : 20676710400 bytes.```

Node.js Path 模块
Node.js path 模块提供了一些用于处理文件路径的小工具，我们可以通过以下方式引入该模块：


```js var path = require("path")```


```js var path = require("path");

// 格式化路径
console.log('normalization : ' + path.normalize('/test/test1//2slashes/1slash/tab/..'));

// 连接路径
console.log('joint path : ' + path.join('/test', 'test1', '2slashes/1slash', 'tab', '..'));

// 转换为绝对路径
console.log('resolve : ' + path.resolve('main.js'));

// 路径中文件的后缀名
console.log('ext name : ' + path.extname('main.js'));```

$ node main.js 

```js normalization : /test/test1/2slashes/1slash
joint path : /test/test1/2slashes/1slash
resolve : /web/com/1427176256_27423/main.js
ext name : .js```

Node.js Net 模块
Net和Http模块的区别，可以查看下边网址了解
odeJS 的数据通信，最基础的两个模块是 Net 和 Http，前者是基于 Tcp 的封装，后者本质还是 Tcp 层，只不过做了比较多的数据封装，我们视为表现层。
http://www.jb51.net/article/59801.htm

Node.js DNS 模块
Node.js DNS 模块用于解析域名。引入 DNS 模块语法格式如下：


```js var dns = require("dns")```



```js var dns = require('dns');

dns.lookup('www.github.com', function onLookup(err, address, family) {
   console.log('ip 地址:', address);
   dns.reverse(address, function (err, hostnames) {
   if (err) {
      console.log(err.stack);
   }

   console.log('反向解析 ' + address + ': ' + JSON.stringify(hostnames));
});  
});```


执行以上代码，结果如下所示:


```js address: 192.30.252.130
reverse for 192.30.252.130: ["github.com"]```

Node.js Domain 模块
Node.js Domain(域) 简化异步代码的异常处理，可以捕捉处理try catch无法捕捉的异常。引入 Domain 模块 语法格式如下：


```js var domain = require("domain")```

domain模块，把处理多个不同的IO的操作作为一个组。注册事件和回调到domain，当发生一个错误事件或抛出一个错误时，domain对象会被通知，不会丢失上下文环境，也不导致程序错误立即推出，与process.on('uncaughtException')不同。
Domain 模块可分为隐式绑定和显式绑定：
隐式绑定: 把在domain上下文中定义的变量，自动绑定到domain对象
显式绑定: 把不是在domain上下文中定义的变量，以代码的方式绑定到domain对象



```js var EventEmitter = require("events").EventEmitter;
var domain = require("domain");

var emitter1 = new EventEmitter();

// 创建域
var domain1 = domain.create();

domain1.on('error', function(err){
   console.log("domain1 处理这个错误 ("+err.message+")");
});

// 显式绑定
domain1.add(emitter1);

emitter1.on('error',function(err){
   console.log("监听器处理此错误 ("+err.message+")");
});

emitter1.emit('error',new Error('通过监听器来处理'));

emitter1.removeAllListeners('error');

emitter1.emit('error',new Error('通过 domain1 处理'));

var domain2 = domain.create();

domain2.on('error', function(err){
   console.log("domain2 处理这个错误 ("+err.message+")");
});

// 隐式绑定
domain2.run(function(){
   var emitter2 = new EventEmitter();
   emitter2.emit('error',new Error('通过 domain2 处理'));   
});


domain1.remove(emitter1);
emitter1.emit('error', new Error('转换为异常，系统将崩溃!'));```


执行以上代码，结果如下所示:


```js 监听器处理此错误 (通过监听器来处理)
domain1 处理这个错误 (通过 domain1 处理)
domain2 处理这个错误 (通过 domain2 处理)

events.js:72
        throw er; // Unhandled 'error' event
              ^
Error: 转换为异常，系统将崩溃!
    at Object.<anonymous> (/www/node/main.js:40:24)
    at Module._compile (module.js:456:26)
    at Object.Module._extensions..js (module.js:474:10)
    at Module.load (module.js:356:32)
    at Function.Module._load (module.js:312:12)
    at Function.Module.runMain (module.js:497:10)
    at startup (node.js:119:16)
    at node.js:929:3```

<strong>Node.js RESTful API</strong>
什么是 REST？
RREST即表述性状态传递（英文：Representational State Transfer，简称REST）是Roy Fielding博士在2000年他的博士论文中提出来的一种软件架构风格。
表述性状态转移是一组架构约束条件和原则。满足这些约束条件和原则的应用程序或设计就是RESTful。需要注意的是，REST是设计风格而不是标准。REST通常基于使用HTTP，URI，和XML（标准通用标记语言下的一个子集）以及HTML（标准通用标记语言下的一个应用）这些现有的广泛流行的协议和标准。REST 通常使用 JSON 数据格式。
HTTP 方法
以下为 REST 基本架构的四个方法：
GET - 用于获取数据。
PUT - 用于添加数据。
DELETE - 用于删除数据。
POST - 用于更新或添加数据。

HTTP 方法
以下为 REST 基本架构的四个方法：
GET - 用于获取数据。
PUT - 用于添加数据。
DELETE - 用于删除数据。
POST - 用于更新或添加数据。

获取用户列表
var express = require('express');
var app = express();
var fs = require("fs");



```js app.get('/listUsers', function (req, res) {
   fs.readFile( __dirname + "/" + "users.json", 'utf8', function (err, data) {
       console.log( data );
       res.end( data );
   });
})

var server = app.listen(8081, function () {

  var host = server.address().address
  var port = server.address().port

  console.log("应用实例，访问地址为 http://%s:%s", host, port)

})```

接下来执行以下命令：
$ node server.js 
应用实例，访问地址为 http://0.0.0.0:8081
在浏览器中访问 http://127.0.0.1:8081/listUsers，显示结果

添加用户


```js var express = require('express');
var app = express();
var fs = require("fs");

//添加的新用户数据
var user = {
   "user4" : {
      "name" : "mohit",
      "password" : "password4",
      "profession" : "teacher",
      "id": 4
   }
}

app.get('/addUser', function (req, res) {
   // 读取已存在的数据
   fs.readFile( __dirname + "/" + "users.json", 'utf8', function (err, data) {
       data = JSON.parse( data );
       data["user4"] = user["user4"];
       console.log( data );
       res.end( JSON.stringify(data));
   });
})

var server = app.listen(8081, function () {

  var host = server.address().address
  var port = server.address().port
  console.log("应用实例，访问地址为 http://%s:%s", host, port)

})```

运行方法是一样的。

显示用户详情


```js var express = require('express');
var app = express();
var fs = require("fs");

app.get('/:id', function (req, res) {
   // 首先我们读取已存在的用户
   fs.readFile( __dirname + "/" + "users.json", 'utf8', function (err, data) {
       data = JSON.parse( data );
       var user = data["user" + req.params.id] 
       console.log( user );
       res.end( JSON.stringify(user));
   });
})

var server = app.listen(8081, function () {

  var host = server.address().address
  var port = server.address().port
  console.log("应用实例，访问地址为 http://%s:%s", host, port)

})```



删除用户



```js var express = require('express');
var app = express();
var fs = require("fs");

var id = 2;

app.get('/deleteUser', function (req, res) {

   // First read existing users.
   fs.readFile( __dirname + "/" + "users.json", 'utf8', function (err, data) {
       data = JSON.parse( data );
       delete data["user" + 2];
       
       console.log( data );
       res.end( JSON.stringify(data));
   });
})

var server = app.listen(8081, function () {

  var host = server.address().address
  var port = server.address().port
  console.log("应用实例，访问地址为 http://%s:%s", host, port)

})```



```js Node.js 多进程```

我们都知道 Node.js 是以单线程的模式运行的，但它使用的是事件驱动来处理并发，这样有助于我们在多核 cpu 的系统上创建多个子进程，从而提高性能。
每个子进程总是带有三个流对象：child.stdin, child.stdout 和child.stderr（分别是标准输出，标准输入和标准错误。）。他们可能会共享父进程的 stdio 流，或者也可以是独立的被导流的流对象。
Node 提供了 child_process 模块来创建子进程，方法有：
exec - child_process.exec 使用子进程执行命令，缓存子进程的输出，并将子进程的输出以回调函数参数的形式返回。
spawn - child_process.spawn 使用指定的命令行参数创建新线程。
fork - child_process.fork 是 spawn()的特殊形式，用于在子进程中运行的模块，如 fork('./son.js') 相当于 spawn('node', ['./son.js']) 。与spawn方法不同的是，fork会在父进程与子进程之间，建立一个通信管道，用于进程之间的通信。

exec() 方法
child_process.exec 使用子进程执行命令，缓存子进程的输出，并将子进程的输出以回调函数参数的形式返回。
语法如下所示：
child_process.exec(command[, options], callback)
参数
参数说明如下：
command： 字符串， 将要运行的命令，参数使用空格隔开
options ：对象，可以是：
cwd ，字符串，子进程的当前工作目录
env，对象 环境变量键值对
encoding ，字符串，字符编码（默认： 'utf8'）
shell ，字符串，将要执行命令的 Shell（默认: 在 UNIX 中为/bin/sh， 在 Windows 中为cmd.exe， Shell 应当能识别 -c开关在 UNIX 中，或 /s /c 在 Windows 中。 在Windows 中，命令行解析应当能兼容cmd.exe）
timeout，数字，超时时间（默认： 0）
maxBuffer，数字， 在 stdout 或 stderr 中允许存在的最大缓冲（二进制），如果超出那么子进程将会被杀死 （默认: 200*1024）
killSignal ，字符串，结束信号（默认：'SIGTERM'）
uid，数字，设置用户进程的 ID
gid，数字，设置进程组的 ID
callback ：回调函数，包含三个参数error, stdout 和 stderr。
exec() 方法返回最大的缓冲区，并等待进程结束，一次性返回缓冲区的内容。

实例
让我们创建两个 js 文件 support.js 和 master.js。
support.js 文件代码：


```js console.log("进程 " + process.argv[2] + " 执行。" );```


master.js 文件代码：


```js const fs = require('fs');
const child_process = require('child_process');

for(var i=0; i<3; i++) {
   var workerProcess = child_process.exec('node support.js '+i,
      function (error, stdout, stderr) {
         if (error) {
            console.log(error.stack);
            console.log('Error code: '+error.code);
            console.log('Signal received: '+error.signal);
         }
         console.log('stdout: ' + stdout);
         console.log('stderr: ' + stderr);
      });

      workerProcess.on('exit', function (code) {
      console.log('子进程已退出，退出码 '+code);
   });
}```


执行以上代码，输出结果为：
$ node master.js 


```js 子进程已退出，退出码 0
stdout: 进程 0 执行。

stderr: 
子进程已退出，退出码 0
stdout: 进程 1 执行。

stderr: 
子进程已退出，退出码 0
stdout: 进程 2 执行。

stderr: ```

spawn() 方法
child_process.spawn 使用指定的命令行参数创建新线程，语法格式如下：
child_process.spawn(command[, args][, options])
参数
参数说明如下：
command： 将要运行的命令
args： Array 字符串参数数组
options Object
cwd String 子进程的当前工作目录
env Object 环境变量键值对
stdio Array|String 子进程的 stdio 配置
detached Boolean 这个子进程将会变成进程组的领导
uid Number 设置用户进程的 ID
gid Number 设置进程组的 ID
spawn() 方法返回流 (stdout & stderr)，在进程返回大量数据时使用。进程一旦开始执行时 spawn() 就开始接收响应。
实例
让我们创建两个 js 文件 support.js 和 master.js。
support.js 文件代码：


```js console.log("进程 " + process.argv[2] + " 执行。" );```


master.js 文件代码：


```js const fs = require('fs');
const child_process = require('child_process');
 
for(var i=0; i<3; i++) {
   var workerProcess = child_process.spawn('node', ['support.js', i]);

   workerProcess.stdout.on('data', function (data) {
      console.log('stdout: ' + data);
   });

   workerProcess.stderr.on('data', function (data) {
      console.log('stderr: ' + data);
   });

   workerProcess.on('close', function (code) {
      console.log('子进程已退出，退出码 '+code);
   });
}```


执行以上代码，输出结果为：
$ node master.js 


```js stdout: 进程 0 执行。

子进程已退出，退出码 0
stdout: 进程 1 执行。

子进程已退出，退出码 0
stdout: 进程 2 执行。

子进程已退出，退出码 0```

fork 方法
child_process.fork 是 spawn() 方法的特殊形式，用于创建进程，语法格式如下：


```js child_process.fork(modulePath[, args][, options])```


参数
参数说明如下：
modulePath： String，将要在子进程中运行的模块
args： Array 字符串参数数组
options：Object
cwd String 子进程的当前工作目录
env Object 环境变量键值对
execPath String 创建子进程的可执行文件
execArgv Array 子进程的可执行文件的字符串参数数组（默认： process.execArgv）
silent Boolean 如果为true，子进程的stdin，stdout和stderr将会被关联至父进程，否则，它们将会从父进程中继承。（默认为：false）
uid Number 设置用户进程的 ID
gid Number 设置进程组的 ID
返回的对象除了拥有ChildProcess实例的所有方法，还有一个内建的通信信道。
实例

support.js 文件代码：


```js console.log("进程 " + process.argv[2] + " 执行。" );
master.js 文件代码：
const fs = require('fs');
const child_process = require('child_process');
 
for(var i=0; i<3; i++) {
   var worker_process = child_process.fork("support.js", [i]);	

   worker_process.on('close', function (code) {
      console.log('子进程已退出，退出码 ' + code);
   });
}```


执行以上代码，输出结果为：
$ node master.js 


```js 进程 0 执行。
子进程已退出，退出码 0
进程 1 执行。
子进程已退出，退出码 0
进程 2 执行。
子进程已退出，退出码 0```



```js Node.js JXcore 打包```

Node.js 是一个开放源代码、跨平台的、用于服务器端和网络应用的运行环境。
JXcore 是一个支持多线程的 Node.js 发行版本，基本不需要对你现有的代码做任何改动就可以直接线程安全地以多线程运行。
但我们这篇文章主要是要教大家介绍 JXcore 的打包功能。

