模块化开发，顾名思义，是用各个模块互相配合构成

那么模块的种类主要有三种

**核心模块（官网的，很少用到）**

**第三方模块（例：jquery等）**

**文件模块（自己写的模块，一定要注意相对路径）**

ps： *核心模块和第三方模块不要加路径*

常用的一些单词： *version(版本)* *description(描述)*  *repositort(仓库)* *author(作者)*

初始化node：

```js
npm init
```

npm 后，我们会看到生成了一个 *package.json* 文件

json语法的特点：

*属性名和属性值加 “”*

*每一个对象的最后一个属性，包括json整个的最后的属性，都不要有 ，*

安装：

**npm install jquery --save(记录到dependencies里面)**

**webpack --save-dev(dev是工具的参数，代表只有在项目下才可以使用)  (记录到devDependencies里面)(项目应用开发依赖环境)**

**webpack -g(全局)(多人合作的使用尽量不要使用，因为不能保证版本一致)**


卸载：

**npm unistall jquery** (如果是全局安装，那么卸载的时候在后面需要加上-g)


在安装第三方模块的时候，如果不清楚具体的版本，那么在&后面写什么，代表的就是该数字下面的最高版本

例：

```
npm i jquery&2 --save //代表2下面的最高的jquery版本
```

有一些安装包，我们是不需要传入github上的，例如node_modules,避免造成代码冗余，解决：

创建.gitigore这个文件，然后将不想传入git的文件名写在这个文件里面，那么github就会自动过滤
