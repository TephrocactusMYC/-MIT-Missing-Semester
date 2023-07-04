## 1.shell简介

## 1.1 什么是shell

什么是shell呢？shell是用C语言编写的程序，它是用户使用 Linux 的桥梁。Shell既是一种命令语言，又是一种程序设计语言。简单来说Shell 是指一种应用程序，这个应用程序提供了一个界面，用户通过这个界面访问操作系统内核的服务。也可以这样认为，linux中的shell就是linux内核的一个外层保护工具，并负责完成用户与内核之间的交互

## 1.2 shell脚本

shell脚本就是一种专门使用shell编写的脚本程序，它虽然没有C++、Java、Python等一系列高级语言功能强大，但是在服务器运维领域以及嵌入式开发领域，shell脚本具有举足轻重的地位。

shell脚本编程如同其他编程语言的一样，只要有一个能编写代码的文本编辑器和一个能解释执行的脚本解释器就可以运行了，而linux下的shell种类众多，常用的用：

+   Bourne Shell（/usr/bin/sh或/bin/sh）
+   **Bourne Again Shell（/bin/bash）**
+   C Shell（/usr/bin/csh）
+   K Shell（/usr/bin/ksh）
+   Shell for Root（/sbin/sh）
+   … …

在诸多linux发行版系统中，最常用的就是Bash，就是Bourne Again Shell，因为其能工提供环境变量以配置用户shell环境，支持历史记录、内置算数功能、支持通配符表达式等高效性能，将linux常用命令进行的简化，被广泛应用于Debian系列的linux发行版中。

## 1.3 运行shell脚本

运行shell脚本的方法有两种：

+   作为可执行程序运行
+   作为解释器参数运行

shell脚本编写如下，并将其保存为test.sh，进入存放此文件目录

```auto
#!/bin/bash
echo "Hello World"
```

+   当作为可执行程序运行时候
    
+   ```auto
    chmod +x test.sh	# 赋予可执行权限
    ./test.sh		    # 执行程序
    ```
    

![在这里插入图片描述](https://img-blog.csdnimg.cn/20200331213405526.png)

+   当作为解释器参数运行时
    
+   ```auto
    /bin/sh test.sh		# 执行命令
    /bin/php test.php	# 执行命令
    ```
    

![在这里插入图片描述](https://img-blog.csdnimg.cn/2020033121341733.png)

## 1.4 shell注释

+   单行注释：和python注释相同，以`#`号开头作为单行注释
    
+   ```auto
    # 这是一个注释
    # author：ohuohuoo
    # date：`date`
    ```
    
+   多行注释：如果在开发过程中，，遇到大段的代码需要临时注释起来，过一会儿又取消注释，可以将其定义为一个花括号的注释函数，也可以用多行注释
    
+   ```auto
    :<<EOF
    注释内容...
    注释内容...
    注释内容...
    EOF
    
    # EOF可以换成其他符号
    :<<E！
    注释内容...
    注释内容...
    注释内容...
    ！
    ```
    

## 1.5 shell编写的基本步骤

+   建立shell文件
+   赋予shell文件可执行程序权限（使用chmod命令修改权限）
+   执行shell文件（直接运行赋予权限后的二进制文件）

## 2.shell变量

## 2.1 命名变量

shell编程中，定义变量是直接定义的，**没有明确的数据类型**，shel允许用户建立变量存储数据，但是将认为赋给变量的值**都解释为一串字符**，如下

```auto
cout=1			# 定义变量		
name="ohuohuo"	 # 定义变量
echo $cout		 # 取变量值
echo $name	     # 取变量值
```

shell中，英文符号`"$"`用于取变量值

![在这里插入图片描述](https://img-blog.csdnimg.cn/20200331213447554.png)

***注意点***：shell编程的变量名的命名和其他语言一样，需要遵循一定的规则，规则如下

+   命名只能使用英文字母，数字和下划线，首个字符不能以数字开头
+   中间不能有空格，可以使用下划线（\_）
+   不能使用标点符号
+   不能使用bash里的关键字（可用help命令查看保留关键字）

如下所示

+   有效的命令
    
+   ```auto
    NAME
    LIBRARY_PATH
    _var
    var2
    ```
    
+   无效的命名
    
+   ```auto
    ?var=123
    user*name=ohuohuo
    ```
    

如果在变量中使用系统命令，需要加上 " \`"符号（ESC键下方），如下所示

+   ```auto
    DATE1=`date`	
    DATE2=$(date)
    ```
    
    +   1
    +   2
    
    两者功能相同
    

![在这里插入图片描述](https://img-blog.csdnimg.cn/20200331213500487.png)

## 2.2 使用变量

使用变量的时，用英文符号`"$"`取变量值，对于较长的变量名，建议加上`{ }`花括号，帮助解释器识别变量的边界，如下

```auto
name="test_name"
echo "My name is ${name}and you"
```

+   1
+   2

加上方括号时即所有便后面的语句不留空格，shell也会自动识别边界，默认添加一个空格

![在这里插入图片描述](https://img-blog.csdnimg.cn/20200331213511512.png)

此外，已经定义过的变量，可以二次定义并重新被赋值覆盖上一次的变量值，这点如同其他语言

![在这里插入图片描述](https://img-blog.csdnimg.cn/20200331213518402.png)

## 2.3 变量类型

shell编程中也同样存在变量类型，在运行shell时会同时存在三种变量

+   **局部变量**：在脚本或命令中定义，仅在当前shell实例中有效，其他shell启动的程序不能访问局部变量
+   环境变量：所有的程序，包括shell启动的程序，都能访问环境变量，必要的时候shell脚本也可以定义环境变量
+   **shell变量**：由shell程序设置的特殊变量。shell变量中有一部分是环境变量，有一部分是局部变量，不同类型的变量保证了shell的正常运行

## 2.4 变量操作

shell中的变量，默认为可读可写类型，如果想要其只可读，如同url一样，需要将其声明为\*\*只读类型变量（\*\*如同`const`），使用`readonly`命令，如下脚本

```auto
#!/bin/bash
Url="http://www.baidu.com"
readonly Url
Url="http://www.csnd.net"
```

这样的话，这句就会报错，提示`/bin/sh: NAME: This variable is read only.`此变量为只读变量

![在这里插入图片描述](https://img-blog.csdnimg.cn/20200331213559462.png)

如果想要**删除变量**，使用`unset`命令解除命令赋值，但是`unset`不能删除可读变量，如下所示

```auto
#!/bin/sh
name="ohuohuo"
Url="http://www.baidu.com"
readonly Url	# 设置可读变量
unset name		# 可以被删除
unset Url		# 不可被删除
echo $name		# 不被打印出
echo $Url		# 打印出
```

![在这里插入图片描述](https://img-blog.csdnimg.cn/20200331213608214.png)

## 3.shell字符串

## 3.1 字符串类型

在shell中字符串是shell编程中最常用最有用的数据类型，字符串可以用单引号，也可以用双引号，也可以不用引号。

使用单引号

```auto
str='this is a string'
```

+   1

![在这里插入图片描述](https://img-blog.csdnimg.cn/20200331213642504.png)

使用单引号的不足：

+   单引号里的任何字符都会原样输出，单引号字符串中的变量是无效的
+   单引号字串中不能出现单独一个的单引号（对单引号使用转义符后也不行），但可成对出现，作为字符串拼接使用。

使用双引号

```auto
name="ohouhuoo"
str="please input your \"$name"\"
echo -e $str
```

输出结果如下图

![在这里插入图片描述](https://img-blog.csdnimg.cn/20200331213651333.png)

使用双引号的优势：

+   可以在双引号中使用变量
+   可以在双引号中使用转移字符

由此可见，双引号较单引号而言有更强大的优势

## 3.2 字符串操作

+   **获取字符串长度**：在对变量进行取值时，使用" # "符号对字符串进行取值
    
+   ```auto
    string="abcd"
    echo ${#string} # 输出 4
    ```
    
    +   1
    +   2

![在这里插入图片描述](https://img-blog.csdnimg.cn/20200331213700924.png)

+   **提取子字符串**：使用字符串的截取命令，用于提取部分字符串
    
+   ```auto
    string="this is a test"
    echo ${string:2:6} # 表示从第3个字符开始截取
    ```
    
    +   1
    +   2
    
    上式输出结果为`is is`，如下图
    

![在这里插入图片描述](https://img-blog.csdnimg.cn/20200331213707902.png)

+   **查找字符串**：用于查找字符的位置，输出结果为字符在字符串中所占的数据位置，如果查找多个字符，那哪个字母先出现就计算哪个，如下查找`it`中`i`和`t`两个字符，`t`先出现，输出为1
    
+   ```auto
    string="this is a test"
    echo `expr index "$string" it`  # 输出 1
    ```
    
    +   1
    +   2

![在这里插入图片描述](https://img-blog.csdnimg.cn/20200331213716146.png)

## 4.shell数组

在bash下，仅仅支持一维数组，并且没有限定数组的大小，不支持多维数组。类似于 C 语言，数组元素的下标由 0 开始编号（上述字符串也是这样）。获取数组中的元素要利用下标，下标可以是整数或算术表达式，其值应大于或等于 0。

## 4.1 定义数组

在 Shell 中，用括号`()`来定义表示数组，数组中元素用"空格"符号分割开。定义数组的一般形式为：

```auto
# 一般定义
array_name=(value1 value2 value3 value4)

# 多级定义
array_test=(
value1 
value2 
value3 
value4
)

# 
array_text[0]=value0
array_text[1]=value1
array_text[3]=value3
... 
...


```

三种定义形式均可

## 4.2 数组操作

+   **读取数组**：和读取变量名相同，使用`$`符号，需要加上下标名
    
+   ```auto
    valuen=${array_name[n]}
    echo ${array_name[@]} # 读取所有
    ```
    
    +   1
    +   2
+   **获取数组长度**：获取数组长度的方法与获取字符串长度的方法相同，如所示
    
+   ```auto
    # 取得数组元素的个数
    length=${#array_name[@]}	# 从头到尾取
    # 或者
    length=${#array_name[*]}	# 取所有
    # 取得数组单个元素的长度
    lengthn=${#array_name[n]}	# 取特定
    ```
    

## 5.shell传递参数

在执行 Shell 脚本时，向脚本传递参数，脚本内获取参数的格式为：`$n`。**n** 代表一个数字，1 为执行脚本的第一个参数，2 为执行脚本的第二个参数，以此类推……，脚本编写如下,保存为test.sh

```auto
echo "传递参数实例！";
echo "执行的文件名：$0";
echo "第一个参数为：$1";
echo "第二个参数为：$2";
echo "第三个参数为：$3";
```

执行脚本如下

```auto
chmod +x test.sh
./test.sh 1 2 3
```

+   1
+   2

输出结果如下图，传递参数的过程在赋予权限执行脚本的过程中就已经完成

![在这里插入图片描述](https://img-blog.csdnimg.cn/20200331213728638.png)

在使用shell传递参数的时候，常常需要用到以下的几个字符来处理参数

| 参数处理 | 说明 |
| --- | --- |
| `$#` | 传递到脚本的参数个数 |
| `$*` | 以一个单字符串显示所有向脚本传递的参数。 如"$\*“用「”」括起来的情况、以"$1 $2 … $n"的形式输出所有参数。 |
| `$$` | 脚本运行的当前进程ID号 |
| `$!` | 后台运行的最后一个进程的ID号 |
| `$@` | 与∗ 相 同 ， 但 是 使 用 时 加 引 号 ， 并 在 引 号 中 返 回 每 个 参 数 。 如 " \*相同，但是使用时加引号，并在引号中返回每个参数。 如"∗相同，但是使用时加引号，并在引号中返回每个参数。如"@“用「”」括起来的情况、以"$1" “2 " … " 2" … "2"…"n” 的形式输出所有参数。 |
| `$-` | 显示Shell使用的当前选项，与set命令功能相同。 |
| `$?` | 显示最后命令的退出状态。0表示没有错误，其他任何值表明有错误。 |

举例如下

```auto
echo "传递参数实例！";
echo "第一个参数为：$1";

echo "参数个数为：$#";
echo "传递的参数作为一个字符串显示：$*";
```

结果如图

![在这里插入图片描述](https://img-blog.csdnimg.cn/2020033121373844.png)

## 6.shell运算符

## 6.1 shell运算符种类

与其他编程语言相同的是，shell同样支持多种运算符：

+   算数运算符
    
+   关系运算符
    
+   布尔运算符
    
+   逻辑运算符
    
+   字符串运算符
    
+   文件测试运算符
    

shell想要使用这些运算符，需要结合其他命令和工具来使用（因为shell中不支持简单的数学运算），**如使用算符运算符就需要搭配的常用的工具有两种**

+   awk
+   **expr**（使用频繁）

**运算规则注意点**：

+   **表达式和运算符之间必须要有空格**，例如 3+2 是不对的，必须写成 3 + 2
+   **完整的表达式要被 两个" \` "包含**（在 Esc 键下边那个键）

如下实例

```auto
#!/bin/bash

val=`expr 3 + 2`
echo "两数之和为 : $val"
```

+   1
+   2
+   3
+   4

执行脚本后，输出结果为

```auto
两数之和为 : 5
```

+   1

![在这里插入图片描述](https://img-blog.csdnimg.cn/20200331213746393.png)

## 6.2 算数运算符

shell支持的常用的如下表，举例中这里假定变量 a 为 10，变量 b 为 20，

| 运算符 | 说明 | 举例 |
| --- | --- | --- |
| + | 加法 | `expr $a + $b` 结果为 30。 |
| \- | 减法 | `expr $a - $b` 结果为 -10。 |
| \* | 乘法 | `expr $a \* $b` 结果为 200。 |
| / | 除法 | `expr $b / $a` 结果为 2。 |
| % | 取余 | `expr $b % $a` 结果为 0。 |
| \= | 赋值 | a=$b 将把变量 b 的值赋给 a。 |
| \== | 相等。用于比较两个数字，相同则返回 true。 | \[ $a == $b \] 返回 false。 |
| != | 不相等。用于比较两个数字，不相同则返回 true。 | \[ $a != $b \] 返回 true。 |

**需要注意的点：**

+   在windows系统中乘号(\*)前边必须加反斜杠()才能实现乘法运算；

## 6.3 关系运算符

shell中的关系运算符和其他编程语言不同，shell中使用特殊的字符表示关系运算符，并且只支持数字，不支持字符串，除非字符串是数字，下表为常用关系运算符，同样指定a为10，b为20

| 运算符 | 说明 | 举例 |
| --- | --- | --- |
| \-eq | 检测两个数是否相等，相等返回 true。 | \[ $a -eq $b \] 返回 false。 |
| \-ne | 检测两个数是否不相等，不相等返回 true。 | \[ $a -ne $b \] 返回 true。 |
| \-gt | 检测左边的数是否大于右边的，如果是，则返回 true。 | \[ $a -gt $b \] 返回 false。 |
| \-lt | 检测左边的数是否小于右边的，如果是，则返回 true。 | \[ $a -lt $b \] 返回 true。 |
| \-ge | 检测左边的数是否大于等于右边的，如果是，则返回 true。 | \[ $a -ge $b \] 返回 false。 |
| \-le | 检测左边的数是否小于等于右边的，如果是，则返回 true。 | \[ $a -le $b \] 返回 true。 |

脚本编写如下

```auto
#!/bin/bash

a=10
b=20

if [ $a -eq $b ]
then
   echo "$a -eq $b : a 等于 b"
else
   echo "$a -eq $b: a 不等于 b"
fi
if [ $a -ne $b ]
then
   echo "$a -ne $b: a 不等于 b"
else
   echo "$a -ne $b : a 等于 b"
fi 
```

将脚本执行结果如下

```auto
10 -eq 20: a 不等于 b
10 -ne 20: a 不等于 b
```

+   1
+   2

![在这里插入图片描述](https://img-blog.csdnimg.cn/20200331213759430.png)

**需要注意的点：**

+   运算符和数之间必须要用空格隔开

## 6.4 布尔运算符

shell中的布尔运算符使用如下表，同样指定a为10，b为20

| 运算符 | 说明 | 举例 |
| --- | --- | --- |
| ! | 非运算，表达式为 true 则返回 false，否则返回 true。 | \[ ! false \] 返回 true。 |
| \-o | 或运算，有一个表达式为 true 则返回 true。 | \[ $a -lt 20 -o $b -gt 100 \] 返回 true。 |
| \-a | 与运算，两个表达式都为 true 才返回 true。 | \[ $a -lt 20 -a $b -gt 100 \] 返回 false。 |

脚本编写如下

```auto
#!/bin/bash

a=10
b=20

if [ $a != $b ]
then
   echo "$a != $b : a 不等于 b"
else
   echo "$a == $b: a 等于 b"
fi 
```

执行脚本，结果如下

```auto
10 != 20 : a 不等于 b
```

+   1

![在这里插入图片描述](https://img-blog.csdnimg.cn/20200331213808566.png)

## 6.5 逻辑运算符

shell中的逻辑运算符和其他编程语言有类似的地方，如下表。假定变量 a 为 10，变量 b 为 20

| 运算符 | 说明 | 举例 |
| --- | --- | --- |
| && | 逻辑的 AND | \[\[ $a -lt 100 && $b -gt 100 \]\] 返回 false |
| || | 逻辑的 OR | \[\[ $a -lt 100 || $b -gt 100 \]\] 返回 true |

编写脚本如下

```auto
#!/bin/bash

a=10
b=20

if [[ $a -lt 100 && $b -gt 100 ]]
then
   echo "返回 true"
else
   echo "返回 false"
fi 
```

+   1
+   2
+   3
+   4
+   5
+   6
+   7
+   8
+   9
+   10
+   11

执行脚本，结果如下

```auto
返回 false
```

+   1

![在这里插入图片描述](https://img-blog.csdnimg.cn/20200331213821775.png)

需要注意的点：

+   这里使用两层的\[ \]符号，将两次关系运算的结果保存在条件句中

## 6.6 字符串运算符

shell中常用的字符串运算符如下表。假定变量 a 为 “abc”，变量 b 为 “efg”

| 运算符 | 说明 | 举例 |
| --- | --- | --- |
| \= | 检测两个字符串是否相等，相等返回 true。 | \[ $a = $b \] 返回 false。 |
| != | 检测两个字符串是否相等，不相等返回 true。 | \[ $a != $b \] 返回 true。 |
| \-z | 检测字符串长度是否为0，为0返回 true。 | \[ -z $a \] 返回 false。 |
| \-n | 检测字符串长度是否不为 0，不为 0 返回 true。 | \[ -n “$a” \] 返回 true。 |
| $ | 检测字符串是否为空，不为空返回 true。 | \[ $a \] 返回 true。 |

编写脚本如下

```auto
#!/bin/bash

a="abc"
b="efg"

if [ $a != $b ]
then
   echo "$a != $b : a 等于 b"
else
   echo "$a != $b: a 不等于 b"
fi 
```

+   1
+   2
+   3
+   4
+   5
+   6
+   7
+   8
+   9
+   10
+   11

执行脚本，结果输出如下

```auto
abc != efg : a 不等于 b
```

+   1

![在这里插入图片描述](https://img-blog.csdnimg.cn/20200331213830784.png)

## 6.7 文件测试运算符

shell中的文件测试运算符用于检测在类unix系统中，文件的各种属性，如下表

| 操作符 | 说明 | 举例 |
| --- | --- | --- |
| \-b file | 检测文件是否是块设备文件，如果是，则返回 true。 | \[ -b $file \] 返回 false。 |
| \-c file | 检测文件是否是字符设备文件，如果是，则返回 true。 | \[ -c $file \] 返回 false。 |
| \-d file | 检测文件是否是目录，如果是，则返回 true。 | \[ -d $file \] 返回 false。 |
| \-f file | 检测文件是否是普通文件（既不是目录，也不是设备文件），如果是，则返回 true。 | \[ -f $file \] 返回 true。 |
| \-g file | 检测文件是否设置了 SGID 位，如果是，则返回 true。 | \[ -g $file \] 返回 false。 |
| \-k file | 检测文件是否设置了粘着位(Sticky Bit)，如果是，则返回 true。 | \[ -k $file \] 返回 false。 |
| \-p file | 检测文件是否是有名管道，如果是，则返回 true。 | \[ -p $file \] 返回 false。 |
| \-u file | 检测文件是否设置了 SUID 位，如果是，则返回 true。 | \[ -u $file \] 返回 false。 |
| \-r file | 检测文件是否可读，如果是，则返回 true。 | \[ -r $file \] 返回 true。 |
| \-w file | 检测文件是否可写，如果是，则返回 true。 | \[ -w $file \] 返回 true。 |
| \-x file | 检测文件是否可执行，如果是，则返回 true。 | \[ -x $file \] 返回 true。 |
| \-s file | 检测文件是否为空（文件大小是否大于0），不为空返回 true。 | \[ -s $file \] 返回 true。 |
| \-e file | 检测文件（包括目录）是否存在，如果是，则返回 true。 | \[ -e $file \] 返回 true。 |

编写脚本如下

```auto
#!/bin/bash

file="/var/www/test/test.sh"
if [ -r $file ]
then
   echo "文件可读"
else
   echo "文件不可读"
fi    
```

+   1
+   2
+   3
+   4
+   5
+   6
+   7
+   8
+   9

执行脚本，结果输出如下

```auto
文件可读
```

+   1

## 7.shell编程中的命令

## 7.1 echo命令

echo命令在shell中用于字符串的输出，调用的格式：

```auto
echo string
```

+   1

echo命令还可显示复杂的输出格式

+   显示普通的字符串
    
    +   ```auto
        echo "this is a test"
        ```
        
        +   1
+   显示转义字符
    
    +   ```auto
        echo "\this is a test\"
        ```
        
        +   1
+   显示变量
    
    +   ```auto
        name="ohuohuo"
        echo "you name is $name"
        ```
        
+   显示换行
    
    +   ```auto
        echo -e "Right!\n " # -e 表示开启转义
        echo "this is other line"
        ```
        
+   显示结果定向重定向至文件
    
    +   ```auto
        echo "this is a test" > testfile
        ```
        
        +   1
+   显示command命令执行结果
    
    +   ```auto
        echo `date`
        ```
        
        +   1

echo命令还有其他使用规则，经常使用就可熟练掌握

## 7.2 printf命令

shell中的printf命令如同C语言中一样，调用格式也大抵相同，只是有一点点不同。与echo命令打印字符串不同的是，printf不会自动调价换行符号，可以手动添加

printf命令的语法：

```auto
printf format-string [arguments...]
```

+   1

参数说明：

+   format-string：格式控制字符串
+   arguments：参数列表

举例如下

```auto
$ echo "Hello, Shell"	# 输入
Hello, Shell		   # 输出
$ printf "Hello, Shell\n" # 输入
Hello, Shell			# 输出
```

printf命令可以较为强大的使用转义字符，shell中常用的转义字符如下表示所示

| 序列 | 说明 |
| --- | --- |
| \\a | 警告字符，通常为ASCII的BEL字符 |
| \\b | 后退 |
| \\c | 抑制（不显示）输出结果中任何结尾的换行字符（只在%b格式指示符控制下的参数字符串中有效），而且，任何留在参数里的字符、任何接下来的参数以及任何留在格式字符串中的字符，都被忽略 |
| \\f | 换页（formfeed） |
| \\n | 换行 |
| \\r | 回车（Carriage return） |
| \\t | 水平制表符 |
| \\v | 垂直制表符 |
| \\ | 一个字面上的反斜杠字符 |
| \\ddd | 表示1到3位数八进制值的字符。仅在格式字符串中有效 |
| \\0ddd | 表示1到3位的八进制值字符 |

## 7.3 test命令

shell中的 test 命令用于检查某个条件是否成立，它可以进行数值、字符和文件三个方面的测试

**数值测试命令表**

| 参数 | 说明 |
| --- | --- |
| \-eq | 等于则为真 |
| \-ne | 不等于则为真 |
| \-gt | 大于则为真 |
| \-ge | 大于等于则为真 |
| \-lt | 小于则为真 |
| \-le | 小于等于则为真 |

应用举例如下

```auto
#！/bin/bash
num1=100
num2=100
if test $[num1] -eq $[num2]
then
    echo '两个数相等！'
else
    echo '两个数不相等！'
fi
```

输出结果

```auto
两个字符串不相等!
```

+   1

**字符串测试表**

| 参数 | 说明 |
| --- | --- |
| \= | 等于则为真 |
| != | 不相等则为真 |
| \-z 字符串 | 字符串的长度为零则为真 |
| \-n 字符串 | 字符串的长度不为零则为真 |

脚本实例如下

```auto
# !/bin/bas
num1="name"
num2="function"
if test $num1 = $num2
then
    echo '两个字符串相等!'
else
    echo '两个字符串不相等!'
fi
```

输出结果

```auto
两个字符串不相等!
```

+   1

**文件测试表**

| 参数 | 说明 |
| --- | --- |
| \-e 文件名 | 如果文件存在则为真 |
| \-r 文件名 | 如果文件存在且可读则为真 |
| \-w 文件名 | 如果文件存在且可写则为真 |
| \-x 文件名 | 如果文件存在且可执行则为真 |
| \-s 文件名 | 如果文件存在且至少有一个字符则为真 |
| \-d 文件名 | 如果文件存在且为目录则为真 |
| \-f 文件名 | 如果文件存在且为普通文件则为真 |
| \-c 文件名 | 如果文件存在且为字符型特殊文件则为真 |
| \-b 文件名 | 如果文件存在且为块特殊文件则为真 |

脚本编写如下

```auto
# !/bin/bash
if test -e ./bash
then
    echo '文件已存在!'
else
    echo '文件不存在!'
fi
```

输出结果如下

```auto
文件已存在!
```

+   1

## 8.shell流程控制

shell作为一种脚本语言，也有着自己的流程控制，而shell中的流程控制主要由条件、循环组成

## 8.1 if else条件

shell中的if else条件具有一定的模版。其调用格式为：

+   if - then - fi：

调用格式如下

```auto
if condition
then
    command1 
    command2
    ...
    commandN 
fi

# 写成单行
if condition;then command1; command2;fi
```

**如果存在不满足的条件的情况**

```auto
if condition
then
    command1 
    command2
    ...
    commandN
else
    command
fi
```

**在多层嵌套条件情况**

```auto
if condition1
then
    command1
elif condition2 
then 
    command2
else
    commandN
fi
```

应用举例

```auto
num1=$[6]
num2=$[8]
if test $[num1] -eq $[num2]
then
    echo '两个数字相等!'
else
    echo '两个数字不相等!'
fi
```

执行脚本，结果输出如下

```auto
两个数字相等!
```

+   1

## 8.2 case条件

shell中case语句为多功能选择语句，与其他语言相通的是，可以用case语句匹配一个值与一个模式，如果匹配成功，执行相匹配的命令。case语句调用格式如下：

```auto
case 值 in
模式1)
    command1
    command2
    ...
    commandN
    ;;
模式2）
    command1
    command2
    ...
    commandN
    ;;
esac
```

需要注意的点：

+   取值后面需要加上in
+   每一模式必须以右括号结束
+   每个模式结束后使用`;;`符号结尾
+   如果没有找到对应的模式。以`*`结尾，并跳出case
+   case需要搭配`esac`结尾，与C语言中的switch … case语句类似

脚本举例如下

```auto
echo '输入 1 到 4 之间的数字:'
echo '你输入的数字为:'
read num
case $num in
    1)  echo '你选择了 1'
    ;;
    2)  echo '你选择了 2'
    ;;
    3)  echo '你选择了 3'
    ;;
    4)  echo '你选择了 4'
    ;;
    *)  echo '你没有输入 1 到 4 之间的数字'
    ;;
esac
```

执行脚本，运行如下

```auto
输入 1 到 5 之间的数字:4
你输入的数字为 4!
输入 1 到 5 之间的数字:8
你输入的数字不是 1 到 5 之间的! 游戏结束
```

case中想要跳出循环有两个命令：break和continu

+   break命令：允许跳出所有循环（中止执行后面所有的循环）
    
    +   使用举例
        
    +   ```auto
        #!/bin/bash
        while :
        do
            echo -n "输入 1 到 5 之间的数字:"
            read num
            case $num in
                1|2|3|4|5) echo "你输入的数字为 $num!"
                ;;
                *) echo "你输入的数字不是 1 到 5 之间的! 游戏结束"
                    break
                ;;
            esac
        done
        ```
        
    +   执行输出如下
        
    +   ```auto
        输入 1 到 5 之间的数字:3
        你输入的数字为 3!
        输入 1 到 5 之间的数字:7
        你输入的数字不是 1 到 5 之间的! 游戏结束
        ```
        
+   contimue：shell中的continue命令与break命令类似，只有一点差别，它不会跳出所有循环，仅仅跳出当前循环。这一点和其他类型的语言相同
    
+   应用举例，同样的将上式修改如下
    
+   ```auto
    #!/bin/bash
    while :
    do
        echo -n "输入 1 到 5 之间的数字: "
        read num
        case $num in
            1|2|3|4|5) echo "你输入的数字为 $num!"
            ;;
            *) echo "你输入的数字不是 1 到 5 之间的!"
                continue
                echo "游戏结束"
            ;;
        esac
    done
    ```
    
+   执行脚本，结果输出如下  
    ![在这里插入图片描述](https://img-blog.csdnimg.cn/20200331213857248.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQxNDg4OTQz,size_16,color_FFFFFF,t_70)
    

## 8.3 for循环

shell中的for循环调用格式和python中的for循环有点类似，也是有模板的：

```auto
for var in item1 item2 ... itemN
do
    command1
    command2
    ...
    commandN
done

# 写成一行同样使用分号将语句分开 
```

需要注意的是：

+   `in`列表中可以包含替换、字符串和文件名等
+   `in`列表是可选的，如果默认不适用，将会循环使用命令行中的位置参数

应用脚本编写如下

```auto
for num in 1 2 3 4 5
do
    echo "The value is: $num"
done
```

输出结果如下

```auto
The value is: 1
The value is: 2
The value is: 3
The value is: 4
The value is: 5
```

![在这里插入图片描述](https://img-blog.csdnimg.cn/20200331213908297.png)

## 8.4 while循环

shell中的while循环用于不断执行一系列命令，也用于从输入文件中读取数据，调用格式如下

```auto
while condition
do
    command
done
```

应用脚本编写如下：

```auto
#!/bin/bash
num=1
while(( $num<=5 ))
do
    echo $num
    let "num++"
done
```

执行脚本，结果运行如下

```auto
1
2
3
4
5
```

只需要知道shell中while循环的格式，同样可以做到和C语言中一样， 使用while循环进行判定或者判断键盘循环，甚至无限循环等，如下使用while循环读取键盘操作

```auto
echo '按下 <Q> 退出'
echo -n '输入你最喜欢的歌名: '
while read SONG
do
    echo "啊！$SONG 真是一首好歌"
done
```

执行脚本，运行结果如下

```auto
按下<Q>退出
输入你最喜欢的歌名: Takeway
啊！Takeway 真是一首好歌
```

![在这里插入图片描述](https://img-blog.csdnimg.cn/20200331213925951.png)

## 8.5 until循环

until 循环执行一系列命令直至条件为 true 时停止。until 循环与 while 循环在处理方式上刚好相反。一般 while 循环优于 until 循环，但在某些时候—也只是极少数情况下，until 循环更加有用。until循环调用格式：

```auto
until condition
do
    command
done
```

`condition` 一般为条件表达式，如果返回值为 false，则继续执行循环体内的语句，否则跳出循环，脚本编写如下

```auto
#!/bin/bash

a=0
until [ ! $a -lt 5 ]
do
   echo $a
   a=`expr $a + 1`
done
```

执行脚本，结果输出如下

```auto
0
1
2
3
4
5
```

## 9.shell函数

## 9.1 定义函数

linux中的shell同样可以定义函数，然后在函数中调用执行相关的shell命令，完成功能，shell中的函数调用格式如下：

```auto
[ function ] funname [()]
{
    action;
    [return int;]
}
```

参数说明：

+   function fun () 表示有返回参数的函数（如同C语言中的有返回类型的函数（int，char等））
+   fun() 表示无返回参数的函数（类似于C语言中的void类型函数）
+   使用return可以返回参数值（一般为数值n），如果不使用，将默认以最后一条命令运行的结果作为返回值

脚本应用举例如下

```auto
#!/bin/bash

FunReturn(){
    echo "两个数字进行相加运算..."
    echo "输入第一个数字: "
    read num
    echo "输入第二个数字: "
    read anothernum
    echo "两个数字分别为 $num 和 $anothernum !"
    return $(($num+$anothernum))	# 分别返回数值
}
FunReturn		# 调用函数
echo "输入的两个数字之和为 $? !" # 使用通配符获取上一条指令的返回值
```

执行脚本，运行如下

```auto
两个数字进行相加运算...
输入第一个数字: 
1
输入第二个数字: 
2
两个数字分别为 1 和 2 !
输入的两个数字之和为 3 !
```

![在这里插入图片描述](https://img-blog.csdnimg.cn/20200331213942867.png)  
需要注意的是：

+   所有的函数在使用前必须定义，这是因为shell解释器是顺序逐层执行的，当shell解释器发现定义的函数时，才会找到其对应的功能，进而执行。

## 9.2 参数定义

此外想要使用shell函数传递参数时，需要在函数体的内部，通过 $n 的形式来获取参数的值，与其他语言不同的是，这不是在定义函数的时候就给定参数，而是在函数体中获取到的参数，例如，$1表示第一个参数，$2表示第二个参数，参数调用列表如下

| 参数处理 | 说明 |
| --- | --- |
| $# | 传递到脚本或函数的参数个数 |
| $\* | 以一个单字符串显示所有向脚本传递的参数 |
| $$ | 脚本运行的当前进程ID号 |
| $! | 后台运行的最后一个进程的ID号 |
| $@ | 与$\*相同，但是使用时加引号，并在引号中返回每个参数。 |
| $- | 显示Shell使用的当前选项，与set命令功能相同。 |
| $? | 显示最后命令的退出状态。0表示没有错误，其他任何值表明有错误。 |

应用脚本举例：

```auto
#!/bin/bash
FunParam(){
    echo "输入第一个参数 $1 !"
    echo "输入第二个参数 $2 !"
    echo "输入第十个个参数 $10 !"
    echo "参数总数共 $# 个!"
    echo "作为一个字符串输出所有参数 $* !"
}
FunParam 1 2 3 4 5 6 7 8 9 10
```

执行脚本如下

```auto
第一个参数为 1 !
第二个参数为 2 !
第十个参数为 10 !
参数总数有 10 个!
作为一个字符串输出所有参数 1 2 3 4 5 6 7 8 9 10！
```

+   ![在这里插入图片描述](https://img-blog.csdnimg.cn/20200331213952615.png)

## 10.shell重定向

+   在之前的学习笔记中，归纳了linux中重定向的使用，这里不再赘述
+   [linux中的重定向](https://blog.csdn.net/qq_41488943/article/details/105214966)

## 11.结尾

shell编程相较于其他编程语言而言较为简单，只要多敲多练，很快就能入手，但是不可忽视shell编程在嵌入式开发和网络开发中的强大作用，至此作为总结归纳，如诺有错误，欢迎指正。

# ref 
[csdn](https://blog.csdn.net/qq_26690505/article/details/109361345)
