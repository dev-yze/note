一、安装过程

```
1、获取资源
	wget http://download.redis.io/releases/redis-4.0.8.tar.gz
2、解压安装
	tar xzvf redis-4.0.8.tar.gz
	cd redis-4.0.8
	make
	cd src
	make install PREFIX=/usr/local/webserver/redis
3、移动配置文件
	cd ../
	mkdir /usr/local/webserver/redis/etc
	cp redis.conf /usr/local/webserver/redis/etc
4、配置redis为后台启动(将配置文件redis.conf中daemonize no改为yes)
	vim /usr/local/webserver/redis/etc/redis.conf
5、将redis加入开机启动(在rc.local文件中添加)
	vim /etc/rc.local
	/usr/local/webserver/redis/bin/redis-server /usr/local/webserver/redis/etc/redis.conf 
6、通过指定配置文件启动redis
	/usr/local/webserver/redis/bin/redis-server /usr/local/webserver/redis/etc/redis.conf
7、将redis指令添加到全局命令
	cp /usr/local/webserver/redis/bin/redis-server /usr/local/bin/
	cp /usr/local/webserver/redis/bin/redis-cli /usr/local/bin/
8、设置redis密码
	运行redis-cli
		config get requirepass
		config set requirepass password
	重启redis
	登录
		redis-cli -h 127.0.0.1 -p 6379 -a password
		或
		redis-cli
		auth 'password'
9、外网访问
	1、阿里云开放端口
	2、设置配置文件
		将redis.conf 里的bind 127.0.0.1 前面加#
		修改daemonize和protected-mode属性
			config get daemonize
			config set daemonize no
			config get protected-mode
			config set protected-mode yes

```



二、常用命令操作

```
1、启动redis
	redis-server &
	或redis-server
2、检测后台是否存在
	ps -ef|grep redis
3、检测端口是否在监听
	netstat -lntp | grep 6379
4、关闭redis
	redis-cli shutdown
```

