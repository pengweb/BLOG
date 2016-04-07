---
title: Angularjs--学习笔记
date: 2016-04-07 15:40:33
tags: [js,笔记,note,javascript,angular,angularjs]

---

一、Angularjs基础总结

module == config == filter == directive == factory/service/provider/value == controller
||
routes

基本命令
ng-directives     扩展HTML
ng-app             定义一个应用程序         （定义一个应用程序）
ng-model           把元素值绑定到应用程序   （数据–程序）
ng-bind            把应用程序绑定到HTML视图（程序–视图）
ng-repeat          类似于遍历一遍写成 ng-repeat=”x in name”

ng-init         可以赋值为数字、数组、对象，而且可以为多个变量赋初始值

ng-init=“name=’Hello World'”

ng-init=“quantity=1;price=5”

ng-init=“names=\[‘Tom’,’Jerry’,’Gaffey’]”

\{ \{ \} \}可以把数据绑定到HTML，类似Javascript代码片段，可以包含文字、运算符和变量，通常在绑定数据中用到，表达式可以绑定数字、字符串、对象、数组，写在双大括号内

ng-if

ng-show =”true”（用ng-if替代，提升性能）

ng-if要比ng-show快很多，在于ng-show指令虽然隐藏了但还是会执行其中的所有绑定，而ng-if就不同了，它只会在等于true的时候也就是显示的时候才去执行其中的绑定
```html
<div ng-app=””>                                          
<p>在输入框中尝试输入：</p>
<p>姓名：<input type=”text” ng-model=”name”></p>
<p ng-bind=”name”></p>
</div>
<script>
function personController($scope){
$scope.person={
firstName:”DOJ”,
lastName:”Lil”,
};
$scope.fullName=function(){
return $scope.person.firstName + $scope.person.lastName;
}
}
</script>
```
$scope是一个原形函数
$scope.$watch()      监听
$scope.$apply()      替换成*函数
$是树形结构，与DOM平行
子$scope会继承$scope的属性和方法
每个应用只有一个$scope
$scope可以向上向下传播事件，类似Dom
通过angular.element($0).scope()进行调试

$emit只能向parent controller传递event与data        (HTML的同级及上级)
$broadcast只能向child controller传递event与data    (HTML的同级及下级)
$on用于接收event与data

5个过程–创建-监控-检测模型变化-观察模型是不是脏啊-自动销毁或者手动销毁不用的模  型

路由原理：①哈希#  ②HTML5的History的新API

指令：templateUrl
加载阶段（找ng-app）-编译阶段（遍历DOM，找到所有指令）-链接阶段

二、表单
```html
<div ng-app=”” ng-controller=”formController”>
<form novalidate>                          <!–novalidate 来验证表单用的–>
First Name:<br>
<input type=”text” ng-model=”user.firstName”><br>
Last Name:<br>
<input type=”text” ng-model=”user.lastName”>
<br><br>
<button ng-click=”reset()”>RESET</button>
</form>
<p>form = {{user }}</p>
<p>master = {{master}}</p>
</div>
<script>
function formController ($scope) {          //1.3已经不再支持全局控制，需要用module，这里暂时没有改
$scope.master = {firstName:”John”, lastName:”Doe”};
$scope.reset = function() {
$scope.user = angular.copy($scope.master);
};
$scope.reset();
}
</script>
```
三、表单验证

$valid         ng-valid         Boolean 告诉我们这一项当前基于你设定的规则是否验证通过
$invalid     ng-invalid         Boolean 告诉我们这一项当前基于你设定的规则是否验证未通过
$pristine     ng-pristine     Boolean 如果表单或者输入框没有使用则为True
$dirty         ng-dirty         Boolean 如果表单或者输入框有使用到则为True
```html
<form ng-app=”” ng-controller=”validateCtrl”
name=”myForm” novalidate>
<p>Username:<br>
<input type=”text” name=”user” ng-model=”user” required>
<span style=”color:red” ng-show=”myForm.user.$dirty && myForm.user.$invalid“>
<span ng-show=”myForm.user.$error.required”>Username is required.</span>
</span>
</p>
<p>Email:<br>
<input type=”email” name=”email” ng-model=”email” required>
<span style=”color:red” ng-show=”myForm.email.$dirty && myForm.email.$invalid“>
<span ng-show=”myForm.email.$error.required”>Email is required.</span>
<span ng-show=”myForm.email.$error.email”>Invalid email address.</span>
</span>
</p>
<p>
<input type=”submit”
ng-disabled=”myForm.user.$dirty && myForm.user.$invalid ||
myForm.email.$dirty && myForm.email.$invalid”>
</p>
</form>
<script src=”http://apps.bdimg.com/libs/angular.js/1.2.15/angular.min.js”></script>
<script>
function validateCtrl($scope) {
$scope.user = ‘John Doe’;
$scope.email = ‘john.doe@gmail.com’;
}
</script>
```
四、遍历
```html
<li ng-repeat=”a in list”
ng-if=”!$last”>
<h4 >{{$index+1+a.address}}</h4>
//$index是给加一个序列号+1+是为了让第一个显示的数字为1
//$first是第一项为true。 $last是最后一项为true，通常用来做判断放在其他ng内,一般都是在li标签这种列表里用
</li>
```
过滤：

/{ \{ name | uppercase\} \}

1.过滤器uppercase、lowercase对字符串转换大、小写
```html
<div ng-app=“” ng-init=“friends = [
{name:’tom’, age:16},
{name:’jerry’, age:20},
{name:’garfield’, age:22}]”>
 
输入过滤:<input type=“text” ng-model=“name” >
<ul style=“list–style–type:none“>
<li> 姓名，年龄</li>
<li ng-repeat=“x in friends | filter:name”>
{{ x.name + ‘ , ‘ + x.age }}
</li>
</ul>
</div>
```
上边这个过滤有点筛选的意思，输入t的时候只显示tom

 

五、XMLHttpRequest
```html
<div ng-app=”” ng-controller=”customerController”>
<table>
<tr ng-repeat=”x in names | orderBy:’Country’”>
<!–这个是按国家的字母顺序开始排列从A-Z–>
<td>{{x.Name}}</td>
<td>{{x.Country}}</td>
</tr>
</table>
</div>
<script>
function customerController($scope,$http){
$http.get(“Customers_JSON.php”)
.success(function(response){
$scope.names = response
});
}
</script>
<!–$http的增删改–>
<script>
angular.module(“app”,[])
.config(function($httpProvider){
})
.controller(“MyCtrl”,function($scope,$http){
$scope.id=””;
$scope.name=””;
$scope.adduser=function(){
$http.post(“Customers_JSON.php”,{id:$scope.id,name:$scope.name})
.success(function(resp) {
if (resp.success) {
alert(“添加成功”)
}
})
}
$scope.deluser=function(){
$http.post(“Customers_JSON_del.php”,{id:$scope.id})
.success(function(resp) {
if (resp.success) {
alert(“删除成功”)
}
})
}
})
</script>
<!–还有一些用法可以查看Service与Provider例子内的http文件–>
```
六、DOM事件

6-1、ng-click   点击事件
```html
<div ng-app=”” ng-controller=”myController” >
<button ng-click=”count=count+1″>点我</button>
{{count}}
</div>
<script>
function myController($scope) {
$scope.count = 0;
}
</script>
<!————————————————->
<div ng-app=”” ng-controller=”myController” >
<button ng-click=”alert()”>点我</button>
</div>
<script>
function myController($scope) {
$scope.alert = function(){
alert(“haha”);
}
}
</script>
```
6-2、ng-hide 隐藏元素
```html
<div ng-app=”” ng-controller=”personController”>
<button ng-click=”toggle()”>隐藏/显示</button>
<p ng-hide=”myVar”>
名: <input type=text ng-model=”person.firstName”><br>
姓: <input type=text ng-model=”person.lastName”><br><br>
姓名: {{person.firstName + ” ” + person.lastName}}
</p>
</div>
<script>
function personController($scope) {
$scope.person = {
firstName: “John”,
lastName: “Doe”
};
$scope.myVar = false;
$scope.toggle = function() {
$scope.myVar = !$scope.myVar;
};
}
</script>
```
6-3、ng-show 显示元素
```html
<div ng-app=”” ng-controller=”personController”>
<button ng-click=”toggle()”>隐藏/显示</button>
<p ng-show=”myVar”>
名: <input type=text ng-model=”person.firstName”><br>
姓: <input type=text ng-model=”person.lastName”><br><br>
姓名: {{person.firstName + ” ” + person.lastName}}
</p>
</div>
<script>
function personController($scope) {
$scope.person = {
firstName: “John”,
lastName: “Doe”
};
$scope.myVar = true;
$scope.toggle = function() {
$scope.myVar = !$scope.myVar;
};
}
</script>
```
七、element用法
```html
<div ng-app=”app” >
<span enter leave>加载</span>                       <!–A的写法–>
<hello></hello>
</div>
<script>
var app = angular.module(“app”,[]);
app.directive(‘enter’,function(){
return {
restrict:’A’,
link:function(scope,element,attrs){
console.log(scope);           //这里可以通过console.log查询element，scope，attrs等的属性
element.bind(“mouseenter”,function(){
element.css(“font-size”,”25px”)
})
}
}
})
app.directive(‘leave’,function(){
return {
restrict:’A’,
link:function(scope,element,attrs){
element.bind(“mouseleave”,function(){
element.css(“font-size”,”12px”)
})
}
}
})
app.directive(‘hello’,function(){
return {
restrict:’E’,
template:”<div><input ng-model=’txt'</div><div>{{txt}}</div>”,
link:function(scope,element){
scope.$watch(‘txt’,function(newVal){    //变量为输入的值   watch为监听事件
if(newVal===’error’){
element.css(“color”,”red”)
}
})
}
}
})
</script>
```
八、directive基础
```html
<div ng-app=”app1″>
<hello></hello>                         <!-;当restrict为E的时候这么写-;>
<div hello></div>                       <!-;A的写法-;>
<div class=”hello”></div>               <!-;C的写法-;>
</div>

<script>
var app = angular.module(“app1″,[]);
app.directive(‘hello’,function(){
return{
restrict:’E’,    //E:element     A：属性（默认），调用的时候直接加在div后就行<div hello>        C:class的意思，调用class=”hello”
replace:true,    //默认为false，当为false的时候显示<hello>标签，为true的时候隐藏<hello>标签
template:'<div>HELLO Angular<div ng-transclude></div>’,    //这个其实可以放到一个独立的文件中，形式改成templateUrl：’hello.html’
//ng-translude是保留hello内的元素，不让这个template里边的元素替换
compile：function(){         //这个是自定义的属性，一般不用，用的话还要写一遍compile因为用的时候会覆盖掉之前默认的
}
link:function(){
alert(“我在这里”)
}
}
})
</script>–>

<!–directive(指令)与controller（控制器）之间的回话
directive(指令)—放一些鼠标的事件及dom操作
controller（控制器）—依赖注入
run为注射器，只执行一次

directive和内部的controller和link怎么用
controller：想将方法暴露出去的话用
link：绑定内部事务

<div ng-app=”app” ng-controller=”AppCtrl”>
<span enter=”loadMoreData()”>加载</span>                       <!–A的写法–>
<span enter=”DelData()”>删除</span>                       <!–A的写法–>
</div>
<script>
var app = angular.module(“app”,[]);
app.controller(‘AppCtrl’,function($scope){
$scope.loadMoreData=function(){
alert(“正在加载。。。”)
};
$scope.DelData=function(){
alert(“正在删除数据。。。”)
}
});
app.directive(‘enter’,function(){
return{               //如果只有link的时候可以直接return一个函数–return function(scope,element,attrs){}
restrict:’A’,    //E:element     A：属性(默认)，调用的时候直接加在div后就行<div hello>        C:class的意思，调用class=”hello”
link:function(scope,element,attrs){
element.bind(‘mouseenter’,function(){
//其实还省略了一个attr.howtoload（），如果定义了这个，那上边应该是howtoload=”loadMoreData()”而不是enter了，下边那句attrs。enter其实就是这句话，这里有一个坑，就是这里必须是小写
scope.$apply(attrs.enter);   //这里的演变过程是第一次是scope.loadMoreData（）
});                                 //第二次是改成了scope.$apply(loadMoreData())
}                                                   //第三次是改成了scope.$apply(attrs.enter)
}
})
</script>
```
九、Service表现形式

value  constant factory service provider()
```html
<div ng-app=”app” ng-controller=”MyCtrl”>    <!–控制器 –>
<p>{{msg}}</p>
<p>{{realname}}</p>
<p>{{http}}</p>
<p>{{date.msg}}</p>
<p>{{uname}}</p>
</div>
<script>
angular.module(“app”,[])
.value(“realname”,’zhouliu’)             //value可以改变
.constant(“http”,”www.baidu.com”)        //constant 不可以改变
.factory(“Data”,function(){
return{                              //factory和service主要区别就是他要先return，还有就是this
msg:”你好啊”,
setMsg:function(){
this.msg=”我”
}
}
})
.service(“User”,function(){           //service类似于factory，这个可以理解为全局变量，所以在哪里都可以调用
this.firstName=”上官”;
this.lastName=”飞燕 “;
this.getName=function(){
return this.firstName+this.lastName;
}
})
.controller(“MyCtrl”,function($scope,realname,http,Data,User){                //依赖注入
$scope.msg=”您好”;
$scope.realname=realname;
$scope.http=http;
$scope.date=Data;
Data.setMsg();             //这个是让Data这个参数从新取值为setMsg
$scope.uname=User.getName();
})
</script>
```
十、templateCache
```js
var myModule = angular.module(“MyModule”, []);
//注射器加载完所有模块时，此方法执行一次
myModule.run(function($templateCache){
$templateCache.put(“hello.html”,”<div>Hello everyone!!!!!!</div>”);    //先缓存模板 用put
});
myModule.directive(“hello”, function($templateCache) {
return {
restrict: ‘AECM’,
template: $templateCache.get(“hello.html”),             //之后在get出来这个模板
replace: true
}
});
```
十一、动感超人示例
```html
<div class=”row”>
<div class=”col-md-3″>
<superman strength>动感超人—力量</superman>
</div>
</div>
<div class=”row”>
<div class=”col-md-3″>
<superman strength speed>动感超人2—力量+敏捷</superman>
</div>
</div>
<div class=”row”>
<div class=”col-md-3″>
<superman strength speed light>动感超人3—力量+敏捷+发光</superman>
</div>
</div>
<script>
/*
directive和内部的controller和link怎么用
controller：想将方法暴露出去的话用
link：绑定内部事务
*/
var myModule = angular.module(“MyModule”, []);
myModule.directive(“superman”, function() {
return {
scope: {},                                      //独立scope
restrict: ‘AE’,
controller: function($scope) {                  //这个controller和MVC的controller不一样
$scope.abilities = [];                      //定义一个abilities数组
this.addStrength = function() {
$scope.abilities.push(“strength”);
};
this.addSpeed = function() {
$scope.abilities.push(“speed”);
};
this.addLight = function() {
$scope.abilities.push(“light”);
};
},
link: function(scope, element, attrs) {
element.addClass(‘btn btn-primary’);
element.bind(“mouseenter”, function() {
console.log(scope.abilities);
});
}
}
});
myModule.directive(“strength”, function() {
return {
require: ‘^superman’,                                   //require是依赖关系
link: function(scope, element, attrs, supermanCtrl) {       //暴露出supermanCtrl方法
supermanCtrl.addStrength();
}
}
});
myModule.directive(“speed”, function() {
return {
require: ‘^superman’,
link: function(scope, element, attrs, supermanCtrl) {
supermanCtrl.addSpeed();
}
}
});
myModule.directive(“light”, function() {
return {
require: ‘^superman’,
link: function(scope, element, attrs, supermanCtrl) {
supermanCtrl.addLight();
}
}
});
</script>
```
十二、八种最常用的指令：

①
ng-repeat

②
ng-model

③
ng-click

④
```html
<span ng-switch on=”person.sex”>
<span ng-switch-when=”1″>you are a boy</span>
<span ng-switch-when=”2″>you are a girl</span>
<span ng-if=”person.sex==1″>you may be a father</span>
<span ng-show=”person.sex==2″>you may be a mother</span>
```
⑤
```html
<input type=”text” name=”inputText” required ng-trim=”true” ng-model=”userNum” ng-pattern=”/^[0-9]*[1-9][0-9]*$/” ng-maxlength=”6″ maxlength=”6″/>
```
ng-trim
ng-minlength   最小长度
ng-maxlength   最大长度
required       必须填写
ng-pattern     正则表达式过滤

⑥
ng-options
```html
<select ng-model=”yourSelected” ng-options=”person.id as person.name in persons”></select>
```
⑦
ng-style
```html
<span ng-style=”myColor”>your color</span>
```
$scope.myColor={color:’blue’};
$scope.myColor={cursor: ‘pointer’,color:’blue’};
⑧
$http

十三、在调用json中所遇到的问题及方法

通常调用json都是放到service里边的，因为调用$http的方法是异步加载，所以不能直接console.log(),必须要用.success（）来进行console.log。还有就是对于回掉函数，ng也提供了$q来做广义的回掉函数的管理机制
```js
Myapp.service(“Myservice”,function($http,$q){
this.userDate=function(){
var deferred =$q.defer();
$http({
method:’GET’,
url:’js/phone.json’
}).success(function(data){
deferred.$$resolve(data)
}).error(function(err){
deferred.$$reject(err)
});
return deferred.promise
}
});
Myapp.controller(“Myctrl”,function($scope,Myservice){
Myservice.userDate().then(
function(data){
console.log(data)     //因为是异步操作，所以必须在then内操作
}),
function(err){
console.log(err)
}
});
```
GET：
```js
function customerController($scope,$http){
$http.get(“Customers_JSON.php”)
.success(function(response){
$scope.names = response;
console.log(“haha”);
});
}
```
POST：
```js
$scope.adduser=function(){
$http.post(“Customers_JSON.php”,{id:$scope.id,name:$scope.name})
.success(function(resp) {
if (resp.success) {
alert(“添加成功”)
}
})
}
```
Controller:
一个控制器没必要同时控制两个试图，一个试图对应一个控制器就可以了，当不同的控制器内用到相同的内容的时候，不要建一个公用的控制器，而是建一个Service来实现通用。
①不要试图复用Controller
②不要再Controller内操纵DOM,操作DOM应该放在Directive内
③不要再Controller内做数据格式化，ng提供了表单控制
④不要再Controller内进行数据过滤，ng提供了$filter服务
⑤不要互相调用Controller，应该放在$scope或者事件内来互相调用

Controller里一般都是控制像（打印haha）
directive里一般都是控制像（鼠标经过这个标签，然后调用controller来打印haha）

Model:
ng-click="$emit('MyEvent')" 向上级进行遍历（一般都是配合ng-repeat来使用）
ng-click="$broadcast('MyEvent')" 向下级开始遍历（一般都是配合ng-repeat来使用）

$scope和$rootScope的关系类似于js的原型继承机制
$scope提供了一些方法$watch()/$apply
$scope和DOM一样都是树形结构，与DOM平行
$scope的5个生命周期：创建-监控-检测模型变化-模型突变（有没有脏）-销毁

ng-class:
ng-class="{error:isError,right:isRight}"
需要后面去触发这个属性变化
$scope.isError=true;
$scope.isRight=false;

ng-model:
来控制checkbox的选中状态的时候也用ng-model=“true”来控制而不再用checked

ng-show:
ng-show="ngShow.show"
$scope.ngShow={show:true};

ngAnimate:
就是利用切换class通过css3来实现动画

Service:
```js app.factory('UserInformation', function() {

var user = {

name: "Angular.js"

};

return user;

});

//下边是分别调用上边公用的user

app.controller('MainCtrl', function($scope, UserInformation) {

$scope.user = UserInformation;

});
//第二个controller调用
app.controller('SecondCtrl', function($scope, UserInformation) {

$scope.user = UserInformation;

});```
提交表单不提示：提交按键的属性必须是submit才行
没有用到的插件，一定不要再module的[]内添加上，这样会报错！
$http的文件引用目录是相对于html页面位置说的

表单默认值：
1.ng-init="user.phone='1'"                   //优先级排第二
2.在controller里直接赋值：$scope.user={"phone":"12"}             //优先级排第三
3.通过$http来获取的值：$secop.user=response;        //优先级排第一
在service中都是用this 且用不到$scope
在controller中不能用var而是$scope
在directive中有很多属性
ng-disabled='' 判断可用不可用

Directive：
directive内使用controller是为了暴露给外界其他directive，但是其他的一定要require：（查看动感超人）！
在link内的函数，是不能暴露给外界的，只能在他自己的directive内使用，他内部的template也是可以使用的

在directive内可以设置独立scope，这样就不会互相影响了,和restrict：‘AE’写法一样
scope:{};
例如
```js return{
restrict:"AE",
scope:{}, //这样html里边放四个这个，就不会同时变化了，就是每个都有每个的scope
template:"

<div&gt;<input type="text" /&gt;{{userName}}</div>
}```
scope的绑定策略
@ 单向绑定-让scope和属性attrs绑定的值相同，传递的是（字符串）不是函数
= 双向的绑定-将@换成=就行了，html里记得把div改成input表单形式，这样才能输入
& 传递一个来自父scope的（函数），稍后调用

@用法
```js 

myModule.controll('Myctrl',function($scope){
$scope.ctrlflavor='百威'
});
myModule.directive('drink',function(){
return{
restrict:'AE',
template:"
<div>{{ctrlflavor}}</div>
"
link:function(scope,element,attrs){ //删除link，替换成scope:{flavor:'@'},效果是相同的
scope.flavor=attrs.flavor
}
}
})```
Service：
service和factory的本质上都是Provider

Service作为运行时依赖，我们把service的名字作为参数传递给controller 函数（使用中括号[])
```js app.controller('ServiceController', ['$scope', 'githubService',
function($scope, githubService) {
}]);```
$filter:
过滤
```js
currency,date,json,limitTo,lowercase,number,orderBy,uppercase
{{1232421551 | date:"yyyy-MM-dd hh:mm:ss}}
自定义filter
{{'haha' | filter1}}
myModule.filter("filter1",function(){
return function(item){
return item+"haha"; //这里的item就是'haha'
}
})
```
$interval和$timeout
定时器指令

<img class="fit-image" style="border: 0px; text-align: center; color: #333333; font-family: 宋体; font-size: 14px; font-style: normal; font-variant: normal; font-weight: normal; letter-spacing: normal; line-height: 28px; orphans: auto; text-indent: 28px; text-transform: none; white-space: normal; widows: 1; word-spacing: 0px; -webkit-text-stroke-width: 0px; background-color: #f8f8f8;" src="http://s9.51cto.com/wyfs01/M00/15/06/wKioJlIIrj7gEgYUAAAUWycAI-4986.jpg" alt="" />

&nbsp;

过滤：filter

例：
```js Total: {{ 1232.12 | currency }}```
自定义过滤：
```js app.filter('capitalize', function() {

return function(input, param) {

return input.substring(0,1).toUpperCase()+input.substring(1);

}

});```
排序：orderBy

例：
```js <span class="tag"><</span><span class="tag-name">li</span> <span class="attribute">ng-repeat</span>=<span class="attribute-value">"person in developers | orderBy:'name'"</span><span class="tag">&gt;</span>```
注：反序排列，你可以用 -name表示。

数据绑定和AJAX

如果是获取jsonp文件一定要加上
```html
<span class="attribute">callback</span>=<span class="attribute-value">JSON_CALLBACK</span>
```
```js  url: 'https://api.github.com/users/' + username + '/' + path + '?<span class="attribute">callback</span>=<span class="attribute-value">JSON_CALLBACK</span>'```
&nbsp;

如果想使用$timeout服务，我们只要简单的把他注入到我们的githubService中就可以了
```js app.controller('ServiceController', ['$scope', '$timeout', 'githubService',
function($scope, $timeout, githubService) {
}]);```