es6的出现，为我们节省了不少的代码，其中比较常用的就是关于es6的赋值

##数组解构赋值

```js
var/let [a,b] = [5,10]
console.log(a,b,c)
```

or

```js
let arr = [5,8,9,'aaa']
let [a,b,c] = arr
console.log(arr)
```

ps: *数组的解构赋值会按照索引匹配*

如果空的会占位，如果是后面的值多，则输出undefined

##字符串解构赋值

```js
let [a,b,c,d,e] = 'hello'
console.log(a+'\n',b+'\n',c+'\n',d+'\n',e+'\n')
```

##对象解构赋值（最常用的）

```js
let {foo,bar} = {foo:'aaa',bar:'bbb'}
console.log(foo,bar)
```

上述代码中，可以看到，对象的解构赋值是按照 *属性名* 去匹配（如果不匹配，输出的是undefined）

扩展：

```js
var obj = {foo:'aaa',bar:'bbb'}
var {bar} = obj
console.log(bar) //bbb
```

#对函数的形参进行解构赋值

```js
function hello({name}){
  console.log('my name is'+name)
}
hello({name:'liulu',age:26,tall:111})
```

es6可以简写

```js
var username = 'liulu'
var password = 'password'
var user = {
  username,
  password,
  say(){
    console.log('hello')
  }
}
console.log(user)
```
