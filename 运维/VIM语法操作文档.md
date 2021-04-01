配置文件.vimrc

```
syntax on                       "支持语法高亮显示
filetype plugin indent on       "启用根据文件类型缩进
set autoindent              "开始新行时处理缩进
set expandtab               "将制表符展开为空格
set tabstop=4               "要计算的空格数
set shiftwidth=4        "用于自动缩进的空格数
set backspace=2         "在多数终端上修正退格键backspace
colorscheme murphy
set directory=$HOME/.vim/swap// "设置swap交换文件位置
"set directory=$HOME/.vim/swap\\ "设置windows版本
set undofile			"设置永久性撤销
if !isdirectory("$HOME/.vim/undodir")
    call mkdir("$HOME/.vim/undodir", "p")
endif
set undodir = "$HOME/.vim/undodir"
```

**注意:**

​	windows下配置文件为_vimrc,linux为.vimrc

​	windows用户目录为%USERPROFILE%_vim



### 模式

正常模式

编辑模式

命令行模式

​	`:w` 保存文件

​	`:w filename` 另存文件

​	`:q` 退出

​	`q!` 强制退出

​	移动

​	`h` 	左

​	`j` 	下

​	`k`	上

​	`l` 	右

​	单词移动

​	`w`	以空白字符（空格、制表符、换行符）分割的字母数字下划线

​	`e`

​	`b`

​	`W` 	由空格分隔的任何非空字符组成的序列

​	`E`

​	`B`

​	段落移动: 两个空行之间的文字为一个段落

​	`{`  向前一个段落

​	`}`  向后一个段落

​	加数字可跳过多个段落,如`3{`

​	修改命令(复合命令): 按下`c`后，选择要替换的文字(根据上面的移动命令选择)，进入插入模式

 	`c`	后面跟着移动命令，选要删除的内容



​	清除整行，后进入插入模式

​	`cc`

​	删除整行

​	`dd`

​	撤销

​	`u`

​	重做

​	`ctrl r`	

​	