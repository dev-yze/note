ssh安装

安装ssh服务

检测openssh-server是否安装

```
yum list installed | grep openssh-server

yum install openssh-server
```

配置

```
cd /etc/ssh
vim sshd_config
去掉下面注释		
		Port 22
        ListenAddress 0.0.0.0
        ListerAddress ::
        PermiRootLogin yes
        PasswordAuthentication yes
```

启动

```
sudo service sshd start
// 检查sshd服务是否开启
ps -ef|grep sshd
// 查看ip地址
ip addr
// 将ssh服务添加至自启动列表
systemctl enable sshd.service
```

