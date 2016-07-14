## vagrant环境
####相关软件
1. virtux box  [https://www.virtualbox.org/wiki/Downloads](https://www.virtualbox.org/wiki/Downloads)
2. vagrant  [https://www.vagrantup.com/](https://www.vagrantup.com/)
3. box  [http://www.vagrantbox.es/](http://www.vagrantbox.es/)

####相关命令
1. vagrant add box ubuntu xxx
2. vagrant init ubuntu `(切换到相关目录)`
3. vagrant up
4. vagrant init
5. vagrant up
6. vagrant ssh

## Linux环境
####换阿里源
1.`sudo cp /etc/apt/sources.list /etc/apt/sources.list_backup`
2.`sudo vim /etc/apt/sources.list`
3.替换为以下内容
`#Trusty(14.04)
deb http://mirrors.aliyun.com/ubuntu/ trusty main restricted universe multiverse
deb http://mirrors.aliyun.com/ubuntu/ trusty-security main restricted universe multiverse
deb http://mirrors.aliyun.com/ubuntu/ trusty-updates main restricted universe multiverse
deb http://mirrors.aliyun.com/ubuntu/ trusty-proposed main restricted universe multiverse
deb http://mirrors.aliyun.com/ubuntu/ trusty-backports main restricted universe multiverse
deb-src http://mirrors.aliyun.com/ubuntu/ trusty main restricted universe multiverse
deb-src http://mirrors.aliyun.com/ubuntu/ trusty-security main restricted universe multiverse
deb-src http://mirrors.aliyun.com/ubuntu/ trusty-updates main restricted universe multiverse
deb-src http://mirrors.aliyun.com/ubuntu/ trusty-proposed main restricted universe multiverse
deb-src http://mirrors.aliyun.com/ubuntu/ trusty-backports main restricted universe multiverse`
