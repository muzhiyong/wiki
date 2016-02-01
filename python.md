*[常见错误合集](errors)*

抓取,提炼html元素 pyquery


[help](#help)
[pip](#pip)
[tab补全](#tab)

#####基础
[变量](#bianlian)
[print](#print)
[列表](#list)
[元组](#yuanzu)
[字典](#zidian)
[内建函数](#neijianhanshu)
[集合](#jihe)
[序列](#xulie)
[字符串](#zifuchuan)


#####流程结构
[if](#if)
[while](#while)
[for](#for)


#####常用方法
[自定义函数](#hanshu)
[模块](#mokuai)
[取参数](#qucanshu)
[对象的使用](#duixiang)



#####文件处理
[文件处理](#file)


[异常处理](python-try-excpet)


模块
[os](python-os)


<h5 id="help">help</h5>

	import os
	for i in dir(os):
		print i         # 模块的方法
	help(os.path)       # 方法的帮助



<h5 id="pip">pip</h5>


* centos安装pip

		yum install python-pip

* ubuntu安装pip

		sudo apt-get install python-pip

* pip官方安装脚本

		wget https://raw.github.com/pypa/pip/master/contrib/get-pip.py
		python get-pip.py
* 源码安装

                wget https://xxx.com/pip-7.1.2.tar.gz
                tar zxvf pip-7.1.2.tar.gz
                cd pip-7.1.2
                python setup.py install

* 加载环境变量

		vim /etc/profile
		export PATH=/usr/local/python27/bin:$PATH
		. /etc/profile

* 常用命令

```
	pip install Package             # 安装包 pip install requests
	pip show --files Package        # 查看安装包时安装了哪些文件
	pip show --files Package        # 查看哪些包有更新
	pip install --upgrade Package   # 更新一个软件包
	pip uninstall Package           # 卸载软件包
```

<h5 id="tab">tab补全</h5>

	# vim /usr/lib/python2.7/dist-packages/tab.py
	# python startup file
	import sys
	import readline
	import rlcompleter
	import atexit
	import os
	# tab completion
	readline.parse_and_bind('tab: complete')
	# history file
	histfile = os.path.join(os.environ['HOME'], '.pythonhistory')



<h5 id="bianlian">变量</h5>


	r=r'\n'          # 输出时原型打印
	u=u'中文'        # 定义为unicode编码
	global x         # 全局变量
	a = 0 or 2 or 1  # 布尔运算赋值,a值为True既不处理后面,a值为2.  None、字符串''、空元组()、空列表[],空字典{}、0、空字符串都是false
	name = raw_input("input:").strip()        # 输入字符串变量
	num = int(raw_input("input:").strip())    # 输入字符串str转为int型
	locals()                                  # 所有局部变量组成的字典
	locals().values()                         # 所有局部变量值的列表
	os.popen("date -d @{0} +'%Y-%m-%d %H:%M:%S'".format(12)).read()    # 特殊情况引用变量 {0} 代表第一个参数


<h5 id="print">print</h5>


	# 字符串 %s  整数 %d  浮点 %f  原样打印 %r
	print '字符串: %s 整数: %d 浮点: %f 原样打印: %r' % ('aa',2,1.0,'r')
	print 'abc',      # 有逗号,代表不换行打印,在次打印会接着本行打印


<h5 id="list">列表</h5>

> 列表和元组的主要区别在于，列表可以修改，元组则不能。

	# 列表元素的个数最多 536870912
	shoplist = ['apple', 'mango', 'carrot', 'banana']
	shoplist[2] = 'aa'
	del shoplist[0]
	shoplist.insert('4','www')
	shoplist.append('aaa')
	shoplist[::-1]    # 倒着打印 对字符翻转串有效

* 列表类型内建函数

```
	list.append(obj)                 # 向列表中添加一个对象obj
	list.count(obj)                  # 返回一个对象obj在列表中出现的次数
	list.extend(seq)                 # 把序列seq的内容添加到列表中
	list.index(obj,i=0,j=len(list))  # 返回list[k] == obj 的k值,并且k的范围在i<=k<j;否则异常
	list.insert(index.obj)           # 在索引量为index的位置插入对象obj
	list.pop(index=-1)               # 删除并返回指定位置的对象,默认是最后一个对象
	list.remove(obj)                 # 从列表中删除对象obj
	list.reverse()                   # 原地翻转列表
	list.sort(func=None,key=None,reverse=False)  # 以指定的方式排序列表中成员,如果func和key参数指定,则按照指定的方式比较各个元素,如果reverse标志被置为True,则列表以反序排列
```

<h5 id="yuanzu">元组</h5>

	# 不可变
	zoo = ('wolf', 'elephant', 'penguin')


<h5 id="zidian">字典</h5>

	ab = {       'Swaroop'   : 'swaroopch@byteofpython.info',
				 'Larry'     : 'larry@wall.org',
		 }
	ab['c'] = 80      # 添加字典元素
	del ab['Larry']   # 删除字典元素
	ab.keys()         # 查看所有键值
	ab.values()       # 打印所有值
	ab.has_key('a')   # 查看键值是否存在
	ab.items()        # 返回整个字典列表


* 字典相关函数

```

	dict([container])     # 创建字典的工厂函数。提供容器类(container),就用其中的条目填充字典
	len(mapping)          # 返回映射的长度(键-值对的个数)
	hash(obj)             # 返回obj哈希值,判断某个对象是否可做一个字典的键值
```

* 字典内建方法

```
	dict.clear()                            # 删除字典中所有元素
	dict copy()                             # 返回字典(浅复制)的一个副本
	dict.fromkeys(seq,val=None)             # 创建并返回一个新字典,以seq中的元素做该字典的键,val做该字典中所有键对的初始值
	dict.get(key,default=None)              # 对字典dict中的键key,返回它对应的值value,如果字典中不存在此键,则返回default值
	dict.has_key(key)                       # 如果键在字典中存在,则返回True 用in和not in代替
	dicr.items()                            # 返回一个包含字典中键、值对元组的列表
	dict.keys()                             # 返回一个包含字典中键的列表
	dict.iter()                             # 方法iteritems()、iterkeys()、itervalues()与它们对应的非迭代方法一样,不同的是它们返回一个迭代子,而不是一个列表
	dict.pop(key[,default])                 # 和方法get()相似.如果字典中key键存在,删除并返回dict[key]
	dict.setdefault(key,default=None)       # 和set()相似,但如果字典中不存在key键,由dict[key]=default为它赋值
	dict.update(dict2)                      # 将字典dict2的键值对添加到字典dict
	dict.values()                           # 返回一个包含字典中所有值得列表 
```

<h5 id="neijianhanshu">内建函数</h5>


	dir(sys)            # 显示对象的属性
	help(sys)           # 交互式帮助
	int(obj)            # 转型为整形
	str(obj)            # 转为字符串
	len(obj)            # 返回对象或序列长度
	open(file,mode)     # 打开文件 #mode (r 读,w 写, a追加)
	range(0,3)          # 返回一个整形列表
	raw_input("str:")   # 等待用户输入
	type(obj)           # 返回对象类型
	abs(-22)            # 绝对值
	random              # 随机数
	random.randrange(9) # 9以内随机数
	choice()            # 随机返回给定序列的一个元素
	divmod(x,y)         # 函数完成除法运算，返回商和余数。
	isinstance(object,int)    # 测试对象类型 int 
	round(x[,n])        # 函数返回浮点数x的四舍五入值，如给出n值，则代表舍入到小数点后的位数
	xrange()            # 函数与range()类似，但xrnage()并不创建列表，而是返回一个xrange对象
		xrange([lower,]stop[,step])
	strip()             # 是去掉字符串两端多于空格,该句是去除序列中的所有字串两端多余的空格
	del                 # 删除列表里面的数据
	cmp(x,y)            # 比较两个对象    #根据比较结果返回一个整数，如果x<y，则返回-1；如果x>y，则返回1,如果x==y则返回0
	max()               # 字符串中最大的字符
	min()               # 字符串中最小的字符
	sorted()            # 对序列排序
	reversed()          # 对序列倒序
	enumerate()         # 返回索引位置和对应的值
	sum()               # 总和
	list()              # 变成列表可用于迭代
	tuple()             # 变成元组可用于迭代   #一旦初始化便不能更改的数据结构,速度比list快
	zip()               # 返回一个列表
		>>> s = ['11','22','33']
		>>> t = ['aa','bb','cc']
		>>> zip(s,t)
		[('11', 'aa'), ('22', 'bb'), ('33', 'cc')]



<h5 id="if">if</h5>

		# 布尔值操作符 and or not 实现多重判断
		if a == b:
			print '=='
		elif a < b:
			print b
		else:
			print a
		fi

<h5 id="while">while</h5>

		while True:
			if a == b:
				print "=="
				break
			print "!="
		else:
			print 'over'
		
		count=0
		while(count<9):
			print count
			count += 1

<h5 id="for">for</h5>

		sorted()           # 返回一个序列(列表)
		zip()              # 返回一个序列(列表)
		enumerate()        # 返回迭代器(类似序列)
		reversed()         # 反序迭代器对象
		dict.iterkeys()    # 通过键迭代
		dict.itervalues()  # 通过值迭代
		dict.iteritems()   # 通过键-值对迭代
		randline()         # 文件迭代
		iter(obj)          # 得到obj迭代器 检查obj是不是一个序列
		iter(a,b)          # 重复调用a,直到迭代器的下一个值等于b
		for i in range(1, 5):
			print i
		else:
			print 'over'

		list = ['a','b','c','b']
		for i in range(len(list)):
			print list[i]
		for x, Lee in enumerate(list):
			print "%d %s Lee" % (x+1,Lee)

* 流程结构简写

		[ i * 2 for i in [8,-2,5]]
		[16,-4,10]
		[ i for i in range(8) if i %2 == 0 ]
		[0,2,4,6]


<h5 id="hanshu">函数</h5>


	def printMax(a, b = 1):
		if a > b:
			print a
			return a
		else:
			print b
			return b
	x = 5
	y = 7
	printMax(x, y)


<h5 id="mokuai">模块</h5>

	# Filename: mymodule.py
	def sayhi():
		print 'mymodule'
	version = '0.1'

	# 导入模块
	import mymodule
	from mymodule import sayhi, version
	# 使用模块中函数
	mymodule.sayhi()

<h5 id="qucanshu">取参数</h5>

> 
	脚本本身为 sys.argv[0]
	第一个参数 sys.argv[1]

	import sys
	print  sys.argv[1]
	# 打印全部参数
	for i in sys.argv:
		print i


<h5 id="duixiang">对象的使用</h5>

	class Person:
		# 实例化初始化的方法
		def __init__(self, name ,age):
			self.name = name
			self.age = age
			print self.name
		# 有self此函数为方法
		def sayHi(self):
			print 'Hello, my name is', self.name
		#对象消逝的时候被调用
		def __del__(self):
			print 'over'
	# 实例化对象
	p = Person('Swaroop')
	# 使用对象方法
	p.sayHi()
	# 继承
	class Teacher(Person):
		def __init__(self, name, age, salary):
			Person.__init__(self, name, age)
			self.salary = salary
			print '(Initialized Teacher: %s)' % self.name
		def tell(self):
			Person.tell(self)
			print 'Salary: "%d"' % self.salary
	t = Teacher('Mrs. Shrividya', 40, 30000)


<h5 id="file">文件处理</h5>


> 
1. 模式: 读'r'  写'w' 追加'a' 读写'r+' 二进制文件'b'  'rb','wb','rb+'
2. 对文件操作完成记得 关闭文件，有open 对应close
3. Python 2 里，file 是文件对象。open 是返回新创建的文件对象的内建函数


* 写文件

		f = file('poem.txt', 'w') 
		f.write("string")
		f.write(str(i))
		f.flush()
		f.close() 

* 读文件

		f = file('/etc/passwd','r')
		while True:
			line = f.readline()    # 返回一行
			if len(line) == 0:
				break
			x = line.split(":")                  # 冒号分割定义序列
			#x = [ x for x in line.split(":") ]  # 冒号分割定义序列
			#x = [ x.split("/") for x in line.split(":") ]  # 先冒号分割,在/分割 打印x[6][1]
			print x[6],"\n",
		f.close() 
	
* 读文件2

		f = file('/etc/passwd')
		c = f.readlines()       # 读入所以文件内容,可反复读取,大文件时占用内存较大
		for line in c:
			print line.rstrip(),
		f.close()

* 读文件3

		for i in open('b.txt'):   # 直接读取也可迭代,并有利于大文件读取,但不可反复读取
			print i,

* with读文件

		with open('a.txt') as f:
			# print f.read()        # 打印所有内容为字符串
			print f.readlines()     # 打印所有内容按行分割的列表

* csv读配置文件  

		192.168.1.5,web # 配置文件按逗号分割
		list = csv.reader(file('a.txt'))
		for line in list:
			print line              #  ['192.168.1.5', 'web']
	
* 追加

		log = open('/home/peterli/xuesong','a')
		print >> log,'faaa'
		log.close()
	

* 文件对象方法

```
	
	file.close()                     # 关闭文件
	file.fileno()                    # 返回文件的描述符
	file.flush()                     # 刷新文件的内部缓冲区
	file.isatty()                    # 判断file是否是一个类tty设备
	file.next()                      # 返回文件的下一行,或在没有其他行时引发StopIteration异常
	file.read(size=-1)               # 从文件读取size个字节,当未给定size或给定负值的时候,读取剩余的所有字节,然后作为字符串返回
	file.readline(size=-1)           # 从文件中读取并返回一行(包括行结束符),或返回最大size个字符
	file.readlines(sizhint=0)        # 读取文件的所有行作为一个列表返回
	file.xreadlines()                # 用于迭代,可替换readlines()的一个更高效的方法
	file.seek(off, whence=0)         # 在文件中移动文件指针,从whence(0代表文件起始,1代表当前位置,2代表文件末尾)偏移off字节
	file.tell()                      # 返回当前在文件中的位置
	file.truncate(size=file.tell())  # 截取文件到最大size字节,默认为当前文件位置
	file.write(str)                  # 向文件写入字符串
	file.writelines(seq)             # 向文件写入字符串序列seq;seq应该是一个返回字符串的可迭代对象

```

* 文件对象的属性

```	
	file.closed          # 表示文件已被关闭,否则为False
	file.encoding        # 文件所使用的编码  当unicode字符串被写入数据时,它将自动使用file.encoding转换为字节字符串;若file.encoding为None时使用系统默认编码
	file.mode            # Access文件打开时使用的访问模式
	file.name            # 文件名
	file.newlines        # 未读取到行分隔符时为None,只有一种行分隔符时为一个字符串,当文件有多种类型的行结束符时,则为一个包含所有当前所遇到的行结束符的列表
	file.softspace       # 为0表示在输出一数据后,要加上一个空格符,1表示不加
```	



<h5 id="jihe">集合</h5>

* 方法
	
```
	s.issubset(t)                # 如果s是t的子集,则返回True   s <= t
	s.issuperset(t)              # 如果t是s的超集,则返回True   s >= t
	s.union(t)                   # 合并操作;返回一个新集合,该集合是s和t的并集   s | t
	s.intersection(t)            # 交集操作;返回一个新集合,该集合是s和t的交集   s & t
	s.difference(t)              # 返回一个新集合,改集合是s的成员,但不是t的成员  s - t
	s.symmetric_difference(t)    # 返回一个新集合,该集合是s或t的成员,但不是s和t共有的成员   s ^ t
	s.copy()                     # 返回一个新集合,它是集合s的浅复制
	obj in s                     # 成员测试;obj是s中的元素 返回True
	obj not in s                 # 非成员测试:obj不是s中元素 返回True
	s == t                       # 等价测试 是否具有相同元素
	s != t                       # 不等价测试 
	s < t                        # 子集测试;s!=t且s中所有元素都是t的成员
	s > t                        # 超集测试;s!=t且t中所有元素都是s的成员
```


* 可变集合方法

```
	s.update(t)                         # 用t中的元素修改s,s现在包含s或t的成员   s |= t
	s.intersection_update(t)            # s中的成员是共用属于s和t的元素          s &= t
	s.difference_update(t)              # s中的成员是属于s但不包含在t中的元素    s -= t
	s.symmetric_difference_update(t)    # s中的成员更新为那些包含在s或t中,但不是s和t共有的元素  s ^= t
	s.add(obj)                          # 在集合s中添加对象obj
	s.remove(obj)                       # 从集合s中删除对象obj;如果obj不是集合s中的元素(obj not in s),将引发KeyError错误
	s.discard(obj)                      # 如果obj是集合s中的元素,从集合s中删除对象obj
	s.pop()                             # 删除集合s中的任意一个对象,并返回它
	s.clear()                           # 删除集合s中的所有元素
```


<h5 id="xulie">序列操作</h5>

* 序列类型操作符

```
	seq[ind]              # 获取下标为ind的元素
	seq[ind1:ind2]        # 获得下标从ind1到ind2的元素集合
	seq * expr            # 序列重复expr次
	seq1 + seq2           # 连接seq1和seq2
	obj in seq            # 判断obj元素是否包含在seq中
	obj not in seq        # 判断obj元素是否不包含在seq中
```

* 序列类型相关的模块

```
	array         # 一种受限制的可变序列类型,元素必须相同类型
	copy          # 提供浅拷贝和深拷贝的能力
	operator      # 包含函数调用形式的序列操作符 operator.concat(m,n)
	re            # perl风格的正则表达式查找
	StringIO      # 把长字符串作为文件来操作 如: read() \ seek()
	cStringIO     # 把长字符串作为文件来操,作速度更快,但不能被继承
	textwrap      # 用作包装/填充文本的函数,也有一个类
	types         # 包含python支持的所有类型
	collections   # 高性能容器数据类型
```

* 序列化

```
	#!/usr/bin/python
	import cPickle
	obj = {'1':['4124','1241','124'],'2':['12412','142','1241']}

	pkl_file = open('account.pkl','wb')
	cPickle.down(obj,pkl_file)
	pkl_file.close()

	pkl_file = open('account.pkl','rb')
	account_list = cPickle.load(pkl_file)
	pkl_file.close()
```


<h5 id="zifuchuan">字符串</h5>

* 字符串相关模块

```
	string         # 字符串操作相关函数和工具
	re             # 正则表达式
	struct         # 字符串和二进制之间的转换
	c/StringIO     # 字符串缓冲对象,操作方法类似于file对象
	base64         # Base16\32\64数据编解码
	codecs         # 解码器注册和基类
	crypt          # 进行单方面加密
	difflib        # 找出序列间的不同
	hashlib        # 多种不同安全哈希算法和信息摘要算法的API
	hma            # HMAC信息鉴权算法的python实现
	md5            # RSA的MD5信息摘要鉴权
	rotor          # 提供多平台的加解密服务
	sha            # NIAT的安全哈希算法SHA
	stringprep     # 提供用于IP协议的Unicode字符串
	textwrap       # 文本包装和填充
	unicodedate    # unicode数据库
```


* 字符串类型内建方法

```
	string.expandtabs(tabsize=8)                  # tab符号转为空格 #默认8个空格
	string.endswith(obj,beg=0,end=len(staring))   # 检测字符串是否已obj结束,如果是返回True #如果beg或end指定检测范围是否已obj结束
	string.count(str,beg=0,end=len(string))       # 检测str在string里出现次数
	string.find(str,beg=0,end=len(string))        # 检测str是否包含在string中
	string.index(str,beg=0,end=len(string))       # 检测str不在string中,会报异常
	string.isalnum()                              # 如果string至少有一个字符并且所有字符都是字母或数字则返回True
	string.isalpha()                              # 如果string至少有一个字符并且所有字符都是字母则返回True
	string.isnumeric()                            # 如果string只包含数字字符,则返回True
	string.isspace()                              # 如果string包含空格则返回True
	string.isupper()                              # 字符串都是大写返回True
	string.islower()                              # 字符串都是小写返回True
	string.lower()                                # 转换字符串中所有大写为小写
	string.upper()                                # 转换字符串中所有小写为大写
	string.lstrip()                               # 去掉string左边的空格
	string.rstrip()                               # 去掉string字符末尾的空格
	string.replace(str1,str2,num=string.count(str1))  # 把string中的str1替换成str2,如果num指定,则替换不超过num次
	string.startswith(obj,beg=0,end=len(string))  # 检测字符串是否以obj开头
	string.zfill(width)                           # 返回字符长度为width的字符,原字符串右对齐,前面填充0
	string.isdigit()                              # 只包含数字返回True
	string.split("分隔符")                        # 把string切片成一个列表
	":".join(string.split())                      # 以:作为分隔符,将所有元素合并为一个新的字符串
```