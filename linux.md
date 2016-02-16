<h5 id="top">顶端</h5> 


<font color="red">目录</font>



通用
[系统命令](#syscmd)
[vim](#vim) 
[ssh](#ssh)
[终端快捷键](#hotkey)
[开机启动脚本顺序](#start)

系统信息
[系统信息](#sysinfo) 
[硬件信息](#hardinfo)

系统状态
[netstat](#netstat)
[network](#network)
[disk](#disk)
[xfs](#xfs)
[nfs](#nfs)
[raid](#raid)
[process](#process)


软件管理
[rpm](rpm)
[yum](yum)

日志
[history](#history)
[日志](#log)

操作
[find](#find)
[sort](#sort)
[解压](#tar)

用户
[user](#user)
[sudo](#sudo)

内核
[ulimit](#ulimit) 

安全
[iptables](iptables)|
[selinux](#selinux)

服务管理
[chkconfig](#chkconfig)
[crontab](crontab)
[at](#at)

系统设置
[date](#date)
[ntp](#ntp) --------

故障排查
[tcpdump](#tcpdump)
[dmesg](#dmesg)   ------

[内核相关](Kernel)



<h5 id="hotkey">终端快捷键</h5> 

		Ctrl+A        　    # 行前
		Ctrl+E        　    # 行尾
		Ctrl+r      　      # 搜索history
		Ctrl+S        　    # 终端锁屏
		Ctrl+Q        　　  # 解锁屏
		Ctrl+D      　　    # 退出

* mac 中

		contrl+A      　    # 行前
		contrl+e      　    # 行尾
		contrl+r      　    # 搜索history

<h5 id="start">开机启动脚本顺序</h5> 

```
第一步：通过/boot/vm进行启动 vmlinuz
第二步：init /etc/inittab
第三步：启动相应的脚本，并且打开终端
rc.sysinit
rc.d(里面的脚本）
rc.local
第四步：启动login登录界面 login
第五步:在用户登录的时候执行sh脚本的顺序：每次登录的时候都会完全执行的
/etc/profile.d/file
/etc/profile
/etc/bashrc
/root/.bashrc
/root/.bash_profile
```

<h5 id="sysinfo">系统信息</h5> 

		uname -a              # 查看Linux内核版本信息
		cat /proc/version     # 查看内核版本
		cat /etc/issue        # 查看系统版本
		cat /etc/redhat-release # 查看系统版本(redhat 7.X)
		lsb_release -a        # 查看系统版本  需安装 centos-release
		locale -a             # 列出所有语系
		hwclock               # 查看时间
		who | w               # 当前在线用户
		whoami                # 查看当前用户名
		logname               # 查看初始登陆用户名
		uptime                # 查看服务器启动时间,系统状态
		sar -n DEV 1 10       # 查看网卡网速流量,查看LAN网卡的流量时 RX为上行流量TX为下行流量
		dmesg                 # 显示开机信息
		lsmod	              # 查看内核模块


<h5 id="hardinfo">硬件信息</h5> 

		more /proc/cpuinfo                                       # 查看cpu信息
		cat /proc/cpuinfo | grep name | cut -f2 -d: | uniq -c    # 查看cpu型号和逻辑核心数
		getconf LONG_BIT                                         # cpu运行的位数
		cat /proc/cpuinfo | grep physical | uniq -c              # 物理cpu个数
		cat /proc/cpuinfo | grep flags | grep ' lm ' | wc -l     # 结果大于0支持64位
		cat /proc/cpuinfo|grep flags                             # 查看cpu是否支持虚拟化   pae支持半虚拟化  IntelVT 支持全虚拟化
		more /proc/meminfo                                       # 查看内存信息
		dmidecode                                                # 查看全面硬件信息
		dmidecode | grep "Product Name"                          # 查看服务器型号
		dmidecode | grep -P -A5 "Memory\s+Device" | grep Size | grep -v Range       # 查看内存插槽
		cat /proc/mdstat                                         # 查看软raid信息
		cat /proc/scsi/scsi                                      # 查看Dell硬raid信息(IBM、HP需要官方检测工具)
		lspci                                                    # 查看硬件信息
		lspci|grep RAID                                          # 查看是否支持raid
		lspci -vvv |grep Ethernet                                # 查看网卡型号
		lspci -vvv |grep Kernel|grep driver                      # 查看驱动模块
		modinfo tg2                                              # 查看驱动版本(驱动模块)
		ethtool -i em1       

<h5 id="syscmd">一般系统命令</h5> 
	write user                  # 给指定用户发消息
	wall        　  　          # 给其它用户发消息
	whereis ls                  # 查找命令的目录
	locate 文件名				#查找文件,依托数据库，updatedb 更新,/var/lib/mlocate/mlocate.db
	which                       # 查看当前要执行的命令所在的路径
	clear                       # 清空整个屏幕
	reset                       # 乱码后重新初始化屏幕
	cal                         # 显示月历
	echo -n 123456 | md5sum     # md5加密
	mkpasswd                    # 随机生成密码   -l位数 -C大小 -c小写 -d数字 -s特殊字符
	netstat -anlp | grep port   # 是否打开了某个端口
	ntpdate stdtime.gov.hk      # 同步时间
	tzselect                    # 选择时区 #+8=(5 9 1 1) # (TZ='Asia/Shanghai'; export TZ)括号内写入 /etc/profile
	/sbin/hwclock -w            # 保存到硬件
	/etc/shadow                 # 账户影子文件
	LANG=en                     # 修改语言
	vim /etc/sysconfig/i18n     # 修改编码  LANG="en_US.UTF-8"
	export LC_ALL=C             # 强制字符集
	vi /etc/hosts               # 查询静态主机名
	alias                       # 别名
	watch uptime                # 监测命令动态刷新
	ipcs -a                     # 查看Linux系统当前单个共享内存段的最大值
	lsof |grep /lib             # 查看加载库文件
	ldconfig                    # 动态链接库管理命令
	dist-upgrade                # 会改变配置文件,改变旧的依赖关系，改变系统版本 
	/boot/grub/grub.conf        # grub启动项配置
	sysctl -p                   # 修改内核参数/etc/sysctl.conf，让/etc/rc.d/rc.sysinit读取生效
	mkpasswd -l 8  -C 2 -c 2 -d 4 -s 0            # 随机生成指定类型密码
	echo 1 > /proc/sys/net/ipv4/tcp_syncookies    # 使TCP SYN Cookie 保护生效  # "SYN Attack"是一种拒绝服务的攻击方式


<h5 id="vim">vim</h5> 

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
	

<h5 id="process">进程管理</h5> 

* ps

		kill
		lsof

* kill
		ps -eaf               # 查看所有进程
		kill -9 PID           # 强制终止某个PID进程
		kill -15 PID          # 安全退出 需程序内部处理信号
		cmd &                 # 命令后台运行
		nohup cmd &           # 后台运行不受shell退出影响
		ctrl+z                # 将前台放入后台(暂停)
		jobs                  # 查看后台运行程序
		bg 2                  # 启动后台暂停进程
		fg 2                  # 调回后台进程
		pstree                # 进程树
		vmstat 1 9            # 每隔一秒报告系统性能信息9次
		sar                   # 查看cpu等状态
		lsof file             # 显示打开指定文件的所有进程
		lsof -i:32768         # 查看端口的进程
		renice +1 180         # 把180号进程的优先级加1
		ps aux |grep -v USER | sort -nk +4 | tail       # 显示消耗内存最多的10个运行中的进程，以内存使用量排序.cpu +3	
		
		top{

			前五行是系统整体的统计信息。
			第一行: 任务队列信息，同 uptime 命令的执行结果。内容如下：
				01:06:48 当前时间
				up 1:22 系统运行时间，格式为时:分
				1 user 当前登录用户数
				load average: 0.06, 0.60, 0.48 系统负载，即任务队列的平均长度。
				三个数值分别为 1分钟、5分钟、15分钟前到现在的平均值。

			第二、三行:为进程和CPU的信息。当有多个CPU时，这些内容可能会超过两行。内容如下：
				Tasks: 29 total 进程总数
				1 running 正在运行的进程数
				28 sleeping 睡眠的进程数
				0 stopped 停止的进程数
				0 zombie 僵尸进程数
				Cpu(s): 0.3% us 用户空间占用CPU百分比
				1.0% sy 内核空间占用CPU百分比
				0.0% ni 用户进程空间内改变过优先级的进程占用CPU百分比
				98.7% id 空闲CPU百分比
				0.0% wa 等待输入输出的CPU时间百分比
				0.0% hi
				0.0% si

			第四、五行:为内存信息。内容如下：
				Mem: 191272k total 物理内存总量
				173656k used 使用的物理内存总量
				17616k free 空闲内存总量
				22052k buffers 用作内核缓存的内存量
				Swap: 192772k total 交换区总量
				0k used 使用的交换区总量
				192772k free 空闲交换区总量
				123988k cached 缓冲的交换区总量。
				内存中的内容被换出到交换区，而后又被换入到内存，但使用过的交换区尚未被覆盖，
				该数值即为这些内容已存在于内存中的交换区的大小。
				相应的内存再次被换出时可不必再对交换区写入。

			进程信息区,各列的含义如下:  # 显示各个进程的详细信息

			序号 列名    含义
			a   PID      进程id
			b   PPID     父进程id
			c   RUSER    Real user name
			d   UID      进程所有者的用户id
			e   USER     进程所有者的用户名
			f   GROUP    进程所有者的组名
			g   TTY      启动进程的终端名。不是从终端启动的进程则显示为 ?
			h   PR       优先级
			i   NI       nice值。负值表示高优先级，正值表示低优先级
			j   P        最后使用的CPU，仅在多CPU环境下有意义
			k   %CPU     上次更新到现在的CPU时间占用百分比
			l   TIME     进程使用的CPU时间总计，单位秒
			m   TIME+    进程使用的CPU时间总计，单位1/100秒
			n   %MEM     进程使用的物理内存百分比
			o   VIRT     进程使用的虚拟内存总量，单位kb。VIRT=SWAP+RES
			p   SWAP     进程使用的虚拟内存中，被换出的大小，单位kb。
			q   RES      进程使用的、未被换出的物理内存大小，单位kb。RES=CODE+DATA
			r   CODE     可执行代码占用的物理内存大小，单位kb
			s   DATA     可执行代码以外的部分(数据段+栈)占用的物理内存大小，单位kb
			t   SHR      共享内存大小，单位kb
			u   nFLT     页面错误次数
			v   nDRT     最后一次写入到现在，被修改过的页面数。
			w   S        进程状态。
				D=不可中断的睡眠状态
				R=运行
				S=睡眠
				T=跟踪/停止
				Z=僵尸进程
			x   COMMAND  命令名/命令行
			y   WCHAN    若该进程在睡眠，则显示睡眠中的系统函数名
			z   Flags    任务标志，参考 sched.h

		}

		linux操作系统提供的信号{
			
			kill -l                    # 查看linux提供的信号
			trap "echo aaa"  2 3 15    # shell使用 trap 捕捉退出信号

			# 发送信号一般有两种原因:
			#   1(被动式)  内核检测到一个系统事件.例如子进程退出会像父进程发送SIGCHLD信号.键盘按下control+c会发送SIGINT信号
			#   2(主动式)  通过系统调用kill来向指定进程发送信号                             
			# 进程结束信号 SIGTERM 和 SIGKILL 的区别:  SIGTERM 比较友好，进程能捕捉这个信号，根据您的需要来关闭程序。在关闭程序之前，您可以结束打开的记录文件和完成正在做的任务。在某些情况下，假如进程正在进行作业而且不能中断，那么进程可以忽略这个SIGTERM信号。
			# 如果一个进程收到一个SIGUSR1信号，然后执行信号绑定函数，第二个SIGUSR2信号又来了，第一个信号没有被处理完毕的话，第二个信号就会丢弃。

			SIGHUP  1          A     # 终端挂起或者控制进程终止
			SIGINT  2          A     # 键盘终端进程(如control+c)
			SIGQUIT 3          C     # 键盘的退出键被按下
			SIGILL  4          C     # 非法指令
			SIGABRT 6          C     # 由abort(3)发出的退出指令
			SIGFPE  8          C     # 浮点异常
			SIGKILL 9          AEF   # Kill信号  立刻停止
			SIGSEGV 11         C     # 无效的内存引用
			SIGPIPE 13         A     # 管道破裂: 写一个没有读端口的管道
			SIGALRM 14         A     # 闹钟信号 由alarm(2)发出的信号 
			SIGTERM 15         A     # 终止信号,可让程序安全退出 kill -15
			SIGUSR1 30,10,16   A     # 用户自定义信号1
			SIGUSR2 31,12,17   A     # 用户自定义信号2
			SIGCHLD 20,17,18   B     # 子进程结束自动向父进程发送SIGCHLD信号
			SIGCONT 19,18,25         # 进程继续（曾被停止的进程）
			SIGSTOP 17,19,23   DEF   # 终止进程
			SIGTSTP 18,20,24   D     # 控制终端（tty）上按下停止键
			SIGTTIN 21,21,26   D     # 后台进程企图从控制终端读
			SIGTTOU 22,22,27   D     # 后台进程企图从控制终端写
			
			缺省处理动作一项中的字母含义如下:
				A  缺省的动作是终止进程
				B  缺省的动作是忽略此信号，将该信号丢弃，不做处理
				C  缺省的动作是终止进程并进行内核映像转储(dump core),内核映像转储是指将进程数据在内存的映像和进程在内核结构中的部分内容以一定格式转储到文件系统，并且进程退出执行，这样做的好处是为程序员提供了方便，使得他们可以得到进程当时执行时的数据值，允许他们确定转储的原因，并且可以调试他们的程序。
				D  缺省的动作是停止进程，进入停止状况以后还能重新进行下去，一般是在调试的过程中（例如ptrace系统调用）
				E  信号不能被捕获
				F  信号不能被忽略





<h5 id="history">history</h5> 

		history                      # 历时命令默认1000条
		HISTTIMEFORMAT="%Y-%m-%d %H:%M:%S "   # 让history命令显示具体时间,写入/etc/profile
		history  -c                  # 清除记录命令
		cat $HOME/.bash_history      # 历史命令记录文件

<h5 id="log">日志</h5> 

		last                         # 查看登陆过的用户信息
		who /var/log/wtmp            # 查看登陆过的用户信息
		lastlog                      # 用户最后登录的时间
		lastb -a                     # 列出登录系统失败的用户相关信息
		/var/log/btmp                # 登录失败二进制日志记录文件
		tail -f /var/log/messages    # 系统日志
		tail -f /var/log/secure      # ssh日志
		dmesg                        # kernel信息,开机信息，运行时内存cpu报错等会显示
		dmesg -c                     # 清除dmesg

<h5 id="selinux">selinux</h5> 

		sestatus -v                    # 查看selinux状态
		getenforce                     # 查看selinux模式
		setenforce 0                   # 设置selinux为宽容模式(可避免阻止一些操作)
		semanage port -l    # 查看selinux端口限制规则
		semanage port -a -t http_port_t -p tcp 8000  # 在selinux中注册端口类型
		vi /etc/selinux/config         # selinux配置文件
		SELINUX=enfoceing              # 关闭selinux 把其修改为  SELINUX=disabled




<h5 id="find">find</h5> 

>
* linux文件无创建时间
* Access 使用时间  
* Modify 内容修改时间  
* Change 状态改变时间(权限、属主)
* 时间默认以24小时为单位,当前时间到向前24小时为0天,向前48-72小时为2天
* -and 且 匹配两个条件 参数可以确定时间范围 -mtime +2 -and -mtime -4
-or 或 匹配任意一个条件

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



<h5 id="sort">sort</h5> 

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
	netstat -anlp |grep 2181  |awk '{print $5}' |awk -F: '{print $1}' |sort |uniq -c | sort -rn  |head  # 查看zookeeper 链接数


<h5 id="tar">归档解压缩</h5> 

>
* v  #显示详情
* z  #压缩

		file 文件     # 查看文件类型
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



<h5 id="date">date</h5> 

		date -s 20091112                     # 设日期
		date -s 18:30:50                     # 设时间
		date -d "7 days ago" +%Y%m%d         # 7天前日期
		date -d "5 minute ago" +%H:%M        # 5分钟前时间
		date -d "1 month ago" +%Y%m%d        # 一个月前
		date +%Y-%m-%d -d '20110902'         # 日期格式转换
		date +%Y-%m-%d_%X                    # 日期和时间
		date +%N                             # 纳秒
		date -d "2012-08-13 14:00:23" +%s    # 换算成秒计算(1970年至今的秒数)
		date -d "@1363867952" +%Y-%m-%d-%T   # 将时间戳换算成日期
		date -d "1970-01-01 UTC 1363867952 seconds" +%Y-%m-%d-%T  # 将时间戳换算成日期
		date -d "`awk -F. '{print $1}' /proc/uptime` second ago" +"%Y-%m-%d %H:%M:%S"    # 格式化系统启动时间(多少秒前)


<h5 id="ulimit">最大连接数</h5> 

>在linux kernel 2.6.25之前通过`ulimit -n(setrlimit(RLIMIT_NOFILE))`设置每个进程的最大打开文件句柄数不能超过NR_OPEN (1024*1024),也就是100w(除非重新编译内核)

		ulimit -SHn 65535  # 修改最大打开文件数(等同最大连接数)
		ulimit -a          # 查看
		
		/etc/security/limits.conf         # 进程最大打开文件数
		# nofile 可以被理解为是文件句柄数 文件描述符 还有socket数
		* soft nofile 65535
		* hard nofile 65535
		# 最大进程数
		* soft nproc 65535
		* hard nproc 65535

		# 如果/etc/security/limits.d/有配置文件，将会覆盖/etc/security/limits.conf里的配置
		# 即/etc/security/limits.d/的配置文件里就不要有同样的参量设置
		/etc/security/limits.d/90-nproc.conf    # centos6.3的最大进程数文件
		* soft nproc 65535       
		* hard nproc 65535

`sysctl -p`  #生效


> 某些情况应用比较变态，系统资源不够用，文件句柄数不够，要开到500w的时候,一般来说限制就是1024*1024 大约100万 ，大于这个数值就没法设置了

```
$ ulimit -n 22222222
-bash: ulimit: open files: cannot modify limit: Operation not permitted
```

> kernel 2.6.25之后，内核导出了一个sys接口可以修改这个最大值(/proc/sys/fs /nr_open).
解决方法, 写到.bash_profile  里面

```
echo 20000500 > /proc/sys/fs/nr_open
ulimit -n 5000000
```


<h5 id="sudo">sudo</h5> 

>visudo     # sudo命令权限添加

* 用户  别名(可用all)=NOPASSWD:命令1，命令2

		wangming linuxfan=NOPASSWD:/sbin/apache start,/sbin/apache restart
		UserName ALL=(ALL) ALL
		peterli        ALL=(ALL)       NOPASSWD:/sbin/service
		Defaults requiretty             # sudo不允许后台运行,注释此行既允许
		Defaults !visiblepw             # sudo不允许远程,去掉!既允许


<h5 id="chkconfig">chkconfig</h5> 

>参数用法：

```
   --add 　增加所指定的系统服务，让chkconfig指令得以管理它，并同时在系统启动的叙述文件内增加相关数据。
   --del 　删除所指定的系统服务，不再由chkconfig指令管理，并同时在系统启动的叙述文件内删除相关数据。
   --level<等级代号> 　指定读系统服务要在哪一个执行等级中开启或关毕。
```

>
      等级0表示：表示关机
      等级1表示：单用户模式
      等级2表示：无网络连接的多用户命令行模式
      等级3表示：有网络连接的多用户命令行模式
      等级4表示：不可用
      等级5表示：带图形界面的多用户模式
      等级6表示：重新启动
      需要说明的是，level选项可以指定要查看的运行级而不一定是当前运行级。对于每个运行级，只能有一个启动脚本或者停止脚本。当切换运行级时，init不会重新启动已经启动的服务，也不会再次去停止已经停止的服务。

```
chkconfig --list                         #列出所有的系统服务
chkconfig --list |grep httpd*            # 查看某些服务的启动状态
chkconfig --list mysqld                  #列出mysqld服务设置情况
chkconfig --add httpd                    #增加httpd服务
chkconfig --del httpd                    #删除httpd服务
chkconfig --level httpd 2345 on          #设置httpd在运行级别为2、3、4、5的情况下都是on（开启）的状态
chkconfig --level 35 mysqld on           #设定mysqld在等级3和5为开机运行服务，--level 35表示操作只在等级3和5执行，on表示启动，off表示关闭
chkconfig mysqld on        #设定mysqld在各等级为on，“各等级”包括2、3、4、5等级
```


如何增加一个服务：

1. 服务脚本必须存放在/etc/ini.d/目录下；

2. 在chkconfig工具服务列表中增加此服务，此时服务会被在/etc/rc.d/rcN.d中赋予K/S入口了；

> chkconfig --add servicename
   
3. 修改服务的默认启动等级。

>chkconfig --level 35 mysqld on


* 查看服务状态

```
service mysql status              
systemctl status  mysql.service   # redhat 7.X
```

<h5 id="network">network</h5> 

* 常用命令

```
	ifconfig eth0 down                  # 禁用网卡
	ifconfig eth0 up                    # 启用网卡
	ifup eth0:0                         # 启用网卡
	vi /etc/resolv.conf                 # 设置DNS  nameserver IP 定义DNS服务器的IP地址
	nslookup www.moon.com               # 解析域名IP
	dig -x www.baidu.com                # 解析域名IP
	curl -I www.baidu.com               # 查看网页http头
	tcpdump tcp port 22                 # 抓包
	wget -P 路径 http地址               # 下载  包名:wgetrc
	curl -d "user=xuesong&pwd=123" http://www.abc.cn/Result    # 提交web页面表单 需查看表单提交地址
	rsync -avzP -e "ssh -p 22" /dir user@$IP:/dir              # 同步目录 # --delete 无差同步 删除目录下其它文件
	ifconfig eth0:0 192.168.1.221 netmask 255.255.255.0        # 增加逻辑IP地址
	mtr -r www.baidu.com                                       # 测试网络链路节点响应时间 # trace ping 结合
	echo 1 > /proc/sys/net/ipv4/icmp_echo_ignore_all           # 禁ping
	ipcalc -m "$ip" -p "$num"                                  # 根据IP和主机最大数计算掩码
	dig +short txt hacker.wp.dg.cx                             # 通过 DNS 来读取 Wikipedia 的hacker词条
	host -t txt hacker.wp.dg.cx                                # 通过 DNS 来读取 Wikipedia 的hacker词条
	net rpc shutdown -I IP_ADDRESS -U username%password        # 远程关掉一台WINDOWS机器
	wget --random-wait -r -p -e robots=off -U Mozilla www.example.com    # 递归方式下载整个网站
	mii-tool em1                        # 查看网线是否连接
	traceroute www.baidu.com            # 测试跳数
	lynx                                # 文本上网
```

* 网卡配置文件

		vi /etc/sysconfig/network-scripts/ifcfg-eth0

		DEVICE=eth0
		BOOTPROTO=none
		BROADCAST=192.168.1.255
		HWADDR=00:0C:29:3F:E1:EA
		IPADDR=192.168.1.55
		NETMASK=255.255.255.0
		NETWORK=192.168.1.0
		ONBOOT=yes        							#为no时网卡关闭
		TYPE=Ethernet
		GATEWAY=192.168.1.1


* route

		route                           								   # 查看路由表
		route add default  gw 192.168.1.1  dev eth0                        # 添加默认路由
		route add -net 172.16.0.0 netmask 255.255.0.0 gw 10.39.111.254     # 添加静态路由网关
		route del -net 172.16.0.0 netmask 255.255.0.0 gw 10.39.111.254     # 删除静态路由网关

* 添加虚拟网卡

		cp /etc/sysconfig/network-scripts/ifcfg-eth0 /etc/sysconfig/network-scripts/ifcfg-eth0:1
		DEVICE=eth0:1
		IPADDR=192.168.1.56
		ONBOOT=yes
		...

		ifup eth0:1    		#启动网卡
		ifdown eth0:1       #关闭网卡




<h5 id="tcpdump">tcpdump</h5> 


* 抓取eth0 11215端口的数据

`tcpdump -i eth0 dst port 11215 -A > tcpdump.log`

* 可以用wireshark分析的包 cap

`tcpdump -i eth0 dst port 20001 -A -s 0  -w tcpdump.cap`

<h5 id="netstat">netstat</h5> 

>性能消耗大，可以用ss 取代。

```
	-a     # 显示所有连接中的Socket
	-t     # 显示TCP连接
	-u     # 显示UDP连接
	-n     # 显示所有已建立的有效连接
	netstat -anlp           # 查看链接
	netstat –r              # 查看路由表
```

并发数查看

```
		netstat -n | awk '/^tcp/ {++S[$NF]} END {for(a in S) print a, S[a]}'
		SYN_RECV     # 正在等待处理的请求
		ESTABLISHED  # 正常数据传输状态,既当前并发数
		TIME_WAIT    # 处理完毕，等待超时结束的请求
```


<h5 id="ssh">ssh</h5> 


		ssh -p 22 user@192.168.1.209                            # 从linux ssh登录另一台linux 
		ssh -p 22 root@192.168.1.209 CMD                        # 利用ssh操作远程主机
		scp -P 22 文件 root@ip:/目录                            # 把本地文件拷贝到远程主机
		sshpass -p '密码' ssh -n root@$IP "echo hello"          # 指定密码远程操作
		ssh -o StrictHostKeyChecking=no $IP                     # ssh连接不提示yes
		ssh -t "su -"                                           # 指定伪终端 客户端以交互模式工作
		scp root@192.168.1.209:远程目录 本地目录                # 把远程指定文件拷贝到本地
		ssh -N -L2001:remotehost:80 user@somemachine            # 用SSH创建端口转发通道
		ssh -t host_A ssh host_B                                # 嵌套使用SSH
		ssh -t -p 22 $user@$Ip /bin/su - root -c {$Cmd};        # 远程su执行命令 Cmd="\"/sbin/ifconfig eth0\""
		ssh-keygen -t rsa                                       # 生成密钥
		ssh-copy-id -i xuesong@10.10.10.133                     # 传送key
		vi $HOME/.ssh/authorized_keys                           # 公钥存放位置
		sshfs name@server:/path/to/folder /path/to/mount/point  # 通过ssh挂载远程主机上的文件夹
		fusermount -u /path/to/mount/point                      # 卸载ssh挂载的目录
		ssh user@host cat /path/to/remotefile | diff /path/to/localfile -                # 用DIFF对比远程文件跟本地文件
		su - user -c "ssh user@192.168.1.1 \"echo -e aa |mail -s test mail@163.com\""    # 切换用户登录远程发送邮件



* 解决ssh链接慢{

		sed -i 's/GSSAPIAuthentication yes/GSSAPIAuthentication no/' /etc/ssh/sshd_config
		sed -i '/#UseDNS yes/a\UseDNS no' /etc/ssh/sshd_config
		/etc/init.d/sshd restart



<h5 id="nmap">nmap</h5> 

		nmap -PT 192.168.1.1-111             # 先ping在扫描主机开放端口
		nmap -O 192.168.1.1                  # 扫描出系统内核版本
		nmap -sV 192.168.1.1-111             # 扫描端口的软件版本
		nmap -sS 192.168.1.1-111             # 半开扫描(通常不会记录日志)
		nmap -P0 192.168.1.1-111             # 不ping直接扫描
		nmap -d 192.168.1.1-111              # 详细信息
		nmap -D 192.168.1.1-111              # 无法找出真正扫描主机(隐藏IP)
		nmap -p 20-30,139,60000-             # 端口范围  表示：扫描20到30号端口，139号端口以及所有大于60000的端口
		nmap -P0 -sV -O -v 192.168.30.251    # 组合扫描(不ping、软件版本、内核版本、详细信息)
		
		# 不支持windows的扫描(可用于判断是否是windows)
		nmap -sF 192.168.1.1-111
		nmap -sX 192.168.1.1-111
		nmap -sN 192.168.1.1-111

<h5 id="disk">disk</h5> 

```	
	df -Ph                                # 查看硬盘容量
	df -T                                 # 查看磁盘分区格式
	df -i                                 # 查看inode节点   如果inode用满后无法创建文件
	du -h 目录                            # 检测目录下所有文件大小
	du -sh *                              # 显示当前目录中子目录的大小
	iostat -x                             # 查看磁盘io状态
	mount                                 # 查看分区挂载情况
	fdisk -l                              # 查看磁盘分区状态
	fdisk /dev/hda3                       # 分区 
	mkfs -t ext3  /dev/hda3               # 格式化分区
	fsck -y /dev/sda6                     # 对文件系统修复
	lsof |grep delete                     # 释放进程占用磁盘空间  列出进程后，查看文件是否存在，不存在则kill掉此进程
	tmpwatch -afv 3                       # 删除3小时内的临时文件
	cat /proc/filesystems                 # 查看当前系统支持文件系统
	mount -o remount,rw /                 # 修改只读文件系统为读写
	smartctl -H /dev/sda                  # 检测硬盘状态
	smartctl -i /dev/sda                  # 检测硬盘信息
	smartctl -a /dev/sda                  # 检测所有信息
	e2label /dev/sda5                     # 查看卷标
	e2label /dev/sda5 new-label           # 创建卷标
	ntfslabel -v /dev/sda8 new-label      # NTFS添加卷标
	tune2fs -j /dev/sda                   # ext2分区转ext3分区
	mke2fs -b 2048 /dev/sda5              # 指定索引块大小
	dumpe2fs -h /dev/sda5                 # 查看超级块的信息
	mount -t iso9660 /dev/dvd  /mnt       # 挂载光驱
	mount -t ntfs-3g /dev/sdc1 /media/yidong        # 挂载ntfs硬盘
	mount -t nfs 10.0.0.3:/opt/images/  /data/img   # 挂载nfs
	mount -o loop  /software/rhel4.6.iso   /mnt/    # 挂载镜像文件
```	


* 新硬盘挂载

```
		fdisk /dev/sdc 
		p	#  打印分区
		d 	#  删除分区
		n	#  创建分区，（一块硬盘最多4个主分区，扩展占一个主分区位置。p主分区 e扩展）
		w	#  保存退出
		mkfs -t ext3 -L 卷标  /dev/sdc1		# 格式化相应分区
		mount /dev/sdc1  /mnt		# 挂载
		vi /etc/fstab               # 添加开机挂载分区
		LABEL=/data            /data                   ext3    defaults        1 2      # 用卷标挂载
		/dev/sdb1              /data4                  ext3    defaults        1 2      # 用真实分区挂载
		/dev/sdb2              /data4                  ext3    noatime,defaults        1 2
```

>		第一个数字"1"该选项被"dump"命令使用来检查一个文件系统应该以多快频率进行转储，若不需要转储就设置该字段为0
		第二个数字"2"该字段被fsck命令用来决定在启动时需要被扫描的文件系统的顺序，根文件系统"/"对应该字段的值应该为1，其他文件系统应该为2。若该文件系统无需在启动时扫描则设置该字段为0
		当以 noatime 选项加载（mount）文件系统时，对文件的读取不会更新文件属性中的atime信息。设置noatime的重要性是消除了文件系统对文件的写操作，文件只是简单地被系统读取。由于写操作相对读来说要更消耗系统资源，所以这样设置可以明显提高服务器的性能.wtime信息仍然有效，任何时候文件被写，该信息仍被更新。

<h5 id="xfs">xfs挂载</h5> 

```
yum install xfsprogs.x86_64 -y
mkdir /data
mkfs.xfs -f /dev/sdb
mount /dev/sdb /data
echo "mount /dev/sdb /data" >> /etc/rc.local
```

<h5 id="nfs">nfs挂载</h5> 


服务器端

1. 启动的服务

```
service portmap start 				# 在5.x系统中
service rpcbind start 				# 在6.x系统中
```

2. 配置文件

```
vim /etc/exports
/data/www-root/img8/ 10.13.81.107(rw,sync,no_root_squash)
service nfs reload
```

客户端

```
service portmap start （不然会报io error）  5.X
service rpcbind restart                      6.X
mount -t nfs smc@10.13.81.130:/data/log/scribelog /opt/scribelog

echo "mount -t nfs smc@10.13.81.130:/data/log/scribelog /opt/scribelog" >> /etc/rc.local
```



<h5 id="raid">raid</h5> 

```
		raid0至少2块硬盘.吞吐量大,性能好,同时读写,但损坏一个就完蛋    
		raid1至少2块硬盘.相当镜像,一个存储,一个备份.安全性比较高.但是性能比0弱
		raid5至少3块硬盘.分别存储校验信息和数据，坏了一个根据校验信息能恢复
		raid6至少4块硬盘.两个独立的奇偶系统,可坏两块磁盘,写性能非常差
```


<h5 id="user">user</h5> 

	users                   # 显示所有的登录用户
	groups                  # 列出当前用户和他所属的组
	who -q                  # 显示所有的登录用户
	groupadd                # 添加组
	useradd user            # 建立用户
	passwd 用户             # 修改密码
	userdel -r              # 删除帐号及家目录
	chown -R user:group     # 修改目录拥有者(R递归)
	chown y\.li:mysql       # 修改所有者用户中包含点"."
	umask                   # 设置用户文件和目录的文件创建缺省屏蔽值
	chgrp                   # 修改用户组
	finger                  # 查找用户显示信息
	echo "xuesong" | passwd user --stdin       # 非交互修改密码
	useradd -g www -M  -s /sbin/nologin  www   # 指定组并不允许登录的用户,nologin允许使用服务
	useradd -g www -M  -s /bin/false  www      # 指定组并不允许登录的用户,false最为严格
	usermod -l 新用户名 老用户名               # 修改用户名
	usermod -g user group                      # 修改用户所属组
	usermod -d 目录 -m 用户                    # 修改用户家目录
	usermod -G group user                      # 将用户添加到附加组
	gpasswd -d user group                      # 从组中删除用户
	su - user -c " #命令1; "                   # 切换用户执行
	
* 恢复密码

		即进入单用户模式: 在linux出现grub后，在安装的系统上面按"e"，然后出现grub的配置文件，按键盘移动光标到第二行"Ker……"，再按"e"，然后在这一行的结尾加上：空格 single或者空格1回车，然后按"b"重启，就进入了"单用户模式"

	
* 特殊权限

		s或 S （SUID）：对应数值4
		s或 S （SGID）：对应数值2
		t或 T ：对应数值1
		大S：代表拥有root权限，但是没有执行权限
		小s：拥有特权且拥有执行权限，这个文件可以访问系统任何root用户可以访问的资源
		T或T（Sticky）：/tmp和 /var/tmp目录供所有用户暂时存取文件，亦即每位用户皆拥有完整的权限进入该目录，去浏览、删除和移动文件


<h5 id="at">at</h5> 

		at 5pm + 3 days /bin/ls  # 单次定时任务 指定三天后下午5:00执行/bin/ls






[top](#top)