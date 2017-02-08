[TOC]

# 2017-02-05-Linux基础

首先打开 Linux 系统，进入黑乎乎的一片……我在哪里？

查看当前的所在位置：`pwd`

​	`/`是什么意思？	比如`/root`，表示根目录下的`root`文件夹，`/`就是根目录。

`cd`是什么意思？	change directory，和 window 系统下使用方法一致。

`ls`查看当前目录下有多少目录（或目录）。我想进入这个目录

`cd temp`：进入temp目录下。可以看看当前目录下有什么，`ls`。

查看详细信息`ls -l`

返回上一级`cd ..`

​	第一列，有`d`的都是目录，比如：`drwxr-xr-x.`

`ls -a`查看隐藏的文件，`vim .test`创建一个名字为`test`的隐藏文件

`ls -lh`，h的中文是 human，人性化的展示文件列表

`ls -lha` ：参数可以合并在一起写

怎么写一些文本？使用 vim 编辑器。

`vim fileName `，`i`进入插入模式，写内容，按下`ESC`键，输入`:wq`退出。

打开文件怎么操作呢？两种方式：`vim fileName`或

`cat fileName`查看文件内容
`more fileName`慢慢的看文件（会显示文件阅读の进度）

`mkdir directory`创建目录

`mv fi_1 fi_2/`移动到**后边的文件夹**下，假如	fi\_1 和 fi\_2 是文件，则会覆盖。

`mkdir -p DIR1/DIR2/DIR3`表示递归式（`-p`）创建目录

`tree DIR`显示 DIR 目录树结构

# 2017-02-06-LInux 常用命令

1.查看命令是干嘛用的，`man`命令显示非常详细，`help`显示不太详细：

```
$ man 命令
$ 命令 --help
$ help cd 查看LINUX命令行一些内置命令
```

2.文件和目录操作（19）

```
# ls 目录
# cp xx xxx //拷贝，可以使用tab键补全
# find 路径 -name "[文件名]"
# find / -name "*.log"
# touch /var/log/app.log //创建文件名
# mkdir oldboyedu  //创建命令
# mkdir -p oldboyedu/edu01/
# mv yum.log /usr/local/    //移动文件
# tree a
	//乱码，# lang = EN
# pwd
# rm xxx //危险，尽量少用
	替代方案：设置一个tmp目录,当作回收站；
	#mv yu.log /etc/tmp
	# dd if=/dev/zero of=data bs=1G count=5 
	清空这个文件：
	# df -h
	# >data   //清空data
```

中间出现了一个小问题，因为`# dd if=/dev/zero of=data bs=1G count=5 `运行时间太长，所以需要结束：

```
# ps -ef | grep dd //ps查看当前运行的命令
# kill 26862  //26862代表dd的id
# kill -9 26862
```

有其他命令`basename`,`dirname`,`chattr`,`lsattr`,`file`,`md5sum`

3.查看文件及内容处理命令(19 个)：

```
# cat 文件				 // 查看文件内容
# grap 文字 文件			// 查看文件里面有没有文字
# grap -n 文字 文件			// -n 参数，显示多少行
# vim install.log +505 		// 可以快速跳到505行
```

4.文件压缩及解压命令（4个）

`tar`打包目录下文件。后接`./*`表示打包所有文件。也可以后接文件名，比如打包 install.log install.md readme.md 这三个文件。

```
# tar zcvf demo.tar.gz ./* 
# tar zcvf demo.tar.gz install.log install.md readme.md
```

可以下载：

```
# sz demo.tar.gz
# yum -y install lrzsz
```

5.信息显示命令(12个)

```
# df -h  		// 查看硬盘大小、使用空间、剩余空间、所占比例
# du -sh  		// 当前文件夹有多大
# ll -h 		// 查看每一个
# free -m		// 以 M 为单位查看服务器内存，剩余内存是第二行最后一个数值
# top 			// 当前服务器哪个程序消耗 CPU 或内存多
# htop
```

6.搜索文件

7.网络操作

```
# ip a 			//查看 ip 地址
```

8.系统安全

```
# useradd oldboy
# chown oldboy.oldboy oldboyedu/		// (用户 属主).(用户组 属组)
```

`rwxr-xr-x`：

- 三个一组：`rwx` 用户权限=7；`r-x`用户组权限=5；`r-x`其他人权限=5。
- `r` 表示 read 读；`w` 表示 write 写；`x` 表示 excute 执行。
- `r` 表示 4 ；`w` 表示 2 ；`x` 表示 1 。

改权限是使用`chmod`命令，权限不同，颜色不同。

```
# chmod 777 oldboyedu/
```

# 2017-02-06-Linux 命令详细

```
# top 			// 当前服务器哪个程序消耗 CPU 或内存多
```

CPU:

​	user: 用户进程所占的CPU

​	system：操作系统本身占用的cpu

​	idle：cpu 空闲率

​	iowait：CPU 等待IO时间比

mem：

​	total：

​	usage：内存使用

​	free：内存空闲	

```
# find / -name caixin
# find / -name *caixin*				//说明caixin可能前面有东西，后面有东西
								  //按文件名模糊查
#find / -size +1000000 |xarg ls sh	
#find / -size +1000000 |xarg ls sl
```

