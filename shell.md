1.文件操作

2.软件






1.文件 

	touch file              # 创建空白文件
	rm -rf 目录名           # 不提示删除非空目录(-r:递归删除 -f强制)
	dos2unix                # windows文本转linux文本  
	unix2dos                # linux文本转windows文本
	enca filename           # 查看编码  安装 yum install -y enca 
	md5sum                  # 查看md5值
	ln 源文件 目标文件      # 硬链接
	ln -s 源文件 目标文件   # 符号连接
	readlink -f /data       # 查看连接真实目录
	cat file | nl |less     # 查看上下翻页且显示行号  q退出
	head                    # 查看文件开头内容
	head -c 10m             # 截取文件中10M内容
	split -C 10M            # 将文件切割大小为10M
	tail -f file            # 查看结尾 监视日志文件
	file                    # 检查文件类型
	umask                   # 更改默认权限
	uniq                    # 删除重复的行
	uniq -c                 # 重复的行出现次数
	uniq -u                 # 只显示不重复行
	paste a b               # 将两个文件合并用tab键分隔开
	paste -d'+' a b         # 将两个文件合并指定'+'符号隔开
	paste -s a              # 将多行数据合并到一行用tab键隔开
	chattr +i /etc/passwd   # 设置不可改变位
	more                    # 向下分面器
	locate 字符串           # 搜索
	wc -l file              # 查看行数
	cp filename{,.bak}      # 快速备份一个文件
	\cp a b                 # 拷贝不提示 既不使用别名 cp -i
	rev                     # 将行中的字符逆序排列
	comm -12 2 3            # 行和行比较匹配
	iconv -f gbk -t utf8 原.txt > 新.txt    # 转换编码
	rename 原模式 目标模式 文件             # 重命名 可正则
	watch -d -n 1 'df; ls -FlAt /path'      # 实时某个目录下查看最新改动过的文件
	cp -v  /dev/dvd  /rhel4.6.iso9660       # 制作镜像
	diff suzu.c suzu2.c  > sz.patch         # 制作补丁
	patch suzu.c < sz.patch                 # 安装补丁
	
	sort排序{
	
		-t  # 指定排序时所用的栏位分隔字符
		-n  # 依照数值的大小排序
		-r  # 以相反的顺序来排序
		-f  # 排序时，将小写字母视为大写字母
		-d  # 排序时，处理英文字母、数字及空格字符外，忽略其他的字符
		-c  # 检查文件是否已经按照顺序排序
		-b  # 忽略每行前面开始处的空格字符
		-M  # 前面3个字母依照月份的缩写进行排序
		-k  # 指定域
		-m  # 将几个排序好的文件进行合并
		+<起始栏位>-<结束栏位>   # 以指定的栏位来排序，范围由起始栏位到结束栏位的前一栏位。
		-o  # 将排序后的结果存入指定的文
		n   # 表示进行排序
		r   # 表示逆序

		sort -n               # 按数字排序
		sort -nr              # 按数字倒叙
		sort -u               # 过滤重复行
		sort -m a.txt c.txt   # 将两个文件内容整合到一起
		sort -n -t' ' -k 2 -k 3 a.txt     # 第二域相同，将从第三域进行升降处理
		sort -n -t':' -k 3r a.txt         # 以:为分割域的第三域进行倒叙排列
		sort -k 1.3 a.txt                 # 从第三个字母起进行排序
		sort -t" " -k 2n -u  a.txt        # 以第二域进行排序，如果遇到重复的，就删除

	}

	find查找{

		# linux文件无创建时间
		# Access 使用时间  
		# Modify 内容修改时间  
		# Change 状态改变时间(权限、属主)
		# 时间默认以24小时为单位,当前时间到向前24小时为0天,向前48-72小时为2天
		# -and 且 匹配两个条件 参数可以确定时间范围 -mtime +2 -and -mtime -4
		# -or 或 匹配任意一个条件

		find /etc -name http         # 按文件名查找
		find . -type f               # 查找某一类型文件
		find / -perm                 # 按照文件权限查找
		find / -user                 # 按照文件属主查找
		find / -group                # 按照文件所属的组来查找文件
		find / -atime -n             # 文件使用时间在N天以内
		find / -atime +n             # 文件使用时间在N天以前
		find / -mtime -n             # 文件内容改变时间在N天以内
		find / -mtime +n             # 文件内容改变时间在N天以前
		find / -ctime +n             # 文件状态改变时间在N天前
		find / -ctime -n             # 文件状态改变时间在N天内
		find / -size +1000000c -print                           # 查找文件长度大于1M字节的文件
		find /etc -name "passwd*" -exec grep "xuesong" {} \;    # 按名字查找文件传递给-exec后命令
		find . -name 't*' -exec basename {} \;                  # 查找文件名,不取路径
		find . -type f -name "err*" -exec  rename err ERR {} \; # 批量改名(查找err 替换为 ERR {}文件
		find 路径 -name *name1* -or -name *name2*               # 查找任意一个关键字

	}

	vim编辑器{

		gconf-editor       # 配置编辑器
		/etc/vimrc         # 配置文件路径
		vim +24 file       # 打开文件定位到指定行
		vim file1 file2    # 打开多个文件	
		vim -O2 file1 file2    # 垂直分屏
		vim -on file1 file2    # 水平分屏
		sp filename        # 上下分割打开新文件
		vsp filename       # 左右分割打开新文件
		Ctrl+W [操作]      # 多个文件间操作  大写W  # 操作: 关闭当前窗口c  屏幕高度一样=  增加高度+  移动光标所在屏 右l 左h 上k 下j 中h  下一个w  
		:n                 # 编辑下一个文件
		:2n                # 编辑下二个文件
		:N                 # 编辑前一个文件
		:rew               # 回到首文件
		:set nu            # 打开行号
		:set nonu          # 取消行号
		200G               # 跳转到200
		:nohl              # 取消高亮
		:set autoindent    # 设置自动缩进
		:set ff            # 查看文本格式
		:set binary        # 改为unix格式
		ctrl+ U            # 向前翻页
		ctrl+ D            # 向后翻页
		%s/字符1/字符2/g   # 全部替换	
		X                  # 文档加密
	
	}

	归档解压缩{

		tar zxvpf gz.tar.gz -C 放到指定目录 包中的目录       # 解包tar.gz 不指定目录则全解压
		tar zcvpf /$path/gz.tar.gz * # 打包gz 注意*最好用相对路径
		tar zcf /$path/gz.tar.gz *   # 打包正确不提示
		tar ztvpf gz.tar.gz          # 查看gz
		tar xvf 1.tar -C 目录        # 解包tar
		tar -cvf 1.tar *             # 打包tar
		tar tvf 1.tar                # 查看tar
		tar -rvf 1.tar 文件名        # 给tar追加文件
		tar --exclude=/home/dmtsai -zcvf myfile.tar.gz /home/* /etc      # 打包/home, /etc ，但排除 /home/dmtsai
		tar -N "2005/06/01" -zcvf home.tar.gz /home      # 在 /home 当中，比 2005/06/01 新的文件才备份
		tar -zcvfh home.tar.gz /home                     # 打包目录中包括连接目录
		zgrep 字符 1.gz              # 查看压缩包中文件字符行
		bzip2  -dv 1.tar.bz2         # 解压bzip2
		bzip2 -v 1.tar               # bzip2压缩
		bzcat                        # 查看bzip2
		gzip A                       # 直接压缩文件 # 压缩后源文件消失
		gunzip A.gz                  # 直接解压文件 # 解压后源文件消失
		gzip -dv 1.tar.gz            # 解压gzip到tar
		gzip -v 1.tar                # 压缩tar到gz
		unzip zip.zip                # 解压zip
		zip zip.zip *                # 压缩zip
		# rar3.6下载:  http://www.rarsoft.com/rar/rarlinux-3.6.0.tar.gz
		rar a rar.rar *.jpg          # 压缩文件为rar包
		unrar x rar.rar              # 解压rar包
		7z a 7z.7z *                 # 7z压缩
		7z e 7z.7z                   # 7z解压

	}
	
	文件ACL权限控制{

		getfacl 1.test                      # 查看文件ACL权限
		setfacl -R -m u:xuesong:rw- 1.test  # 对文件增加用户的读写权限 -R 递归

	}
	
	svn更新代码{

		--force # 强制覆盖
		/usr/bin/svn --username user --password passwd co  $Code  ${SvnPath}src/                 # 检出整个项目
		/usr/bin/svn --username user --password passwd export  $Code$File ${SvnPath}src/$File    # 导出个别文件

	}

	恢复rm删除的文件{

		# debugfs针对 ext2   # ext3grep针对 ext3   # extundelete针对 ext4
		df -T   # 首先查看磁盘分区格式
		umount /data/     # 卸载挂载,数据丢失请首先卸载挂载,或重新挂载只读
		ext3grep /dev/sdb1 --ls --inode 2         # 记录信息继续查找目录下文件inode信息
		ext3grep /dev/sdb1 --ls --inode 131081    # 此处是inode
		ext3grep /dev/sdb1 --restore-inode 49153  # 记录下inode信息开始恢复目录

	}
	

2.软件

	rpm{

		rpm -ivh lynx          # rpm安装
		rpm -e lynx            # 卸载包
		rpm -e lynx --nodeps   # 强制卸载
		rpm -qa                # 查看所有安装的rpm包
		rpm -qa | grep lynx    # 查找包是否安装
		rpm -ql                # 软件包路径
		rpm -Uvh               # 升级包
		rpm --test lynx        # 测试
		rpm -qc                # 软件包配置文档
		rpm --import  /etc/pki/rpm-gpg/RPM-GPG-KEY-CentOS-6     # 导入rpm的签名信息

	}

	yum{

		yum list                 # 查找所有列表
		yum install 包名         # 安装包和依赖包
		yum -y update            # 升级所有包版本,依赖关系，系统版本内核都升级
		yum -y update 软件包名   # 升级指定的软件包
		yum -y upgrade           # 不改变软件设置更新软件，系统版本升级，内核不改变
		yum search mail          # yum搜索相关包
		yum grouplist            # 软件包组
		yum -y groupinstall "Virtualization"   # 安装软件包组
		
	}

	yum扩展源{

		# 包下载地址:http://download.fedoraproject.org/pub/epel   # 选择版本
		wget http://download.fedoraproject.org/pub/epel/5/i386/epel-release-5-4.noarch.rpm
		rpm -Uvh epel-release-5-4.noarch.rpm

	}

	自定义yum源{

		find /etc/yum.repos.d -name "*.repo" -exec mv {} {}.bak \;
		
		vim /etc/yum.repos.d/yum.repo
		[yum]
		#http
		baseurl=http://10.0.0.1/centos5.5
		#挂载iso
		#mount -o loop CentOS-5.8-x86_64-bin-DVD-1of2.iso /data/iso/
		#本地
		#baseurl=file:///data/iso/
		enable=1

		#导入key
		rpm --import  /etc/pki/rpm-gpg/RPM-GPG-KEY-CentOS-5

	}

	编译{

		源码安装{

			./configure --help                   # 查看所有编译参数
			./configure  --prefix=/usr/local/    # 配置参数
			make                                 # 编译
			make install                         # 安装包
			make clean                           # 清除编译结果

		}

		perl程序编译{

			perl Makefile.PL
			make
			make test
			make install

		}

		python程序编译{

			python file.py
			
			# 源码包编译安装
			python setup.py build
			python setup.py install

		}
		
		编译c程序{

			gcc -g hello.c -o hello

		}
	
	}
	

