# webpack-start
学习webpack-demo

----------------------------------------------------------------------


## 常用命令
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


## 配置loader
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
