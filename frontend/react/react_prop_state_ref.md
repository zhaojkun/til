# React Basic

一个`component`只能包含一个element，如果想返回多个element，那么就需要使用div等其他方式进行具体的返回。

##### prop
* propTypes里边设置属性的类型，如`React.PropTypes.string`,`React.PropTypes.number.isRequired`等
* defaultProp设置属性的默认值
* 在Component里边获取属性的方式是`this.props.xxx`，如`this.props.txt`

##### state
```
class App extends React.Component{
	constructor(){
    	super();
        this.state={
        	txt:'this is the state txt',
            cat:0
        }
    }
    update(e){
    	this.setState({txt:e.target.value})
    }
    render(){
    	return (
        	<div>
            <input type="text" onChange={this.update.bind(this)}/>
            </div>
        )
    }
}

```

##### ref
this.refs 顾名思义就是参考的意思，可以透过这个属性，指向内部元件，有点想dom的id的意思
```
 var App = React.createClass({
    getInitialState: function() {
      return {userInput: ''};
    },
    handleChange: function(e) {
      this.setState({userInput: e.target.value});
    },
    clearAndFocusInput: function() {
      // Clear the input
      this.setState({userInput: ''}, function() {
        // This code executes after the component is re-rendered

        this.refs.theInput.getDOMNode().focus();   // Boom! Focused!

      });
    },
    render: function() {
      return (
        <div>
          <div onClick={this.clearAndFocusInput}>
            Click to Focus and Reset
          </div>
          <input ref="theInput"
            value={this.state.userInput}
            onChange={this.handleChange}
          />
        </div>
      );
    }
  });
```
当component被产生出来之后，就会调用componentDidMount,此时就可以使用refs取得实际的dom对象了，然后可以进行相应的一些操作。

下面这个操作，是针对input做的focus的操作。
```
var Focus = React.createClass({
  componentDidMount() {
    this.refs.myText.getDOMNode().focus(); //指向myText物件，然後要求對DOM進行.focus() 操作
  },
  render() {
    return (
      <div>
        <p>set focus</p>
        <input type="text" ref="myText" />
      </div>
    );
  }
});
```
参考 : http://jamestw.logdown.com/posts/256990-usage-of-thisrefs 

date:2016-02-29
