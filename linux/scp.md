#Scp

Date: 2016-03-07

Tag: linux

scp 命令可以在linux之间复制文件和目录，命令的基本格式：

```
  scp [可选参数] file_source file_target
```
#### 从本地到远端

复制文件：
 * `scp local_file remote_username@remote_ip:remote_folder`
 * `scp local_file remote_username@remote_ip:remote_file`
 * `scp local_file remote_ip:remote_folder`
 * `scp local_file remote_ip:remote_file`

复制目录：
* `scp -r local_folder remote_username@remote_ip:remote_folder`
* `scp -r local_folder remote_ip:remote_folder`

#### 从远端到本地

  * `scp root@www.cumt.edu.cn:/home/root/others/music/a.txt ./`
  * `scp root@www.cumt.edu.cn:/home/root/others/music ./`

#### 可能用到的几个参数
* -v 大和多数linux命令中的-v意思一样，用来显示进度，可以用来查看连接，认证或是配置错误
* -C 使能压缩选项
*  -P 选择端口，注意-p 已经被rcp使用
*   -4 强行使用IPV4地址
*   -6 强行使用IPV6地址
