*[常见错误合集](errors)*

抓取,提炼html元素 pyquery

[help](#help)
[pip](#pip)
[tab补全](#tab)

#####字符变量

[变量](#bianlian)
[print](#print)
[列表](#list)
[元组](#yuanzu)
[字典](#zidian)


#####流程结构

[if](#if)
[while](#while)
[for](#for)


#####常用方法

[函数](#hanshu)
[模块](#mokuai)
[取参数](#qucanshu)
[对象的使用](#duixiang)

#####文件处理
[文件处理](#file)

[异常处理](#yichangchuli)
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

	# 列表元素的个数最多 536870912
	shoplist = ['apple', 'mango', 'carrot', 'banana']
	shoplist[2] = 'aa'
	del shoplist[0]
	shoplist.insert('4','www')
	shoplist.append('aaa')
	shoplist[::-1]    # 倒着打印 对字符翻转串有效

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
	

	

<h5 id="yichangchuli">异常处理</h5>

* 一般处理方法

```
    try:
       语句1
       语句2
      .
      .
      语句N
    except .........:
        do something .......
```
        
捕获异常的方法

* 方法一：捕获所有异常

```  
    try:  
        a=b  
        b=c  
    except Exception,e:  
        print Exception,":",e
```

* 方法二：采用traceback模块查看异常

> 引入python中的traceback模块，跟踪错误，打印出来，并保存在日志中

    import traceback  
    try:  
        a=b  
        b=c  
    except:  
        traceback.print_exc()
        f=open("c:log.txt",'a')  
        traceback.print_exc(file=f)  
        f.flush()  
        f.close()


* 方法三：采用sys模块回溯最后的异常

> 引入sys模块

    import sys  
    try:  
        a=b  
        b=c  
    except:  
        info=sys.exc_info()  
        print info[0],":",info[1]


*实例

	class ShortInputException(Exception):
		'''A user-defined exception class.'''
		def __init__(self, length, atleast):
			Exception.__init__(self)
			self.length = length
			self.atleast = atleast
	try:
		s = raw_input('Enter something --> ')
		if len(s) < 3:
			raise ShortInputException(len(s), 3)
	except EOFError:
		print '\nWhy did you do an EOF on me?'
	except ShortInputException, x:
		print 'ShortInputException: The input was of length %d, \
			  was expecting at least %d' % (x.length, x.atleast)
	else:
		print 'No exception was raised.' 
