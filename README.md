# **webpack-start**
学习webpack-demo

----------------------------------------------------------------------


## **常用命令**
```base
# 查看 webpack 版本信息
$ npm info webpack

# 安装指定版本的 webpack
$ npm install webpack@1.12.x --save-dev

# 如果需要使用 Webpack 开发工具，要单独安装：
$ npm install webpack-dev-server --save-dev

# 如果创建了配置文件，执行webpack命令即可将模块打包
$ webpack
```


## **加载器（loader）**
### 什么是loader
加载器（loader）其实就是一个转换器。webpack只会讲js文件视为模块，那么对于非js文件（如：.vue、.css、.sass/.scss、图片、jsx、coffescript等）怎么办呢？这就是loader的作用，将这些文件（原文件）转换为js文件（新的资源模块）。

### 配置loader
这里有一点需要注意的，那就是webpack从2.0版后就不再支持配置loader时缩写了。让我们看一看下面示例：

在1.x版时，你可以这样配置loader。
```js
loaders: [
    { test: /\.css$/, loader: 'style!css' },
    //另一种语法
    { test: /\.css$/, loaders: ["style", "css"] },
]
```

但是，从2.x后，上面的写法会报错，你就必须像下面这样写才行了。
```js
loaders: [
    { test: /\.css$/, loader: 'style-loader!css-loader'}
]
```



## 插件（Plugins）

### 什么是Plugin？
插件（plugin）是功能更强大的loader。

### 常用的一些插件

*html-webpack-plugin*
html-webpack-plugin可以根据你设置的模板，在每次运行后生成对应的模板文件，同时所依赖的CSS/JS也都会被引入，如果CSS/JS中含有hash值，则html-webpack-plugin生成的模板文件也会引入正确版本的CSS/JS文件。

安装（Install）：
```js
npm install html-webpack-plugin --save-dev
```


在webpack.config.js中引入。
```js
const HtmlWebpackPlugin = require('html-webpack-plugin');
```

配置:
```js
module.exports = {
    entry: './app/index.js',
    output: {
        ...
    },
    module: {
        ...
    },
    plugins: [
        new HtmlWebpackPlugin({
            title: "This is the result", //生成的HTML模板的title，如果模板中有设置title的名字，则会忽略这里的设置
            filename: "./index.html", //生成的模板文件的名字
            template: "./app/index.html",  // 模板来源文件
            inject: "body",  //引入模块的注入位置；取值有true/false/body/head
            favicon: "",  //指定页面图标；
            minify: { //是html-webpack-plugin中集成的 html-minifier ，生成模板文件压缩配置，有很多配置项
                caseSensitive: false,  //是否大小写敏感
                collapseBooleanAttributes: true, //是否简写boolean格式的属性如：disabled="disabled" 简写为disabled 
                collapseWhitespace: true //是否去除空格
            },
            //是否生成hash添加在引入文件地址的末尾，类似于我们常用的时间戳，比如最终引入是：<script type="text/javascript" src="bundle.049424f7d7ea5fa50656.js?049424f7d7ea5fa50656"></script>。这个可以避免缓存带来的麻烦
            hash: true,
            //是否需要缓存，如果填写true，则文件只有在改变时才会重新生成 
            cache: true,
            //是否将错误信息写在页面里，默认true，出现错误信息则会包裹在一个pre标签内添加到页面上
            showErrors: true,
            //引入的模块，这里指定的是entry中设置多个js时，在这里指定引入的js，如果不设置则默认全部引入
            chunks: "",
            //引入模块的排序方式
            chunksSortMode: "auto",
            //排除的模块
            excludeChunks: "",
            //生成的模板文档中标签是否自动关闭，针对xhtml的语法，会要求标签都关闭，默认false
            xhtml: false
        })
    ]
};
```
