## 蓝屏错误排除



1、找到蓝屏收集的错误文件路径`C:\Windows\Minidump`

2、使用WinDbg Preview打开

3、





## 常用DOS命令

### `echo`

- ECHO [ON | OFF]   

打开回显或关闭回显功能(回显是否显示dos执行命令)

- ECHO 

显示当前回显设置    查看回显是关闭还是开启

- ECHO [message]

显示后面的信息

### `@`

关闭当前行命令回显

demo测试

```
##################################### .bat文件##################################
echo ON
echo on1打开了回显
echo on2测试打开了回显
echo on3接下来关闭回显
echo OFF
echo of1关闭了回显
echo of2测试关闭了回显以后,接下来打开回显
echo ON
echo on4测试重新打开了回显
@echo a测试关闭本行回显

####################################执行结果#####################################
D:\leaning-plan\bat\test>test01.bat
D:\leaning-plan\bat\test>echo ON
D:\leaning-plan\bat\test>echo on1打开了回显
on1打开了回显
D:\leaning-plan\bat\test>echo on2测试打开了回显
on2测试打开了回显
D:\leaning-plan\bat\test>echo on3接下来关闭回显
on3接下来关闭回显
D:\leaning-plan\bat\test>echo OFF
of1关闭了回显
of2测试关闭了回显以后,接下来打开回显
D:\leaning-plan\bat\test>echo on4测试重新打开了回显
on4测试重新打开了回显
a测试关闭本行回显
D:\leaning-plan\bat\test>

```

### `dir`

显示指定路径上全部文件或文件夹的信息
`dir [盘符:][路径][文件名称] [參数]`

### `md(mkdir)`

`md[盘符:][路径]`

### `rd(rmdir`)

删除文件夹

### `cd`

进入指定的文件夹

### `copy`

复制文件

`copy [源][目的]`

### `del`

删除文件

`DEL [盘符][文件路径][文件名称][参数]`  

-P 能够使用户在删除多个文件时对每一个文件都显示删除询问

### ren(rename)

### type

discopy

deltree

mem

chkdsk

sys



pass

cls

time

date

ver

### `goto`



### `rem`



### pause



### call



### start



### if

- if 
- if exist
- if errorlevel number
- else

- 比较运算符
  - EQU
  - NEQ
  - LSS
  - LEQ
  - GTR
  - GEQ

### choice



### for

### ping



### telnet



### color 



### random



### exit



### `netstat`

用于显示与IP、TCP、UDP和ICMP协议相关的统计数据，一般用于检验本机端口的网络连接情况

- netstat /?  查询参数参考信息
- netstat -an 以数字方式显示所有连接和监听的端口号

状态：

LISTEN: 监听中

established:监听中

ESTABLISHED: 已建立连接

TIME_WAIT : 等待

## bat脚本

### 创建文件夹

### 启动javajar包

#### 查看java进程

- windows

  jps

  jps -l			显示java进程的ID和软件路径名称

- linux

  - `ps -ef|grep java`

  - `jps -l`        显示java进程和软件名称

  - `jps -lmv`     显示java进程的ID和软件名称，显示启动main输入参数；虚拟机参数

