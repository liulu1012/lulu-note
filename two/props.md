不用redux实现组件之间的通讯

原理：

>通过子组件，修改父组件的 state ，然后把父组件的 state 作为所有子组件的 props 值传入各个子组件

这样就实现了各个兄弟组件的通讯

##子组件修改父组件的state

demo:

>子组件Child.js

```js
import React from 'react'
class  Child extends React.Component{
  handleClick = () =>{
    this.props.changeColor('green')
  }
  render(){
    return(
      <div>
        <button onClick={this.handleClick}>child button</button>
      </div>
      )
  }
}
export default Child
```

>父组件App.js

```js
import React from 'react'
class App extends React.Component{
  state = {
    bgColor:'red'
  }
  changeBackground = (color) => {
    this.setState({
      bgColor :color
    })
  }
  render(){
    return(
      <div>
        <Child changeColor={this.changeBackground}/>
      </div>
    )
  }
}
```


redux-hello项目中:

[use component props](https://github.com/liulu1012/new-redux-hello/commit/9428b10d959caf57b3cc0902bb5b1b4dc4689e5f)
