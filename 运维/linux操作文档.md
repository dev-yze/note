# Linux管理

## 文件目录管理

### 文件系统架构

### 文件管理

### 目录管理

### 移动复制删除

### 文件目录权限

#### 文件和目录权限有3种:

- 读取(r)

- 写入(w)

- 可执行(x)

  可执行文件有两类：一是直接由CPU执行的二进制代码，二是Shell脚本程序

#### 查看文件目录属性

- ls 
- ls -l [filename]

```
文件类型-文件所有者权限-文件组权限-其它人权限 链接数目	文件属主	文件属组	文件大小	时间
```

#### 改变文件所有权

##### `chown`

##### `chgrp`


#### 改变文件权限

##### `chmod`

| 八进制 | 二进制 | 权限 |八进制|二进制|权限|
| ---------- | ---------- | -------- | ---------- | ---------- | ---------- |
| 0 | 000 | --- |4|100|r--|
| 1 | 001 | --x |5|101|r-x|
| 2 | 010 | -w- |6|110|rw-|
| 3 | 011 | -wx |7|111|rwx|



### 文件类型

### 输入输出重定向

输出重定向：将命令查询的信息输出到指定文件中

输入重定向：1）读取文件 2）通过键盘输入

```
#输出重定向
ls -l > ls_out  # 将ls命令查询的信息输出到ls_out文件中
ls -l >> ls_out # 将ls命令查询的信息追加到ls_out文件中
```



### 管道

使用" | "将一条命令的输出连接到另一条命令的输入



### 常用实例



## 文件查看

- `ls`

参数：

|                  参数选项                  | 解释说明 |
| :----------------------------------------: | :------: |
|                     -l                     |          |
|                     -a                     |          |
|                     -t                     |          |
|                     r                      |          |
|                     -F                     |          |
|                     -p                     |          |
|                     -i                     |          |
|                     -d                     |          |
|                     -h                     |          |
|                     -A                     |          |
|                     -S                     |          |
|                     -R                     |          |
|                     -x                     |          |
|                     -X                     |          |
|                     -c                     |          |
|                     -u                     |          |
|         –color={never,always,auto}         |          |
|                 —full-teim                 |          |
| –time-style={full-iso,long-iso,iso,locale} |          |
|            —time={attime,ctime}            |          |

范例：

```
显示完整时间、大小
[root@dreamym logs]# ls -lh --time-style=long-iso
total 186M
-rw-r--r-- 1 root root  85M 2020-11-23 13:20 dorm.log
-rw-r--r-- 1 root root 101M 2020-11-23 12:43 pixiu-2020-11-23.0.log


```



- `dir` 和 `vdir`
- `cat` 和 `more`

```
cat   							## 查看文件所有内容
cat filename
cat -n filename 				## 显示行号

more							## 分页显示文件
more filename
	## 空格  向下翻页
	## enter  滚动一行
	## q 退出
```



- `head`和 `tail` 显示文件头部或尾部



tail参数

| 参数选项 | 解释说明                                   |
| :------: | ------------------------------------------ |
|    -c    | 指定显示的字节数                           |
|    -n    | 指定显示的行数                             |
|    -f    | 实时输出文件变化后追加的数据               |
|    -F    | 功能等同于-f –retry                        |
|  –retry  | 不停地尝试打开文件，直到文件打开为止       |
|   —pid   | 与-f参数连用，在进程结束后自动退出tail命令 |
|    -s    |                                            |
|    -q    |                                            |
|    -v    |                                            |



```shell
head							## 查看文件的开头
head -n 2 filename1 filename2
tail							## 查看文件的结尾

tail -n 2 filename1 filename2
tail -f filename ##滚动日志


```

- `less`

```
less filename
	使用光标键在文件中前后左右滚屏
	使用行号和百分比作为书签浏览文件
	实现复杂的检索、高亮显示操作
	兼容vim键盘
	阅读到文件结束不会退出
	文件底部：号
		使用正斜杠“/”跟上想要查找的内容
		
```



- `grep`

```
grep target filename[,filename1, filename2]
```



- `find`

- 









## 进程

`w命令`

当前时间 运行天数 连接用户 负载

`查看cpu信息`

cat /proc/cpuinfo

- processor：cau标志
- model name : cpu型号
- physical id: 真实cpu和标识
- cpu cores: 真实cpu内核数

`查看cpu进程`

grep -c 'processor' /proc/cpuinfo

```
root@zhuoluDB:/# w
 10:44:58 up 847 days, 23:14,  2 users,  load average: 3.74, 3.82, 3.76
USER     TTY      FROM              LOGIN@   IDLE   JCPU   PCPU WHAT
root     pts/5    115.199.111.114  09:54    0.00s  0.19s  0.00s w
root     pts/6    115.199.111.114  10:00    2:00   0.25s  0.13s top


root@zhuoluDB:/# cat /proc/cpuinfo
processor	: 0
vendor_id	: GenuineIntel
cpu family	: 6
model		: 85
model name	: Intel(R) Xeon(R) Platinum 8163 CPU @ 2.50GHz
stepping	: 4
microcode	: 0x1
cpu MHz		: 2500.032
cache size	: 33792 KB
physical id	: 0
siblings	: 8
core id		: 0
cpu cores	: 4
apicid		: 0
initial apicid	: 0
fpu		: yes
fpu_exception	: yes
cpuid level	: 13
wp		: yes
flags		: fpu vme de pse tsc msr pae mce cx8 apic sep mtrr pge mca cmov pat pse36 clflush mmx fxsr sse sse2 ss ht syscall nx pdpe1gb rdtscp lm constant_tsc rep_good nopl pni pclmulqdq ssse3 fma cx16 pcid sse4_1 sse4_2 x2apic movbe popcnt tsc_deadline_timer aes xsave avx f16c rdrand hypervisor lahf_lm abm 3dnowprefetch xsaveopt fsgsbase bmi1 avx2 smep bmi2 erms
bogomips	: 5000.06
clflush size	: 64
cache_alignment	: 64
address sizes	: 46 bits physical, 48 bits virtual
power management:

processor	: 1
...
physical id	: 0
siblings	: 8
core id		: 0
cpu cores	: 4
apicid		: 1
initial apicid	: 1
fpu		: yes
fpu_exception	: yes
cpuid level	: 13
wp		: yes
flags		: fpu vme de pse tsc msr pae mce cx8 apic sep mtrr pge mca cmov pat pse36 clflush mmx fxsr sse sse2 ss ht syscall nx pdpe1gb rdtscp lm constant_tsc rep_good nopl pni pclmulqdq ssse3 fma cx16 pcid sse4_1 sse4_2 x2apic movbe popcnt tsc_deadline_timer aes xsave avx f16c rdrand hypervisor lahf_lm abm 3dnowprefetch xsaveopt fsgsbase bmi1 avx2 smep bmi2 erms
bogomips	: 5000.06
clflush size	: 64
cache_alignment	: 64
address sizes	: 46 bits physical, 48 bits virtual
power management:

processor	: 2
...
physical id	: 0
siblings	: 8
core id		: 1
cpu cores	: 4
apicid		: 2
initial apicid	: 2
...


processor	: 3
...
physical id	: 0
siblings	: 8
core id		: 1
cpu cores	: 4
apicid		: 3
initial apicid	: 3
...


processor	: 4
...
physical id	: 0
siblings	: 8
core id		: 2
cpu cores	: 4
apicid		: 4
initial apicid	: 4
...


processor	: 5
...
physical id	: 0
siblings	: 8
core id		: 2
cpu cores	: 4
apicid		: 5
initial apicid	: 5
...


processor	: 6
...
physical id	: 0
siblings	: 8
core id		: 3
cpu cores	: 4
apicid		: 6
initial apicid	: 6
...


processor	: 7
...
physical id	: 0
siblings	: 8
core id		: 3
cpu cores	: 4
apicid		: 7
initial apicid	: 7
...



grep -c 'processor' /proc/cpuinfo
8

```





# Shell编程

## 脚本概述

#### 脚本格式

```
#! /bin/bash  # 声明使用什么解释器
# 注释，后面写脚本
```

#### 脚本执行方式

- `bash script-name`

脚本文件本身没有可执行权限时使用或没有指定解释器

- `path/script-name`

需要添加可执行权限

- `source script-name` 或 `. script-name`

读入文件后在父进程shell中执行脚本



## 变量

### 环境变量

#### 查询

set	输出所有变量（全局变量和局部变量）

env   只显示全局变量

declare	输出所有的变量、函数、整数和已经导出的变量

#### 定义全局环境变量

#### 定义用户环境变量

### 普通变量

变量名=值

- 不使用引号

解释变量

- 使用单引号

当作字符串输出，不解释变量

- 使用双引号

解释其中的变量和路径

```bash
# 定义变量
a=192.168.0.1
b='192.168.0.1'
c="192.168.0.1"
echo "a=${a}"
echo "b=${b}"
echo "c=${c}"
a=192.168.0.1-$a
b='192.168.0.1-$a'
c="192.168.0.1-$a"
echo "a=${a}"
echo "b=${b}"
echo "c=${c}"

========================输出===============================
a=192.168.0.1
b=192.168.0.1
c=192.168.0.1
a=192.168.0.1-192.168.0.1
b=192.168.0.1-$a
c=192.168.0.1-192.168.0.1-192.168.0.1

# 将命令的结果作为变量内容赋值
now_user_home=$(ls -l ../)
echo "now_user_home= ${now_user_home}"
========================输出===============================
now_user_home= 总用量 0
drwxrwxr-x. 2 develop-yze develop-yze 19 3月   8 17:35 shell-test
drwxr-xr-x. 2 develop-yze develop-yze  6 2月   2 01:44 公共
drwxr-xr-x. 2 develop-yze develop-yze  6 2月   2 01:44 模板
drwxr-xr-x. 2 develop-yze develop-yze  6 2月   2 01:44 视频
drwxr-xr-x. 2 develop-yze develop-yze  6 2月   2 01:44 图片
drwxr-xr-x. 2 develop-yze develop-yze  6 2月   2 01:44 文档
drwxr-xr-x. 3 develop-yze develop-yze 77 2月   2 01:54 下载
drwxr-xr-x. 2 develop-yze develop-yze  6 2月   2 01:44 音乐
drwxr-xr-x. 2 develop-yze develop-yze  6 2月   2 16:50 桌面


```

使用`$varname`或`${varname}`输出变量

将命令的结果作为变量的内容赋值



条件测试与比较



函数



循环



数组



开发规范



调试技巧



开发环境配置和优化

