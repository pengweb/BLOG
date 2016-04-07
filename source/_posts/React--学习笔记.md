---
title: React--学习笔记
date: 2016-04-07 15:40:57
tags: [js,笔记,note,javascript,react]

---

# 1.准备
Babel   将es6转化成es5的工具（服务器端）
browser   将es6转化成es5的工具（浏览器端）


# 2.组件

```js
var helloMessage = React.creatclass({render:function(){return }})
```

组件类的第一个字母必须大写，否则会报错，应改为**HelloMessage**
```js
var helloMessage = React.creatclass({render:function(){return <h1></h1><p></p>}})
```


组件类只能包含一个顶层标签，否则也会报错。**h1和p**都是顶层标签了
**如果一定要含有两层或更多的话，记得用()括起来，return (<h1></h1><p></p>)**

```js
<HelloMessage name="John" class="错的" for="错的">
```

添加组件的时候class 属性需要写成 **className** ，for 属性需要写成 **htmlFor** ，这是因为 class 和 for 是 JavaScript 的保留字

# 3.this.props.children 

的值有三种可能：如果当前组件没有子节点，它就是 undefined ;如果有一个子节点，数据类型是 object ；如果有多个子节点，数据类型就是 array 。所以，处理 this.props.children 的时候要小心。
React 提供一个工具方法 React.Children 来处理 this.props.children 。我们可以用 **React.Children.map** 来遍历子节点，而不用担心 this.props.children 的数据类型是 undefined 还是 object。
用法
```js
var NotesList = React.createClass({
  render: function() {
    return (
      <ol>
      {
        React.Children.map(this.props.children, function (child) {
          return <li>{child}</li>;
        })
      }
      </ol>
    );
  }
});

ReactDOM.render(
  <NotesList>
    <span>hello</span>
    <span>world</span>
  </NotesList>,
  document.body
);
```

# 4.PropTypes

```js
 propTypes: {
    title: React.PropTypes.string.isRequired,
  }
```
上边这句是设置title属性必须为字符串，且必须存在
```js
getDefaultProps : function () {
    return {
      title : 'Hello World'
    };
  },
```

设置属性默认值

# 5.获取真实的DOM节点

```js
var MyComponent = React.createClass({
  handleClick: function() {
    this.refs.myTextInput.focus(alert('haha'));  //当点击之后，会弹出haha,只有当点击才会触发这个
  },
  render: function() {
    return (
      <div>
        <input type="text" ref="myTextInput" />   //必须有这个ref来进行定位，并且获取这里的值
        <input type="button" value="Focus the text input" onClick={this.handleClick} />
      </div>
    );
  }
});
```
所有的DOM操作都在虚拟DOM上发生，然在在反应到真实的DOM上，叫DOM diff。

# 6.this.state

```js
var LikeButton = React.createClass({
  getInitialState: function() {       //设定一个初始状态
    return {liked: false};
  },
  handleClick: function(event) {
    this.setState({liked: !this.state.liked});    //修改状态
  },
  render: function() {
    var text = this.state.liked ? 'like' : 'haven\'t liked';
    return (
      <p onClick={this.handleClick}>         //onClick触发
        You {text} this. Click to toggle.
      </p>
    );
  }
});
```

this.props 表示那些一旦定义，就不再改变的特性，而 this.state 是会随着用户互动而产生变化的特性


# 7.表单

```js
var Input = React.createClass({
  getInitialState: function() {
    return {value: 'Hello!'};
  },
  handleChange: function(event) {
    this.setState({value: event.target.value});   //当内容被改变不是初始值的时候，使用event.target.value获取现在值
  },
  render: function () {
    var value = this.state.value;   //获取从ReactDom.render()来的值
    return (
      <div>
        <input type="text" value={value} onChange={this.handleChange} />   //onChange 触发
        <p>{value}</p>
      </div>
    );
  }
});
```

表单为变动的所以用this.state并且通过 event.target.value 读取用户输入的值


# 8.组件生命周期

```js
var Hello = React.createClass({
  getInitialState: function () {
    return {
      opacity: 1.0
    };
  },

  componentDidMount: function () {
    this.timer = setInterval(function () {
      var opacity = this.state.opacity;
      opacity -= .05;
      if (opacity < 0.1) {
        opacity = 1.0;
      }
      this.setState({
        opacity: opacity
      });
    }.bind(this), 100);
  },

  render: function () {
    return (
      <div style={{opacity: this.state.opacity}}>
        Hello {this.props.name}
      </div>
    );
  }
});
```
组件的生命周期分成三个状态：
Mounting：已插入真实 DOM
Updating：正在被重新渲染
Unmounting：已移出真实 DOM
React 为每个状态都提供了两种处理函数，**will 函数在进入状态之前调用**，**did 函数在进入状态之后调用**，三种状态共计五种处理函数。

componentWillMount()
componentDidMount()
componentWillUpdate(object nextProps, object nextState)
componentDidUpdate(object prevProps, object prevState)
componentWillUnmount()
此外，React 还提供两种特殊状态的处理函数。
componentWillReceiveProps(object nextProps)：已加载组件收到新的参数时调用
shouldComponentUpdate(object nextProps, object nextState)：组件判断是否重新渲染时调用
执行顺序
**getInitialState->componentWillMount->已经在页面显示出来了->componentDidMount**

组件的style属性的设置方式也值得注意，不能写成

```js
style="opacity:{this.state.opacity};"
```

而要写成

style=\{ \{opacity: this.state.opacity}}
这是因为 React 组件样式是一个对象，所以**第一重大括号**表示这是 JavaScript 语法，**第二重大括号**表示样式对象。


# 9.Ajax
```js
var UserGist = React.createClass({
  getInitialState: function() {
    return {
      username: '',
      lastGistUrl: ''
    };
  },

  componentDidMount: function() {
    $.get(this.props.source, function(result) {
      var lastGist = result[0];
      if (this.isMounted()) {     //当处于挂载状态下，才能触发setState
        this.setState({
          username: lastGist.owner.login,
          lastGistUrl: lastGist.html_url
        });
      }
    }.bind(this));
  },

  render: function() {
    return (
      <div>
        {this.state.username}'s last gist is
        <a href={this.state.lastGistUrl}>here</a>.
      </div>
    );
  }
});

ReactDOM.render(
  <UserGist source="https://api.github.com/users/octocat/gists" />,
  document.body
);
```
isMounted只有组件还处于挂载状态下，才有setState从而更新视图的意义


# 下边是平时遇到的问题
通过要寻找某个节点
```js
React.findDomNode(this.refs.tip)
```
其中render是这么写的
```js
render:function(){
  return <div refs="tip"></div>
}
```