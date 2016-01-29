
##正则表达式

* 通用
	
		^  	      # 行首定位
		$ 	      # 行尾定位
		. 	      # 匹配除换行符以外的任意字符
		*	      # 匹配0或多个重复字符
		+ 	      # 重复一次或更多次
		? 	      # 重复零次或一次
		?         # 结束贪婪因子 .*? 表示最小匹配
		[]	      # 匹配一组中任意一个字符
		[^]	      # 匹配不在指定组内的字符
		\	      # 用来转义元字符
		<	      # 词首定位符(支持vi和grep)  <love
		>	      # 词尾定位符(支持vi和grep)  love>
		x\{m\}    # 重复出现m次
		x\{m,\}   # 重复出现至少m次
		x\{m,n\}  # 重复出现至少m次不超过n次
		X? 	      # 匹配出现零次或一次的大写字母 X
		X+ 	      # 匹配一个或多个字母 X
		()        # 括号内的字符为一组
		(ab|de)+  # 匹配一连串的（最少一个） abc 或 def；abc 和 def 将匹配
		[[:alpha:]]    # 代表所有字母不论大小写
		[[:lower:]]    # 表示小写字母 
		[[:upper:]]    # 表示大写字母
		[[:digit:]]    # 表示数字字符
		[[:digit:][:lower:]]    # 表示数字字符加小写字母 

* 元字符

			\d 	  # 匹配任意一位数字
			\D 	  # 匹配任意单个非数字字符
			\w 	  # 匹配任意单个字母数字下划线字符，同义词是 [:alnum:]
			\W    # 匹配非数字型的字符


* 字符类:空白字符

			\s 	  # 匹配任意的空白符
			\S    # 匹配非空白字符
			\b 	  # 匹配单词的开始或结束
			\n    # 匹配换行符
			\r    # 匹配回车符
			\t    # 匹配制表符
			\b    # 匹配退格符
			\0    # 匹配空值字符


* 字符类:锚定字符

			\b    # 匹配字边界(不在[]中时)
			\B    # 匹配非字边界
			\A    # 匹配字符串开头
			\Z    # 匹配字符串或行的末尾
			\z    # 只匹配字符串末尾
			\G    # 匹配前一次m//g离开之处


* 捕获

			(exp)                # 匹配exp,并捕获文本到自动命名的组里
			(?<name>exp)         # 匹配exp,并捕获文本到名称为name的组里，也可以写成(?'name'exp)
			(?:exp)              # 匹配exp,不捕获匹配的文本，也不给此分组分配组号


* 零宽断言

			(?=exp)              # 匹配exp前面的位置
			(?<=exp)             # 匹配exp后面的位置
			(?!exp)              # 匹配后面跟的不是exp的位置
			(?<!exp)             # 匹配前面不是exp的位置
			(?#comment)	         # 注释不对正则表达式的处理产生任何影响，用于注释



* 特殊字符

			http://en.wikipedia.org/wiki/Ascii_table
			^H  \010 \b  
			^M  \015 \r
			匹配特殊字符: ctrl+V ctrl不放在按H或M 即可输出^H,用于匹配