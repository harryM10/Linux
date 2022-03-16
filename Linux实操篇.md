# Linux实操篇

# 1、远程登录Linux

## 1.1、为什么远程登录？

1. Linux服务器是开发小组共享的。
2. 正式上网的项目是运行在公网的。
3. 远程登录客户端有Xshell，Xftp等。



## 1.2、Xshell使用

**Xshell**是目前最好的远程登录到Linux的操作软件，流畅的速度，可以解决中文乱码的问题。可以运行在Windows界面下用来访问远端不同系统的服务器。

通过Xshell远程登录Linux服务器，需要打开**sshd**服务。

**sshd（secure shell）**服务使用ssh协议远程开启其他主机shell的服务。



## 1.3、 远程文件上传下载 Xftp5

Xftp5：是一个基于windows平台的功能强大的SFTP、FTP文件传输文件，使用了Xftp后，windows用户能安全地在UNIX/Linux 和 windows PC之间传输文件。

如何解决Xftp中文乱码问题：使用UTF-8编码即可。



# 2、Linux关机重启用户

## 2.1、关机重启

**shutdown** 关机

`shutdown -h now` ：表示立即关机

`shutdown -h 1 `: 表示一分钟后关机

`shutdown -r now` : 立即重启

**halt** 就是直接使用，效果等同关机

**reboot** ：重启系统 

**syn **： 把内存的数据同步到磁盘中

**当我们关机或者重启时，应该先执行以下sync 指令，把内存数据写入磁盘，防止数据丢失。**



## 2.2、用户登录注销

**基本介绍：**

- 少使用root账号登录，尽量使用普通用户登录，登录后使用`su - username `切换成系统管理员身份。
- 在提示符下输入`logout` 即可注销用户。

使用细节：

- logout注销指令在图形运行级别无效，在运行级别3下有效。



# 3、Linux用户管理

Linux系统是一个多任务多用户的操作系统。Linux的用户至少要属于一个组。

## 3.1、添加用户

**基本语法：**`useradd [options] username` ， `useradd -m username`

**指定密码**：**`passwd username`**



# 4、Linux实用指令

## 4.1、帮助指令

当我们对某个指令不熟悉时，可以使用Linux提供的帮助指令来了解指令用法。

**man**：`man ls`，`man cat` ，功能描述。获取帮助信息

**help**：`help cd` ，功能描述，获取shell内置命令的帮助信息



## 4.2、文件目录类

**pwd**：显示当前工作目录绝对路径。

**ls**：显示目录或者文件

- **`ls -a`** 显示当前目录所有文件或目录，包括隐藏的
- **`ls -l`** 以列表方式显示

**mkdir**：初建目录

- 创建多级目录 **`mkdir -p animal/cat`**

**rmdir**：删除空目录

- 删除非空目录  **`rm -rf animal`**

**touch**：创建一个空文件

- 可以一次创建多个文件

**cp**：拷贝文件到指定目录

- 拷贝单个文件：**`cp linux/hello.txt study/`**
- 递归复制整个文件夹：**`cp -r linux/ study`**

**rm：**删除文件或目录

- -r：递归删除整个文件夹
- -f：强制删除

**mv：**移动文件与目录或者重命名 

- 文件重命名：`**mv hello.txt world.txt**`
- 移动文件：**`mv world.txt ../study/`**



## 4.3 文件查看

**cat：**查看文件内容，只能看。

- 查看文件内容：**`cat demo.c`**
- 可以显示行号：**`cat -n demo.c`**
- 与more结合使用，可分页显示：  **`cat -n demo.c | more`**

**more**：是一个基于vi编辑器的文本过滤器，它以全屏幕的方式按页显示文本文件的内容。more还内置了很多快捷键。

- **空白键(Space) **: 向下翻一页
- **Enter**：向下翻一行
- **q**: 离开more
- **Ctrl + F**：向下滚动一屏
- Ctrl + B：返回上一屏
- **=**：输出当前行的行号
- :f 输出文件名和当前行的行号

**less**：用来分屏查看文件内容，与more类似，但是功能更加强大，支持各种终端显示。ess指令在显示文件内容时，并不是一次将整个文件加载之后才显示，而是根据显示需要加载内容。对于显示大型文件具有较高的效率。

- **查看文件**：**`less demo.c`**
- **空格，[pagedown]**: 向下翻页
- **[pageup]**: 向上翻页
- **q** : 离开

**>输出重定向**：输出重定向。如果不存在会创建文件，否则会将原来的文件内容覆盖。

- 列表内容写入test.txt : `**ls -l > test.txt**` 

**>指令,追加** : 如果不存在会创建文件，否则不会覆盖原来的文件内容，而是追加到文件的尾部。

- 内容追加到 test.txt ：`**echo 1234 >> test.txt**`

**echo**：输出内容到控制台

**head**：显示文件开头

- 显示文件前两行：**`head demo.c -n 2`**

**tail**：显示文件结尾

- 显示文档所有更新：**`tail -f demo.c`**

**history**:** **查看历史指令

 

## 4.4 时间与日期

**date**：显示日期和时间

- 显示当前年份：**`date “+%Y”`**
- 显示年-月-日 时：分：秒  **`date “+%Y-%m-%d %H:%M:%S”`**

**cal**：查看日历

- 查看某年或某月日历：**`cal 6 2020`**



## 4.5 文件查找

**find**：在指定目录向下递归其各个子目录

基本用法: find [搜素范围] [选项]

选项： -name 按名字， -user 按用户， -size按大小

寻找大于20M的文件： **`find / -size +20M`**



**locate**: 可以快速定位文件路径，利用事先建立的系统中所有文件名称级路径的locate数据库实现卢埃苏定位给定的文件。为了保证查询结果的准确度，必须定期更新locate

注：第一次运行前，使用**`updatedb`**指令创建locate数据库



**grep指令和管道符号 |** 

**| 管道符**：表示将前一个命令的处理结果输出传递给后面的命令处理。

**grep基本语法**：grep [选项] 查找内容 源文件

**选项**： -n 显示匹配行号， -i 忽略字母大小写

查找PV.c文件中包含fill的行：**`cat PV.c | grep -n fill`**



## 4.6 压缩和解压缩

**gzip**：**`gzip hello.txt`**实现文件压缩, 压缩后源文件不存在

**gunzip**：**`gunzip hello.txt.gz`** 实现文件解压缩，解决后压缩文件不存在



**zip/unzip**, 在项目打包中很有用

**`zip -r linux.zip linux`**, 将linux文件夹下所有文件压缩，-r 实现递归压缩

`**unzip -d study/ linux.zip**`, 将linux.zip 解压到study文件夹下，-d 指定目录



**tar**：是打包指令，最后打包后的文件是.tar.gz 的文件。

基本语法：tar [选项] XXX.tar.gz

- -c 产生.tar打包文件夹
- -v 显示详细信息
- -f 指定压缩后的文件名
- -z 打包同时压缩
- -x 解包tar文件

打包：**zcvf**，解包：**zxvf**

案例1：压缩多个文件，将a1.txt，a2.txt 压缩成a.tar.gz

**`tar -zcvf a.tar.gz a1.txt a2.txt`**

案例2：将a.tar.gz解压到指定目录

**`tar -zxvf a.tar.gz -C opt`**



