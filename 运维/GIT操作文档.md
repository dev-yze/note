## 基本提交命令

```c
git add --a								##将文件添加到暂存区
git commit -m ""						##将暂存区的内容提交到当前分支
git pull origin develop					##拉取服务器端代码比较
git push origin develop					##上传代码到服务器
    
git reset --hard commitId 				## 版本回退
    
git 
```

#### 二、版本回退和信息查询

#### 版本回到上一个   git reset --hard HEAD^

####  回到指定版本      git reset --hard commitId

##查看每次提交的commitId    git reflog

```
查看config
   git config -l
   git config --system --list  // 系统config
   git config --global --list  // 全局config
   git config --local --list   // 当前config
设置config
	git config user.name ""
	git config --global user.name
	git config --global --unset user.name



```



#### 三、分支管理和日志查看

##### 1、仓库管理



##### 2、分支管理

```
查看仓库所有分支: git branch (-av 查看远程分支)
新建分支: git branch name
切换分支: git checkout name | git switch name
切换并创建分支:  git checkout -b name | git switch -c dev
删除分支: git branch -d name
合并分支: git merge name
分支改名: git branch -m oldname newname
创建并提交到远程分支: git push --set-upstream origin dev
删除远程分支: git push origin --delete branchName
```

##### 3、查看状态和日志

```
查看日志(最近->最远)：git log     简略输出: git log --pretty=online
查看当前状态: git status
根据status查看修改过的文件: git dif filename
	git diff   // 查看执行git status的结果的详细信息
	git diff  // 尚未缓存的改动
	git diff --cached  // 查看已缓存的改动
	git diff HEAD   // 查看已缓存的与尚未缓存的所有改动
	git diff --start
```







4、修改属性

- remote

  ```
  18856@A-yze MINGW64 /g/Code/zhuolu/develop/web/zhuolu-web-pages (master)
  $ git remote -v
  origin  git@github.com:develop-yang/vue-temp.git (fetch)
  origin  git@github.com:develop-yang/vue-temp.git (push)
  
  18856@A-yze MINGW64 /g/Code/zhuolu/develop/web/zhuolu-web-pages (master)
  $ git remote remove origin
  
  18856@A-yze MINGW64 /g/Code/zhuolu/develop/web/zhuolu-web-pages (master)
  $ git remote -v
  ```

  

#### 四、临时保存和回复修改

```
## 保存
git stash [save message]
## 所有保存记录列表
git stash list
## 恢复，通过git stash list可查看具体值，只能恢复一次
git stash pop stash@{num}
## 恢复，通过git stash list查看具体值，可回复多次
git stash apply stash@{num}
## 删除某个保存
git stash drop stash@{num}
## 删除所有保存
git stash clear
    
git stash show 显示做了哪些改动,默认第一个存储
git stash show stash@{$num} -p

```



#### 五、操作

##### 1、初始化仓库

```
## 提交数据
git init
git config user.email "18856235862@163.com"
git config user.name "develop-yang"
git add --a
git commit -m ""
## 连接到远程仓库
git remote add origin git@163:develop-yang/vue-temp.git
## 推送到master分支
git push -u origin master
## 创建其它分支,推送
git checkout -b vue+axios
git push -u origin vue+axios
```

2、分支管理

3、状态查询和日志查询

4、临时保存和回复修改

#### 六、git多账号管理

注意：如果没有.ssh文件夹, 先设置全局用户名和密码，后取消

##### 1、生成密钥，产生默认文件id_rsa、id_rsa.pub

```
ssh-keygen -t rsa -C "12356@qq.com"
```

##### 2、将id_rsa*.pub中内容复制到github设置中的SSH and GPG key中， new SSH key

##### 3、配置config(自己创建)

操作实例:

```c
18856@DESKTOP-EBLB3S0 MINGW64 ~
$ cd ~/.ssh
18856@DESKTOP-EBLB3S0 MINGW64 ~/.ssh
$ ls     // 浏览目录
config  id_rsa.pub  id_rsa_163.pub  id_rsa_google.pub
id_rsa  id_rsa_163  id_rsa_google   known_hosts
18856@DESKTOP-EBLB3S0 MINGW64 ~/.ssh
$
18856@DESKTOP-EBLB3S0 MINGW64 ~/.ssh
$ cat config            // 查看多账户管理配置文件  ，如果git新安装，创建touch config
# 163
Host 163
   HostName github.com
   User develop-yang
   IdentityFile ~/.ssh/id_rsa_163
# zhuolu
Host zl
   HostName 47.99.192.207
   User yangzhangen
   IdentityFile ~/.ssh/id_rsa
# google
Host google
   HostName github.com
   User yangzhangen
   IdentityFile ~/.ssh/id_rsa_google

18856@DESKTOP-EBLB3S0 MINGW64 ~/.ssh
$

```



##### 4、将私钥交给ssh-agent代管

```
ssh-agent bash
ssh-add id_rsa_163
ssh-add id_rsa_google
```

##### 5、取消全局命名

`git config --global --unset user.name`

`git config --global --unset user.email`

```c
18856@DESKTOP-EBLB3S0 MINGW64 ~/.ssh
$ git config --list
core.symlinks=false
core.autocrlf=true
core.fscache=true
color.diff=auto
color.status=auto
color.branch=auto
color.interactive=true
help.format=html
rebase.autosquash=true
http.sslcainfo=G:/develop/Git/mingw64/ssl/certs/ca-bundle.crt
http.sslbackend=openssl
diff.astextplain.textconv=astextplain
filter.lfs.clean=git-lfs clean -- %f
filter.lfs.smudge=git-lfs smudge -- %f
filter.lfs.process=git-lfs filter-process
filter.lfs.required=true
credential.helper=manager
user.name=yangzhangen
user.email=12356@qq.come
18856@DESKTOP-EBLB3S0 MINGW64 ~/.ssh
$ git config --global --unset user.name
18856@DESKTOP-EBLB3S0 MINGW64 ~/.ssh
$ git config --global --unset user.email
18856@DESKTOP-EBLB3S0 MINGW64 ~/.ssh
$ git config --list
core.symlinks=false
core.autocrlf=true
core.fscache=true
color.diff=auto
color.status=auto
color.branch=auto
color.interactive=true
help.format=html
rebase.autosquash=true
http.sslcainfo=G:/develop/Git/mingw64/ssl/certs/ca-bundle.crt
http.sslbackend=openssl
diff.astextplain.textconv=astextplain
filter.lfs.clean=git-lfs clean -- %f
filter.lfs.smudge=git-lfs smudge -- %f
filter.lfs.process=git-lfs filter-process
filter.lfs.required=true
credential.helper=manager
```



##### 6、为具体项目配置对应的email和user

```
18856@DESKTOP-EBLB3S0 MINGW64 /g/Code/zhuolu/develop
$ cd moose-vue/
18856@DESKTOP-EBLB3S0 MINGW64 /g/Code/zhuolu/develop/moose-vue (develop)
$ git add --a
18856@DESKTOP-EBLB3S0 MINGW64 /g/Code/zhuolu/develop/moose-vue (develop)
$ git commit -m "新增加或修改bug"

*** Please tell me who you are.
Run
  git config --global user.email "you@example.com"
  git config --global user.name "Your Name"
to set your account's default identity.
Omit --global to set the identity only in this repository.
fatal: unable to auto-detect email address (got '18856@DESKTOP-EBLB3S0.(none)')
// 配置邮箱
18856@DESKTOP-EBLB3S0 MINGW64 /g/Code/zhuolu/develop/moose-vue (develop)
$ git config user.email "12356@qq.com"
// 配置密码
18856@DESKTOP-EBLB3S0 MINGW64 /g/Code/zhuolu/develop/moose-vue (develop)
$ git config user.name "yangzhangen"

18856@DESKTOP-EBLB3S0 MINGW64 /g/Code/zhuolu/develop/moose-vue (develop)
$ git commit -m "新增加或修改bug"
[develop 1124d61] 新增加或修改bug
 9 files changed, 362 insertions(+), 40 deletions(-)
 create mode 100644 src/views/sales/machine-disinfection/index.vue
18856@DESKTOP-EBLB3S0 MINGW64 /g/Code/zhuolu/develop/moose-vue (develop)
$ git pull
Already up to date.
18856@DESKTOP-EBLB3S0 MINGW64 /g/Code/zhuolu/develop/moose-vue (develop)
$ git push origin develop
remote:
remote: To create a merge request for develop, visit:
remote:   http://47.99.192.207/gitlab/wash/moose-vue/merge_requests/new?merge_request%5Bsource_branch%5D=develop
remote:
To 47.99.192.207:wash/moose-vue.git
   c3731ce..1124d61  develop -> develop
```



##### 7、克隆对应项目

```
## 163账号
git clone git@163:develop-yang/dorm.git
## google账号
git clone git@google:develop-yang/dorm.git
## zl账户
git clone git@zl:develop-yang/dorm.git
```



#### 七、git安装

1、linux源码安装

```c
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

// 更新源文件
[root@yang git-2.22.0]#source /etc/profile
// 查看git版本
git --version
```



#### 八、gitlab安装和使用

安装步骤

```
[root@iZbp1guce5swcrv200qekvZ webserver]# yum install -y curl openssh-server openssh-clients cronie
Loaded plugins: fastestmirror
Determining fastest mirrors
base                                                                           | 3.6 kB  00:00:00
epel                                                                           | 4.7 kB  00:00:00
extras                                                                         | 2.9 kB  00:00:00
updates                                                                        | 2.9 kB  00:00:00
(1/5): epel/x86_64/group_gz                                                    |  95 kB  00:00:00
(2/5): extras/7/x86_64/primary_db                                              | 205 kB  00:00:00
(3/5): epel/x86_64/updateinfo                                                  | 1.0 MB  00:00:00
(4/5): epel/x86_64/primary_db                                                  | 6.8 MB  00:00:00
(5/5): updates/7/x86_64/primary_db                                             | 3.0 MB  00:00:00
Package openssh-server-7.4p1-21.el7.x86_64 already installed and latest version
Package openssh-clients-7.4p1-21.el7.x86_64 already installed and latest version
Package cronie-1.4.11-23.el7.x86_64 already installed and latest version
Resolving Dependencies
--> Running transaction check
---> Package curl.x86_64 0:7.29.0-54.el7_7.2 will be updated
---> Package curl.x86_64 0:7.29.0-57.el7 will be an update
--> Processing Dependency: libcurl = 7.29.0-57.el7 for package: curl-7.29.0-57.el7.x86_64
--> Running transaction check
---> Package libcurl.x86_64 0:7.29.0-54.el7_7.2 will be updated
--> Processing Dependency: libcurl = 7.29.0-54.el7_7.2 for package: libcurl-devel-7.29.0-54.el7_7.2.x8                      6_64
---> Package libcurl.x86_64 0:7.29.0-57.el7 will be an update
--> Running transaction check
---> Package libcurl-devel.x86_64 0:7.29.0-54.el7_7.2 will be updated
---> Package libcurl-devel.x86_64 0:7.29.0-57.el7 will be an update
base/7/x86_64/filelists_db                                                     | 7.1 MB  00:00:00
--> Finished Dependency Resolution

Dependencies Resolved

======================================================================================================
 Package                    Arch                Version                       Repository         Size
======================================================================================================
Updating:
 curl                       x86_64              7.29.0-57.el7                 base              270 k
Updating for dependencies:
 libcurl                    x86_64              7.29.0-57.el7                 base              223 k
 libcurl-devel              x86_64              7.29.0-57.el7                 base              303 k

Transaction Summary
======================================================================================================
Upgrade  1 Package (+2 Dependent packages)

Total download size: 796 k
Downloading packages:
Delta RPMs disabled because /usr/bin/applydeltarpm not installed.
(1/3): curl-7.29.0-57.el7.x86_64.rpm                                           | 270 kB  00:00:00
(2/3): libcurl-7.29.0-57.el7.x86_64.rpm                                        | 223 kB  00:00:00
(3/3): libcurl-devel-7.29.0-57.el7.x86_64.rpm                                  | 303 kB  00:00:00
------------------------------------------------------------------------------------------------------
Total                                                                 1.4 MB/s | 796 kB  00:00:00
Running transaction check
Running transaction test
Transaction test succeeded
Running transaction
  Updating   : libcurl-7.29.0-57.el7.x86_64                                                       1/6
  Updating   : curl-7.29.0-57.el7.x86_64                                                          2/6
  Updating   : libcurl-devel-7.29.0-57.el7.x86_64                                                 3/6
  Cleanup    : libcurl-devel-7.29.0-54.el7_7.2.x86_64                                             4/6
  Cleanup    : curl-7.29.0-54.el7_7.2.x86_64                                                      5/6
  Cleanup    : libcurl-7.29.0-54.el7_7.2.x86_64                                                   6/6
  Verifying  : curl-7.29.0-57.el7.x86_64                                                          1/6
  Verifying  : libcurl-devel-7.29.0-57.el7.x86_64                                                 2/6
  Verifying  : libcurl-7.29.0-57.el7.x86_64                                                       3/6
  Verifying  : curl-7.29.0-54.el7_7.2.x86_64                                                      4/6
  Verifying  : libcurl-7.29.0-54.el7_7.2.x86_64                                                   5/6
  Verifying  : libcurl-devel-7.29.0-54.el7_7.2.x86_64                                             6/6

Updated:
  curl.x86_64 0:7.29.0-57.el7

Dependency Updated:
  libcurl.x86_64 0:7.29.0-57.el7                 libcurl-devel.x86_64 0:7.29.0-57.el7

Complete!
[root@iZbp1guce5swcrv200qekvZ webserver]# lokkit -s http -s ssh
-bash: lokkit: command not found
[root@iZbp1guce5swcrv200qekvZ webserver]# yum install lokkit
Loaded plugins: fastestmirror
Loading mirror speeds from cached hostfile
Resolving Dependencies
--> Running transaction check
---> Package system-config-firewall-base.noarch 0:1.2.29-10.el7 will be installed
--> Processing Dependency: iptables-ipv6 for package: system-config-firewall-base-1.2.29-10.el7.noarch
--> Running transaction check
---> Package iptables-services.x86_64 0:1.4.21-34.el7 will be installed
--> Processing Dependency: iptables = 1.4.21-34.el7 for package: iptables-services-1.4.21-34.el7.x86_6                      4
--> Running transaction check
---> Package iptables.x86_64 0:1.4.21-33.el7 will be updated
---> Package iptables.x86_64 0:1.4.21-34.el7 will be an update
--> Finished Dependency Resolution

Dependencies Resolved

======================================================================================================
 Package                               Arch             Version                  Repository      Size
======================================================================================================
Installing:
 system-config-firewall-base           noarch           1.2.29-10.el7            base           414 k
Installing for dependencies:
 iptables-services                     x86_64           1.4.21-34.el7            base            52 k
Updating for dependencies:
 iptables                              x86_64           1.4.21-34.el7            base           432 k

Transaction Summary
======================================================================================================
Install  1 Package  (+1 Dependent package)
Upgrade             ( 1 Dependent package)

Total download size: 899 k
Is this ok [y/d/N]: y
Downloading packages:
Delta RPMs disabled because /usr/bin/applydeltarpm not installed.
(1/3): iptables-services-1.4.21-34.el7.x86_64.rpm                              |  52 kB  00:00:00
(2/3): iptables-1.4.21-34.el7.x86_64.rpm                                       | 432 kB  00:00:00
(3/3): system-config-firewall-base-1.2.29-10.el7.noarch.rpm                    | 414 kB  00:00:00
------------------------------------------------------------------------------------------------------
Total                                                                 1.3 MB/s | 899 kB  00:00:00
Running transaction check
Running transaction test
Transaction test succeeded
Running transaction
  Updating   : iptables-1.4.21-34.el7.x86_64                                                      1/4
  Installing : iptables-services-1.4.21-34.el7.x86_64                                             2/4
  Installing : system-config-firewall-base-1.2.29-10.el7.noarch                                   3/4
  Cleanup    : iptables-1.4.21-33.el7.x86_64                                                      4/4
  Verifying  : iptables-services-1.4.21-34.el7.x86_64                                             1/4
  Verifying  : iptables-1.4.21-34.el7.x86_64                                                      2/4
  Verifying  : system-config-firewall-base-1.2.29-10.el7.noarch                                   3/4
  Verifying  : iptables-1.4.21-33.el7.x86_64                                                      4/4

Installed:
  system-config-firewall-base.noarch 0:1.2.29-10.el7

Dependency Installed:
  iptables-services.x86_64 0:1.4.21-34.el7

Dependency Updated:
  iptables.x86_64 0:1.4.21-34.el7

Complete!
[root@iZbp1guce5swcrv200qekvZ webserver]# lokkit -s http -s ssh
[root@iZbp1guce5swcrv200qekvZ webserver]# curl -sS https://packages.gitlab.com/install/repositories/gi                      tlab/gitlab-ce/script.rpm.sh | sudo bash

Detected operating system as centos/7.
Checking for curl...
Detected curl...
Downloading repository file: https://packages.gitlab.com/install/repositories/gitlab/gitlab-ce/config_                      file.repo?os=centos&dist=7&source=script
done.
Installing pygpgme to verify GPG signatures...
Loaded plugins: fastestmirror
Loading mirror speeds from cached hostfile
gitlab_gitlab-ce-source/signature                                              |  862 B  00:00:00
Retrieving key from https://packages.gitlab.com/gitlab/gitlab-ce/gpgkey
Importing GPG key 0x51312F3F:
 Userid     : "GitLab B.V. (package repository signing key) <packages@gitlab.com>"
 Fingerprint: f640 3f65 44a3 8863 daa0 b6e0 3f01 618a 5131 2f3f
 From       : https://packages.gitlab.com/gitlab/gitlab-ce/gpgkey
Retrieving key from https://packages.gitlab.com/gitlab/gitlab-ce/gpgkey/gitlab-gitlab-ce-3D645A26AB9FB                      D22.pub.gpg
gitlab_gitlab-ce-source/signature                                              |  951 B  00:00:01 !!!
gitlab_gitlab-ce-source/primary                                                |  175 B  00:00:06
Package pygpgme-0.3-9.el7.x86_64 already installed and latest version
Nothing to do
Installing yum-utils...
Loaded plugins: fastestmirror
Loading mirror speeds from cached hostfile
Resolving Dependencies
--> Running transaction check
---> Package yum-utils.noarch 0:1.1.31-54.el7_8 will be installed
--> Processing Dependency: python-kitchen for package: yum-utils-1.1.31-54.el7_8.noarch
--> Processing Dependency: libxml2-python for package: yum-utils-1.1.31-54.el7_8.noarch
--> Running transaction check
---> Package libxml2-python.x86_64 0:2.9.1-6.el7.4 will be installed
--> Processing Dependency: libxml2 = 2.9.1-6.el7.4 for package: libxml2-python-2.9.1-6.el7.4.x86_64
---> Package python-kitchen.noarch 0:1.1.1-5.el7 will be installed
--> Processing Dependency: python-chardet for package: python-kitchen-1.1.1-5.el7.noarch
--> Running transaction check
---> Package libxml2.x86_64 0:2.9.1-6.el7_2.3 will be updated
---> Package libxml2.x86_64 0:2.9.1-6.el7.4 will be an update
---> Package python-chardet.noarch 0:2.2.1-3.el7 will be installed
--> Finished Dependency Resolution

Dependencies Resolved

======================================================================================================
 Package                    Arch               Version                      Repository           Size
======================================================================================================
Installing:
 yum-utils                  noarch             1.1.31-54.el7_8              updates             122 k
Installing for dependencies:
 libxml2-python             x86_64             2.9.1-6.el7.4                base                247 k
 python-chardet             noarch             2.2.1-3.el7                  base                227 k
 python-kitchen             noarch             1.1.1-5.el7                  base                267 k
Updating for dependencies:
 libxml2                    x86_64             2.9.1-6.el7.4                base                668 k

Transaction Summary
======================================================================================================
Install  1 Package  (+3 Dependent packages)
Upgrade             ( 1 Dependent package)

Total download size: 1.5 M
Downloading packages:
Delta RPMs disabled because /usr/bin/applydeltarpm not installed.
(1/5): libxml2-python-2.9.1-6.el7.4.x86_64.rpm                                 | 247 kB  00:00:00
(2/5): libxml2-2.9.1-6.el7.4.x86_64.rpm                                        | 668 kB  00:00:00
(3/5): python-chardet-2.2.1-3.el7.noarch.rpm                                   | 227 kB  00:00:00
(4/5): python-kitchen-1.1.1-5.el7.noarch.rpm                                   | 267 kB  00:00:00
(5/5): yum-utils-1.1.31-54.el7_8.noarch.rpm                                    | 122 kB  00:00:00
------------------------------------------------------------------------------------------------------
Total                                                                 5.8 MB/s | 1.5 MB  00:00:00
Running transaction check
Running transaction test
Transaction test succeeded
Running transaction
  Updating   : libxml2-2.9.1-6.el7.4.x86_64                                                       1/6
  Installing : libxml2-python-2.9.1-6.el7.4.x86_64                                                2/6
  Installing : python-chardet-2.2.1-3.el7.noarch                                                  3/6
  Installing : python-kitchen-1.1.1-5.el7.noarch                                                  4/6
  Installing : yum-utils-1.1.31-54.el7_8.noarch                                                   5/6
  Cleanup    : libxml2-2.9.1-6.el7_2.3.x86_64                                                     6/6
  Verifying  : python-chardet-2.2.1-3.el7.noarch                                                  1/6
  Verifying  : python-kitchen-1.1.1-5.el7.noarch                                                  2/6
  Verifying  : libxml2-python-2.9.1-6.el7.4.x86_64                                                3/6
  Verifying  : libxml2-2.9.1-6.el7.4.x86_64                                                       4/6
  Verifying  : yum-utils-1.1.31-54.el7_8.noarch                                                   5/6
  Verifying  : libxml2-2.9.1-6.el7_2.3.x86_64                                                     6/6

Installed:
  yum-utils.noarch 0:1.1.31-54.el7_8

Dependency Installed:
  libxml2-python.x86_64 0:2.9.1-6.el7.4              python-chardet.noarch 0:2.2.1-3.el7
  python-kitchen.noarch 0:1.1.1-5.el7

Dependency Updated:
  libxml2.x86_64 0:2.9.1-6.el7.4

Complete!
Generating yum cache for gitlab_gitlab-ce...
Importing GPG key 0x51312F3F:
 Userid     : "GitLab B.V. (package repository signing key) <packages@gitlab.com>"
 Fingerprint: f640 3f65 44a3 8863 daa0 b6e0 3f01 618a 5131 2f3f
 From       : https://packages.gitlab.com/gitlab/gitlab-ce/gpgkey
Generating yum cache for gitlab_gitlab-ce-source...

The repository is setup! You can now install packages.
[root@iZbp1guce5swcrv200qekvZ webserver]# yum install -y gitlab-ce
Loaded plugins: fastestmirror
Loading mirror speeds from cached hostfile
Resolving Dependencies
--> Running transaction check
---> Package gitlab-ce.x86_64 0:13.1.4-ce.0.el7 will be installed
--> Processing Dependency: policycoreutils-python for package: gitlab-ce-13.1.4-ce.0.el7.x86_64
--> Running transaction check
---> Package policycoreutils-python.x86_64 0:2.5-34.el7 will be installed
--> Processing Dependency: policycoreutils = 2.5-34.el7 for package: policycoreutils-python-2.5-34.el7                      .x86_64
--> Processing Dependency: setools-libs >= 3.3.8-4 for package: policycoreutils-python-2.5-34.el7.x86_                      64
--> Processing Dependency: libsemanage-python >= 2.5-14 for package: policycoreutils-python-2.5-34.el7                      .x86_64
--> Processing Dependency: audit-libs-python >= 2.1.3-4 for package: policycoreutils-python-2.5-34.el7                      .x86_64
--> Processing Dependency: python-IPy for package: policycoreutils-python-2.5-34.el7.x86_64
--> Processing Dependency: libqpol.so.1(VERS_1.4)(64bit) for package: policycoreutils-python-2.5-34.el                      7.x86_64
--> Processing Dependency: libqpol.so.1(VERS_1.2)(64bit) for package: policycoreutils-python-2.5-34.el                      7.x86_64
--> Processing Dependency: libcgroup for package: policycoreutils-python-2.5-34.el7.x86_64
--> Processing Dependency: libapol.so.4(VERS_4.0)(64bit) for package: policycoreutils-python-2.5-34.el                      7.x86_64
--> Processing Dependency: checkpolicy for package: policycoreutils-python-2.5-34.el7.x86_64
--> Processing Dependency: libqpol.so.1()(64bit) for package: policycoreutils-python-2.5-34.el7.x86_64
--> Processing Dependency: libapol.so.4()(64bit) for package: policycoreutils-python-2.5-34.el7.x86_64
--> Running transaction check
---> Package audit-libs-python.x86_64 0:2.8.5-4.el7 will be installed
---> Package checkpolicy.x86_64 0:2.5-8.el7 will be installed
---> Package libcgroup.x86_64 0:0.41-21.el7 will be installed
---> Package libsemanage-python.x86_64 0:2.5-14.el7 will be installed
---> Package policycoreutils.x86_64 0:2.5-33.el7 will be updated
---> Package policycoreutils.x86_64 0:2.5-34.el7 will be an update
---> Package python-IPy.noarch 0:0.75-6.el7 will be installed
---> Package setools-libs.x86_64 0:3.3.8-4.el7 will be installed
--> Finished Dependency Resolution

Dependencies Resolved

======================================================================================================
 Package                        Arch           Version                 Repository                Size
======================================================================================================
Installing:
 gitlab-ce                      x86_64         13.1.4-ce.0.el7         gitlab_gitlab-ce         703 M
Installing for dependencies:
 audit-libs-python              x86_64         2.8.5-4.el7             base                      76 k
 checkpolicy                    x86_64         2.5-8.el7               base                     295 k
 libcgroup                      x86_64         0.41-21.el7             base                      66 k
 libsemanage-python             x86_64         2.5-14.el7              base                     113 k
 policycoreutils-python         x86_64         2.5-34.el7              base                     457 k
 python-IPy                     noarch         0.75-6.el7              base                      32 k
 setools-libs                   x86_64         3.3.8-4.el7             base                     620 k
Updating for dependencies:
 policycoreutils                x86_64         2.5-34.el7              base                     917 k

Transaction Summary
======================================================================================================
Install  1 Package  (+7 Dependent packages)
Upgrade             ( 1 Dependent package)

Total download size: 705 M
Downloading packages:
Delta RPMs disabled because /usr/bin/applydeltarpm not installed.
(1/9): audit-libs-python-2.8.5-4.el7.x86_64.rpm                                |  76 kB  00:00:00
(2/9): libcgroup-0.41-21.el7.x86_64.rpm                                        |  66 kB  00:00:00
(3/9): libsemanage-python-2.5-14.el7.x86_64.rpm                                | 113 kB  00:00:00
(4/9): checkpolicy-2.5-8.el7.x86_64.rpm                                        | 295 kB  00:00:00
(5/9): policycoreutils-2.5-34.el7.x86_64.rpm                                   | 917 kB  00:00:00
(6/9): python-IPy-0.75-6.el7.noarch.rpm                                        |  32 kB  00:00:00
(7/9): policycoreutils-python-2.5-34.el7.x86_64.rpm                            | 457 kB  00:00:00
(8/9): setools-libs-3.3.8-4.el7.x86_64.rpm                                     | 620 kB  00:00:00
warning: /var/cache/yum/x86_64/7/gitlab_gitlab-ce/packages/gitlab-ce-13.1.4-ce.0.el7.x86_64.rpm: Heade                      r V4 RSA/SHA1 Signature, key ID f27eab47: NOKEY
Public key for gitlab-ce-13.1.4-ce.0.el7.x86_64.rpm is not installed
(9/9): gitlab-ce-13.1.4-ce.0.el7.x86_64.rpm                                    | 703 MB  02:36:05
------------------------------------------------------------------------------------------------------
Total                                                                  77 kB/s | 705 MB  02:36:05
Retrieving key from https://packages.gitlab.com/gitlab/gitlab-ce/gpgkey
Importing GPG key 0x51312F3F:
 Userid     : "GitLab B.V. (package repository signing key) <packages@gitlab.com>"
 Fingerprint: f640 3f65 44a3 8863 daa0 b6e0 3f01 618a 5131 2f3f
 From       : https://packages.gitlab.com/gitlab/gitlab-ce/gpgkey
Retrieving key from https://packages.gitlab.com/gitlab/gitlab-ce/gpgkey/gitlab-gitlab-ce-3D645A26AB9FB                      D22.pub.gpg
Importing GPG key 0xF27EAB47:
 Userid     : "GitLab, Inc. <support@gitlab.com>"
 Fingerprint: dbef 8977 4ddb 9eb3 7d9f c3a0 3cfc f9ba f27e ab47
 From       : https://packages.gitlab.com/gitlab/gitlab-ce/gpgkey/gitlab-gitlab-ce-3D645A26AB9FBD22.pu                      b.gpg
Running transaction check
Running transaction test
Transaction test succeeded
Running transaction
  Installing : setools-libs-3.3.8-4.el7.x86_64                                                   1/10
  Installing : audit-libs-python-2.8.5-4.el7.x86_64                                              2/10
  Installing : libcgroup-0.41-21.el7.x86_64                                                      3/10
  Installing : python-IPy-0.75-6.el7.noarch                                                      4/10
  Installing : libsemanage-python-2.5-14.el7.x86_64                                              5/10
  Updating   : policycoreutils-2.5-34.el7.x86_64                                                 6/10
  Installing : checkpolicy-2.5-8.el7.x86_64                                                      7/10
  Installing : policycoreutils-python-2.5-34.el7.x86_64                                          8/10
  Installing : gitlab-ce-13.1.4-ce.0.el7.x86_64                                                  9/10
  Cleanup    : policycoreutils-2.5-33.el7.x86_64                                                10/10
It looks like GitLab has not been configured yet; skipping the upgrade script.

       *.                  *.
      ***                 ***
     *****               *****
    .******             *******
    ********            ********
   ,,,,,,,,,***********,,,,,,,,,
  ,,,,,,,,,,,*********,,,,,,,,,,,
  .,,,,,,,,,,,*******,,,,,,,,,,,,
      ,,,,,,,,,*****,,,,,,,,,.
         ,,,,,,,****,,,,,,
            .,,,***,,,,
                ,*,.



     _______ __  __          __
    / ____(_) /_/ /   ____ _/ /_
   / / __/ / __/ /   / __ `/ __ \
  / /_/ / / /_/ /___/ /_/ / /_/ /
  \____/_/\__/_____/\__,_/_.___/


Thank you for installing GitLab!
GitLab was unable to detect a valid hostname for your instance.
Please configure a URL for your GitLab instance by setting `external_url`
configuration in /etc/gitlab/gitlab.rb file.
Then, you can start your GitLab instance by running the following command:
  sudo gitlab-ctl reconfigure

For a comprehensive list of configuration options please see the Omnibus GitLab readme
https://gitlab.com/gitlab-org/omnibus-gitlab/blob/master/README.md

  Verifying  : checkpolicy-2.5-8.el7.x86_64                                                      1/10
  Verifying  : gitlab-ce-13.1.4-ce.0.el7.x86_64                                                  2/10
  Verifying  : policycoreutils-2.5-34.el7.x86_64                                                 3/10
  Verifying  : libsemanage-python-2.5-14.el7.x86_64                                              4/10
  Verifying  : python-IPy-0.75-6.el7.noarch                                                      5/10
  Verifying  : policycoreutils-python-2.5-34.el7.x86_64                                          6/10
  Verifying  : libcgroup-0.41-21.el7.x86_64                                                      7/10
  Verifying  : audit-libs-python-2.8.5-4.el7.x86_64                                              8/10
  Verifying  : setools-libs-3.3.8-4.el7.x86_64                                                   9/10
  Verifying  : policycoreutils-2.5-33.el7.x86_64                                                10/10

Installed:
  gitlab-ce.x86_64 0:13.1.4-ce.0.el7

Dependency Installed:
  audit-libs-python.x86_64 0:2.8.5-4.el7              checkpolicy.x86_64 0:2.5-8.el7
  libcgroup.x86_64 0:0.41-21.el7                      libsemanage-python.x86_64 0:2.5-14.el7
  policycoreutils-python.x86_64 0:2.5-34.el7          python-IPy.noarch 0:0.75-6.el7
  setools-libs.x86_64 0:3.3.8-4.el7

Dependency Updated:
  policycoreutils.x86_64 0:2.5-34.el7

Complete!

```

相关命令

```
gitlab-ctl start  #启动全部服务
gitlab-ctl restart #重启全部服务
gitlab-ctl stop		#停止全部服务
gitlab-ctl restart nginx	# 重启单个服务
gitlab-ctl status		#查看服务状态
gitlab-ctl reconfigure	# 使配置文件失效
gitlab-ctl show-config	# 验证配置文件
gitlab-ctl uninstall	# 删除gitlab
gitlab-ctl cleanse		# 删除所有数据
gitlab-ctl tail <service name>	# 查看服务日志
gitlab-ctl tail nginx		# 如查看gitlab下nginx日志
gitlab-rails console		#进入控制台
```



gitlab常用组件



gitlab安装目录



备份与恢复

#### 九、github使用技巧

```
in:name example
in:readme example
in:description example
starts:> 1000
forks:>1000
```



#### 十、问题

1、githubhttps需要输入密码

```
## 查询连接方式
git remote -v

## 更改为git
git remote rm origin
git remote add origin git@github.com:develop-yang/dorm.git
```



