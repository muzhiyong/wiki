[regex](regex)  

[awk](awk) |[sed](sed)



[variable](variable)

[if](#if)|[for](#for)|[while](#while) | [case](#case)|[until](#until)

[xargs](#xargs) | [test](#test)

[except](except)

[read](linuxread)

[重定向](#chongdingxiang) | [运算符](#yunsuanfu) |[数学运算](#shuxueyunsuan)

[tr](#tr) | [seq](#seq) | [grep](#grep)


#####不常用

[select菜单](#selectcaidan) |[shift](#shift) |[getopts给脚本加参数](#getopts) |[tclsh](#tclsh) |[dialog菜单](#dialogcaidan)




[example](shellexample)
[监控](jiankong)



<font color="red">This is some text!</font>




*常用

	#!/bin/sh         # 在脚本第一行脚本头 # sh为当前系统默认shell,可指定为bash等shell
	sh -x             # 执行过程
	sh -n             # 检查语法
	(a=bbk)           # 括号创建子shell运行
	basename /a/b/c   # 从全路径中保留最后一层文件名或目录
	dirname           # 取路径
	$RANDOM           # 随机数
	$$                # 进程号
	source FileName   # 在当前bash环境下读取并执行FileName中的命令  # 等同 . FileName
	sleep 5           # 间隔睡眠5秒
	trap              # 在接收到信号后将要采取的行动
	trap "" 2 3       # 禁止ctrl+c
	$PWD              # 当前目录
	$HOME             # 家目录
	$OLDPWD           # 之前一个目录的路径
	cd -              # 返回上一个目录路径
	local ret         # 局部变量
	yes               # 重复打印
	yes |rm -i *      # 自动回答y或者其他
	ls -p /home       # 查看目录所有文件夹
	ls -d /home/      # 查看匹配完整路径
	echo -n aa;echo bb                    # 不换行执行下一句话 将字符串原样输出
	echo -e "s\tss\n\n\n"                 # 使转义生效
	echo $a | cut -c2-6                   # 取字符串中字元
	echo {a,b,c}{a,b,c}{a,b,c}            # 排列组合(括号内一个元素分别和其他括号内元素组合)
	echo $((2#11010))                     # 二进制转10进制
	echo aaa | tee file                   # 打印同时写入文件 默认覆盖 -a追加
	echo {1..10}                          # 打印10个字符
	printf '%10s\n'|tr " " a              # 打印10个字符
	pwd | awk -F/ '{ print $2 }'          # 返回目录名
	tac file |sed 1,3d|tac                # 倒置读取文件  # 删除最后3行
	tail -3 file                          # 取最后3行
	outtmp=/tmp/$$`date +%s%N`.outtmp     # 临时文件定义
	:(){ :|:& };:                         # 著名的 fork炸弹,系统执行海量的进程,直到系统僵死
	echo -e "\e[32m颜色\e[0m"             # 打印颜色
	echo -e "\033[32m颜色\033[m"          # 打印颜色
	echo -e "\033[0;31mL\033[0;32mO\033[0;33mV\033[0;34mE\t\033[0;35mY\033[0;36mO\033[0;32mU\e[m"    # 打印颜色
	

	
<h5 id="if">if</h5> 

			if [ $a == $b ]
			then
			    echo "等于"
			else
			    echo "不等于"
			fi

		
<h5 id="case">case</h5> 

			case $xs in
			    0) echo "0" ;;
			    1) echo "1" ;;
			    *) echo "其他" ;;
			esac


		
<h5 id="while">while</h5> 

>			break N     #  跳出几层循环
			continue N  #  跳出几层循环，循环次数不变
			continue    #  重新循环次数不变


			# while true  等同   while :
			# 读文件为整行读入
			num=1
			while [ $num -lt 10 ]
			do
			    echo $num
			    ((num=$num+2))
			done
			###########################
			grep a  a.txt | while read a
			do
			    echo $a
			done
			###########################
			while read a
			do
			    echo $a
			done < a.txt 


		
<h5 id="for">for</h5> 

			# 读文件已空格分隔
			w=`awk -F ":" '{print $1}' c`
			for d in $w
			do
			    $d
			done
			

			for ((i=0;i<${#o[*]};i++))
			do
			    echo ${o[$i]}
			done


		
<h5 id="until">until</h5> 

			#当command不为0时循环
			until command	
			do
			    body
			done

<h5 id="xargs">xargs</h5> 

		# 命令替换
		-t 先打印命令，然后再执行
		-i 用每项替换 {}
		find / -perm +7000 | xargs ls -l                    # 将前面的内容，作为后面命令的参数
		seq 1 10 |xargs  -i date -d "{} days " +%Y-%m-%d    # 列出10天日期


<h5 id="test">test</h5> 

		符号 [ ] 等同  test命令

* expression为字符串操作

			-n str   # 字符串str是否不为空
			-z str   # 字符串str是否为空


* expression为文件操作

			-a     # 并且，两条件为真
			-b     # 是否块文件     
			-p     # 文件是否为一个命名管道
			-c     # 是否字符文件   
			-r     # 文件是否可读
			-d     # 是否一个目录   
			-s     # 文件的长度是否不为零
			-e     # 文件是否存在   
			-S     # 是否为套接字文件
			-f     # 是否普通文件   
			-x     # 文件是否可执行，则为真
			-g     # 是否设置了文件的 SGID 位 
			-u     # 是否设置了文件的 SUID 位
			-G     # 文件是否存在且归该组所有 
			-w     # 文件是否可写，则为真
			-k     # 文件是否设置了的粘贴位  
			-t fd  # fd 是否是个和终端相连的打开的文件描述符（fd 默认为 1）
			-o     # 或，一个条件为真
			-O     # 文件是否存在且归该用户所有
			!      # 取反


* expression为整数操作

			expr1 -a expr2   # 如果 expr1 和 expr2 评估为真，则为真
			expr1 -o expr2   # 如果 expr1 或 expr2 评估为真，则为真

		

* 两值比较

			整数	 字符串
			-lt      <         # 小于
			-gt      >         # 大于
			-le      <=        # 小于或等于
			-ge      >=        # 大于或等于
			-eq      ==        # 等于
			-ne      !=        # 不等于


		test 10 -lt 5       # 判断大小
		echo $?             # 查看上句test命令返回状态  # 结果0为真,1为假
		test -n "hello"     # 判断字符串长度是否为0
		[ $? -eq 0 ] && echo "success" || exit　　　# 判断成功提示,失败则退出



<h5 id="chongdingxiang">重定向</h5> 

	
		#  标准输出 stdout 和 标准错误 stderr  标准输入stdin
		cmd 1> fiel              # 把 标准输出 重定向到 file 文件中
		cmd > file 2>&1          # 把 标准输出 和 标准错误 一起重定向到 file 文件中
		cmd 2> file              # 把 标准错误 重定向到 file 文件中
		cmd 2>> file             # 把 标准错误 重定向到 file 文件中(追加)
		cmd >> file 2>&1         # 把 标准输出 和 标准错误 一起重定向到 file 文件中(追加)
		cmd < file >file2        # cmd 命令以 file 文件作为 stdin(标准输入)，以 file2 文件作为 标准输出
		cat <>file               # 以读写的方式打开 file
		cmd < file cmd           # 命令以 file 文件作为 stdin
		cmd << delimiter
		cmd; #从 stdin 中读入，直至遇到 delimiter 分界符
delimiter

		>&n    # 使用系统调用 dup (2) 复制文件描述符 n 并把结果用作标准输出
		<&n    # 标准输入复制自文件描述符 n
		<&-    # 关闭标准输入（键盘）
		>&-    # 关闭标准输出
		n<&-   # 表示将 n 号输入关闭
		n>&-   # 表示将 n 号输出关闭


<h5 id="yunsuanfu">运算符</h5> 

>		
		$[]等同于$(())  # $[]表示形式告诉shell求中括号中的表达式的值
		~var            # 按位取反运算符,把var中所有的二进制为1的变为0,为0的变为1
		var\<<str       # 左移运算符,把var中的二进制位向左移动str位,忽略最左端移出的各位,最右端的各位上补上0值,每做一次按位左移就有var乘2
		var>>str        # 右移运算符,把var中所有的二进制位向右移动str位,忽略最右移出的各位,最左的各位上补0,每次做一次右移就有实现var除以2
		var&str         # 与比较运算符,var和str对应位,对于每个二进制来说,如果二都为1,结果为1.否则为0
		var^str         # 异或运算符,比较var和str对应位,对于二进制来说如果二者互补,结果为1,否则为0
		var|str         # 或运算符,比较var和str的对应位,对于每个二进制来说,如二都该位有一个1或都是1,结果为1,否则为0

* 运算符优先级

			级别      运算符                                  说明
			1      =,+=,-=,/=,%=,*=,&=,^=,|=,<<=,>>==     # 赋值运算符
			2         ||                                  # 逻辑或 前面不成功执行
			3         &&                                  # 逻辑与 前面成功后执行
			4         |                                   # 按位或
			5         ^                                   # 按异位与
			6         &                                   # 按位与
			7         ==,!=                               # 等于/不等于
			8         <=,>=,<,>                           # 大于或等于/小于或等于/大于/小于 
			9        \<<,>>                               # 按位左移/按位右移 (无转意符号)
			10        +,-                                 # 加减
			11        *,/,%                               # 乘,除,取余
			12        ! ,~                                # 逻辑非,按位取反或补码
			13        -,+                                 # 正负


<h5 id="shuxueyunsuan">数学运算</h5> 

	
		$(( ))        # 整数运算
		+ - * / **    # 分別为 "加、減、乘、除、密运算"
		& | ^ !       # 分別为 "AND、OR、XOR、NOT" 运算
		%             # 余数运算

* let
		
			let # 运算  
			let x=16/4
			let x=5**5


* expr
		
			expr 14 % 9                    # 整数运算
			SUM=`expr 2 \* 3`              # 乘后结果赋值给变量
			LOOP=`expr $LOOP + 1`          # 增量计数(加循环即可) LOOP=0
			expr length "bkeep zbb"        # 计算字串长度
			expr substr "bkeep zbb" 4 9    # 抓取字串
			expr index "bkeep zbb" e       # 抓取第一个字符数字串出现的位置
			expr 30 / 3 / 2                # 运算符号有空格
			expr bkeep.doc : '.*'          # 模式匹配(可以使用expr通过指定冒号选项计算字符串中字符数)
			expr bkeep.doc : '\(.*\).doc'  # 在expr中可以使用字符串匹配操作，这里使用模式抽取.doc文件附属名

			* 数值测试

				#如果试图计算非整数，则会返回错误
				rr=3.4
				expr $rr + 1
				expr: non-numeric argument
				rr=5
				expr $rr + 1
				6
		
* bc

			echo "m^n"|bc            # 次方计算
			seq -s '+' 1000 |bc      # 从1加到1000
			seq 1 1000 |tr "\n" "+"|sed 's/+$/\n/'|bc   # 从1加到1000


<h5 id="grep">grep</h5> 
	

		-c    # 显示匹配到得行的数目，不显示内容
		-h    # 不显示文件名
		-i    # 忽略大小写
		-l    # 只列出匹配行所在文件的文件名
		-n    # 在每一行中加上相对行号
		-s    # 无声操作只显示报错，检查退出状态
		-v    # 反向查找
		-e    # 使用正则表达式
		-A3   # 打印匹配行和下三行
		-w    # 精确匹配
		-wc   # 精确匹配次数
		-o    # 查询所有匹配字段
		-P    # 使用perl正则表达式
		
* grep用于if判断{

			if echo abc | grep "a"  > /dev/null 2>&1
			then
				echo "abc"
			else
				echo "null"
			fi

* 实例
		grep -v "a" txt                              # 过滤关键字符行
		grep -w 'a\>' txt                            # 精确匹配字符串
		grep -i "a" txt                              # 大小写敏感
		grep  "a[bB]" txt                            # 同时匹配大小写
		grep '[0-9]\{3\}' txt                        # 查找0-9重复三次的所在行
		grep -E "word1|word2|word3"   file           # 任意条件匹配
		grep word1 file | grep word2 |grep word3     # 同时匹配三个
		echo quan@163.com |grep -Po '(?<=@.).*(?=.$)'                           # 零宽断言截取字符串  #　63.co
		echo "I'm singing while you're dancing" |grep -Po '\b\w+(?=ing\b)'      # 零宽断言匹配		
		echo 'Rx Optical Power: -5.01dBm, Tx Optical Power: -2.41dBm' |grep -Po '(?<=:).*?(?=d)'           # 取出d前面数字 # ?为最小匹配
		echo 'Rx Optical Power: -5.01dBm, Tx Optical Power: -2.41dBm' | grep -Po '[-0-9.]+'                # 取出d前面数字 # ?为最小匹配
		echo '["mem",ok],["hardware",false],["filesystem",false]' |grep -Po '[^"]+(?=",false)'             # 取出false前面的字母
		echo '["mem",ok],["hardware",false],["filesystem",false]' |grep -Po '\w+",false'|grep -Po '^\w+'   # 取出false前面的字母



<h5 id="tr">tr</h5> 
	
		-c          # 用字符串1中字符集的补集替换此字符集，要求字符集为ASCII
		-d          # 删除字符串1中所有输入字符
		-s          # 删除所有重复出现字符序列，只保留第一个:即将重复出现字符串压缩为一个字符串
		[a-z]       # a-z内的字符组成的字符串
		[A-Z]       # A-Z内的字符组成的字符串
		[0-9]       # 数字串
		\octal      # 一个三位的八进制数，对应有效的ASCII字符
		[O*n]       # 表示字符O重复出现指定次数n。因此[O*2]匹配OO的字符串

* tr中特定控制字符表达方式

			\a Ctrl-G    \007    # 铃声
			\b Ctrl-H    \010    # 退格符
			\f Ctrl-L    \014    # 走行换页
			\n Ctrl-J    \012    # 新行
			\r Ctrl-M    \015    # 回车
			\t Ctrl-I    \011    # tab键
			\v Ctrl-X    \030

		
* 实例

		tr A-Z a-z                             # 将所有大写转换成小写字母
		tr " " "\n"                            # 将空格替换为换行
		tr -s "[\012]" < plan.txt              # 删除空行
		tr -s ["\n"] < plan.txt                # 删除空行
		tr -s "[\015]" "[\n]" < file           # 删除文件中的^M，并代之以换行
		tr -s "[\r]" "[\n]" < file             # 删除文件中的^M，并代之以换行
		tr -s "[:]" "[\011]" < /etc/passwd     # 替换passwd文件中所有冒号，代之以tab键
		tr -s "[:]" "[\t]" < /etc/passwd       # 替换passwd文件中所有冒号，代之以tab键
		echo $PATH | tr ":" "\n"               # 增加显示路径可读性
		1,$!tr -d '\t'                         # tr在vi内使用，在tr前加处理行范围和感叹号('$'表示最后一行)
		tr "\r" "\n"<macfile > unixfile        # Mac -> UNIX
		tr "\n" "\r"<unixfile > macfile        # UNIX -> Mac
		tr -d "\r"<dosfile > unixfile          # DOS -> UNIX  Microsoft DOS/Windows 约定，文本的每行以回车字符(\r)并后跟换行符(\n)结束
		awk '{ print $0"\r" }'<unixfile > dosfile   # UNIX -> DOS：在这种情况下，需要用awk，因为tr不能插入两个字符来替换一个字符


<h5 id="seq">seq</h5> 


		# 不指定起始数值，则默认为 1
		-s   # 选项主要改变输出的分格符, 预设是 \n
		-w   # 等位补全，就是宽度相等，不足的前面补 0
		-f   # 格式化输出，就是指定打印的格式

		seq 10 100               # 列出10-100
		seq 1 10 |tac            # 倒叙列出
		seq -s '+' 90 100 |bc    # 从90加到100
		seq -f 'dir%g' 1 10 | xargs mkdir     # 创建dir1-10
		seq -f 'dir%03g' 1 10 | xargs mkdir   # 创建dir001-010




<h5 id="trap">trap</h5> 

>
		信号         说明
		HUP(1)     # 挂起，通常因终端掉线或用户退出而引发
		INT(2)     # 中断，通常因按下Ctrl+C组合键而引发
		QUIT(3)    # 退出，通常因按下Ctrl+\组合键而引发
		ABRT(6)    # 中止，通常因某些严重的执行错误而引发
		ALRM(14)   # 报警，通常用来处理超时
		TERM(15)   # 终止，通常在系统关机时发送
		
>
		trap捕捉到信号之后，可以有三种反应方式：
			1、执行一段程序来处理这一信号
			2、接受信号的默认操作
			3、忽视这一信号
		
		第一种形式的trap命令在shell接收到 signal list 清单中数值相同的信号时，将执行双引号中的命令串：
		trap 'commands' signal-list   # 单引号，要在shell探测到信号来的时候才执行命令和变量的替换，时间一直变
		trap "commands" signal-list   # 双引号，shell第一次设置信号的时候就执行命令和变量的替换，时间不变


<h5 id="dialogcaidan">dialog菜单</h5> 

>	
		# 默认将所有输出用 stderr 输出，不显示到屏幕   使用参数  --stdout 可将选择赋给变量
		# 退出状态  0正确  1错误

* 窗体类型

			--calendar          # 日历
			--checklist         # 允许你显示一个选项列表，每个选项都可以被单独的选择 (复选框)
			--form              # 表单,允许您建立一个带标签的文本字段，并要求填写
			--fselect           # 提供一个路径，让你选择浏览的文件
			--gauge             # 显示一个表，呈现出完成的百分比，就是显示出进度条。
			--infobox           # 显示消息后，（没有等待响应）对话框立刻返回，但不清除屏幕(信息框)
			--inputbox          # 让用户输入文本(输入框)
			--inputmenu         # 提供一个可供用户编辑的菜单（可编辑的菜单框）
			--menu              # 显示一个列表供用户选择(菜单框)
			--msgbox(message)   # 显示一条消息,并要求用户选择一个确定按钮(消息框)
			--password          # 密码框，显示一个输入框，它隐藏文本
			--pause             # 显示一个表格用来显示一个指定的暂停期的状态
			--radiolist         # 提供一个菜单项目组，但是只有一个项目，可以选择(单选框)
			--tailbox           # 在一个滚动窗口文件中使用tail命令来显示文本
			--tailboxbg         # 跟tailbox类似，但是在background模式下操作
			--textbox           # 在带有滚动条的文本框中显示文件的内容  (文本框)
			--timebox           # 提供一个窗口，选择小时，分钟，秒
			--yesno(yes/no)     # 提供一个带有yes和no按钮的简单信息框
		

* 窗体参数

			--separate-output          # 对于chicklist组件,输出结果一次输出一行,得到结果不加引号 
			--ok-label "提交"          # 确定按钮名称
			--cancel-label "取消"      # 取消按钮名称
			--title "标题"             # 标题名称
			--stdout                   # 将所有输出用 stdout 输出
			--backtitle "上标"         # 窗体上标
			--no-shadow                # 去掉窗体阴影
			--menu "菜单名" 20 60 14   # 菜单及窗口大小
			--clear                    # 完成后清屏操作
			--no-cancel                # 不显示取消项
			--insecure                 # 使用星号来代表每个字符
			--begin <y> <x>            # 指定对话框左上角在屏幕的上的做坐标
			--timeout <秒>             # 超时,返回的错误代码255,如果用户在指定的时间内没有给出相应动作,就按超时处理
			--defaultno                # 使选择默认为no
			--default-item <str>       # 设置在一份清单，表格或菜单中的默认项目。通常在框中的第一项是默认
			--sleep 5                  # 在处理完一个对话框后静止(延迟)的时间(秒)
			--max-input size           # 限制输入的字符串在给定的大小之内。如果没有指定，默认是2048
			--keep-window              # 退出时不清屏和重绘窗口。当几个组件在同一个程序中运行时，对于保留窗口内容很有用的
		

		dialog --title "Check me" --checklist "Pick Numbers" 15 25 3 1 "one" "off" 2 "two" "on"         # 多选界面[方括号]
		dialog --title "title" --radiolist "checklist" 20 60 14 tag1 "item1" on tag2 "item2" off        # 多选界面(圆括号)
		dialog --title "title" --menu "MENU" 20 60 14 tag1 "item1" tag2 "item2"                         # 单选界面
		dialog --title "Installation" --backtitle "Star Linux" --gauge "Linux Kernel"  10 60 50         # 进度条
		dialog --title "标题" --backtitle "Dialog" --yesno "说明" 20 60                                 # 选择yes/no		
		dialog --title "公告标题" --backtitle "Dialog" --msgbox "内容" 20 60                            # 公告
		dialog --title "hey" --backtitle "Dialog" --infobox "Is everything okay?" 10 60                 # 显示讯息后立即离开
		dialog --title "hey" --backtitle "Dialog" --inputbox "Is okay?" 10 60 "yes"                     # 输入对话框
		dialog --title "Array 30" --backtitle "All " --textbox /root/txt 20 75                          # 显示文档内容
		dialog --title "Add" --form "input" 12 40 4 "user" 1 1 "" 1 15 15 0 "name" 2 1 "" 2 15 15 0     # 多条输入对话框
		dialog --title  "Password"  --insecure  --passwordbox  "请输入密码"  10  35                     # 星号显示输入--insecure
		dialog --stdout --title "日历"  --calendar "请选择" 0 0 9 1 2010                                # 选择日期
		dialog --title "title" --menu "MENU" 20 60 14 tag1 "item1" tag2 "item2" 2>tmp                   # 取到结果放到文件中(以标准错误输出结果)
		a=`dialog --title "title"  --stdout --menu "MENU" 20 60 14 tag1 "item1" tag2 "item2"`           # 选择操作赋给变量(使用标准输出)
		
* 实例

			while :
			do
			clear
			menu=`dialog --title "title"  --stdout --menu "MENU" 20 60 14 1 system 2 custom`
			[ $? -eq 0 ] && echo "$menu" || exit         # 判断dialog执行,取消退出
				while :
				do
					case $menu in
					1)
						list="1a "item1" 2a "item2""     # 定义菜单列表变量
					;;
					2)
						list="1b "item3" 2b "item4""
					;;
					esac
					result=`dialog --title "title"  --stdout --menu "MENU" 20 60 14 $list` 
					[ $? -eq 0 ] && echo "$result" || break    # 判断dialog执行,取消返回菜单,注意:配合上层菜单循环
					read
				done
			done
		

<h5 id="selectcaidan">select菜单</h5> 


>		输入项不在菜单自动会提示重新输入

		select menuitem in pick1 pick2 pick3 退出
		do
			echo $menuitem
			case $menuitem in
			退出)
				exit
			;;
			*)
				select area in area1 area2 area3 返回
				do
					echo $area
					case area in
					返回)
						break
					;;
					*)
						echo "对$area操作"
					;;
					esac
				done
			;;
			esac
		done


<h5 id="shift">shift</h5> 


		./cs.sh 1 2 3
		#!/bin/sh
		until [ $# -eq 0 ]
		do
			echo "第一个参数为: $1 参数个数为: $#"
			#shift 命令执行前变量 $1 的值在shift命令执行后不可用
			shift
		done


<h5 id="getopts">getopts给脚本加参数</h5> 
		

		#!/bin/sh
		while getopts :ab: name
		do
			case $name in
			a)  
				aflag=1
			;;
			b)  
				bflag=1
				bval=$OPTARG
			;;
			\?) 
				echo "USAGE:`basename $0` [-a] [-b value]"
				exit  1
			;;
			esac
		done
		if [ ! -z $aflag ] ; then
			echo "option -a specified"
			echo "$aflag"
			echo "$OPTIND"
		fi
		if [ ! -z $bflag ] ; then
			echo  "option -b specified"
			echo  "$bflag"
			echo  "$bval"
			echo  "$OPTIND"
		fi
		echo "here  $OPTIND"
		shift $(($OPTIND -1))
		echo "$OPTIND"
		echo " `shift $(($OPTIND -1))`  "


<h5 id="tclsh">tclsh</h5> 


		set foo "a bc"                   # 定义变量
		set b {$a};                      # 转义  b的值为" $a " ,而不是变量结果
		set a 3; incr a 3;               # 数字的自增.  将a加3,如果要减3,则为 incr a –3;
		set c [expr 20/5];               # 计算  c的值为4
		puts $foo;                       # 打印变量
		set qian(123) f;                 # 定义数组
		set qian(1,1,1) fs;              # 多维数组
		parray qian;                     # 打印数组的所有信息
		string length $qian;             # 将返回变量qian的长度
		string option string1 string2;   # 字符相关串操作
		# option 的操作选项:
		# compare           按照字典的排序方式进行比较。根据string1 <,=,>string2分别返回-1,0,1
		# first             返回string2中第一次出现string1的位置，如果没有出现string1则返回-1
		# last              和first相反
		# trim              从string1中删除开头和结尾的出现在string2中的字符
		# tolower           返回string1中的所有字符被转换为小写字符后的新字符串
		# toupper           返回string1中的所有字符串转换为大写后的字符串
		# length            返回string1的长度
		set a 1;while {$a < 3} { set a [incr a 1;]; };puts $a    # 判断变量a小于3既循环
		for {initialization} {condition} {increment} {body}      # 初始化变量,条件,增量,具体操作
		for {set i 0} {$i < 10} {incr i} {puts $i;}              # 将打印出0到9
		if { 表达式 } {
			 #运算;
		} else {
			 #其他运算;
		}
		switch $x {
			字符串1 { 操作1 ;}
			字符串2 { 操作2 ;}
		}
		foreach element {0 m n b v} {    
		# 将在一组变元中进行循环，并且每次都将执行他的循环体
			   switch $element {
					 # 判断element的值
			 }
		}

