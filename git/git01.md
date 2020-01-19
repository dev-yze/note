一、配置和初始化

1、配置git用户名和邮箱

2、创建一个文件夹，初始化仓库

```c
ZhangEn@DESKTOP-5UOLCEG MINGW64 /g/EditPlus
$ cd gitTest/
ZhangEn@DESKTOP-5UOLCEG MINGW64 /g/EditPlus/gitTest
$ git init
Initialized empty Git repository in G:/EditPlus/gitTest/.git/
ZhangEn@DESKTOP-5UOLCEG MINGW64 /g/EditPlus/gitTest (master)
$ ls -a
./  ../  .git/
```

二、基本命令

1、git add --a

2、git commit -m ""

3、git diff 



4、git log



5、git reset --hard 

6、git reflog

7、git chekout -- fileName

8、创建、切换和合并新分支

```c
git branch dev			// 创建分支dev
git checkout dev		// 切换分支dev
```

```c
git checkout -b dev		  // 创建并切换到dev
```

```c
git checkout master		// 切换回master分支
git merge dev			// 将dev分支合并到master分支
git branch -d dev		// 删除dev分支
```

9、切换分支 switch

```
git switch -c dev		// 创建并切换到新分支
git switch master 	// 切换到已有分支
```

10、git reset HEAD