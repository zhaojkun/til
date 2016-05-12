# React render html

Date: 2016-03-04

Tag: react

react中如下进行渲染HTML，其中html字符串保存在state中。
```
 <div dangerouslySetInnerHTML={{
             __html:this.state.html,
         }}>
  </div>
```
