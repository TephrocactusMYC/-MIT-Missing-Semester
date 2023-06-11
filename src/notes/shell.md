# Shell (lecture 1 & 2)

We have learned to use command lines instead of just terminal.

Here are some really basic command:
```
cd      # change work path
echo    # output
touch   # make a file
mkdir   # make a directory
ls      # lists all files
cat     # output a file's content
mv      # move
man     # show the documents
```
*and so on...*

And what's more, we should learn to use these:
```
|  # pipe
>  # redirect
<  # redirect
>> # append
```

So, the first class is so easy and simple, if you have know something about Linux, shell and other things.

**However, if you just want to write and run your code on Windows, you do not have to Learn the whole class.**
# More about shell
*The accent of the Indian friend is too unfriendly for a Chinese person who is not good at English. Fortunately, I am watching the Chinese translated version. (Laughing)*

We need to learn the syntax of bash scripts.

Below are some useful argvs:
- $0 - Name of the script
- $1 to $9 - Arguments to the script. $1 is the first argument and so on.
- $@ - All the arguments
- $# - Number of arguments
- $? - Return code of the previous command
- $$ - Process identification number (PID) for the current script
- !! - Entire last command, including arguments. A common pattern is to execute a command only for it to fail due to missing permissions; - you can quickly re-execute the command with sudo by doing sudo !!
- $_ - Last argument from the last command. If you are in an interactive shell, you can also quickly get this value by typing Esc followed by . or Alt+.

What another important thing the lecture tought is globbing!
##  short-circuiting
If you have learned C++ or any other language, you will understand this more easily.
## Shebang and env
Finally know what Shebang is. :(

It is good practice to write shebang lines using the env command that will resolve to wherever the command lives in the system, increasing the portability of your scripts.
# Shell Tools
I think this section is a relatively innovative part.

Here are some useful tools:
- find
- tldr # excellent tools!
- grep
- fzf

Furthermore, I believe this lecture introduced many command-line tools of the Rust language.
- fd
- ripgrep
and so on...

 Among them, `ripgrep` is a star project in Rust language. For more information on other contents, please refer to these two links：
- [Chinese Zhihu](https://www.zhihu.com/question/511866354)
- [English Github](https://gist.github.com/sts10/daadbc2f403bdffad1b6d33aff016c0a)

I believe that command-line tools written in Rust are more modern. By "modern" I mean that these tools have advantages such as a nicer GUI, more intuitive output format, lower learning curve, and better performance.

# 以下是一些自学内容
首先，学shell基本上得先了解一些linux。
## Linux
Linux shell是用户和Linux kernel 之间的接口程序。

shell是个用户程序，有自己内建的命令集，也能被其他程序调用。

Linux有七个运行级别，常用1 3 5，其他的不怎么用。

## 快捷键
CTRL+U：清空行

CTRL+R: 搜索先前使用的命令。

这两个很有用。

## Shell
Linux 里应该是有不同种类的shell，最常用应该是bash。
### shell和terminal有啥区别
shell是程序，负责接收指令、执行程序并返回结果。终端是命令的 IO 环境，分为终端设备和终端模拟器。早期计算机很贵，所以一个计算机接入很多显示器和很多IO设备，显示器和IO设备被称为终端。

现代都是个人电脑，因此集成到了一起，所以用的terminal都是终端模拟器。
### shell的变量
有系统变量和shell变量。

常用有HOME PATH PS1 PWD.

变量用$
### shell语法
赋值，唯一需要注意的是默认赋值是字符串，想弄成数值要用let

printf，和C类似，常用的分类符表和转义字符表可以现查。

变量引用使用双引号，当然这并不是必要的。单引号往往可以解决特殊字符的问题，因为单引号不允许引用变量。

export unset分别用于设置和删除变量，不过unset不能删除只读的变量，想删除需要使用gdb。

检查变量是否存在使用问好。

history可以查看历史命令，但是我使用的`atuin`把这一切都集成好了。

### 扩展
大括号扩展就是missing semester之中第二讲的作业四的一部分。

其实就在掌握{a...z}类似的排序方式即可

和python的range语法非常类似

然后就是通配符实现的文件名扩展。主要记住*?[...]即可

### 别名
可以使用alias创建别名。
### PS1
这个是用来设置bash提示符的，如果想要自己更改提示符还是很有用的。不过要是不改的话，也许也没问题？
```shell
PS1="\[$(tput setaf 7)\]\342\224\214\342\224\200\[$(tput sgr0)\]\$([[ \$? != 0 ]] && echo \"\[$(tput bold setaf 1)\][Fail]\[$(tput sgr0)\]\")\[$(tput setaf 7)\][\[\033[1;38;5;214m\]\u\[$(tput bold setaf 7)\]@\[$(tput bold setaf 6)\]\h\[$(tput setaf 7)\]]\[$(tput setaf 7)\]\342\224\200[\[$(tput setaf 2)\]\w\[$(tput setaf 7)\]]\n\[$(tput setaf 7)\]\342\224\224\342\224\200\342\224\200\342\225\274\[$(tput sgr0)\][\[\033[1;38;5;28m\]\t\[$(tput sgr0)\]]\$ "
```
*这个真屌，我真喜欢。*
### bash行为
set +-o或者shopt -u/-s可以设置一些bash行为的开关
## 常用shell命令
### ls
很重要。

文件的颜色:
- 白色字体：普通文件
- 绿色字体:可执行文件
- 红色字体：压缩文件
- 蓝色：目录
- 青色：链接文件（相当于windows的快捷方式）
- 黄色：  设备文件：会把硬件设备抽象为文件：例：block块可以表示硬盘，char字符表示键盘，fifo管道
- 灰色：其他文件
```
ls -ltr #以长列表格式俺修改时间倒序
ls -ls  #按文件大小顺序列出
ls -a   #列出所有文件包括隐藏文件
```
### cat
-n 显示行号
-e 行尾显示美元符号
然后就是重定向的内容，在missing semester讲过了。
### more less
```
cat README | more
```
less更值得推荐

可以搜索
```
/
?
```
还有一些快捷键：
```
ctrl+F #前翻一个窗口
ctrl+B #后翻一个窗口
ctrl+D #前翻半个窗口
ctrl+U #后翻半个窗口
q #退出
```

还可以打开多个文件。
### head tail
指定行数，短时间用处不大
### file wc
这两个都是用来查看信息的。

file我感觉很有用，很多文件没有后缀靠这个能知道是什么文件。

### find
**非常重要的命令。**

常用的是：
```
find . -iname example
find . -type d -name dir
find . -type f -name "*.cpp"
```
### -exec
这个就是把输出的用来执行，特别有用
```
原命令： -exec rm -rf {}\;
```
### 操作文件和目录
这里很简单，常用的有touch, mkdir .

touch 要了解一下-t时间戳，mkdir要了解一下 -p

更多的内容是cp, ln, mv

cp要了解 -R, ln 感觉初级阶段简单了解即可。mv，要记得使用-i。

#### rm
这个很吊，最好使用-i，是为了让用户确认的。

千万不要使用
```
rm -rf *
```
这个命令我曾经在想要重置虚拟机的时候使用，后果是什么都没有了，系统只能重装了，很离谱。不过那个剩下的类似于server的系统很适合锻炼linux这些shell命令（绝了）
### 权限
r w x是基础。

#### chmod
**非常重要的东西！**
符号表达式模式：
- u:所有者
- g:用户组成员
- o:不在用户组的其他用户
- a:所有用户
默认是a的效果

操作符：
- +：添加权限
- -：移除权限
- =：只有这个权限

例子：
```
chmod u+x example.sh
```
这个就是给用户增加执行权限的，最常用的了吧。

数字模式：

用读（4）写（2）执行（1）表示权限，相加就是最后拥有的权限。

比如著名的
```
chmod 777 example.sh
```
就是给所有人所有权限的意思了。

#### chown chgrp
看缩写就知道是改变所有者和用户组的。目前感觉作用不大，此处以后用到了再学吧。

#### setuid setgid
暂时不知道有啥用，以后用到了再学。

### 文本处理
sort排序 uniq去重 看不出有啥用

tr 字符替换，感觉有点儿用。-s用于压缩重复空格，-d用于删除
#### grep
**很重要的命令。**用于搜索文件之中的字符串

```
grep -rl string dir
```
更推荐使用ripgrep，速度快，还好用。

#### 别的
其他的就随便玩儿了，比如date,uname之类的东西。

## shell 进阶
diff用于对比，paste用于合并。

dd用于拷贝和备份（玩儿树莓派一个月了，终于知道是啥玩意儿了。。。）
```
dd if=/dev/sda of=/dev/sdb
dd if=/dev/sda of=dvd.iso
```
如果要擦除，需要/dev/zero，这个文件所有内容都是空字符。就是哦你过来初始化和擦除的。

当然，bs=1024 和count=1024也需要知道。

### gzip bzip2
```
gzip -c file1 > file1.gz #可以使用重定向保留原文件
```
解压使用-d

bzip2和gzip差不多，压缩率更好，但速度更慢。
### gunzip bunzip2
解压命令，不常用，用上了到时候现查吧。
### tar
**特别重要！**

```
tar -cvf name.tar # 压缩
tar -xvf name.tar #解压
tar -xzvf name.tar.gz #解压
tar -xjvf name.tar.bz2 #解压
```
### df du
df唯一有用的就是
```
df -h
```

du我不推荐用，我推荐更好用的dust，是rust重写的命令行工具。
### cron crontab
等我有服务器了我再看。

### nohup
这个很有用，就是no hang up
```
nohup sh example.sh &
```










