# Redux入门

Date: 2016-03-05

Tag: react

####　在`redux`中比较关键的是`connect()`函数，其将相关的`props`和`callback`传入对应的组件中


> Action

`Action`是把数据从应用传到store的有效载荷，它是store数据的唯一来源。一般来说你会通过store.dispatch()将action传到store

`Action创建函数`就是生成action的方法，Redux中的action创建函数是纯函数，它没有任何副作用，只是返回action对象而已。
```
function addTodo(text){
	return {
    	type:ADD_TODO,
        text
    }
}
```
这让代码更易于测试和移植，只需把action创建函数的结果传递个`dispatch()`方法即可实例化dispatch.
```
dispatch(addTodo(text));
dispatch(completeTodo(text));
```
或者创建一个被绑定的action创建函数来自动dispatch
```
const boundAddTodo=(text) => dispatch(addTodo(text));
const boundCompleteTodo=(index)=>dispatch(CompleteTodo(index));
```

> Reducer


Action只是描述了有事情发生了这一事实，并没有指明应用如何更新state，这正是reducer要做的事情。reducer就是一个函数，接受旧的state和action，返回新的state。
```
(previousState,action) => newState
```
永远不要在reducer里做如下操作：

 * 修改传入参数
 *  执行有副作用的操作，如API请求和路由跳转
 *  调用非纯函数，如Date.now()或Math.random()
 
 ```
 使用Object.assign()新建一个副本，不能这样使用Object.assign(state,{visibilityFilter:action.filter})，因为它会改变第一个参数的值。必须将第一个参数设置为空对象。
 在default情况下返回旧的state。遇到未知的action时，一定要返回旧的state。
 ```
 
 > Store
 
 使用action来描述发生了什么，使用reducers来根据action更新state的用法。`Store`就是把它们联系到一起的对象。Store有如下职责：
 * 维持应用的state
 * 提供getState()方法来获取state
 * 提供dispatch(action)方法更新state
 * 提供subscribe(listener)注册监听器

Redux应用只有一个单一的Store，当需要拆分处理数据的逻辑时，使用reducer组合，而不是创建多个store创建store的方式如下：
```
import { createStore } from 'redux'
import todoApp from './reducers'
let store=createStore(todoApp)
```
`createStore`的第二个参数可以设置初始状态，这对开发同构应用时非常有用，可以把服务器端生成的state转变后在浏览器端传递个应用。
```
let store=createStore(todoApp,window.STATE_FROM_SERVER);
```
发起Actions
```
import {addTodo,completeTodo,setVisibilityFilter,VisibilityFilters} from './actions'
console.log(store.getState());
//监听state更新时，打印日志
//注意subscribe()返回一个函数用来注销监听器
let unsubscribe=store.subscribe(()=>console.log(store.getState()))
发起一系列action
store.dispatch(addTodo('Learn about actions'))
store.dispatch(addTodo('Learn about reducers'))
store.dispatch(addTodo('Learn about store'))
store.dispatch(completeTodo(0));
store.dispatch(completeTodo(1));
store.dispatch(setVisibilityFilter(VisibilityFilters.SHOW_COMPLETED));
//停止监听state更新
unsubscribe();
```
> 数据流

严格的单向数据流是Redux架构的设计核心。Redux应用中的数据的生命周期遵循下面4个步骤：
* 调用store.dispatch(action) 
    
	action就是一个描述发生了什么的普通对象，可以在任何地方调用，包括组件中，XHR回调中，甚至定时器中。
  
 * Redux store调用传入reducer函数
 
     store会把两个参数传入reducer:当前的state树和aciton
     
 * 根reducer应该把多个子reducer输出合并成一个单一的state树
 * Redux store保存了根reducer返回的完整的state树

	这个新的树就是应用的下一个state，所有订阅store.subscribe(listener)的监听器都将被调用；监听器里可以调用`store.getState()`获取当前state。这样就可以应用新的state来更新UI了。
    
    
 将React连接到Redux
 * 首先需要获取从之前安装好的`react-redux`提供的Provider，并在渲染之前将根组件包装进<Provider>
 * 接着，我们想要通过`react-redux`提供的`connect()`方法将包装好的组件连接到Redux。任何一个从`connect`包装好的组件都可以得到一个dispatch方法作为组件的props，以及得到全局state中所需的任何内容。connect()的唯一参数是selector,此方法可以从Redux Store接受全局的state，然后返回组件中需要的props。

Redux的React绑定库包含了容器组件和展示组件相分离的开发思想。明智的做法是只在最顶层组件（如路由操作）里使用Redux，其余内容组件仅仅是展示性的，所有数据都通过props传入。

|         | 容器组件         | 展示组件  |
| ------------- |:-------------:| :-----:|
|Location|最顶层，路由处理|中间和子组件
|Aware of Redux|是|否
|读取数据|从Redux获取State|从props获取数据
|修改数据|向Redux派发actions|从props调用回调函数

参考文献：http://camsong.github.io/redux-in-chinese/index.html
