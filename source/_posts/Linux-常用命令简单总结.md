title: Linux 常用命令简单总结
author: suijiafeng
date: 2018-05-06 13:06:10
tags:
---
## 包管理器 ##
apt-get Debian/Ubuntu系统包管理器
apt-get 是Debian/Ubuntu系统中 一个用于快速下载/安装的简单命令行管理工具！

使用示例：
	
	# 检索 新的包列表
	apt-get update
	 
	# 升级 可更新的所有软件包（注意这个命令会升级所有的软件包，所以会升级很长时间）
	apt-get upgrade
	 
	# 安装 Nginx 软件包
	apt-get install nginx
	 
	# 卸载 Nginx 软件包
	apt-get remove nginx
	 
	# 卸载 Nginx 软件包 并删除所有相关配置文件
	apt-get remove --purge nginx
	 
	# 在安装软件和卸载的时候，为了避免误操作，都会询问是否继续，每次都要输入 y 来确定会很麻烦，可以加上 -y 参数
	# 安装 Nginx 软件包 并不显示确定提示
	apt-get install nginx -y
	 
	# 卸载 Nginx 软件包，删除所有相关配置文件 并不显示提示
	apt-get remove --purge nginx -y
	 
	# 清除 旧的/无用 的软件包
	apt-get clean && apt-get autoclean
	 
	# 下载 Nginx 二进制软件包到当前目录，但不解压和安装
	apt-get download nginx -d
	 
	# 更多的命令可以用 apt-get --help 查看。

yum CentOS系统包管理器
yum 是CentOS系统中 一个用于快速下载/安装的简单命令行管理工具！
	
	使用示例：
	
	# 检索 新的包列表
	yum update
	 
	# 安装 Nginx 软件包
	yum install nginx
	 
	# 安装 Development Tools 软件包组（这个软件包组中包含了编译所需的软件）
	# 注意：当软件包或者软件包组的名字中包含空格的时候，请把 软件包或软件包组 加上双引号！
	yum groupinstall "Development Tools"
	 
	# 卸载 Nginx 软件包
	yum erase nginx / yum remove nginx
	 
	# 卸载 Development Tools 软件包组
	yum groupremove "Development Tools"
	 
	# 升级 所有可更新的软件包
	yum upgrade
	 
	# 升级 Nginx 可更新的软件包
	yum upgrade nginx
	 
	# 在安装软件和卸载的时候，为了避免误操作，都会询问是否继续，每次都要输入 y 来确定会很麻烦，可以加上 -y 参数
	# 安装 Nginx 软件包 并不显示确定提示
	yum install nginx -y
	 
	# 卸载 Nginx 软件包 并不显示确定提示
	yum erase nginx -y / yum remove nginx -y
	 
	# 搜索 Nginx 软件包是否存着
	yum search nginx
	 
	# 列出 可用的软件包
	yum list
	 
	# 列出 可用的软件包组
	yum grouplist
	 
	# 清除 缓存目录中的所有软件包
	yum clean
	 
	# 清除 缓存目录中的 Nginx 软件包
	yum clean nginx
	 
	# 重装 Nginx 软件包
	yum reinstall nginx


## 文件/文件夹 操作 ##
以下除特殊说明，都以当前目录为 /root 示例。

mkdir 新建 文件夹
点击展开 查看 mkdir命令说明
	
	# 在当前文件夹新建一个 bash 文件夹，完整的绝对路径就是 /root/bash
	mkdir bash
	 
	# 更多的命令可以用 mkdir --help 查看。
	cd 进入 文件夹
	点击展开 查看 cd命令说明
	
	# 你当前在 /root目录中，使用这个命令会进入 /root/bash目录，这是相对路径
	cd bash
	# 如果你不在 /root目录中的话，就不能用上面的相对路径了，就需要绝对路径
	cd /root/bash
	————————————————————————————————————————————————————————————————————————————
	# 假设你当前在 /root/bash目录中，使用相对路径，你可以用这个命令进入上一级 /root目录， .. 代表相对路径 上级目录
	cd ..
	# 当然你也可以用绝对路径来进入上一级 /root目录
	cd /root

cp 复制或重命名 文件/文件夹
 查看 cp命令说明
	
	# 复制当前目录内的 log.txt文件到 /var目录
	cp log.txt /var/log.txt
	# 复制当前目录内的 bash文件夹到 /home目录
	cp -R bash /home/bash
	————————————————————————————————————————————————————————————————————————————
	# 复制当前目录内的所有.txt后缀的文件到 /var/log目录
	cp *.txt /var/log
	# 复制当前目录内的所有以 doubi开头的文件到 /var/log目录
	cp doubi* /var/log
	# 复制当前目录内的所有以 doubi开头 以.txt后缀结尾的文件到 /var/log目录
	cp doubi*.txt /var/log
	————————————————————————————————————————————————————————————————————————————
	# 假设当前目录是 /root/doubi/log，要把这个目录中的所有.txt后缀的文件复制到上一级目录 /root/doubi，那么这样做
	cp *.txt ..
	# .. 就是相对路径，代表上一级目录，当然你也可以用绝对路径，这样更不容易出错
	cp *.txt /root/doubi
	————————————————————————————————————————————————————————————————————————————
	# 重命名当前目录内的 log.txt文件为 log2.txt
	cp log.txt log2.txt
	# 复制当前目录内的 log.txt文件到 /var目录并重命名为 log1.txt
	cp log.txt /var/log1.txt
	# 复制当前目录内的 bash文件夹到 /home目录并重命名为 bash2
	cp -R bash /home/bash2
	————————————————————————————————————————————————————————————————————————————
	# 复制当前目录内的 log.txt文件到 /var目录，但是 /var 目录中已经存着 log.txt，那么会提示 cp: overwrite `/var/log.txt'? 可以用 -f 强制覆盖
	cp -f log /var/log.txt
	# 复制当前目录内的 log.txt log1.txt log2.txt文件和 log233目录到 /home/log目录中
	cp -R log.txt log1.txt log2.txt log233 /home/log
	 
	# 更多的命令可以用 cp --help 查看。
mv 移动或重命名 文件/文件夹
 查看 mv命令说明

	# 关于 mv 命令，可以参考上面 cp 的使用方法，没什么区别，只是一个是复制，一个是移动，把上面 cp 命令改成 mv 就能套用了。
	 
	# 移动当前目录内的 log.txt文件到 /var目录
	mv log.txt /var/log.txt
	# 移动当前目录内的 bash文件夹到 /home目录
	mv bash /home/bash
	————————————————————————————————————————————————————————————————————————————
	# 重命名当前目录内的 log.txt文件为 log2.txt
	mv log.txt log2.txt
	# 复制当前目录内的 log.txt文件到 /var目录并重命名为 log1.txt
	mv log.txt /var/log1.txt
	# 复制当前目录内的 bash文件夹到 /home目录并重命名为 bash2
	mv bash /home/bash2
	 
	# 更多的命令可以用 mv --help 查看。
rm 删除 文件/文件夹
 查看 rm命令说明
	
	# 删除当前目录下的 log.txt文件
	rm log.txt
	# 删除当前目录下所有.txt后缀的文件
	rm *.txt
	# 使用 rm 命令删除时，会提示你是否确定删除，输入 y 即删除，输入 n 则取消
	# rm: remove regular file `log.txt'? y
	————————————————————————————————————————————————————————————————————————————
	# 删除当前目录下所有.txt后缀的文件
	rm *.txt
	# 删除当前目录下所有以 doubi开头的文件
	rm doubi*
	# 删除当前目录下所有以 doubi开头 以.txt后缀结尾的文件
	rm doubi*.txt
	————————————————————————————————————————————————————————————————————————————
	# 当你用 rm 删除目录的时候会发现提示这不是一个文件
	# rm bash
	# rm: cannot remove `bash': Is a directory
	# 可以加上 -r 来归递删除目录及其目录下的内容
	rm -r bash
	————————————————————————————————————————————————————————————————————————————
	# 因为为了避免手误删除错误，所以 rm默认是加上了 -i 的参数，也就是每一次删除文件/目录都会提示，如果觉得烦可以用 -rf 参数
	rm -rf bash
	# rm -rf 这个命令请慎重使用，而且千万不要使用 rm -rf / 或者 rm -rf /* 之类的命令(系统自杀)，可能会让你系统爆炸，所以使用请慎重！
	 
	# 更多的命令可以用 rm --help 查看。
## 查看/编辑文件 操作 ##
ls 显示目录中文件
 查看 ls命令说明
	
	# 显示当前目录下的所有文件
	ls -a
	————————————————————————————————————————————————————————————————————————————
	# 命令后面加上 绝对路径/相对路径 就会显示指定文件夹内的所有文件
	ls -a bash/log
	# 相对路径，当前目录是 /root ，欲查看的目录是 /root/bash/log
	ls -a /root/bash/log
	# 绝对路径， 当前目录是 /root ，欲查看的目录是 /root/bash/log
	 
	# 更多的命令可以用 ls --help 来查看。
du 查看 文件/文件夹 占用磁盘空间的大小
 查看 du命令说明
	
	使用示例：
	
	# 显示 /root 文件夹的大小，但不显示其子目录和文件的大小
	du -sh
	 
	# 显示 /root 文件夹的大小，并显示其子目录和文件的大小
	du -ah
	 
	# 待写...
	 
	# 更多的命令可以用 du --help 来查看。
cat 查看文件内容
	 查看 cat命令说明
	
	假设 log.txt文件的内容为：
	
	doubi233
	doubi
	 
	 
	doubi666
	 
	doubi2366
	doubi8888
	查看文件：
	
	# 查看 log.txt文件的所有内容
	cat log.txt
	# 输出示例如下
	doubi233
	doubi
	 
	 
	doubi666
	 
	doubi2366
	doubi8888
	 
	# 查看 log.txt文件的所有内容，并对所有行编号
	cat -n log.txt
	# 输出示例如下：
	     1	doubi233
	     2	doubi
	     3	
	     4	
	     5	doubi666
	     6	
	     7	doubi2366
	     8	doubi8888
	 
	# 查看 log.txt文件的所有内容，并对非空行编号
	cat -b log.txt
	# 输出示例如下：
	     1	doubi233
	     2	doubi
	 
	 
	     3	doubi666
	 
	     4	doubi2366
	     5	doubi8888
	 
	# 查看 log.txt文件的所有内容，并对非空行编号，且不输出多行空行
	cat -bs log.txt
	# 输出示例如下：
	     1	doubi233
	     2	doubi
	 
	     3	doubi666
	 
	     4	doubi2366
	     5	doubi8888
	清空文件：
	
	# 清空当前目录中的 log.txt 文件
	cat /dev/null > log.txt
	 
	# 清空 /var目录中的 log.txt 文件
	cat /dev/null > /var/log.txt
	写入文件：
	
	# 写入文本到当前目录中的 log.txt文件中(加入文本到文件内容最后)
	cat >> log.txt <<-EOF
	doubi
	doubi233
	doubi666
	EOF
	 
	# 清空文件并写入文本到 /var目录中的 log.txt文件中(先清空后写入)
	cat > /var/log.txt <<-EOF
	doubi
	doubi233
	doubi666
	EOF
	 
	# 更多的命令可以用 cat --help 来查看。
head 查看文件内容（主要用于正查）
	
	使用示例：
	
	假设 log.txt 文件内容为：
	
	doubi1
	doubi2
	doubi3
	doubi4
	doubi5
	# 查看 log.txt文件的全部内容
	head log.txt
	 
	# 查看 log.txt文件的前 4字节的内容
	head -c 4 log.txt
	 
	# 输出示例
	doub
	 
	# 查看 log.txt文件的前 2行的内容
	head -n 2 log.txt
	 
	# 输出示例
	doubi1
	doubi2
	 
	# 查看 log.txt文件的从倒数第2行到行首的内容
	head -n -2 log.txt
	 
	# 输出示例
	doubi1
	doubi2
	doubi3
	 
	# 查看 log.txt log1.txt log2.txt文件的前 3行内容
	head -n 3 log.txt log1.txt log2.txt
	 
	# 更多的命令可以用 head --help 来查看。
tail 查看文件内容（主要用于倒查）
	
	使用示例：
	
	假设 log.txt 文件内容为：
	
	doubi1
	doubi2
	doubi3
	doubi4
	doubi5
	# 查看 log.txt文件的全部内容
	tail log.txt
	 
	# 查看 log.txt文件从行首 第25字节到最后的内容
	tail -c +25 log.txt
	 
	# 输出示例
	bi4
	doubi5
	 
	# 查看 log.txt文件从行尾 第4字节到最前面的内容
	tail -c -4 log.txt
	 
	# 输出示例
	bi5
	 
	# 查看 log.txt文件的从第2行到最后一行的内容
	tail -n +2 log.txt
	 
	# 输出示例
	doubi2
	doubi3
	doubi4
	doubi5
	 
	# 查看 log.txt文件的后 2行的内容
	tail -n -2 log.txt
	 
	# 输出示例
	doubi4
	doubi5
	 
	# 持续查看（监视） log.txt文件的变化内容（新增加的内容），使用 Ctrl＋C 终止
	tail -f log.txt
	 
	# 查看 log.txt log1.txt log2.txt文件的前 3行内容
	tail -n 3 log.txt log1.txt log2.txt
	 
	# 更多的命令可以用 tail --help 来查看。
sed 查看/编辑文件内容
 查看 sed命令说明
	
	参数介绍：
	
	-i ：操作后应用保存到原文件（如果不加这个参数，那么任何修改都不会影响原文件里的内容，只会把结果输出）
	# 待写...
	 
	# 更多的命令可以用 sed --help 来查看。
	使用示例：
	
	# 查看 log.txt 第3行的内容
	sed '3p' log.txt
	 
	# 查看 log.txt 第2-8行的内容
	sed '2,8p' log.txt
	 
	# 删除 log.txt 第4行
	sed -i '4d' log.txt
	 
	# 删除 log.txt 第3-7行
	sed -i '3,7d' log.txt
	 
	# 删除 log.txt 第1行
	sed -i '1d' log.txt
	 
	# 删除 log.txt 最后1行
	sed -i '$d' log.txt
	 
	# 删除 log.txt 文件中所有包含 233内容的行
	sed -i '/233/d' log.txt
	 
	# 替换 log.txt 文件中所有 233为666
	sed -i 's/233/666/' log.txt
	 
	# 替换 log.txt 文件中所有 /ver 为 doubi/，因为有斜杠，所以需要使用 \ 转义，但是单引号会导致无法转义，所以要改成双引号。
	sed -i "s/\/ver/doubi\//" log.txt
	 
	# 待写...
	 
	# 更多的命令可以用 sed --help 来查看。
## vim 编辑文件内容 ##
 查看 vim 命令说明

vim 介绍

vim 相当于 vi的扩展或者加强版，一些系统只安装了 vi，所以想要用 vim还需要手动安装( yum install vim -y / apt-get install vim -y)，安装 vim后，会自动替换或者说整合 vi。

当你使用 vi 命令的时候，首先进入的是 命令行模式，这个模式就是 vi 自身的功能，而点击 I 键 后就会进入编辑模式(插入模式)，这时候就可以直接输入字符了，这个就是 vim的扩展功能了。当修改完成后，按 ESC键 即可退出编辑模式回到命令行模式，这时候输入 :wq 并回车代表保存并退出，如果不想保存可以使用 :q! 不保存强制退出。

vim的命令行 命令很多，我也没打算都写出来，只写出最常用的好了。
	
	# 打开当前目录下的 log.txt文件，如果没有那么会新建 log.txt文件（安装vim后，使用 vi和 vim打开文件没区别）
	vi log.txt
	vim log.txt
	 
	# 在命令行模式下，直接输入以下 符号和字母(区分大小写)
	## 进入编辑模式（插入模式，按 Esc键 即可返回命令行模式）
	i
	## 删除光标当前所在的一行
	dd
	## 删除文件内所有内容
	dddG
	## 复制光标当前所在的一行
	yy
	## 粘贴刚才复制的一行内容
	p
	## 撤销上个操作（误操作可以用这个恢复）
	u
	## 保存当前文件（ : 是英文的冒号）
	:w
	## 另存当前文件内容为 log2.txt
	:w log2.txt
	## 退出当前文件
	:q
	## 不保存 并强制退出当前文件
	:q!
	## 保存并退出当前文件
	:wq
	 
	# 更多的命令可以用 vi --help / vim --help 来查看。
 
## 解压缩 操作 ##
在Linux中经常会下载到压缩文件，而压缩文件的格式有很多，比如 zip、rar、gz、xz、tar.gz、tar.xz等。

tar gz zip等 解压 压缩包 示例
 查看 解压压缩包说明
	
	# 解压后缀为 .tar 的压缩包
	tar -xf log.tar
	————————————————————————————————————————————————————————————————————————————
	# 解压后缀为 .tar.xz 的压缩包
	tar -xJf log.tar.xz
	————————————————————————————————————————————————————————————————————————————
	# 解压后缀为 .tar.gz 的压缩包，有两个方法
	tar -xzf log.tar.gz
	————————————————————————————————————————————————————————————————————————————
	# 解压后缀为 .gz 的压缩包，有两个方法，如提示命令不存在，请安装 yum install gzip -y / apt-get install gzip -y
	gzip -d log.gz
	gunzip log.gz
	————————————————————————————————————————————————————————————————————————————
	# 解压后缀为 .bz / .bz2 / tar.bz2 的压缩包，有两个方法
	bzip2 -d log.bz
	bunzip2 log.bz
	tar -jxf log.tar.bz
	 
	bzip2 -d log.bz2
	bunzip2 log.bz2
	tar -jxf log.tar.bz2
	————————————————————————————————————————————————————————————————————————————
	# 解压后缀为 .Z / tar.Z 的压缩包，有两个方法
	uncompress log.Z log.txt
	uncompress log.Z log
	————————————————————————————————————————————————————————————————————————————
	tar xZf log.tar.Z log.txt
	tar xZf log.tar.Z log
	————————————————————————————————————————————————————————————————————————————
	# 解压后缀为 .rar 的压缩包，如提示命令不存在，请安装 yum install unrar -y / apt-get install unrar -y ，注意 rar 和 unrar 是分开的
	unrar x log.rar
	————————————————————————————————————————————————————————————————————————————
	# 解压后缀为 .zip 的压缩包，如提示命令不存在，请安装 yum install unzip -y / apt-get install unzip -y，注意 zip 和 unzip 是分开的
	unzip log.zip
	 
	# 更多的命令可以用 tar --help / gzip --help / unrar --help / unzip --help 来查看。
	压缩 文件/文件夹 示例
	点击展开 查看 压缩文件/文件夹说明
	
	# 分别压缩当前目录下的 log.txt文件 / log文件夹为 log.tar 压缩包
	tar -cf log.tar log.txt
	tar -cf log.tar log
	————————————————————————————————————————————————————————————————————————————
	# 如果要压缩多个文件和文件夹，那么只需要在后面一直加下去即可
	tar -cf log.tar log.txt doub.txt log bash
	————————————————————————————————————————————————————————————————————————————
	# 分别压缩当前目录下的 log.txt文件 / log文件夹为 log.tar.xz 压缩包，以下的其他后缀压缩命令都是一样
	tar -cJf log.tar.xz log.txt
	tar -cJf log.tar.xz log
	————————————————————————————————————————————————————————————————————————————
	# 分别压缩当前目录下的 log.txt文件 / log文件夹为 log.tar.gz 压缩包
	tar -czf log.tar.gz log.txt
	tar -czf log.tar.gz log
	————————————————————————————————————————————————————————————————————————————
	# 分别压缩当前目录下的 log.txt文件 / log文件夹为 log.gz 压缩包
	gzip log.gz log.txt
	gzip log.gz log
	————————————————————————————————————————————————————————————————————————————
	# 分别压缩当前目录下的 log.txt文件 / log文件夹为 log.tar.bz 压缩包
	暂时没查到
	————————————————————————————————————————————————————————————————————————————
	# 分别压缩当前目录下的 log.txt文件 / log文件夹为 log.bz / log.tar.bz / log.bz2 / log.tar.bz2压缩包
	bzip2 -z log.txt
	bzip2 -z log
	 
	tar cjf log.tar.bz2 log.txt
	tar cjf log.tar.bz2 log
	————————————————————————————————————————————————————————————————————————————
	# 分别压缩当前目录下的 log.txt文件 / log文件夹为 log.Z / log.tar.Z 压缩包
	compress log.txt
	compress log
	 
	tar cZf log.tar.Z log.txt
	tar cZf log.tar.Z log
	————————————————————————————————————————————————————————————————————————————
	# 分别压缩当前目录下的 log.txt文件 / log文件夹为 log.rar 压缩包，如提示命令不存在，请安装 yum install rar -y / apt-get install rar -y ，注意 rar 和 unrar 是分开的
	unrar a log.rar log.txt
	unrar a log.rar log
	————————————————————————————————————————————————————————————————————————————
	# 分别压缩当前目录下的 log.txt文件 / log文件夹为 log.zip 压缩包，如提示命令不存在，请安装 yum install zip -y / apt-get install zip -y ，注意 zip 和 unzip 是分开的
	zip log.zip log.txt
	zip log.zip log
	 
	# 更多的命令可以用 tar --help / gzip --help / rar --help / zip --help 来查看。
## 网络工具 ##
wget 下载工具
wget 是Linux系统最常用的工具之一，命令行方式的多功能下载工具，支持HTTP，HTTPS和FTP协议。

 查看 wget命令说明
	
	使用示例：
	
	# 下载一个文件到当前目录
	wget https://softs.fun/100MB.bin
	 
	# 下载文件到当前目录并重命名为 200MB.bin
	wget -O "200MB.bin" https://softs.fun/100MB.bin
	 
	# 下载文件到 /root目录（-P只能指定下载目录，并不能指定文件名）
	wget -P "/root" https://softs.fun/100MB.bin
	 
	# 下载文件到 /root/doubi目录并重命名为 200MB.bin
	wget -O "/root/doubi/200MB.bin" https://softs.fun/100MB.bin
	 
	# 下载文件完成之前 wget进程结束了，那么可以使用断点续传重新下载中断的文件（前提是下载服务器支持断点续传）
	wget -c https://softs.fun/100MB.bin
	# 通过后台下载文件到 /root/doubi目录并重命名为 200MB.bin
	wget -b -O "/root/doubi/200MB.bin" https://softs.fun/100MB.bin
	# Continuing in background, pid 2333.
	# Output will be written to `wget-log'.
	# 后台下后，你可以使用以下命令来查看下载进度：
	tail -f wget-log
	 
	# 有时候一些Linux系统中的SSL证书不完整，会导致下载一些 HTTPS网站文件的时候会验证SSL证书失败，可以这样做
	# 不验证服务器SSL证书，下载文件到当前目录并重命名为 200MB.bin
	wget --no-check-certificate -O "200MB.bin" https://softs.fun/100MB.bin
	 
	# 使用wget发送POST请求数据
	wget --post-data "user=doubi&passwd=23333" https://xxx.xx/
	 
	# 下载文件到当前目录 并仅通过IPv4连接 只获取比本地新的文件，限速 200KB/S
	wget --limit-rate=200k -N -4 https://softs.fun/100MB.bin
	 
	# 下载文件到当前目录 并重试次数为 1，超时时间为 2秒
	wget -t1 -T2 https://softs.fun/100MB.bin
	 
	# 通过 wget来获取服务器的外网IP（-qO- 代表运行完会输出下载的信息，并不会保存到本地文件）
	wget -qO- ipinfo.io/ip
	 
	# 更多的命令可以用 wget --help 来查看。

curl 下载工具
curl是Linux系统一个利用URL规则在命令行下工作的文件传输工具，是一款很强大的HTTP命令行工具。它支持文件的上传和下载，是综合传输工具，但习惯称curl为下载工具。
点击展开 查看 curl命令说明

使用示例：
	
	# 获取当前服务器的外网IP
	curl ipinfo.io/ip
	 
	# 获取一个文件保存到当前目录中
	wget -O https://softs.fun/Bash/ssr.sh
	 
	# 获取一个文件保存到 /root/doubi目录中 并修改文件名为 233.sh
	curl -o "/root/doubi/233.sh" https://softs.fun/Bash/ssr.sh
	 
	# 下载文件完成之前 curl进程结束了，那么可以使用断点续传重新下载中断的文件（前提是下载服务器支持断点续传）
	curl -C -O https://softs.fun/100MB.bin
	 
	# 有时候一些Linux系统中的SSL证书不完整，会导致访问/下载一些 HTTPS网站/文件的时候会验证SSL证书失败，可以这样做
	# 不验证服务器SSL证书，下载文件到当前目录并重命名为 233.sh
	curl -k -o "233.sh" https://softs.fun/Bash/ssr.sh
	 
	# 使用curl发送GET请求数据
	curl https://xxx.xx/?user=doubi
	 
	# 使用curl发送POST请求数据
	curl --data "user=doubi&passwd=23333" https://xxx.xx/
	 
	# 下载文件到当前目录 并仅通过IPv4连接，限速 200KB/S
	curl --limit-rate 200K -4 https://softs.fun/100MB.bin
	 
	# 下载文件到当前目录 并重试次数为 1，超时时间为 2秒
	curl --retry 1 -m 10 https://softs.fun/100MB.bin
	 
	# 更多的命令可以用 curl --help 来查看。
netstat 查看链接和端口监听等信息
  查看 netstat命令说明
	
	使用示例：
	
	# 显示当前服务器的所有连接信息
	netstat -a
	 
	# 显示当前服务器的所有 TCP连接信息
	netstat -at
	 
	# 显示当前服务器的所有 UDP连接信息
	netstat -au
	一般来说经常使用这个命令：
	
	# 显示当前服务器的所有正在监听 TCP端口的信息，并且 显示进程PID和进程名，但不显示别名（域名以IP显示），这个命令算是最常用的了。
	netstat -lntp
	 
	# 输出示例
	Active Internet connections (only servers)
	Proto Recv-Q Send-Q Local Address           Foreign Address         State       PID/Program name
	tcp        0      0 0.0.0.0:80              0.0.0.0:*               LISTEN      14233/nginx.conf
	tcp        0      0 0.0.0.0:22              0.0.0.0:*               LISTEN      1555/sshd       
	tcp        0      0 0.0.0.0:443             0.0.0.0:*               LISTEN      14233/nginx.conf
	tcp6       0      0 :::22                   :::*                    LISTEN      1555/sshd
	# 显示监听 80端口的进程PID和进程名，grep是匹配并显示 符合关键词的行。
	netstat -lntp|grep ":80"
	 
	# 输出示例
	Active Internet connections (only servers)
	Proto Recv-Q Send-Q Local Address           Foreign Address         State       PID/Program name
	tcp        0      0 0.0.0.0:80              0.0.0.0:*               LISTEN      14233/nginx.conf
	 
	# 显示 ssh的监听情况，grep是匹配并显示 符合关键词的行。
	netstat -lntp|grep "ssh"
	 
	# 输出示例
	Active Internet connections (only servers)
	Proto Recv-Q Send-Q Local Address           Foreign Address         State       PID/Program name
	tcp        0      0 0.0.0.0:22              0.0.0.0:*               LISTEN      1555/sshd
	表头解释：
	
	Proto ：连接协议（tcp/udp是IPv4，tcp6/udp6是IPv6）
	Recv-Q ： 接收队列（基本都是0，如果不是代表堆积）
	Send-Q ：发送队列（基本都是0，如果不是代表堆积）
	Local Address ：本地地址和端口
	Foreign Address ：对外地址和端口
	State ：连接状态
	PID/Program name ：进程PID/进程名
	# 每隔 1秒显示一次当前服务器的所有连接信息
	netstat -c
	 
	# 每隔 1秒显示一次当前服务器的所有 TCP连接信息
	netstat -ct
	 
	# 每隔 1秒显示一次当前服务器的所有 UDP连接信息
	netstat -cu
	 
	# 显示当前服务器的路由表
	netstat -r
	 
	# 显示当前服务器的网络接口信息（网卡）
	netstat -i
	 
	# 显示当前服务器的网络统计信息
	netstat -s
	 
	# 更多的命令可以用 netstat --help 来查看。

在使用 netstat命令中，会显示一些连接状态，下面是各状态的意思：
	
	LISTEN
	# 监听来自远程连接的 TCP端口连接请求
	SYN-SENT
	# 在发送连接请求后，等待匹配的连接请求
	SYN-RECEIVED
	# 在收到和发送一个连接请求后，等待对方对连接请求的确认
	ESTABLISHED
	# 代表一个打开的连接
	FIN-WAIT-1
	# 等待远程 TCP连接中断请求，或先前的连接中断请求的确认
	FIN-WAIT-2
	# 从远程 TCP等待连接中断请求 
	CLOSE-WAIT
	# 等待从本地用户发来的连接中断请求 
	CLOSING
	# 等待远程TCP对连接中断的确认 
	LAST-ACK
	# 等待原来的发向远程TCP的连接中断请求的确认 
	TIME-WAIT
	# 等待足够的时间，以确保远程TCP接收到连接中断请求的确认 
	CLOSED
	# 没有任何连接状态（或者关闭了连接）
	系统命令

date 查看/设置 系统时间
	 查看 date命令说明
	
	使用示例：
	
	# 显示 当前系统时间
	date
	# 输出：Wed Apr 5 12:38:44 CST 2017
	 
	# 显示当前系统的 UTC时间
	date -u
	# 输出：Wed Apr 5 04:30:06 UTC 2017
	# 显示 log.txt 文件的最后修改时间
	date -r log.txt
	# 显示 当前日期的年份
	date +%Y
	# 输出：2017
	 
	# 显示 当前日期的月份
	date +%m
	# 输出：4
	 
	# 显示 各种格式类型的日期
	date +%D
	# 输出：04/05/17
	 
	date +%Y-%m-%d
	# 输出：2017-04-05
	 
	date +%m/%d/%y
	# 输出：04/05/17
	 
	date +%m/%d/%Y
	# 输出：04/05/2017
	 
	# 显示 Unix时间戳
	date +%s
	# 输出：1491367399
	 
	# 显示一个完整的时间（年、月、日、小时、分钟、秒钟、周几 时区）
	date "+%Y-%m-%d %H:%M:%S %u %Z"
	# 输出：2017-04-05 12:12:15 3 CST
	 
	# 设置 系统时间（年、月、日）
	date -s "2017-04-05"
	 
	# 设置 系统时间（小时、分钟、秒钟）
	date -s "10:29:05"
	 
	# 设置 系统时间（年、月、日、小时、分钟、秒钟）
	date -s "2017-04-05 10:29:05"
	 
	# 更多的命令可以用 date --help 来查看。

再教你们一个修改时区为上海（北京）时区的方法：

cp /usr/share/zoneinfo/Asia/Shanghai /etc/localtime
然后再用 date 查看时间，就会发现时区变为 CST 了。

chmod 修改 文件/文件夹 权限
点击展开 查看 chmod命令说明

	参数介绍：
	
	-c :只输出被改变权限的文件信息
	-f :当chmod不能改变文件模式时，不通知文件的用户
	-R :可递归遍历子目录，把修改应到目录下所有文件和子目录
	-v :无论修改是否成功，输出每个文件的信息
	 
	# 操作符号：
	 
	+ :添加某个权限。
	- :取消某个权限。
	= :赋予给定权限并取消其他所有权限（如果有的话）。
	 
	# 权限设置字母：
	 
	r :可读
	w :可写
	x :可执行
	X :只有目标文件对某些用户是可执行的或该目标文件是目录时才追加x 属性
	s :在文件执行时把进程的属主或组ID置为该文件的文件属主。方式“u＋s”设置文件的用户ID位，“g＋s”设置组ID位
	t :保存程序的文本到交换设备上
	u :当前用户的权限
	g :当前用户同组的权限
	o :其他用户的权限
	 
	# 权限设定数字：
	 
	# 数字表示的属性含义：
	0 ：表示没有权限
	1 ：表示可执行权限
	2 ：表示可写权限
	4 ：表示可读权限
	 
	# 然后将其相加，所以数字属性的格式应为3个从0到7的八进制数，其顺序是（u）（g）（o）。
	# 如果想让某个文件的属主有“读/写”二种权限，需要把4（可读）+2（可写）＝6（读/写）。
	 
	# 更多的命令可以用 chmod --help 来查看。
	使用示例：
	
	# 当需要运行 可执行的脚本或者程序（比如 Go语言编写的软件）的时候，需要赋予执行权限
	chmod +x ssr.sh
	 
	# 赋予 log.txt 文件可读权限
	chmod 444 log.txt
	 
	# 赋予 /ver/log 文件夹 可读、可写权限
	chmod 666 log.txt
	 
	# 赋予 /home/www 文件夹 可读、可写、可执行权限
	chmod 777 log.txt
	 
	# 赋予 /home/www 文件夹极其所有子目录和文件 可读、可写、可执行权限
	chmod -R 777 log.txt
	# 更多的命令可以用 chmod --help 来查看。
## uname 获取操作系统信息 ##
 查看 uname命令说明

		使用示例：
		
		root@doub.date:~# uname       #在使用 uname 的时候，相当于是使用 uname -s
		Linux
		root@doub.date:~# uname -a
		Linux doub.date 2.6.32-042stab120.6 #1 SMP Thu Oct 27 16:59:03 MSK 2016 i686 GNU/Linux
		root@doub.date:~# uname -m       #输出一般是64位: x86_64 / 32位: i386 或分支 i686 
		i686
		root@doub.date:~# uname -n
		doub.date
		root@doub.date:~# uname -r
		2.6.32-042stab120.6
		root@doub.date:~# uname -s
		Linux
		root@doub.date:~# uname -v
		#1 SMP Thu Oct 27 16:59:03 MSK 2016
		root@doub.date:~# uname -p
		unknown
		root@doub.date:~# uname -i
		unknown
		root@doub.date:~# uname -o
		GNU/Linux
        
我暂时总结到这里，我以后用到还会继续慢慢添加的，