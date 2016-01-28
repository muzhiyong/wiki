[vim](#vim) |[进程](#process)


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
		}

	}