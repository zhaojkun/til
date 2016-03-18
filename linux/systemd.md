# init & systemd

### init
当我们需要开机启动自己的脚本是，只需要将可执行脚本丢在`/etc/init.d`目录下，然后在`/etc/rc.d/rc*.d`中建立软连接即可。

### systemd

使用systemd，就不需要再用`init`了，systemd取代了initd,成为系统的第一个进程(PID等于1)，其他进程都是它的子进程。`systemctl --version`用来查看`Systemd`的版本

unit文件位于`/etc/systemd/system`，配置文件示例：
```
[Unit]
Description=MyApp
After=docker.service
Requires=docker.service

[Service]
TimeoutStartSec=0
ExecStartPre=-/usr/bin/docker kill busybox1
ExecStartPre=-/usr/bin/docker rm busybox1
ExecStartPre=/usr/bin/docker pull busybox
ExecStart=/usr/bin/docker run --name busybox1 busybox /bin/sh -c "while true;do echo Hello World;sleep 1;done"

[Install]
WantedBy=multi-user.target
```
具体:
* `Description`会显示在`systemd`的日志和其他几个位置。
* `After`和`Requires`表示这个服务只有在需要的服务启动成功之后才运行，可以定义多个类似的额服务



参考：
* https://www.freedesktop.org/software/systemd/man/systemd.service.html
* http://blog.jobbole.com/98667/?utm_source=top.jobbole.com&utm_medium=relatedArticles
