首先全局安装 *create-react-app* 这个工具

先来说一下json文件：

里面的属性名和属性值都要有 ""

”main” ： 对应的入口文件（一般都是index.js）

“scripts” ： 可以定义执行的脚本


"scripts"(脚本)里面加上

编辑器中 ：“hello”:"node-v"

bash中 ： npm run hello

言归正传，说回 create-react-app ,这个工具的作用：

**初始化项目，相当于已存在的环境**

使用的原因： *因为react需要一个环境的支持，所以需要create-react-app来初始化这个环境*

实例：

bash: create-react-app es6-demo //此时在桌面就生成了一个es6-demo文件夹

进入 es6-demo 编辑自己写的代码 //所有自己写的代码都放在src中，其中一定要保留index.js(因为package.json的入口文件就是index.js)
