Redux 是数据流管理工具。使用Redux的最重要的一句话：

>一切数据都要保存在store中，组件自己不保留自己的state数据

后续所学的一切技巧基本服务于一个关系：组件和Store的关系

###为何要统一存放到Store中？

把所有的数据都存放到Store中，然后所有的组件都订阅Store的数据。那么数据就有了Single Source of Truth(唯一可信数据源)。这样的好处就是：

>>第一，各个组件都统一读写同一个数据，组件间通信变得不成问题了
>>第二，就是数据统一存放，代码比较不容易写乱

###创建Store

Store的主体就是写到store.js中的数据

类似：

```js
let comments = [
  'hello1',
  'hello2'
]
```

但是，store中的数据，必然要涉及读和写的操作，所以要安装一个包辅助后续操作：

```
npm i --save redux
```

到store.js中导入
```
import {createStore} from 'redux'
```

由此可以推理出的导出的步骤：

```
let store = createStore(comments)
export default store
```

但是，createStore的[官方文档](http://cn.redux.js.org/docs/api/createStore.html)中指明这个函数是至少多传入一个参数的。这个参数就是 **reducer**

读一读官方文档，发现createStore可以接收三个参数：

>>reducer，这一项是必须填写的
>>preloadeState,预加载State，可选
>>enhancer,增强器，可选

ps：如何快速找到接口文档->用google搜索，会用google和科学上网是程序员的基本素质
接口文档上，有中括号的参数是可选的(optional)

##reducer

reducer 和store一样是redux三大核心概念之一。reducer是 **一个函数** ，用来修改store中的数据

demo：

```js
function commentReducer(state=[],action){
  // console.log(state,action)
  switch(action.type){
    case 'ADD_COMMENT' :
      //console.log([...state,action.comment])
      return [...state,action.comment]
    default :
      return state
  }
}
```

上面的代码暂时先不用理解，只需要知道reducer的基本格式是：

```js
(oldState,action) => nextState
```

下面的代码实现了，数据存储到store.js同时组件内部读取store.js中的数据：

[createStore](https://github.com/liulu1012/new-redux-hello/commit/39a93efb61fb91a81cd761a023432d37d6fc9884)

##修改Store中的数据

前面实现了从Store中通过 **store.getState()** 读取数据。下面来实现修改数据的操作。这个主要通过Redux三大概念的另外两个： *action*，*reducer* 来配合使用

>基本原理：组件发出 action ,action 触发 reducer ， 真正修改数据，是通过 reducer 来完成

##先来看action

前面的用词是 **组件发出 action** 可见action是名词。那么redux这里action其实就是一个如下的对象：

```js
let action = {
  type : 'ADD_COMMENT',
  comment : 'hello3'
}
```

action对象有两个部分组成：

>>第一部分：要有一个 *type* 属性，值是一个 *字符串*
>>第二部分：payload，也就是这个action携带的数据

上面这个形式，让我们联想起了axios发POST请求(action的接收方就是reducer)

发出一个action就是在 **组件内部**

```js
store.dispatch(action)
```

dispatch就是发出(分发)的意思，可以用它发出action

发出之后，需要有专门对应的reducer进行接收

##reducer

它的左右就是接收action，然后根据action修改store中的数据

代码：
[dispatch action](https://github.com/liulu1012/new-redux-hello/commit/dfd171f88f915fcffd785cbba359b10105190d69)

这样，每次dispatch action 之后，reducer都可以去修改state值了

整个store中存储的state值，我们都会把它叫做 **状态树** (state tree)。状态树的具体值就是 *store.getState()* 的返回值。整个项目，*就只有一个状态树*

##修改数据的时间维度的执行流程

首先，用户点提交按钮

```js
store.dispatch({type,payload})
```

然后，由store.js中的commentReducer来接收

```js
function commentReducer(state=[],action){
  //console.log(state,action)
  switch(action.type){
    case 'ADD_COMMENT':
      //console.log([...state,action.comment])
      return [...state,action.comment]
    default :
      return state
  }
}
```

也就是commentReducer要开始执行，执行的时候，state是什么呢？

可以看到commentReducer中的state的默认值是[],也就是说如果state我们不给它赋值，后续执行中它的值就是[]

并且这里比较奇怪的是，我们也没有看到commentReducer的调用语句，类似：

```js
let state = [
  ...
]
commentReducer(state,action)
```

所以感觉上是没有给state。但是，其实redux采用的是 **函数式编程** 的思想

commentReducer的调用是在

```js
const store = createStore(commentReducer,comments)
```

并且，调用过程中，state也赋值为 comments

当```return [...state,action.comment]```执行之后，store.getState()的值就被改变了

代码：

[ADD_COMMENT works](https://github.com/liulu1012/new-redux-hello/commit/89b509fb3189aa14d7cff5c8476bef3fb92f61cc)

##思考

如果PostBody.js写成这样

```js
import React,{Component} from 'react'
import store from './store'

class PostBody extends Component{
  constructor(){
    super()
    this.state = {
      num : store.getState().length
    }
  }
  render(){
    return(
      <div className='post-body'>
        <div className='comment-num'>
          {this.state.num}
        </div>
      </div>
    )
  }
}

export default PostBody
```

那么，初始条件下，是可以从store中读取评论数量的，但是为什么，store数据更新后，这里的评论数量不会变？？

答案：就是这里的 *store.getState()* 没有再次被执行(当然，即使store.getState()自动有了新值也不行的，因为constructor()只会执行一次)

那么如何得到更新后的评论数量呢？

##总体框图

总之，我们就是需要组件有这样的能力，也就是每当 store 中的数据有了变化，组件会自动重新 render 。

问题的解决方案就在下图中（注意我们还没有碰的功能模块是哪一个）

答案就是：**react-redux**
