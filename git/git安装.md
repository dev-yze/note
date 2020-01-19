一、linux源码安装

​	默认安装路径为:  /usr/libexec/git-core

​	

```
// 下载
[root@yang develop]# wget https://github.com/git/git/archive/v2.22.0.tar.gz
// 解压
[root@yang develop]# tar -zxvf v2.22.0.tar.gz
// 下载依赖
[root@yang develop]# yum install curl-devel expat-devel gettext-devel openssl-devel zlib-devel gcc perl-ExtUtils-MakeMaker
// 卸载安装依赖时安装的git
[root@yang develop]# yum remove git
// 编译安装
[root@yang git-2.22.0]# make prefix=/usr/local/git/ all
[root@yang git-2.22.0]# make prefix=/usr/local/git install
// 配置环境变量
vim /etc/profile
加入
PATH=$PATH:/usr/local/git/bin
export PATH
// 更新源文件
[root@yang git-2.22.0]#source /etc/profile
// 查看git版本
git --version

```



二、使用yum安装

/ucd 