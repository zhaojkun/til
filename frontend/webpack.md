# Webpack

Datetime: 2016-03-15

Tag: webpack frontend tools

`Webpack`是一个module bundler,模块管理工具。主要有以下特性：
* 同时支持commonjs和AMD规范（甚至混合形式）
* 可以打成一个完整的包，也可以分成多个部分，在运行时异步加载（可以减少第一次加载的时间）
* 依赖在编译时即处理完毕，可以减少运行时包的大小
* Loaders可以使文件在编译时得到预处理，这可以帮我们做很多事情，比如说模块的预编译，图片的base64处理
* 丰富和可扩展的插件可以适应多变的需求。

配置代码示例：
```
var webpack=require('webpack');
module.exports={
	entry:[
    	'web/hot/only-dev-server',
        './js/app.js'
    ],
    output:{
    	path:'./build',
        filename:'bundle.js'
    },
    module:{
    	loaders:[
        {test:/\.js?$/,loaders:['react-hot','babel'],exclude:/node_modules/},
        {test::/\.js$/,exclude:/node_modules/,loader:'babel-loader'},
        {test:/\.css$/,loader:'style!css'},
        {test:/\.less/,loader:'style-loader!css-loader!less-loader'}
        ]
    },
    resolve:{
    	extensions:['','.js','.json']
    },
    plugins:[
    	new webpack.NoErrorsPlugin()
    ]
};
```
webpack.config.js文件通常放在项目的根目录中，它本身也是一个标准的Commonjs规范的模块。在导出的配置对象中有几个关键的参数:

#### 1. entry
entry可以是个字符串或者数组或者是对象。当entry是个字符串的时候，用来定义入口文件：`entry:'./js/main.js'`

当entry是个数组的时候，里面同样包含入口js文件，另外一个参数可以是用来配置webpack提供的一个静态资源服务器，webpack-dev-server。webpack-dev-server会监控项目中的每一个文件的变化，实时的进行构建，并且自动刷新页面：
```
entry:[
	'webpack/hot/only-dev-server',
    './js/app.js'
]
```
当entry是个对象的时候，我们可以将不同的文件构建成不同的文件，按需使用，比如我的hello页面中只要`<script src='build/Profile.js'></script>`引入hello.js即可：
```
entry:{
	hello:'./js/hello.js',
    form:'./js/form.js'
}
```
#### 2 Output

output参数是个对象，用于定义构建后的文件输出。其中包含path和filename:
```
output:{
	path:'./build',
    filename:'bundle.js'
}
```
当我们在entry中定义构建多个文件时，filename可以对应的更改为[name].js用于定义不同文件构建后的名字。

#### 3 module
关于模块的加载相关，我们就定义在module.loaders中。这里通过正则表达式去匹配不同的文件名，然后给他们定义不同的加载器，比如说给less文件定义串联的三个加载器（!用来定义级联关系）
```
module:{
	loaders:[
    	{test:/\.js?$/,loaders:['react-hot','babel'],exclude:/node_modules/},
        {test:/\.js/,exclude:/node_modules/,loader:'babel-loader'},
        {test:/\.css$/,loader:'style!css'},
        {test:/\.less/,loader:'style-loader!css-loader!less-loader'}
    ]
}
```
此外还可以添加用来定义png,jpg这样的图片资源在小于10k时自动处理为base64图片的加载器：
```
{test:/\.(png|jpg)$/,loader:'url-loader?limit=10000'}
```
给css和less还有图片添加了loader之后，我们不仅可以想在node中那样require.js文件了，我们还可以require css,less甚至图片文件：
```
require('./bootstrap.css');
require('./myapp.less')
var img=document.createElement('img')
img.src=require('./glyph.png')
```
但是需要知道的是，这样require来的文件会内联到js bundle中，如果我们呢需要把保留require的写法又想把css文件单独拿出来，可以使用下面提到的`extract-text-webpack-plugin`插件。
#### 4.resolve
webpack在构建包的时候会按目录进行目录的查找，resolve属性中的extension数组中用于配置程序可以自动补全哪些文件后缀：
```
resolve:{
	extensions:['','.js','.json']
}
```
然后我们想加载一个js文件时，只要require('common')就可以加载common.js文件了。
#### 5.plugin
webpack提供了丰富的组件，用于满足不同的需求，当然我们也可以自行实现一个组件来满足自己的需求，在我的项目中没有特殊的需求，于是便只是配置了NoErrorsPlugin插件，用来跳过编译时出错的代码并记录，使编译后运行时包不会发生错误：
```
plugins:[
	new webpack.NoErrorsPlugin()
]
```

参考文献：
http://www.cnblogs.com/Leo_wl/p/4862714.html 