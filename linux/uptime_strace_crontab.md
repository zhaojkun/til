# Shell脚本学习指南---第13章进程

Date: 2016-03-20

Tag: linux uptime strace crontab

### uptime
`uptime`命令能够打印系统总共运行了多长时间和系统的平均负载。uptime命令可以显示的信息依次为：现在时间、系统已经运行了多长时间、目前多多少登陆用户、系统1分钟、5分钟、15分钟内的平均负载。

系统的平均负载是指在特定时间间隔内运行队列中的平均进程数。

如果每个CPU内核的当前活动进程数不大于3的话，那么系统的性能是良好的。如果每个CPU内核的任务数大于5，那么这台机器的性能有严重问题。`Load average are not normalized for the number of CPUs in a system`

### 删除进程

以删除进程来说，必须要知道有四个信号：`ABRT`,`HUP`,`KILL`和`TERM`

* `TERM`:快速地清除并离开，如果未指定信号，kill命令将送出此信号
* `ABRT`类似`TERM`，不过它会抑制清除操作，并产生今次那个内存影像的副本，并将其置于核心，即`program.core`或`core.pid`
* `HUP`信号，有点儿类似中断。对于大多数的`daemon`来说，它时常表示应先停止现在正在作的事情，然后准备处理新的工作，好像它重新被启动一样。例如，在改变配置文件后，HUP信号可令daemon重新设置文件。
* 有两个信号是没有任何进程可捕捉或忽略的:`KILL`和`STOP`

一般惯例是：
	
	1.先发出HUP信号给进程，让进程有机会优雅的中止
	2.如果没有马上离开，再试试TERM信号
	3.如果这样做还是无法离开，在使用最后手段KILL信号

### strace

strace用来跟踪进程执行时的系统调用和所接受的信号。其输出的每一行都是一条系统调用，等号左边是系统调用的函数名及其参数，右边是该调用的返回值。

命令参数
* -p pid   ：绑定到一个由pid对应的正在运行的进程，此参数常用来调试后台进程
* -e函数名  ：只追踪定义的函数名
* -e trace=set ：只追踪指定系列的系统调用，如-e trace=open,close,read,write，则表示只追踪这四个系统调用，默认值为set=all。
	* trace=file 只追踪有关文件操作的系统调用
	* trace=process 只追踪有关进程控制 的系统调用
	* trace=signal 只追踪与系统信号有关的系统调用
	* trace=ipc只追踪进程通信相关的系统调用	
* -f :除了跟踪当前进程外，还跟踪其子进程
* -f 尝试跟踪vfork调用，在-f时，vfork不被跟踪。
* -o file :将输出信息写到文件file中，而不是显示到标准错误输出（stderr）
* -u username 以username的UID和GID执行被跟踪的命令
* -T显示每一个调用所讯号的时间
* -tt在输出中的每一行前加上时间信息，微妙级
	
### crontab 定时任务

通过crontab命令，我们可以在固定的时间间隔执行指定的系统指令或shell script脚本。时间间隔的单位可以是分钟、小时、日、月、周及以上的任意组合。
```
crontab [-u user] [-e|-l|-r]
```
* -u user用来设定某个用的的crontab服务
* file: file是命令文件的名字，表示将file作为crontab的任务列表文件并载入crontab。如果在命令行中没有指定这个文件，crontab命令将接受标准输入上键入的命令，并将它们载入crontab
* -e 编辑某个用户的crontab文件内容，如果不指定用户，则表示编辑当前用户的crontab文件
* -l 显示某个用户的crontab文件内容
* -r 从/var/spool/cron目录中删除某个用户的crontab文件
* -i 在删除用户的crontab文件时给确定提示

##### crontab的文件格式
`分` `时` `日` `月` `星期` `要运行的命令`
* 第一列：分钟1~59
* 第二列：小时1~23（0表示子夜）
* 第三列：日1~31
* 第四列：月1-12
* 第五列：星期0~6（0表示星期日）
* 第六列：要运行的命令

`多个时间可以用逗号隔开，范围可以用连字符给出，星号可以做通配符，"/"代表每的意思，"*/5"表示每5个单元。空格用来分开字段`，如下示例：
* `*0,*5 9-16 * 1-5,9-12 1-5 /home/user/bin/i_love_cron.sh`表示会在夏天（六、七、八月）之外的每周周一到周五的上午9点到下午4点之间每隔5分钟执行一次`i_love_cron.sh`脚本
* `0 23-7/2,8 * * * echo "have a good dream"` 每天11点到早上8点之间每隔两个小时

参考文献：
* SHELL脚本学习指南
* https://wiki.archlinux.org/index.php/Cron_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87)
* http://linuxtools-rst.readthedocs.org/zh_CN/latest/tool/crontab.html
