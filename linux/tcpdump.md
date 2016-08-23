# tcpdump

#### 命令行参数

* `-n` 直接显示IP地址，不对其进行解析
* `-nn` 不对IP地址与port 进行协议解析
* `-X` 对数据包的内容显示十六进制与ascii
* `-S` 显示seq number的绝对数字
* `-s`指定数据包的抓取大小。`0`表示全部抓取
* `-c` 仅抓取若干个包，然后定制
* `icmp`只抓取icmp包

#### Filter

通过表达式可以对数据包进行过滤。共有三种表达式：

* type
  * host
  * net
  * port
* dir
  * src
  * dst
  * src or dst
  * src and dst
* proto

例如：

* `tcpdump host 1.2.3.4`
* `tcpdump src 2.3.4.5`
* `tcpdump dst 3.4.5.6`
* `tcpdump net 1.2.3.0/24`
* `tcpdump icmp`
* `tcpdump port 3389`
* `tcpdump src port 1025`
* `tcpdump src port 1025 and tcp`
* `tcpdump udp and src port 53`
* `tcpdump portrange 21-23 #Port Range`
* `tcpdump less 32 #根据数据包大小`
* `tcpdump greater 128`
* `tcpdump 'tcp[13] & 16 !=0' # ACK`

参考文献：

* https://danielmiessler.com/study/tcpdump/
