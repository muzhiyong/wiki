[regex](regex)  

[awk](awk)

[if](#if)|[for](#for)|[while](#while) | [case](#case)|[until](#until)

<font color="red">This is some text!</font>

<h5 id="find">find</h5> 



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
