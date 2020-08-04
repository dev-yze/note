### 一、Docker容器化技术介绍和使用场景



### 二、安装与镜像操作

#### (一)  win10安装

#### (二)  linux安装

```
安装环境: centos 7
安装条件: docker官方要求3.8以上
docker版本
	docker EE 企业版本
	docker CE 社区版本
关闭防火墙	systemctl stop firewalld.service vi /etc/selinux/config
安装 docker ce
安装 wget命令
下载阿里云docker社区版yum源
cd /etc/yum.repos.d/
wget http://mirrors.aliyun.com/docker-ce/linux/centos/docker-ce.repo
查看docker安装包
	yum list | grep docker
安装docker ce版本
	yum install -y docker-ce.x86_64
设置开机启动
	systemctl enable docker
更新xfsprogs
	yum -y update xfsprogs
启动docker
	systemctl start docker
查看版本
	docker version
查看详细版本
	docker info
```



#### (三)  镜像操作

##### 1、镜像搜索下载安装

- 查看本地镜像:  `docker images`
- 搜索镜像:  `docker search centos`
- 搜索镜像并过滤是官方的:  `docker search --filter "is-official=true" centos`
- 搜索镜像并过滤大于多少颗星星: `docker search --filter starts=10 centos`
- 下载centos7镜像: `docker pull centos:7`
- 修改本地镜像名字:  `docker tag centos:7 mycentos:1`
- 本地镜像的删除:  `docker rmi centos:7`

##### 2、容器操作

- 构建容器
- 查看本地所有的容器
- 查看本地正在运行的容器
- 停止容器
- 一次性停止所有容器
- 启动容器
- 重启容器
- 删除容器
- 强制删除容器
- 查看容器详细信息
- 进入容器

##### 3、文件复制与挂载





### 三、自定义镜像



### 四、网络模式与特权指令



### 五、实战：利用Compose操作容器



### 六、镜像仓库

