使用antd组件能大大的提高我们的开发效率，里面的样式功能齐全

我们首先想到的是引入这个antd库

个性定制有三种情况：

>一，使用create-react-app创建的项目：找到node_modules->react-scripts->config->webpack.config.dev.js当中找到plugins添加以下代码：

```js
["import", { libraryName: "antd", style: "css" }]
```

>>二，自己建的环境：创建.
