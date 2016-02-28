# React 环境搭建


环境安装,index.html用来保存html,App.js用来保存React组件，main.js React的入口文件,webpack.config.js用来设置webpack

```
npm init
npm install react react-dom --save
npm install babel-loader babel-core babel-preset-es2015 babel-preset-react
touch index.html App.js main.js webpack.config.js
npm install babel webpack webpack-dev-server -g
```

webpack.config.js

```
module.exports={
	entry:'./main.js',
    output:{
    	path:'./',
        filename:'index.js'
    },
    devServer:{
    	inline:true,
        port:3333,
    },
    module:{
    	loaders:[
        {
        	test:/\.js$/,
            exclude:/node_modules/,
            loader:'babel',
            query:{
            	presets:['es2015','react']
            }
        }
        ]
    }	
}
```
index.html
```
<!DOCTYPE html>
<html lang="en">
	<head>
		<meta charset="utf-8">
		<title>Setup</title>
	</head>
	<body>
		<div id="app"></div>
		<script src="index.js"></script>
		<div>
			</div>
	</body>
</html>
```

App.js
```
import React from 'react';
class App extends React.Component{
	render(){
    	return <div>Hello</div>
    }
}
export default App
```
main.js
```
import React from 'react';
import ReactDOM from 'react-dom';
import App from './App';
ReactDOM.render(<App />,document.getElementById("app"))
```
package.js
```
修改scripts中
"start":"webpack-dev-server"
```
所有代码可参见 [react_helloworld](https://gitlab.com/zhaojkun/react_helloworld)

参考：[react-react-fundamentals-development-environment-setup](https://egghead.io/lessons/react-react-fundamentals-development-environment-setup)
