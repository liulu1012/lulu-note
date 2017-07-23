###React 内部state的基本使用

使用每个组件自己的 State 来达成基本评论框效果。

##任务一：显示两条假的评论

这里的体现出 React 的特点，就是所有的组件显示出来的动态数据，都要存放到 state 值之中。

但是数据到底要存储成何种数据类型呢？也即是数据的存储格式要怎么样？

```
this.state = {
  comment1: "hello1",
  comment2: "hello2"，
}
```

这样写，如果只是展示两条死数据，完全没有问题。但是如果有一百条评论，就得有一百个 state 值。但是 React 组件其实一旦写成，它里面的 state 变量名的数量是固定的。代码运行过程中，一般不能添加新的 state 变量进来。只能修改已有的 state 变量值。

数据结构的采用，完全根据实际需要来选择。首先要设置一个 state 变量，就叫 comments 。 同时这个变量里面，可以有多个元素，可以任意增加或者减少元素数量（数组）。

```
this.state = {
  comments: [
    "hello1",
    "hello2"
  ]
}
```
代码：
**[two comments](https://github.com/liulu1012/new-redux-hello/commit/1ef85539088d29bf8e553f82f7767be07ff73d79)**

##任务二：添加form

代码：
[add form](https://github.com/liulu1012/new-redux-hello/commit/1d49545addd1189d0dac4e01a3d0437045caa6b8)


##任务三：发布评论

发布评论的过程：

*1.点一下 submit 这个按钮，浏览器发成的 event （事件）就是 “表单提交（ form submit ）”*

*2.事件触发之后，我们如何来写对应的”事件处理函数“一般会叫 handleXXX ，意思是”处理XXX事件“*

*3.如何把”事件处理函数“跟事件本身绑定起来呢？纯 html 中用 action 属性来处理。但是有了 React 就不用 action 。用 onSubmit （ on 的意思就是”当发生“ )*

```
 <form onSubmit={this.handleSubmit} ></form>
```

每次提交，页面都会刷新，而我们写的是”单页面应用“，所以页面不允许刷新,使用e.preventDefault()
```
handleSubmit = (e)=>{
  e.preventDefault()
}
```

使用ref给input设置属性，然后使用对象展开重新设置组件内的state的值

```
handleSubmit = (e)=>{
  e.preventDefault()
  let newComment = this.commentInput.value
  this.setState({
    comments:[...this.state.comments,newComment]
    })
}
```

在input中：
```
<input ref={value=>this.commentInput =value}/>
```

>上述代码中：this.commentInput输出是整个input的节点，然后.value是添加value属性，
而我们要拿的就是之前默认的评论，以及新的input中所提交的value值


代码：
**[submit commit](https://github.com/liulu1012/new-redux-hello/commit/38e88eacaf58ca45264e6ec1aa3c3f01eedf2d16)**





在提交之后，清空input中的输入值，即为reset form：
同理，给form标签加上ref属性，然后使用form的reset方法即可

```
<form ref={value=>this.commentForm=value}

```
然后在handleSubmit中：

```
this.commentForm.reset()
```

清空input代码：
**[reset form](https://github.com/liulu1012/new-redux-hello/commit/e6ac961cfbd4495469dd19765484ad3831aaa59c)**


###不可写性

注意，不能直接使用下面的代码：

```
handleSubmit(e) {
  e.preventDefault()
  let content = this.refs.content.value
  let comments =   this.state.comments // 需要添加 .slice()
  comments.push(content)
  this.setState({ comments })
}
```

因为这样会直接修改 state 值。可行的方式是用 slice() 或者用数组展开运算符。
