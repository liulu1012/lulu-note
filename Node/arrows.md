箭头函数，让我们的代码更加简练

之前

```js
function sum(x,y){
  return x*y
}
```

现在

```js
let sum = (x,y) => x*y //箭头后面写的就是返回值
```

#没有函数的参数

```js
let sum = () => 666
console.log(sum())
```

#一个参数的时候，可以不写()

>多位或者没有参数的函数，必须有()

```js
let sum = num => 110*num
let a = sum(5)
console.log(a)  //550
```

#返回值执行多条js语句

>1.箭头后面是一个{} 2.手动设置返回值

```js
let sum = num =>{
  console.log(1)
  console.log(2)
  console.log(3)
  return num
}
let a = sum(5)
console.log(a)
```

#返回对象的时候

```js
let sum = num => ({})
```

#如果有js语句，并要返回对象

```js
let sum = num => {
  console.log(1)
  return {
    name:'liulu',
    age:26
  }
}
```
