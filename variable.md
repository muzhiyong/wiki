
变量

* 实例
		
		A="a b c def"           # 将字符串复制给变量
		A=`cmd`                 # 将命令结果赋给变量
		A=$(cmd)                # 将命令结果赋给变量
		eval a=\$$a             # 间接调用
		i=2&&echo $((i+3))      # 计算后打印新变量结果
		i=2&&echo $[i+3]        # 计算后打印新变量结果
		a=$((2>6?5:8))          # 判断两个值满足条件的赋值给变量
		$1  $2  $*              # 位置参数 *代表所有参数
		env                     # 查看环境变量
		env | grep "name"       # 查看定义的环境变量
		set                     # 查看环境变量和本地变量
		read name               # 输入变量
		readonly name           # 把name这个变量设置为只读变量,不允许再次设置
		readonly                # 查看系统存在的只读文件
		export name             # 变量name由本地升为环境
		export name="RedHat"    # 直接定义name为环境变量
		export Stat$nu=2222     # 变量引用变量赋值
		unset name              # 变量清除
		export -n name          # 去掉只读变量
		shift                   # 用于移动位置变量,调整位置变量,使$3的值赋给$2.$2的值赋予$1
		name + 0                # 将字符串转换为数字
		number " "              # 将数字转换成字符串
		
* 数组

			A=(a b c def)         # 将变量定义为数組
			${#A[*]}              # 数组个数
			${A[*]}               # 数组所有元素
			${A[@]}               # 数组所有元素(标准)
			${A[2]}               # 脚本的一个参数或数组第三位
		


* 定义变量类型

			declare 或 typeset
			-r 只读(readonly一样)
			-i 整形
			-a 数组
			-f 函数
			-x export
			declare -i n=0


* 系统变量

			$0   #  脚本启动名(包括路径)
			$n   #  第n个参数,n=1,2,…9
			$*   #  所有参数列表(不包括脚本本身)
			$@   #  所有参数列表(独立字符串)
			$#   #  参数个数(不包括脚本本身)
			$$   #  当前程式的PID
			$!   #  执行上一个指令的PID
			$?   #  执行上一个指令的返回值



* 变量引用技巧

			${name:+value}        # 如果设置了name,就把value显示,未设置则为空
			${name:-value}        # 如果设置了name,就显示它,未设置就显示value
			${name:?value}        # 未设置提示用户错误信息value 
			${name:=value}        # 如未设置就把value设置并显示<写入本地中>
			${#A}                 # 可得到变量中字节
			${A:4:9}              # 取变量中第4位到后面9位
			${A/www/http}         # 取变量并且替换每行第一个关键字
			${A//www/http}        # 取变量并且全部替换每行关键字
				
			定义了一个变量： file=/dir1/dir2/dir3/my.file.txt
			${file#*/}     # 去掉第一条 / 及其左边的字串：dir1/dir2/dir3/my.file.txt
			${file##*/}    # 去掉最后一条 / 及其左边的字串：my.file.txt
			${file#*.}     # 去掉第一个 .  及其左边的字串：file.txt
			${file##*.}    # 去掉最后一个 .  及其左边的字串：txt
			${file%/*}     # 去掉最后条 / 及其右边的字串：/dir1/dir2/dir3
			${file%%/*}    # 去掉第一条 / 及其右边的字串：(空值)
			${file%.*}     # 去掉最后一个 .  及其右边的字串：/dir1/dir2/dir3/my.file
			${file%%.*}    # 去掉第一个 .  及其右边的字串：/dir1/dir2/dir3/my
			#   # 是去掉左边(在键盘上 # 在 $ 之左边)
			#   % 是去掉右边(在键盘上 % 在 $ 之右边)
			#   单一符号是最小匹配﹔两个符号是最大匹配
