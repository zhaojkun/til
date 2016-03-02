# Bash,Zsh初始化脚本

Date: 2016-03-02

Tag: linux

在linux中配置环境变量经常会遇到不生效的时候，下边两个表格是用来展示`bash`和`zsh`两个shell中配置文件的执行顺序。

##### bash

其中`B1,B2,B3`表示按顺序查找，执行找到的第一个文件。


|         | Interactive login           | Interactive non-login  | Script| 
| ------------- |:-------------:| :-----:| :---------:|
| /etc/profile    | A |  |
| /etc/bash.bashrc     | A      |   |
| ~/.bashrc |       |  B |
| ~/.bash_profile| B1|
| ~/.bash_login| B2
| ~/.profile|B3
|BASH_ENV|||A|
|~/.bash_logout|C|

##### zsh 

|         | Interactive login           | Interactive non-login  | Script| 
| ------------- |:-------------:| :-----:| :---------:|
|/etc/zshenv|A|A|A
|~/.zshenv|B|B|B
|/etc/zprofile|C
|~/.zprofile|D
|/etc/zshrc|E|C
|~/.zshrc|F|D
|/etc/zlogin|G
|~/.zlogin|H
|~/.zlogout|I
|/etc/zlogout|J


所以对于bash来说，将配置信息放到~/.bashrc中，对于zsh来说，将配置信息放在~/.zshrc中。

参考文献：https://shreevatsa.wordpress.com/2008/03/30/zshbash-startup-files-loading-order-bashrc-zshrc-etc/
