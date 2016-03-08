# Iptables

Date: 2016-03-08

Tag: net linux

Linux内核通过`netfilter`模块实现网络访问控制功能，在用户层我们可以通过iptables程序对netfilter进行控制管理。

| **Filtering point(chain)**| | **Table** |  |
| ------------- |:-------------:| :-----:|:-------------:| :-----:|
| | **filter** |  **net**  |**mangle** |
| INPUT| Y |   | Y |
| FORWARD| Y |   | Y |
| OUTPUT | Y | Y | Y |
| PREROUTING |  |Y | Y |
| POSTROUTING |  |Y | Y |



* `filtering point`为过滤点
*  filter用于对数据进行过滤
*  net用于对数据包的源，目标地址进行修改
*  mangle用于对数据包进行高级修改


![](http://ww1.sinaimg.cn/mw1024/4a3f01ffjw1f1pehipkqbj20d209jq3g.jpg)

### 常用的功能
* 作为服务器使用
  * 过滤到本机的流量  input链，filter表
  * 过滤到本机打出的流量  output链，filter表
* 作路由器使用
  * 过滤转发的流量  forward链,filter表
  * 对转发数据的源，目的IP进行修改（NAT功能） prerouting/postrouting链，nat表

`不同的功能是由不同的表实现的`

### 规则

* iptables通过规则对数据进行访问控制
* 一个规则使用一行配置
* 规则按顺序排列
* 当收到，发出，转发数据包时，使用规则对数据包进行匹配，按规则顺序进行逐条匹配
* 数据包按照第一个匹配上的规则执行相关动作：丢弃，放行，修改
* 没有匹配规则，则使用默认动作（每个chain拥有各自默认的动作）

通过iptables命令创建一个规则，一条规则包含以下几个部分：
iptables -t 表 -A 链  匹配属性  动作
如`iptables -t filter -A input -s 192.168.1.1 -j DROP`
* 表:规定使用的表（filter，nat,mangle，不同表有不同功能）
* 链：规定过滤点
* 匹配属性：规定匹配数据包的特征
* 匹配后的动作：放行、丢弃、记录

### 常用命令

* 列出现有的iptables规则：`iptables -L`
* 插入一个规则:`iptables -i input 3 -p tcp --dport 22 -j accept`
* 删除一个iptables规则：
  * `iptables -D input 3`
  * `iptables -D input -s 192.18.1.2 -j DROP`

匹配参数
* 基于ip地址：
  * -s 192.168.1.1
  * -d 10.0.0.0/8
* 基于接口：
  * -i eth0
  * -o eth1
* 排除参数:
  * -s "!" 19.168.1.0/24
* 基于协议及端口：
  * -p tcp --dport 23
  * -p udp --sport 53
  * -p icmp
  
参考文献：
* https://www.youtube.com/watch?v=RO3ug2Y5q3o 
* https://www.frozentux.net/iptables-tutorial/cn/iptables-tutorial-cn-1.1.19.html