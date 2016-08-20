# benchttp

###程序原理

该程序通过命令行传递相关参数，然后对目标发起HTTP请求，对其进行压测。支持的参数有：

* `-n `次数
* `-d` 持续时间
* `-c` 并发
* `-i` 是否只做`head`请求
* `-u` `BasicAuth`参数

在命令行参数定的时候，`flagNumber`,`flagDuration`,`flagConcurrency`默认值分别为0,0,1。如果`flagDuration`和`flagNumber`都为0，则默认设置`flagNumber`为1000，并且不能同时设置这两个值。

### 相关技术

* `log`包
  `log.SetFlags`函数可以设置日志输出的前缀。通过相关常量可以设置输出：`日期`,`时间`，`毫秒`,`文件名及行号`等
* `flag.Var`包
  `flag.Var`函数可以通过实现`flag.Value`接口来实现对命令行参数的自定义解析

### 其他

* 命名
  这个库的命名，相对来说命名都比较长。如相关flag参数都有前缀`flag`。

  通过命令行输入的url，命名为`argURL`，

  BasicAuth参数设置为`flagAuth`

* 并发

  使用`chan`实现HTTP的并发请求。首先根据并发数预创建`concurrency`个`http.Client`。然后在每次请求结束之后，再将其传递回来，以实现对并发数的限定。在创建`http.Client`时，设置`keepAlive`为`false`，以便在每次请求结束之后关闭连接。

* repo地址：https://github.com/siadat/benchttp
