#### ab 压测工具
ab

#### 修改文件描述符限制数
直接用ulimit -n 65535，但重启后消失，新shell也没有修改。如何修改打开文件数限制并重启后生效呢？
1.修改limits.conf
`sudo vi /etc/security/limits.conf`
在文件尾部增加
`*  hard nofile 65535`
`*  soft nofile 65535`
保存文件
注：*表示所有用户名。