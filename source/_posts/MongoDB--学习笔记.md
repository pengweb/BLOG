---
title: MongoDB--学习笔记
date: 2016-04-07 15:42:18
tags: [nodejs,笔记,note,mongoDB]

---
一、创建数据目录
```js c:\data\bd\```
二、命令行下运行 MongoDB 服务器
```js mongod.exe --dbpath c:\data\db //有的时候可以去掉.exe```
三、将MongoDB服务器作为Windows服务运行
```js mongod.exe
--bind_ip yourIPadress
--port yourPortNumber
--logpath "C:\data\mongodb.log"
--logappend --dbpath "C:\data\db"
--serviceName "YourServiceName"
--serviceDisplayName "YourServiceName"
--install```
```js mongod.exe --logpath "C:\data\mongodb.log" --logappend --dbpath "C:\data\db" --serviceName "zhp" --serviceDisplayName "zhpdisplay" --install```
--bind_ip 绑定服务IP，若绑定127.0.0.1，则只能本机访问，不指定默认本地所有IP
--logpath 定MongoDB日志文件，注意是指定文件不是目录
--logappend 使用追加的方式写日志
--dbpath 指定数据库路径
--port 指定服务端口号，默认端口27017
--serviceName 指定服务名称
--serviceDisplayNam 指定服务名称，有多个mongodb服务时执行。
--install 指定作为一个Windows服务安装。

MongoDB后台管理 Shell
如果你需要进入MongoDB后台管理，你需要先打开mongodb装目录的下的bin目录，然后执行mongo.exe文件，MongoDB Shell是MongoDB自带的交互式Javascript shell,用来对MongoDB进行操作和管理的交互式环境。
当你进入mongoDB后台后，它默认会链接到 test 文档（数据库）：
```js > mongo
MongoDB shell version: 3.0.6
connecting to: test
……```
db 命令用于查看当前操作的文档（数据库）：
```js > db
test
>```
插入一些简单的记录并查找它：
> db.pengweb.insert({x:10})
WriteResult({ "nInserted" : 1 })
> db.pengweb.find()
{ "_id" : ObjectId("5604ff74a274a611b0c990aa"), "x" : 10 }
>
第一个命令将数字 10 插入到 pengweb 集合的 x 字段中。

MongoDB 概念解析
不管我们学习什么数据库都应该学习其中的基础概念，在mongodb中基本的概念是文档、集合、数据库，下面我们挨个介绍。
下表将帮助您更容易理解Mongo中的一些概念：

&nbsp;
<table class="reference">
<tbody>
<tr>
<th>SQL术语/概念</th>
<th>MongoDB术语/概念</th>
<th>解释/说明</th>
</tr>
<tr>
<td>database</td>
<td>database</td>
<td>数据库</td>
</tr>
<tr>
<td>table</td>
<td>collection</td>
<td>数据库表/集合</td>
</tr>
<tr>
<td>row</td>
<td>document</td>
<td>数据记录行/文档</td>
</tr>
<tr>
<td>column</td>
<td>field</td>
<td>数据字段/域</td>
</tr>
<tr>
<td>index</td>
<td>index</td>
<td>索引</td>
</tr>
<tr>
<td>table joins</td>
<td></td>
<td>表连接,MongoDB不支持</td>
</tr>
<tr>
<td>primary key</td>
<td>primary key</td>
<td>主键,MongoDB自动将_id字段设置为主键</td>
</tr>
</tbody>
</table>
通过下图实例，我们也可以更直观的的了解Mongo中的一些概念：

<img src="http://www.runoob.com/wp-content/uploads/2013/10/Figure-1-Mapping-Table-to-Collection-1.png" alt="" />

数据库
一个mongodb中可以建立多个数据库。
MongoDB的默认数据库为"db"，该数据库存储在data目录中。
MongoDB的单个实例可以容纳多个独立的数据库，每一个都有自己的集合和权限，不同的数据库也放置在不同的文件中。
"show dbs" 命令可以显示所有数据的列表。
```js $ ./mongo
MongoDB shell version: 3.0.6
connecting to: test
> show dbs
local 0.078GB
test 0.078GB
>```
执行 "db" 命令可以显示当前数据库对象或集合。
```js $ ./mongo
MongoDB shell version: 3.0.6
connecting to: test
> db
test
>```
运行"use"命令，可以连接到一个指定的数据库。
```js > use local
switched to db local
> db
local
>```
数据库也通过名字来标识。数据库名可以是满足以下条件的任意UTF-8字符串。
不能是空字符串（"")。
不得含有' '（空格)、.、$、/、\和\0 (空宇符)。
应全部小写。
最多64字节。

文档
文档是mongodb中的最核心的概念，是其核心单元，我们可以将文档类比成关系型数据库中的每一行数据。
多个键及其关联的值有序的放置在一起就是文档。MongoDB使用了BSON这种结构来存储数据和网络数据交换。
BSON数据可以理解为在JSON的基础上添加了一些json中没有的数据类型。
如果我们会JSON，那么BSON我们就已经掌握了一半了，至于新添加的数据类型后面我会介绍。
文档例子如下：
{ site : "runoob.com" }
通常，"object（对象）" 术语是指一个文档。
文档类似于一个RDBMS的记录

集合
集合就是一组文档的组合。如果将文档类比成数据库中的行，那么集合就可以类比成数据库的表。
在mongodb中的集合是无模式的，也就是说集合中存储的文档的结构可以是不同的，比如下面的两个文档可以同时存入到一个集合中：
```js {"name":"mengxiangyue"}
{"Name":"mengxiangyue","sex":"nan"}```
当第一个文档插入时，集合就会被创建。
合法的集合名
集合名不能是空字符串""。
集合名不能含有\0字符（空字符)，这个字符表示集合名的结尾。
集合名不能以"system."开头，这是为系统集合保留的前缀。
用户创建的集合名字不能含有保留字符。有些驱动程序的确支持在集合名里面包含，这是因为某些系统生成的集合中包含该字符。除非你要访问这种系统创建的集合，否则千万不要在名字里出现$。
如下实例：
```js db.col.findOne() //col是集合名 findOne是方法```
capped collections
Capped collections 就是固定大小的collection。
它有很高的性能以及队列过期的特性(过期按照插入的顺序). 有点和 "RRD" 概念类似。
Capped collections是高性能自动的维护对象的插入顺序。它非常适合类似记录日志的功能 和标准的collection不同，你必须要显式的创建一个capped collection， 指定一个collection的大小，单位是字节。collection的数据存储空间值提前分配的。
要注意的是指定的存储大小包含了数据库的头信息。
db.createCollection("mycoll", {capped:true, size:100000})
在capped collection中，你能添加新的对象。
能进行更新，然而，对象不会增加存储空间。如果增加，更新就会失败 。
数据库不允许进行删除。使用drop()方法删除collection所有的行。
注意: 删除之后，你必须显式的重新创建这个collection。
在32bit机器中，capped collection最大存储为1e9( 1X109)个字节。
元数据
数据库的信息是存储在集合中。它们使用了系统的命名空间：
dbname.system.*
在MongoDB数据库中名字空间 .system.* 是包含多种系统信息的特殊集合(Collection)，如下:
集合命名空间 描述
dbname.system.namespaces 列出所有名字空间。
dbname.system.indexes 列出所有索引。
dbname.system.profile 包含数据库概要(profile)信息。
dbname.system.users 列出所有可访问数据库的用户。
dbname.local.sources 包含复制对端（slave）的服务器信息和状态。
对于修改系统集合中的对象有如下限制。
在{{system.indexes}}插入数据，可以创建索引。但除此之外该表信息是不可变的(特殊的drop index命令将自动更新相关信息)。
{{system.users}}是可修改的。 {{system.profile}}是可删除的。

MongoDB - 连接
通过shell连接MongoDB服务
你可以通过执行以下命令来连接MongoDB的服务。
注意：localhost为主机名，这个选项是必须的：
mongodb://localhost
当你执行以上命令时

MongoDB连接命令格式
使用用户名和密码连接到MongoDB服务器，你必须使用 'username:password@hostname/dbname' 格式，'username'为用户名，'password' 为密码。
使用用户名和密码连接登陆到默认数据库：
```js $ ./mongo
MongoDB shell version: 3.0.6
connecting to: test
mongodb://admin:123456@localhost/```
以上命令中，用户 admin 使用密码 123456 连接到本地的 MongoDB 服务上。输出结果如下所示：&lt;、p>
```js > mongodb://admin:123456@localhost/
...```
更多连接实例
连接本地数据库服务器，端口是默认的。
```js mongodb://localhost```
使用用户名fred，密码foobar登录localhost的admin数据库。
```js mongodb://fred:foobar@localhost```
使用用户名fred，密码foobar登录localhost的baz数据库。
```js mongodb://fred:foobar@localhost/baz```
连接 replica pair, 服务器1为example1.com服务器2为example2。
```js mongodb://example1.com:27017,example2.com:27017```
连接 replica set 三台服务器 (端口 27017, 27018, 和27019):
```js mongodb://localhost,localhost:27018,localhost:27019```
连接 replica set 三台服务器, 写入操作应用在主服务器 并且分布查询到从服务器。
```js mongodb://host1,host2,host3/?slaveOk=true```
直接连接第一个服务器，无论是replica set一部分或者主服务器或者从服务器。
```js mongodb://host1,host2,host3/?connect=direct;slaveOk=true```
当你的连接服务器有优先级，还需要列出所有服务器，你可以使用上述连接方式。
安全模式连接到localhost:
```js mongodb://localhost/?safe=true```
以安全模式连接到replica set，并且等待至少两个复制服务器成功写入，超时时间设置为2秒。
```js mongodb://host1,host2,host3/?safe=true;w=2;wtimeoutMS=2000```
参数说明：请查看api

MongoDB 创建数据库
语法
MongoDB 创建数据库的语法格式如下：
```js use DATABASE_NAME```
如果数据库不存在，则创建数据库，否则切换到指定数据库。

我们刚创建的数据库 runoob 并不在数据库的列表中， 要显示它，我们需要向 runoob 数据库插入一些数据。
```js > db.runoob.insert({"name":"菜鸟教程"})
WriteResult({ "nInserted" : 1 })
> show dbs
local 0.078GB
runoob 0.078GB
test 0.078GB
>```
MongoDB 中默认的数据库为 test，如果你没有创建新的数据库，集合将存放在 test 数据库中。

MongoDB 删除数据库
语法
MongoDB 删除数据库的语法格式如下：
db.dropDatabase()
删除当前数据库，默认为 test，你可以使用 db 命令查看当前数据库名。

执行删除命令：
```js > db.dropDatabase() //切换到要删除的目录下，执行这个语句，就会删除了
{ "dropped" : "runoob", "ok" : 1 }```
MongoDB 插入文档
本章节中我们将向大家介绍如何将数据插入到MongoDB的集合中。
文档的数据结构和JSON基本一样。
所有存储在集合中的数据都是BSON格式。
BSON是一种类json的一种二进制形式的存储格式,简称Binary JSON。
插入文档
MongoDB 使用 insert() 或 save() 方法向集合中插入文档，语法如下：
```js db.COLLECTION_NAME.insert(document)```
实例
以下文档可以存储在 MongoDB 的 runoob 数据库 的 col集合中：
```js >db.col.insert({title: 'MongoDB 教程',
description: 'MongoDB 是一个 Nosql 数据库',
by: '菜鸟教程',
url: 'http://www.runoob.com',
tags: ['mongodb', 'database', 'NoSQL'],
likes: 100
})```
以上实例中 col 是我们的集合名，前一章节我们已经创建过了，如果该集合不在该数据库中， MongoDB 会自动创建该集合比插入文档。
查看已插入文档：
```js > db.col.find()
{ "_id" : ObjectId("56064886ade2f21f36b03134"), "title" : "MongoDB 教程", "description" : "MongoDB 是一个 Nosql 数据库", "by" : "菜鸟教程", "url" : "http://www.runoob.com", "tags" : [ "mongodb", "database", "NoSQL" ], "likes" : 100 }
>```
我们也可以将数据定义为一个变量，如下所示：
```js > document=({title: 'MongoDB 教程',
description: 'MongoDB 是一个 Nosql 数据库',
by: '菜鸟教程',
url: 'http://www.runoob.com',
tags: ['mongodb', 'database', 'NoSQL'],
likes: 100
});```
执行后显示结果如下：
```js {
"title" : "MongoDB 教程",
"description" : "MongoDB 是一个 Nosql 数据库",
"by" : "菜鸟教程",
"url" : "http://www.runoob.com",
"tags" : [
"mongodb",
"database",
"NoSQL"
],
"likes" : 100
}```
执行插入操作：
```js > db.col.insert(document)
WriteResult({ "nInserted" : 1 })
>```
MongoDB 更新文档
MongoDB 使用 update() 和 save() 方法来更新集合中的文档。接下来让我们详细来看下两个函数的应用及其区别。
update() 方法
update() 方法用于更新已存在的文档。语法格式如下：
```js db.collection.update(
,
,
{
upsert: ,
multi: ,
writeConcern:
}
)```
参数说明：
query : update的查询条件，类似sql update查询内where后面的。
update : update的对象和一些更新的操作符（如$,$inc...）等，也可以理解为sql update查询内set后面的
upsert : 可选，这个参数的意思是，如果不存在update的记录，是否插入objNew,true为插入，默认是false，不插入。
multi : 可选，mongodb 默认是false,只更新找到的第一条记录，如果这个参数为true,就把按条件查出来多条记录全部更新。
writeConcern :可选，抛出异常的级别。
```js >db.col.insert({
title: 'MongoDB 教程',
description: 'MongoDB 是一个 Nosql 数据库',
by: '菜鸟教程',
url: 'http://www.runoob.com',
tags: ['mongodb', 'database', 'NoSQL'],```
likes: 100
})
接着我们通过 update() 方法来更新标题(title):
```js >db.col.update({'title':'MongoDB 教程'},{$set:{'title':'MongoDB'}})
WriteResult({ "nMatched" : 1, "nUpserted" : 0, "nModified" : 1 }) # 输出信息
> db.col.find().pretty()
{
"_id" : ObjectId("56064f89ade2f21f36b03136"),
"title" : "MongoDB",
"description" : "MongoDB 是一个 Nosql 数据库",
"by" : "菜鸟教程",
"url" : "http://www.runoob.com",
"tags" : [
"mongodb",
"database",
"NoSQL"
],
"likes" : 100
}
>```
save() 方法
save() 方法通过传入的文档来替换已有文档。语法格式如下：
db.collection.save(
,
{
writeConcern:
}
)
参数说明：
document : 文档数据。
writeConcern :可选，抛出异常的级别。
实例
以下实例中我们替换了 _id 为 56064f89ade2f21f36b03136 的文档数据：
```js >db.col.save({
"_id" : ObjectId("56064f89ade2f21f36b03136"),
"title" : "MongoDB",
"description" : "MongoDB 是一个 Nosql 数据库",
"by" : "Runoob",
"url" : "http://www.runoob.com",
"tags" : [
"mongodb",
"NoSQL"
],
"likes" : 110
})```
替换成功后，我们可以通过 find() 命令来查看替换后的数据
```js >db.col.find().pretty()
{
"_id" : ObjectId("56064f89ade2f21f36b03136"),
"title" : "MongoDB",
"description" : "MongoDB 是一个 Nosql 数据库",
"by" : "Runoob",
"url" : "http://www.runoob.com",
"tags" : [
"mongodb",
"NoSQL"
],
"likes" : 110
}
>```
更多实例
只更新第一条记录：
```js db.col.update( { "count" : { $gt : 1 } } , { $set : { "test2" : "OK"} } );```
全部更新：
```js db.col.update( { "count" : { $gt : 3 } } , { $set : { "test2" : "OK"} },false,true );```
只添加第一条：
```js db.col.update( { "count" : { $gt : 4 } } , { $set : { "test5" : "OK"} },true,false );```
全部添加加进去:
```js db.col.update( { "count" : { $gt : 5 } } , { $set : { "test5" : "OK"} },true,true );```
全部更新：
```js db.col.update( { "count" : { $gt : 15 } } , { $inc : { "count" : 1} },false,true );```
只更新第一条记录：
```js db.col.update( { "count" : { $gt : 10 } } , { $inc : { "count" : 1} },false,false );```
MongoDB 删除文档
在前面的几个章节中我们已经学习了MongoDB中如何为集合添加数据和更新数据。在本章节中我们将继续学习MongoDB集合的删除。
MongoDB remove()函数是用来移除集合中的数据。
MongoDB数据更新可以使用update()函数。在执行remove()函数前先执行find()命令来判断执行的条件是否正确，这是一个比较好的习惯。
语法
remove() 方法的基本语法格式如下所示：
```js db.collection.remove(
,

)```
如果你的 MongoDB 是 2.6 版本以后的，语法格式如下：
```js db.collection.remove(
,
{
justOne: ,
writeConcern:
}
)```
参数说明：
query :（可选）删除的文档的条件。
justOne : （可选）如果设为 true 或 1，则只删除一个文档。
writeConcern :（可选）抛出异常的级别。

实例
以下文档我们执行两次插入操作：
```js >db.col.insert({title: 'MongoDB 教程',
description: 'MongoDB 是一个 Nosql 数据库',
by: '菜鸟教程',
url: 'http://www.runoob.com',
tags: ['mongodb', 'database', 'NoSQL'],
likes: 100
})```
使用 find() 函数查询数据：
```js > db.col.find()
{ "_id" : ObjectId("56066169ade2f21f36b03137"), "title" : "MongoDB 教程", "description" : "MongoDB 是一个 Nosql 数据库", "by" : "菜鸟教程", "url" : "http://www.runoob.com", "tags" : [ "mongodb", "database", "NoSQL" ], "likes" : 100 }
{ "_id" : ObjectId("5606616dade2f21f36b03138"), "title" : "MongoDB 教程", "description" : "MongoDB 是一个 Nosql 数据库", "by" : "菜鸟教程", "url" : "http://www.runoob.com", "tags" : [ "mongodb", "database", "NoSQL" ], "likes" : 100 }
接下来我们移除 title 为 'MongoDB 教程' 的文档：
>db.col.remove({'title':'MongoDB 教程'})
WriteResult({ "nRemoved" : 2 }) # 删除了两条数据
>db.col.find()
…… # 没有数据```
如果你只想删除第一条找到的记录可以设置 justOne 为 1，如下所示：
```js >db.COLLECTION_NAME.remove(DELETION_CRITERIA,1)```
如果你想删除所有数据，可以使用以下方式（类似常规 SQL 的 truncate 命令）：
```js >db.col.remove({})
>db.col.find()
>```
MongoDB 查询文档
语法
MongoDB 查询数据的语法格式如下：
```js >db.COLLECTION_NAME.find()```
find() 方法以非结构化的方式来显示所有文档。
如果你需要以易读的方式来读取数据，可以使用 pretty() 方法，语法格式如下：
>db.col.find().pretty()
pretty() 方法以格式化的方式来显示所有文档。
实例
```js > db.col.find().pretty()```
除了 find() 方法之外，还有一个 findOne() 方法，它只返回一个文档。

MongoDB 与 RDBMS Where 语句比较
如果你熟悉常规的 SQL 数据，通过下表可以更好的理解 MongoDB 的条件语句查询：
操作 格式 范例 RDBMS中的类似语句
等于 {:} db.col.find({"by":"菜鸟教程"}).pretty() where by = '菜鸟教程'
小于 {:{$lt:}} db.col.find({"likes":{$lt:50}}).pretty() where likes &lt; 50
小于或等于 {:{$lte:}} db.col.find({"likes":{$lte:50}}).pretty() where likes &lt;= 50
大于 {:{$gt:}} db.col.find({"likes":{$gt:50}}).pretty() where likes > 50
大于或等于 {:{$gte:}} db.col.find({"likes":{$gte:50}}).pretty() where likes >= 50
不等于 {:{$ne:}} db.col.find({"likes":{$ne:50}}).pretty() where likes != 50

MongoDB AND 条件
MongoDB 的 find() 方法可以传入多个键(key)，每个键(key)以逗号隔开，及常规 SQL 的 AND 条件。
语法格式如下：
>db.col.find({key1:value1, key2:value2}).pretty()
实例
以下实例通过 by 和 title 键来查询 菜鸟教程 中 MongoDB 教程 的数据
```js > db.col.find({"by":"菜鸟教程", "title":"MongoDB 教程"}).pretty()
{
"_id" : ObjectId("56063f17ade2f21f36b03133"),
"title" : "MongoDB 教程",
"description" : "MongoDB 是一个 Nosql 数据库",
"by" : "菜鸟教程",
"url" : "http://www.runoob.com",
"tags" : [
"mongodb",
"database",
"NoSQL"
],
"likes" : 100
}```
以上实例中类似于 WHERE 语句：WHERE by='菜鸟教程' AND title='MongoDB 教程'

MongoDB OR 条件
MongoDB OR 条件语句使用了关键字 $or,语法格式如下：
```js >db.col.find(
{
$or: [
{key1: value1}, {key2:value2}
]
}
).pretty()```
实例
以下实例中，我们演示了查询键 by 值为 菜鸟教程 或键 title 值为 MongoDB 教程 的文档。
```js >db.col.find({$or:[{"by":"菜鸟教程"},{"title": "MongoDB 教程"}]}).pretty()
{
"_id" : ObjectId("56063f17ade2f21f36b03133"),
"title" : "MongoDB 教程",
"description" : "MongoDB 是一个 Nosql 数据库",
"by" : "菜鸟教程",
"url" : "http://www.runoob.com",
"tags" : [
"mongodb",
"database",
"NoSQL"
],
"likes" : 100
}
>```
AND 和 OR 联合使用
以下实例演示了 AND 和 OR 联合使用，类似常规 SQL 语句为： 'where url='http://www.runoob.com' AND (by = '菜鸟教程' OR title = 'MongoDB 教程')'
```js >db.col.find({"likes": {$gt:50}, $or: [{"by": "菜鸟教程"},{"title": "MongoDB 教程"}]}).pretty()
{
"_id" : ObjectId("56063f17ade2f21f36b03133"),
"title" : "MongoDB 教程",
"description" : "MongoDB 是一个 Nosql 数据库",
"by" : "菜鸟教程",
"url" : "http://www.runoob.com",
"tags" : [
"mongodb",
"database",
"NoSQL"
],
"likes" : 100
}```
MongoDB 条件操作符

描述
条件操作符用于比较两个表达式并从mongoDB集合中获取数据。
在本章节中，我们将讨论如何在MongoDB中使用条件操作符。
MongoDB中条件操作符有：
(>) 大于 - $gt
(&lt;) 小于 - $lt (>=) 大于等于 - $gte
(&lt;= ) 小于等于 - $lte
我们使用的数据库名称为"runoob" 我们的集合名称为"col"，以下为我们插入的数据。
为了方便测试，我们可以先使用以下命令清空集合 "col" 的数据：
```js db.col.remove({})```
MongoDB (>) 大于操作符 - $gt
如果你想获取 "col" 集合中 "likes" 大于 100 的数据，你可以使用以下命令：
```js db.col.find({"likes" : {$gt : 100}})```
类似于SQL语句：
Select * from col where likes > 22;
输出结果：
> db.col.find({"likes" : {$gt : 100}})
{ "_id" : ObjectId("56066542ade2f21f36b0313a"), "title" : "PHP 教程", "description" : "PHP 是一种创建动态交互性站点的强有力的服务器端脚本语言。", "by" : "菜鸟教程", "url" : "http://www.runoob.com", "tags" : [ "php" ], "likes" : 200 }
{ "_id" : ObjectId("56066549ade2f21f36b0313b"), "title" : "Java 教程", "description" : "Java 是由Sun Microsystems公司于1995年5月推出的高级程序设计语言。", "by" : "菜鸟教程", "url" : "http://www.runoob.com", "tags" : [ "java" ], "likes" : 150 }
>

MongoDB (>) 大于操作符 - $gt
如果你想获取 "col" 集合中 "likes" 大于 100 的数据，你可以使用以下命令：
```js db.col.find({"likes" : {$gt : 100}})```
类似于SQL语句：
```js Select * from col where likes > 22;```
输出结果：
```js > db.col.find({"likes" : {$gt : 100}})
{ "_id" : ObjectId("56066542ade2f21f36b0313a"), "title" : "PHP 教程", "description" : "PHP 是一种创建动态交互性站点的强有力的服务器端脚本语言。", "by" : "菜鸟教程", "url" : "http://www.runoob.com", "tags" : [ "php" ], "likes" : 200 }
{ "_id" : ObjectId("56066549ade2f21f36b0313b"), "title" : "Java 教程", "description" : "Java 是由Sun Microsystems公司于1995年5月推出的高级程序设计语言。", "by" : "菜鸟教程", "url" : "http://www.runoob.com", "tags" : [ "java" ], "likes" : 150 }
>```
MongoDB（>=）大于等于操作符 - $gte
如果你想获取"col"集合中 "likes" 大于等于 100 的数据，你可以使用以下命令：
```js db.col.find({likes : {$gte : 100}})```
类似于SQL语句：
Select * from col where likes >=100;

MongoDB (&lt;) 小于操作符 - $lt
如果你想获取"col"集合中 "likes" 小于 150 的数据，你可以使用以下命令：
```js db.col.find({likes : {$lt : 150}})```
类似于SQL语句：
Select * from col where likes &lt; 150;

MongoDB (&lt;=) 小于操作符 - $lte
如果你想获取"col"集合中 "likes" 小于等于 150 的数据，你可以使用以下命令：
```js db.col.find({likes : {$lte : 150}})```
类似于SQL语句：
Select * from col where likes &lt;= 150;

MongoDB 使用 (&lt;) 和 (>) 查询 - $lt 和 $gt
如果你想获取"col"集合中 "likes" 大于100，小于 200 的数据，你可以使用以下命令：
```js db.col.find({likes : {$lt :200, $gt : 100}})```
类似于SQL语句：
Select * from col where likes>100 AND likes&lt;200;

MongoDB $type 操作符

描述
在本章节中，我们将继续讨论MongoDB中条件操作符 $type。
$type操作符是基于BSON类型来检索集合中匹配的数据类型，并返回结果。
MongoDB 中可以使用的类型如下表所示：
我们使用的数据库名称为"runoob" 我们的集合名称为"col"，以下为我们插入的数据。
简单的集合"col"： 和条件操作符一样，在集合col中插入3个文档

MongoDB 操作符 - $type 实例
如果想获取 "col" 集合中 title 为 String 的数据，你可以使用以下命令：
```js db.col.find({"title" : {$type : 2}})```
Double 1
String 2
Object 3
Array 4
Binary data 5
Undefined 6 已废弃。
Object id 7
Boolean 8
Date 9
Null 10
Regular Expression 11
JavaScript 13
Symbol 14
JavaScript (with scope) 15
32-bit integer 16
Timestamp 17
64-bit integer 18
Min key 255 Query with -1.
Max key 127

MongoDB Limit与Skip方法
MongoDB Limit() 方法
如果你需要在MongoDB中读取指定数量的数据记录，可以使用MongoDB的Limit方法，limit()方法接受一个数字参数，该参数指定从MongoDB中读取的记录条数。
语法
limit()方法基本语法如下所示：
```js >db.COLLECTION_NAME.find().limit(NUMBER)```
以上实例为显示查询文档中的两条记录：
```js > db.col.find({},{"title":1,_id:0}).limit(2)
//第一个{}是集合名，title后边的1是只显示title，默认是显示_id的，所以让他为0，这样他就不会显示了，limit是显示几个文档
{ "title" : "PHP 教程" }
{ "title" : "Java 教程" }
>```
MongoDB Skip() 方法
我们除了可以使用limit()方法来读取指定数量的数据外，还可以使用skip()方法来跳过指定数量的数据，skip方法同样接受一个数字参数作为跳过的记录条数。
语法
skip() 方法脚本语法格式如下：
```js >db.COLLECTION_NAME.find().limit(NUMBER).skip(NUMBER)```
实例
以上实例只会显示第二条文档数据
```js >db.col.find({},{"title":1,_id:0}).limit(1).skip(1)
{ "title" : "Java 教程" }
>```
MongoDB 排序
MongoDB sort()方法
在MongoDB中使用使用sort()方法对数据进行排序，sort()方法可以通过参数指定排序的字段，并使用 1 和 -1 来指定排序的方式，其中 1 为升序排列，而-1是用于降序排列。
语法
sort()方法基本语法如下所示：
```js >db.COLLECTION_NAME.find().sort({KEY:1})```
以下实例演示了 col 集合中的数据按字段 likes 的降序排列：
```js >db.col.find({},{"title":1,_id:0}).sort({"likes":-1})
{ "title" : "PHP 教程" }
{ "title" : "Java 教程" }
{ "title" : "MongoDB 教程" }
>```
实例
在后台创建索引：
```js db.values.ensureIndex({open: 1, close: 1}, {background: true})```
其中open后的1表示升序，如果是-1则是降序，background是ensureIndex的可选参数，创建工作在后台运行
通过在创建索引时加background:true 的选项，让创建工作在后台执行

MongoDB 聚合
MongoDB中聚合(aggregate)主要用于处理数据(诸如统计平均值,求和等)，并返回计算后的数据结果。有点类似sql语句中的 count(*)。
aggregate() 方法
MongoDB中聚合的方法使用aggregate()。
语法
aggregate() 方法的基本语法格式如下所示：
```js >db.COLLECTION_NAME.aggregate(AGGREGATE_OPERATION)```
现在我们通过以上集合计算每个作者所写的文章数，使用aggregate()计算结果如下：
```js > db.mycol.aggregate([{$group : {_id : "$by_user", num_tutorial : {$sum : 1}}}])
//$group是管道聚合有讲，通过by_user进行数据分组，num_tutorial这个是自定义的，$sum是说求和的意思
{
"result" : [ //result固定格式
{
"_id" : "w3cschool.cc",
"num_tutorial" : 2
},
{
"_id" : "Neo4j",
"num_tutorial" : 1
}
],
"ok" : 1 //ok固定格式
}
>```
管道的概念
管道在Unix和Linux中一般用于将当前命令的输出结果作为下一个命令的参数。
MongoDB的聚合管道将MongoDB文档在一个管道处理完毕后将结果传递给下一个管道处理。管道操作是可以重复的。
表达式：处理输入文档并输出。表达式是无状态的，只能用于计算当前聚合管道的文档，不能处理其它的文档。
这里我们介绍一下聚合框架中常用的几个操作：
$project：修改输入文档的结构。可以用来重命名、增加或删除域，也可以用于创建计算结果以及嵌套文档。
$match：用于过滤数据，只输出符合条件的文档。$match使用MongoDB的标准查询操作。
$limit：用来限制MongoDB聚合管道返回的文档数。
$skip：在聚合管道中跳过指定数量的文档，并返回余下的文档。
$unwind：将文档中的某一个数组类型字段拆分成多条，每条包含数组中的一个值。
$group：将集合中的文档分组，可用于统计结果。
$sort：将输入文档排序后输出。
$geoNear：输出接近某一地理位置的有序文档。
管道操作符实例

1、$project实例
```js db.article.aggregate(
{ $project : {
title : 1 ,
author : 1 ,
}}
);```
这样的话结果中就只还有_id,tilte和author三个字段了，默认情况下_id字段是被包含的，如果要想不包含_id话可以这样:
```js db.article.aggregate(
{ $project : {
_id : 0 ,
title : 1 ,
author : 1
}});```
2.$match实例
```js db.articles.aggregate( [
{ $match : { score : { $gt : 70, $lte : 90 } } },
{ $group: { _id: null, count: { $sum: 1 } } }
] );```
$match用于获取分数大于70小于或等于90记录，然后将符合条件的记录送到下一阶段$group管道操作符进行处理。
3.$skip实例
```js db.article.aggregate(
{ $skip : 5 });```
经过$skip管道操作符处理后，前五个文档被"过滤"掉。

MongoDB 复制（副本集）
MongoDB复制是将数据同步在多个服务器的过程。
复制提供了数据的冗余备份，并在多个服务器上存储数据副本，提高了数据的可用性， 并可以保证数据的安全性。
复制还允许您从硬件故障和服务中断中恢复数据。
什么是复制?
保障数据的安全性
数据高可用性 (24*7)
灾难恢复
无需停机维护（如备份，重建索引，压缩）
分布式读取数据
MongoDB复制原理
mongodb的复制至少需要两个节点。其中一个是主节点，负责处理客户端请求，其余的都是从节点，负责复制主节点上的数据。
mongodb各个节点常见的搭配方式为：一主一从、一主多从。
主节点记录在其上的所有操作oplog，从节点定期轮询主节点获取这些操作，然后对自己的数据副本执行这些操作，从而保证从节点的数据与主节点一致。
MongoDB复制结构图如下所示：

<img src="http://www.runoob.com/wp-content/uploads/2013/12/replication.png" alt="MongoDB复制结构图" />
MongoDB复制结构图
以上结构图总，客户端总主节点读取数据，在客户端写入数据到主节点是， 主节点与从节点进行数据交互保障数据的一致性。
副本集特征：
N 个节点的集群
任何节点可作为主节点
所有写入操作都在主节点上
自动故障转移
自动恢复

MongoDB副本集设置
在本教程中我们使用同一个MongoDB来做MongoDB主从的实验， 操作步骤如下：
1、关闭正在运行的MongoDB服务器。
现在我们通过指定 --replSet 选项来启动mongoDB。--replSet 基本语法格式如下：
```js mongod --port "PORT" --dbpath "YOUR_DB_DATA_PATH" --replSet "REPLICA_SET_INSTANCE_NAME"```
实例
```js mongod --port 27017 --dbpath "D:\set up\mongodb\data" --replSet rs0```
以上实例会启动一个名为rs0的MongoDB实例，其端口号为27017。
启动后打开命令提示框并连接上mongoDB服务。
在Mongo客户端使用命令rs.initiate()来启动一个新的副本集。
我们可以使用rs.conf()来查看副本集的配置
查看副本集姿态使用 rs.status() 命令

副本集添加成员
添加副本集的成员，我们需要使用多条服务器来启动mongo服务。进入Mongo客户端，并使用rs.add()方法来添加副本集的成员。
语法
rs.add() 命令基本语法格式如下：
```js >rs.add(HOST_NAME:PORT)```
实例
假设你已经启动了一个名为mongod1.net，端口号为27017的Mongo服务。 在客户端命令窗口使用rs.add() 命令将其添加到副本集中，命令如下所示：
```js >rs.add("mongod1.net:27017")
>```
MongoDB中你只能通过主节点将Mongo服务添加到副本集中， 判断当前运行的Mongo服务是否为主节点可以使用命令db.isMaster() 。
MongoDB的副本集与我们常见的主从有所不同，主从在主机宕机后所有服务将停止，而副本集在主机宕机后，副本会接管主节点成为主节点，不会出现宕机的情况。

MongoDB 分片
分片
在Mongodb里面存在另一种集群，就是分片技术,可以满足MongoDB数据量大量增长的需求。
当MongoDB存储海量的数据时，一台机器可能不足以存储数据也足以提供可接受的读写吞吐量。这时，我们就可以通过在多台机器上分割数据，使得数据库系统能存储和处理更多的数据。
为什么使用分片
复制所有的写入操作到主节点
延迟的敏感数据会在主节点查询
单个副本集限制在12个节点
当请求量巨大时会出现内存不足。
本地磁盘不足
垂直扩展价格昂贵
MongoDB分片
下图展示了在MongoDB中使用分片集群结构分布：

<img src="http://www.runoob.com/wp-content/uploads/2013/12/sharding.png" alt="" />

上图中主要有如下所述三个主要组件：
Shard:
用于存储实际的数据块，实际生产环境中一个shard server角色可由几台机器组个一个relica set承担，防止主机单点故障
Config Server:
mongod实例，存储了整个 ClusterMetadata，其中包括 chunk信息。
Query Routers:
前端路由，客户端由此接入，且让整个集群看上去像单一数据库，前端应用可以透明使用。
分片实例（完全没看懂）
分片结构端口分布如下：
Shard Server 1：27020
Shard Server 2：27021
Shard Server 3：27022
Shard Server 4：27023
Config Server ：27100
Route Process：40000
步骤一：启动Shard Server
[root@100 /]# mkdir -p /www/mongoDB/shard/s0
[root@100 /]# mkdir -p /www/mongoDB/shard/s1
[root@100 /]# mkdir -p /www/mongoDB/shard/s2
[root@100 /]# mkdir -p /www/mongoDB/shard/s3
[root@100 /]# mkdir -p /www/mongoDB/shard/log
[root@100 /]# /usr/local/mongoDB/bin/mongod --port 27020 --dbpath=/www/mongoDB/shard/s0 --logpath=/www/mongoDB/shard/log/s0.log --logappend --fork
....
[root@100 /]# /usr/local/mongoDB/bin/mongod --port 27023 --dbpath=/www/mongoDB/shard/s3 --logpath=/www/mongoDB/shard/log/s3.log --logappend --fork
步骤二： 启动Config Server
[root@100 /]# mkdir -p /www/mongoDB/shard/config
[root@100 /]# /usr/local/mongoDB/bin/mongod --port 27100 --dbpath=/www/mongoDB/shard/config --logpath=/www/mongoDB/shard/log/config.log --logappend --fork
注意：这里我们完全可以像启动普通mongodb服务一样启动，不需要添加—shardsvr和configsvr参数。因为这两个参数的作用就是改变启动端口的，所以我们自行指定了端口就可以。
步骤三： 启动Route Process
/usr/local/mongoDB/bin/mongos --port 40000 --configdb localhost:27100 --fork --logpath=/www/mongoDB/shard/log/route.log --chunkSize 500
mongos启动参数中，chunkSize这一项是用来指定chunk的大小的，单位是MB，默认大小为200MB.
步骤四： 配置Sharding
接下来，我们使用MongoDB Shell登录到mongos，添加Shard节点
[root@100 shard]# /usr/local/mongoDB/bin/mongo admin --port 40000
MongoDB shell version: 2.0.7
connecting to: 127.0.0.1:40000/admin
mongos> db.runCommand({ addshard:"localhost:27020" })
{ "shardAdded" : "shard0000", "ok" : 1 }
......
mongos> db.runCommand({ addshard:"localhost:27029" })
{ "shardAdded" : "shard0009", "ok" : 1 }
mongos> db.runCommand({ enablesharding:"test" }) #设置分片存储的数据库
{ "ok" : 1 }
mongos> db.runCommand({ shardcollection: "test.log", key: { id:1,time:1}})
{ "collectionsharded" : "test.log", "ok" : 1 }
步骤五： 程序代码内无需太大更改，直接按照连接普通的mongo数据库那样，将数据库连接接入接口40000

MongoDB 备份(mongodump)与恢复(mongorerstore)
MongoDB数据备份
在Mongodb中我们使用mongodump命令来备份MongoDB数据。该命令可以导出所有数据到指定目录中。
mongodump命令可以通过参数指定导出的数据量级转存的服务器。
语法
mongodump命令脚本语法如下：
```js >mongodump -h dbhost -d dbname -o dbdirectory```
-h：
MongDB所在服务器地址，例如：127.0.0.1，当然也可以指定端口号：127.0.0.1:27017
-d：
需要备份的数据库实例，例如：test
-o：
备份的数据存放位置，例如：c:\data\dump，当然该目录需要提前建立，在备份完成后，系统自动在dump目录下建立一个test目录，这个目录里面存放该数据库实例的备份数据。
实例
在本地使用 27017 启动你的mongod服务。打开命令提示符窗口，进入MongoDB安装目录的bin目录输入命令mongodump:
```js >mongodump```
MongoDB数据恢复
mongodb使用 mongorerstore 命令来恢复备份的数据。
语法
mongorestore命令脚本语法如下：
```js >mongorestore -h dbhost -d dbname --directoryperdb dbdirectory```
-h：
MongoDB所在服务器地址
-d：
需要恢复的数据库实例，例如：test，当然这个名称也可以和备份时候的不一样，比如test2
--directoryperdb：
备份数据所在位置，例如：c:\data\dump\test，这里为什么要多加一个test，而不是备份时候的dump，读者自己查看提示吧！
--drop：
恢复的时候，先删除当前数据，然后恢复备份的数据。就是说，恢复后，备份后添加修改的数据都会被删除，慎用哦！
接下来我们执行以下命令:
```js >mongorestore```
MongoDB 监控
在你已经安装部署并允许MongoDB服务后，你必须要了解MongoDB的运行情况，并查看MongoDB的性能。这样在大流量得情况下可以很好的应对并保证MongoDB正常运作。
MongoDB中提供了mongostat 和 mongotop 两个命令来监控MongoDB的运行情况。
mongostat 命令
mongostat是mongodb自带的状态检测工具，在命令行下使用。它会间隔固定时间获取mongodb的当前运行状态，并输出。如果你发现数据库突然变慢或者有其他问题的话，你第一手的操作就考虑采用mongostat来查看mongo的状态。
启动你的Mongod服务，进入到你安装的MongoDB目录下的bin目录， 然后输入mongostat命令，如下所示：
```js D:\set up\mongodb\bin>mongostat```
mongotop 命令
mongotop也是mongodb下的一个内置工具，mongotop提供了一个方法，用来跟踪一个MongoDB的实例，查看哪些大量的时间花费在读取和写入数据。 mongotop提供每个集合的水平的统计数据。默认情况下，mongotop返回值的每一秒。
启动你的Mongod服务，进入到你安装的MongoDB目录下的bin目录， 然后输入mongotop命令，如下所示：
```js D:\set up\mongodb\bin>mongotop```
带参数实例
```js E:\mongodb-win32-x86_64-2.2.1\bin>mongotop 10```
后面的10是参数 ，可以不使用，等待的时间长度，以秒为单位，mongotop等待调用之间。通过的默认mongotop返回数据的每一秒。
```js E:\mongodb-win32-x86_64-2.2.1\bin>mongotop --locks```
报告每个数据库的锁的使用中，使用mongotop - 锁

输出结果字段说明：
ns：
包含数据库命名空间，后者结合了数据库名称和集合。
db：
包含数据库的名称。名为 . 的数据库针对全局锁定，而非特定数据库。
total：
mongod花费的时间工作在这个命名空间提供总额。
read：
提供了大量的时间，这mongod花费在执行读操作，在此命名空间。
write：
提供这个命名空间进行写操作，这mongod花了大量的时间。

MongoDB 关系
MongoDB 的关系表示多个文档之间在逻辑上的相互联系。
文档间可以通过嵌入和引用来建立联系。
MongoDB 中的关系可以是：
1:1 (1对1)
1: N (1对多)
N: 1 (多对1)
N: N (多对多)
接下来我们来考虑下用户与用户地址的关系。
一个用户可以有多个地址，所以是一对多的关系。
以下是 user 文档的简单结构：
```js {
"_id":ObjectId("52ffc33cd85242f436000001"),
"name": "Tom Hanks",
"contact": "987654321",
"dob": "01-01-1991"
}```
以下是 address 文档的简单结构：
```js {
"_id":ObjectId("52ffc4a5d85242602e000000"),
"building": "22 A, Indiana Apt",
"pincode": 123456,
"city": "Los Angeles",
"state": "California"
}```
嵌入式关系
使用嵌入式方法，我们可以把用户地址嵌入到用户的文档中：
```js "_id":ObjectId("52ffc33cd85242f436000001"),
"contact": "987654321",
"dob": "01-01-1991",
"name": "Tom Benzamin",
"address": [
{
"building": "22 A, Indiana Apt",
"pincode": 123456,
"city": "Los Angeles",
"state": "California"
},
{
"building": "170 A, Acropolis Apt",
"pincode": 456789,
"city": "Chicago",
"state": "Illinois"
}]
}```
以上数据保存在单一的文档中，可以比较容易的获取很维护数据。 你可以这样查询用户的地址：
```js >db.users.findOne({"name":"Tom Benzamin"},{"address":1})```
注意：以上查询中 db 和 users 表示数据库和集合。
这种数据结构的缺点是，如果用户和用户地址在不断增加，数据量不断变大，会影响读写性能。

引用式关系
引用式关系是设计数据库时经常用到的方法，这种方法把用户数据文档和用户地址数据文档分开，通过引用文档的 id 字段来建立关系。
{
"_id":ObjectId("52ffc33cd85242f436000001"),
"contact": "987654321",
"dob": "01-01-1991",
"name": "Tom Benzamin",
"address_ids": [
ObjectId("52ffc4a5d85242602e000000"),
ObjectId("52ffc4a5d85242602e000001")
]
}
以上实例中，用户文档的 address_ids 字段包含用户地址的对象id（ObjectId）数组。
我们可以读取这些用户地址的对象id（ObjectId）来获取用户的详细地址信息。
这种方法需要两次查询，第一次查询用户地址的对象id（ObjectId），第二次通过查询的id获取用户的详细地址信息。
>var result = db.users.findOne({"name":"Tom Benzamin"},{"address_ids":1})
>var addresses = db.address.find({"_id":{"$in":result["address_ids"]}})

MongoDB 数据库引用
在上一章节MongoDB关系中我们提到了MongoDB的引用来规范数据结构文档。
MongoDB 引用有两种：
手动引用（Manual References）
DBRefs
DBRefs vs 手动引用
考虑这样的一个场景，我们在不同的集合中 (address_home, address_office, address_mailing, 等)存储不同的地址（住址，办公室地址，邮件地址等）。
这样，我们在调用不同地址时，也需要指定集合，一个文档从多个集合引用文档，我们应该使用 DBRefs。
使用 DBRefs
DBRef的形式：
```js { $ref : , $id : , $db : }```
三个字段表示的意义为：
$ref：集合名称
$id：引用的id
$db:数据库名称，可选参数
以下实例中用户数据文档使用了 DBRef, 字段 address：
```js {
"_id":ObjectId("53402597d852426020000002"),
"address": {
"$ref": "address_home",
"$id": ObjectId("534009e4d852427820000002"),
"$db": "w3cschoolcc"},
"contact": "987654321",
"dob": "01-01-1991",
"name": "Tom Benzamin"
}```
address DBRef 字段指定了引用的地址文档是在 address_home 集合下的 w3cschoolcc 数据库，id 为 534009e4d852427820000002。
以下代码中，我们通过指定 $ref 参数（address_home 集合）来查找集合中指定id的用户地址信息：
>var user = db.users.findOne({"name":"Tom Benzamin"})
>var dbRef = user.address
>db[dbRef.$ref].findOne({"_id":(dbRef.$id)})
以上实例返回了 address_home 集合中的地址数据：
```js {
"_id" : ObjectId("534009e4d852427820000002"),
"building" : "22 A, Indiana Apt",
"pincode" : 123456,
"city" : "Los Angeles",
"state" : "California"
}```
MongoDB 覆盖索引查询
官方的MongoDB的文档中说明，覆盖查询是以下的查询：
所有的查询字段是索引的一部分
所有的查询返回字段在同一个索引中
由于所有出现在查询中的字段是索引的一部分， MongoDB 无需在整个数据文档中检索匹配查询条件和返回使用相同索引的查询结果。
因为索引存在于RAM中，从索引中获取数据比通过扫描文档读取数据要快得多。
使用覆盖索引查询
为了测试盖索引查询，使用以下 users 集合:
```js {
"_id": ObjectId("53402597d852426020000002"),
"contact": "987654321",
"dob": "01-01-1991",
"gender": "M",
"name": "Tom Benzamin",
"user_name": "tombenzamin"
}```
我们在 users 集合中创建联合索引，字段为 gender 和 user_name :
>db.users.ensureIndex({gender:1,user_name:1})
现在，该索引会覆盖以下查询：
```js >db.users.find({gender:"M"},{user_name:1,_id:0})```
也就是说，对于上述查询，MongoDB的不会去数据库文件中查找。相反，它会从索引中提取数据，这是非常快速的数据查询。
由于我们的索引中不包括 _id 字段，_id在查询中会默认返回，我们可以在MongoDB的查询结果集中排除它。
下面的实例没有排除_id，查询就不会被覆盖：
```js >db.users.find({gender:"M"},{user_name:1})```
最后，如果是以下的查询，不能使用覆盖索引查询：
所有索引字段是一个数组
所有索引字段是一个子文档

MongoDB 查询分析
MongoDB 查询分析可以确保我们建议的索引是否有效，是查询语句性能分析的重要工具。
MongoDB 查询分析常用函数有：explain() 和 hint()。
使用 explain()
explain 操作提供了查询信息，使用索引及查询统计等。有利于我们对索引的优化。
接下来我们在 users 集合中创建 gender 和 user_name 的索引：
```js >db.users.ensureIndex({gender:1,user_name:1})```
现在在查询语句中使用 explain ：
```js >db.users.find({gender:"M"},{user_name:1,_id:0}).explain()```
以上的 explain() 查询返回如下结果：
```js {
"cursor" : "BtreeCursor gender_1_user_name_1",
"isMultiKey" : false,
"n" : 1,
"nscannedObjects" : 0,
"nscanned" : 1,
"nscannedObjectsAllPlans" : 0,
"nscannedAllPlans" : 1,
"scanAndOrder" : false,
"indexOnly" : true,
"nYields" : 0,
"nChunkSkips" : 0,
"millis" : 0,
"indexBounds" : {
"gender" : [
[
"M",
"M"
]
],
"user_name" : [
[
{
"$minElement" : 1
},
{
"$maxElement" : 1
}
]
]
}
}```
现在，我们看看这个结果集的字段：
indexOnly: 字段为 true ，表示我们使用了索引。
cursor：因为这个查询使用了索引，MongoDB中索引存储在B树结构中，所以这是也使用了BtreeCursor类型的游标。如果没有使用索引，游标的类型是BasicCursor。这个键还会给出你所使用的索引的名称，你通过这个名称可以查看当前数据库下的system.indexes集合（系统自动创建，由于存储索引信息，这个稍微会提到）来得到索引的详细信息。
n：当前查询返回的文档数量。
nscanned/nscannedObjects：表明当前这次查询一共扫描了集合中多少个文档，我们的目的是，让这个数值和返回文档的数量越接近越好。
millis：当前查询所需时间，毫秒数。
indexBounds：当前查询具体使用的索引。
使用 hint()
虽然MongoDB查询优化器一般工作的很不错，但是也可以使用hints来强迫MongoDB使用一个指定的索引。
这种方法某些情形下会提升性能。 一个有索引的collection并且执行一个多字段的查询(一些字段已经索引了)。
如下查询实例指定了使用 gender 和 user_name 索引字段来查询：
```js >db.users.find({gender:"M"},{user_name:1,_id:0}).hint({gender:1,user_name:1})```
可以使用 explain() 函数来分析以上查询：
```js >db.users.find({gender:"M"},{user_name:1,_id:0}).hint({gender:1,user_name:1}).explain()```
MongoDB 原子操作
mongodb不支持事务，所以，在你的项目中应用时，要注意这点。无论什么设计，都不要要求mongodb保证数据的完整性。
但是mongodb提供了许多原子操作，比如文档的保存，修改，删除等，都是原子操作。
所谓原子操作就是要么这个文档保存到Mongodb，要么没有保存到Mongodb，不会出现查询到的文档没有保存完整的情况。
原子操作数据模型
考虑下面的例子，图书馆的书籍及结账信息。
实例说明了在一个相同的文档中如何确保嵌入字段关联原子操作（update：更新）的字段是同步的。
```js book = {
_id: 123456789,
title: "MongoDB: The Definitive Guide",
author: [ "Kristina Chodorow", "Mike Dirolf" ],
published_date: ISODate("2010-09-24"),
pages: 216,
language: "English",
publisher_id: "oreilly",
available: 3,
checkout: [ { by: "joe", date: ISODate("2012-10-15") } ]
}```
你可以使用 db.collection.findAndModify() 方法来判断书籍是否可结算并更新新的结算信息。
在同一个文档中嵌入的 available 和 checkout 字段来确保这些字段是同步更新的:
```js db.books.findAndModify ( {
query: {
_id: 123456789,
available: { $gt: 0 }
},
update: {
$inc: { available: -1 },
$push: { checkout: { by: "abc", date: new Date() } }
}
} )```
原子操作常用命令
```js $set```
用来指定一个键并更新键值，若键不存在并创建。
{ $set : { field : value } }
$unset
用来删除一个键。
```js { $unset : { field : 1} }```
$inc
$inc可以对文档的某个值为数字型（只能为满足要求的数字）的键进行增减的操作。
```js { $inc : { field : value } }```
$push
用法：
```js { $push : { field : value } }```
把value追加到field里面去，field一定要是数组类型才行，如果field不存在，会新增一个数组类型加进去。
$pushAll
同$push,只是一次可以追加多个值到一个数组字段内。
```js { $pushAll : { field : value_array } }```
$pull
从数组field内删除一个等于value值。
```js { $pull : { field : _value } }```
$addToSet
增加一个值到数组内，而且只有当这个值不在数组内才增加。
$pop
删除数组的第一个或最后一个元素
```js { $pop : { field : 1 } }```
$rename
修改字段名称
```js { $rename : { old_field_name : new_field_name } }```
$bit
位操作，integer类型
```js {$bit : { field : {and : 5}}}```
偏移操作符
```js > t.find() { "_id" : ObjectId("4b97e62bf1d8c7152c9ccb74"), "title" : "ABC", "comments" : [ { "by" : "joe", "votes" : 3 }, { "by" : "jane", "votes" : 7 } ] }

> t.update( {'comments.by':'joe'}, {$inc:{'comments.$.votes':1}}, false, true )

> t.find() { "_id" : ObjectId("4b97e62bf1d8c7152c9ccb74"), "title" : "ABC", "comments" : [ { "by" : "joe", "votes" : 4 }, { "by" : "jane", "votes" : 7 } ] }```
MongoDB 高级索引
考虑以下文档集合（users ）:
```js {
"address": {
"city": "Los Angeles",
"state": "California",
"pincode": "123"
},
"tags": [
"music",
"cricket",
"blogs"
],
"name": "Tom Benzamin"
}```
以上文档包含了 address 子文档和 tags 数组。
索引数组字段
假设我们基于标签来检索用户，为此我们需要对集合中的数组 tags 建立索引。
在数组中创建索引，需要对数组中的每个字段依次建立索引。所以在我们为数组 tags 创建索引时，会为 music、cricket、blogs三个值建立单独的索引。
使用以下命令创建数组索引：
```js >db.users.ensureIndex({"tags":1})```
创建索引后，我们可以这样检索集合的 tags 字段：
```js >db.users.find({tags:"cricket"})```
为了验证我们使用使用了索引，可以使用 explain 命令：
```js >db.users.find({tags:"cricket"}).explain()```
以上命令执行结果中会显示 "cursor" : "BtreeCursor tags_1" ，则表示已经使用了索引。
索引子文档字段
假设我们需要通过city、state、pincode字段来检索文档，由于这些字段是子文档的字段，所以我们需要对子文档建立索引。
为子文档的三个字段创建索引，命令如下：
```js >db.users.ensureIndex({"address.city":1,"address.state":1,"address.pincode":1})```
一旦创建索引，我们可以使用子文档的字段来检索数据：
```js >db.users.find({"address.city":"Los Angeles"})```
记住查询表达式必须遵循指定的索引的顺序。所以上面创建的索引将支持以下查询：
```js >db.users.find({"address.city":"Los Angeles","address.state":"California"})```
同样支持以下查询：
```js >db.users.find({"address.city":"LosAngeles","address.state":"California","address.pincode":"123"})```
MongoDB 索引限制
额外开销
每个索引占据一定的存储空间，在进行插入，更新和删除操作时也需要对索引进行操作。所以，如果你很少对集合进行读取操作，建议不使用索引。
内存(RAM)使用
由于索引是存储在内存(RAM)中,你应该确保该索引的大小不超过内存的限制。
如果索引的大小大于内存的限制，MongoDB会删除一些索引，这将导致性能下降。
查询限制
索引不能被以下的查询使用：
正则表达式及非操作符，如 $nin, $not, 等。
算术运算符，如 $mod, 等。
$where 子句
所以，检测你的语句是否使用索引是一个好的习惯，可以用explain来查看。
索引键限制
从2.6版本开始，如果现有的索引字段的值超过索引键的限制，MongoDB中不会创建索引。
插入文档超过索引键限制
如果文档的索引字段值超过了索引键的限制，MongoDB不会将任何文档转换成索引的集合。与mongorestore和mongoimport工具类似。
最大范围
集合中索引不能超过64个
索引名的长度不能超过125个字符
一个复合索引最多可以有31个字段

MongoDB ObjectId
在前面几个章节中我们已经使用了MongoDB 的对象 Id(ObjectId)。
在本章节中，我们将了解的ObjectId的结构。
ObjectId 是一个12字节 BSON 类型数据，有以下格式：
前4个字节表示时间戳
接下来的3个字节是机器标识码
紧接的两个字节由进程id组成（PID）
最后三个字节是随机数。
MongoDB中存储的文档必须有一个"_id"键。这个键的值可以是任何类型的，默认是个ObjectId对象。
在一个集合里面，每个集合都有唯一的"_id"值，来确保集合里面每个文档都能被唯一标识。
MongoDB采用ObjectId，而不是其他比较常规的做法（比如自动增加的主键）的主要原因，因为在多个 服务器上同步自动增加主键值既费力还费时。
创建信的ObjectId
使用以下代码生成新的ObjectId：
```js >newObjectId = ObjectId()```
上面的语句返回以下唯一生成的id：
```js ObjectId("5349b4ddd2781d08c09890f3")```
你也可以使用生成的id来取代MongoDB自动生成的ObjectId：
```js >myObjectId = ObjectId("5349b4ddd2781d08c09890f4")```
创建文档的时间戳
由于 ObjectId 中存储了 4 个字节的时间戳，所以你不需要为你的文档保存时间戳字段，你可以通过 getTimestamp 函数来获取文档的创建时间:
```js >ObjectId("5349b4ddd2781d08c09890f4").getTimestamp()```
以上代码将返回 ISO 格式的文档创建时间：
```js ISODate("2014-04-12T21:49:17Z")```
ObjectId 转换为字符串
在某些情况下，您可能需要将ObjectId转换为字符串格式。你可以使用下面的代码：
```js >new ObjectId.str```
以上代码将返回Guid格式的字符串：：
```js 5349b4ddd2781d08c09890f3```
MongoDB Map Reduce
Map-Reduce是一种计算模型，简单的说就是将大批量的工作（数据）分解（MAP）执行，然后再将结果合并成最终结果（REDUCE）。
MongoDB提供的Map-Reduce非常灵活，对于大规模数据分析也相当实用。
MapReduce 命令
以下是MapReduce的基本语法：
```js >db.collection.mapReduce(
function() {emit(key,value);}, //map 函数
function(key,values) {return reduceFunction}, //reduce 函数
{
out: collection,
query: document,
sort: document,
limit: number
}
)```
使用 MapReduce 要实现两个函数 Map 函数和 Reduce 函数,Map 函数调用 emit(key, value), 遍历 collection 中所有的记录, 将key 与 value 传递给 Reduce 函数进行处理。
Map 函数必须调用 emit(key, value) 返回键值对。
参数说明:
map ：映射函数 (生成键值对序列,作为 reduce 函数参数)。
reduce 统计函数，reduce函数的任务就是将key-values变成key-value，也就是把values数组变成一个单一的值value。。
out 统计结果存放集合 (不指定则使用临时集合,在客户端断开后自动删除)。
query 一个筛选条件，只有满足条件的文档才会调用map函数。（query。limit，sort可以随意组合）
sort 和limit结合的sort排序参数（也是在发往map函数前给文档排序），可以优化分组机制
limit 发往map函数的文档数量的上限（要是没有limit，单独使用sort的用处不大）
使用 MapReduce
考虑以下文档结构存储用户的文章，文档存储了用户的 user_name 和文章的 status字段：
```js {
"post_text": "w3cschool.cc 菜鸟教程，最全的技术文档。",
"user_name": "mark",
"status":"active"
}```
现在，我们将在 posts 集合中使用 mapReduce 函数来选取已发布的文章，并通过user_name分组，计算每个用户的文章数：
```js >db.posts.mapReduce(
function() { emit(this.user_id,1); },
function(key, values) {return Array.sum(values)},
{
query:{status:"active"},
out:"post_total"
}
)```
以上 mapReduce 输出结果为：
```js {
"result" : "post_total",
"timeMillis" : 9,
"counts" : {
"input" : 4,
"emit" : 4,
"reduce" : 2,
"output" : 2
},
"ok" : 1,
}```
结果表明，共有4个符合查询条件（status:"active"）的文档， 在map函数中生成了4个键值对文档，最后使用reduce函数将相同的键值分为两组。
具体参数说明：
result：储存结果的collection的名字,这是个临时集合，MapReduce的连接关闭后自动就被删除了。
timeMillis：执行花费的时间，毫秒为单位
input：满足条件被发送到map函数的文档个数
emit：在map函数中emit被调用的次数，也就是所有集合中的数据总量
ouput：结果集合中的文档个数（count对调试非常有帮助）
ok：是否成功，成功为1
err：如果失败，这里可以有失败原因，不过从经验上来看，原因比较模糊，作用不大
使用 find 操作符来查看 mapReduce 的查询结果：
```js >db.posts.mapReduce(
function() { emit(this.user_id,1); },
function(key, values) {return Array.sum(values)},
{
query:{status:"active"},
out:"post_total"
}
).find()```
以上查询显示如下结果，两个用户 tom 和 mark 有两个发布的文章:
```js { "_id" : "tom", "value" : 2 }
{ "_id" : "mark", "value" : 2 }```
用类似的方式，MapReduce可以被用来构建大型复杂的聚合查询。
Map函数和Reduce函数可以使用 JavaScript 来实现，是的MapReduce的使用非常灵活和强大。

MongoDB 全文检索
全文检索对每一个词建立一个索引，指明该词在文章中出现的次数和位置，当用户查询时，检索程序就根据事先建立的索引进行查找，并将查找的结果反馈给用户的检索方式。
这个过程类似于通过字典中的检索字表查字的过程。
MongoDB 从 2.4 版本开始支持全文检索，目前支持15种语言(暂时不支持中文)的全文索引。

启用全文检索
MongoDB 在 2.6 版本以后是默认开启全文检索的，如果你使用之前的版本，你需要使用以下代码来启用全文检索:
```js >db.adminCommand({setParameter:true,textSearchEnabled:true})```
或者使用命令：
```js mongod --setParameter textSearchEnabled=true```
创建全文索引
考虑以下 posts 集合的文档数据，包含了文章内容（post_text）及标签(tags)：
```js {
"post_text": "enjoy the mongodb articles on w3cschool.cc",
"tags": [
"mongodb",
"w3cschool"
]
}```
我们可以对 post_text 字段建立全文索引，这样我们可以搜索文章内的内容：
```js >db.posts.ensureIndex({post_text:"text"})```
使用全文索引
现在我们已经对 post_text 建立了全文索引，我们可以搜索文章中的关键词w3cschool.cc：
```js >db.posts.find({$text:{$search:"w3cschool.cc"}})```
以下命令返回了如下包含w3cschool.cc关键词的文档数据：
```js {
"_id" : ObjectId("53493d14d852429c10000002"),
"post_text" : "enjoy the mongodb articles on w3cschool.cc",
"tags" : [ "mongodb", "w3cschool" ]
}
{
"_id" : ObjectId("53493d1fd852429c10000003"),
"post_text" : "writing tutorials on w3cschool.cc",
"tags" : [ "mongodb", "tutorial" ]
}```
如果你使用的是旧版本的MongoDB，你可以使用以下命令：
```js >db.posts.runCommand("text",{search:" w3cschool.cc"})```
使用全文索引可以提高搜索效率。
删除全文索引
删除已存在的全文索引，可以使用 find 命令查找索引名：
```js >db.posts.getIndexes()```
通过以上命令获取索引名，本例的索引名为post_text_text，执行以下命令来删除索引：
```js >db.posts.dropIndex("post_text_text")```
MongoDB 正则表达式
正则表达式是使用单个字符串来描述、匹配一系列符合某个句法规则的字符串。
许多程序设计语言都支持利用正则表达式进行字符串操作。
MongoDB 使用 $regex 操作符来设置匹配字符串的正则表达式。
MongoDB使用PCRE (Perl Compatible Regular Expression) 作为正则表达式语言。
不同于全文检索，我们使用正则表达式不需要做任何配置。
考虑以下 posts 集合的文档结构，该文档包含了文章内容和标签：
```js {
"post_text": "enjoy the mongodb articles on tutorialspoint",
"tags": [
"mongodb",
"tutorialspoint"
]
}```
使用正则表达式
以下命令使用正则表达式查找包含 w3cschool.cc 字符串的文章：
```js >db.posts.find({post_text:{$regex:"w3cschool.cc"}})```
以上查询也可以写为：
```js >db.posts.find({post_text:/w3cschool.cc/})```
不区分大小写的正则表达式
如果检索需要不区分大小写，我们可以设置 $options 为 $i。
以下命令将查找不区分大小写的字符串 w3cschool.cc：
```js >db.posts.find({post_text:{$regex:"w3cschool.cc",$options:"$i"}})```
集合中会返回所有包含字符串 w3cschool.cc 的数据，且不区分大小写：
```js {
"_id" : ObjectId("53493d37d852429c10000004"),
"post_text" : "hey! this is my post on W3Cschool.cc",
"tags" : [ "tutorialspoint" ]
}```
数组元素使用正则表达式
我们还可以在数组字段中使用正则表达式来查找内容。 这在标签的实现上非常有用，如果你需要查找包含以 tutorial 开头的标签数据(tutorial 或 tutorials 或 tutorialpoint 或 tutorialphp)， 你可以使用以下代码：
```js >db.posts.find({tags:{$regex:"tutorial"}})```
优化正则表达式查询
如果你的文档中字段设置了索引，那么使用索引相比于正则表达式匹配查找所有的数据查询速度更快。
如果正则表达式是前缀表达式，所有匹配的数据将以指定的前缀字符串为开始。例如： 如果正则表达式为 ^tut ，查询语句将查找以 tut 为开头的字符串。
这里面使用正则表达式有两点需要注意：
正则表达式中使用变量。一定要使用eval将组合的字符串进行转换，不能直接将字符串拼接后传入给表达式。否则没有报错信息，只是结果为空！实例如下：
```js var name=eval("/" + 变量值key +"/i");```
以下是模糊查询包含title关键词, 且不区分大小写:
```js title:eval("/"+title+"/i") // 等同于 title:{$regex:title,$Option:"$i"}```
MongoDB GridFS
GridFS 用于存储和恢复那些超过16M（BSON文件限制）的文件(如：图片、音频、视频等)。
GridFS 也是文件存储的一种方式，但是它是存储在MonoDB的集合中。
GridFS 可以更好的存储大于16M的文件。
GridFS 会将大文件对象分割成多个小的chunk(文件片段),一般为256k/个,每个chunk将作为MongoDB的一个文档(document)被存储在chunks集合中。
GridFS 用两个集合来存储一个文件：fs.files与fs.chunks。
每个文件的实际内容被存在chunks(二进制数据)中,和文件有关的meta数据(filename,content_type,还有用户自定义的属性)将会被存在files集合中。
以下是简单的 fs.files 集合文档：
```js {
"filename": "test.txt",
"chunkSize": NumberInt(261120),
"uploadDate": ISODate("2014-04-13T11:32:33.557Z"),
"md5": "7b762939321e146569b07f72c62cca4f",
"length": NumberInt(646)
}```
以下是简单的 fs.chunks 集合文档：
{
"files_id": ObjectId("534a75d19f54bfec8a2fe44b"),
"n": NumberInt(0),
"data": "Mongo Binary Data"
}
GridFS 添加文件
现在我们使用 GridFS 的 put 命令来存储 mp3 文件。 调用 MongoDB 安装目录下bin的 mongofiles.exe工具。
打开命令提示符，进入到MongoDB的安装目录的bin目录中，找到mongofiles.exe，并输入下面的代码：
```js >mongofiles.exe -d gridfs put song.mp3```
GridFS 是存储文件的数据名称。如果不存在该数据库，MongoDB会自动创建。Song.mp3 是音频文件名。
使用以下命令来查看数据库中文件的文档：
>db.fs.files.find()
以上命令执行后返回以下文档数据：
```js {
_id: ObjectId('534a811bf8b4aa4d33fdf94d'),
filename: "song.mp3",
chunkSize: 261120,
uploadDate: new Date(1397391643474), md5: "e4f53379c909f7bed2e9d631e15c1c41",
length: 10401959
}```
我们可以看到 fs.chunks 集合中所有的区块，以下我们得到了文件的 _id 值，我们可以根据这个 _id 获取区块(chunk)的数据：
```js >db.fs.chunks.find({files_id:ObjectId('534a811bf8b4aa4d33fdf94d')})```
以上实例中，查询返回了 40 个文档的数据，意味着mp3文件被存储在40个区块中。

MongoDB 固定集合（Capped Collections）
MongoDB 固定集合（Capped Collections）是性能出色且有着固定大小的集合，对于大小固定，我们可以想象其就像一个环形队列，当集合空间用完后，再插入的元素就会覆盖最初始的头部的元素！
创建固定集合
我们通过createCollection来创建一个固定集合，且capped选项设置为true：
```js >db.createCollection("cappedLogCollection",{capped:true,size:10000})```
还可以指定文档个数,加上max:1000属性：
```js >db.createCollection("cappedLogCollection",{capped:true,size:10000,max:1000})```
判断集合是否为固定集合:
```js >db.cappedLogCollection.isCapped()```
如果需要将已存在的集合转换为固定集合可以使用以下命令：
```js >db.runCommand({"convertToCapped":"posts",size:10000})```
以上代码将我们已存在的 posts 集合转换为固定集合。
固定集合查询
固定集合文档按照插入顺序储存的,默认情况下查询就是按照插入顺序返回的,也可以使用$natural调整返回顺序。
```js >db.cappedLogCollection.find().sort({$natural:-1})```
固定集合的功能特点
可以插入及更新,但更新不能超出collection的大小,否则更新失败,不允许删除,但是可以调用drop()删除集合中的所有行,但是drop后需要显式地重建集合。
在32位机子上一个cappped collection的最大值约为482.5M,64位上只受系统文件大小的限制。
固定集合属性及用法
属性
属性1:对固定集合进行插入速度极快
属性2:按照插入顺序的查询输出速度极快
属性3:能够在插入最新数据时,淘汰最早的数据
用法
用法1:储存日志信息
用法2:缓存一些少量的文档

MongoDB 自动增长
MongoDB 没有像 SQL 一样有自动增长的功能， MongoDB 的 _id 是系统自动生成的12字节唯一标识。
但在某些情况下，我们可能需要实现 ObjectId 自动增长功能。
由于 MongoDB 没有实现这个功能，我们可以通过编程的方式来实现，以下我们将在 counters 集合中实现_id字段自动增长。
使用 counters 集合
考虑以下 products 文档。我们希望 _id 字段实现 从 1,2,3,4 到 n 的自动增长功能。
```js {
"_id":1,
"product_name": "Apple iPhone",
"category": "mobiles"
}```
为此，创建 counters 集合，序列字段值可以实现自动长：
>db.createCollection("counters")
现在我们向 counters 集合中插入以下文档，使用 productid 作为 key:
```js {
"_id":"productid",
"sequence_value": 0
}```
sequence_value 字段是序列通过自动增长后的一个值。
使用以下命令插入 counters 集合的序列文档中：
```js >db.counters.insert({_id:"productid",sequence_value:0})```
创建 Javascript 函数
现在，我们创建函数 getNextSequenceValue 来作为序列名的输入， 指定的序列会自动增长 1 并返回最新序列值。在本文的实例中序列名为 productid 。
```js >function getNextSequenceValue(sequenceName){
var sequenceDocument = db.counters.findAndModify(
{
query:{_id: sequenceName },
update: {$inc:{sequence_value:1}},
new:true
});
return sequenceDocument.sequence_value;
}```
使用 Javascript 函数
接下来我们将使用 getNextSequenceValue 函数创建一个新的文档， 并设置文档 _id 自动为返回的序列值：
```js >db.products.insert({
"_id":getNextSequenceValue("productid"),
"product_name":"Apple iPhone",
"category":"mobiles"})

>db.products.insert({
"_id":getNextSequenceValue("productid"),
"product_name":"Samsung S3",
"category":"mobiles"})```
就如你所看到的，我们使用 getNextSequenceValue 函数来设置 _id 字段。
为了验证函数是否有效，我们可以使用以下命令读取文档：
```js >db.prodcuts.find()```
以上命令将返回以下结果，我们发现 _id 字段是自增长的：
```js { "_id" : 1, "product_name" : "Apple iPhone", "category" : "mobiles"}

{ "_id" : 2, "product_name" : "Samsung S3", "category" : "mobiles" }```
停止服务：
```js kill -9 PID```
正常停止：
```js kill -2 PID```
或者
```js use admin
db.shutdownServer()```
注意：如果再次启动的时候报错，则删除lock文件

&nbsp;
<h1 id="数据库管理">数据库管理</h1>
<strong>新建数据库</strong>

MongoDB的shell没有提供新建数据库的功能，不过你可以这样：
<pre><code>use accounts
db.createCollection('accounts')
</code></pre>
当你使用“use accounts”切换到名为accounts的数据库时，实际上什么也没发生，只有当你调用了db.createCollection之后，新的数据库才被保存，然后你使用“show dbs”就可以看到新建的库。

<strong>删除数据库</strong>

删除数据库需要切换到指定的库，然后调用dropDatabase()。如下：
<pre><code>use accounts
db.dropDatabase()
</code></pre>
调用dropDatabase之后，可以使用“show dbs”查看。

<strong>创建集合</strong>

之前新建数据库时已用到，调用createCollection即可。

<strong>显示集合</strong>

这样：
<pre><code>use accounts
show collections
</code></pre>
<strong>获取指定名字的集合</strong>

要得到集合对象，可以这样：
<pre><code>use accounts
coll = db.getCollection("accounts")
</code></pre>
<strong>删除集合</strong>

要删除集合，需要调用集合对象的drop()方法。这样：
<pre><code>use accounts
coll = db.getCollection("accounts")
coll.drop();
</code></pre>
<strong>向集合中添加文档</strong>

要把文档添加到集合，需要先得到collection对象，然后调用insert(document)方法。document参数是一个JSON对象。下面的命令往accounts集合里添加了两个用户：
<pre><code>use accounts
coll = db.getCollection("accounts")
coll.insert({name:"ZhangSan",password:"123456"})
coll.insert({name:"WangEr",password:"nicai"})
</code></pre>
<strong>在集合中查找</strong>

使用集合对象的find()方法，可以列出集合里的所有文档。这样：
<pre><code>use accounts
coll = db.getCollection("accounts")
coll.find()
</code></pre>
带参数的find()方法可以根据某个字段来查找：
<pre><code>coll.find({name:"ZhangSan"})
</code></pre>
<strong>从集合中删除文档</strong>

使用collection对象的remove(object)方法可以删除文档。它的参数是JS对象，它通过将你传入对象的属性与数据库内数据比对来匹配某一个文档，匹配到后删除，匹配不上就拉倒。假如你传递一个空的JS对象，就会删除这个集合里所有的文档。比如下面这样：
<pre><code>use accounts
coll = db.getCollection("accounts")
coll.insert({name:"QianQi",password:"888888"})
coll.find()
coll.remove({name:"WangEr"})
coll.find()
coll.remove({})
coll.find()
</code></pre>
<strong>更新集合中的文档</strong>

collection对象提供了两种方法来更新文档：save(object)和update(query, update, options)。

save可以直接更新一个对象，下面的代码将ZhangSan的密码修改为567890：
<pre><code>coll.save({_id:ObjectId("55cc25b360bcee730bafd2bf"),name:"ZhangSan",password:"567890"})
</code></pre>
下面的update方法与上面的save效果一样：
<pre><code>coll.update({name:"ZhangSan"},{name:"ZhangSan",password:"567890"})
</code></pre>
update()的第二个参数update是一个对象，能指定更新时用的运算符，比如$set可以设置字段的值，下面代码与前面等效：
<pre><code>coll.update({name:"ZhangSan"},{$set: {password:"567890"}});</code></pre>