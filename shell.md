[find](#find) |[sort](#sort)


<h5 id="find">find</h5> 


>		# linux文件无创建时间
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


