[regex](regex)  

[awk](awk) |[sed](sed)



[variable](variable)

[if](#if)|[for](#for)|[while](#while) | [case](#case)|[until](#until)

[xargs](#xargs)

[except](except)

[example](shellexample)

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
