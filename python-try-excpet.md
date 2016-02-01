<h5 id="yichangchuli">异常处理</h5>


* 异常说明

	NameError:              # 尝试访问一个未申明的变量
	ZeroDivisionError:      # 除数为零
	SyntaxErrot:            # 解释器语法错误
	IndexError:             # 请求的索引元素超出序列范围
	KeyError:               # 请求一个不存在的字典关键字
	IOError:                # 输入/输出错误
	AttributeError:         # 尝试访问未知的对象属性
	ImportError             # 没有模块
	IndentationError        # 语法缩进错误
	KeyboardInterrupt       # ctrl+C
	SyntaxError             # 代码语法错误
	ValueError              # 值错误
	TypeError               # 传入对象类型与要求不符合
	
* 触发异常

		raise exclass            # 触发异常,从exclass生成一个实例(不含任何异常参数)
		raise exclass()          # 触发异常,但现在不是类;通过函数调用操作符(function calloperator:"()")作用于类名生成一个新的exclass实例,同样也没有异常参数
		raise exclass, args      # 触发异常,但同时提供的异常参数args,可以是一个参数也可以是元组
		raise exclass(args)      # 触发异常,同上
		raise exclass, args, tb  # 触发异常,但提供一个跟踪记录(traceback)对象tb供使用
		raise exclass,instance   # 通过实例触发异常(通常是exclass的实例)
		raise instance           # 通过实例触发异常;异常类型是实例的类型:等价于raise instance.__class__, instance
		raise string             # 触发字符串异常
		raise string, srgs       # 触发字符串异常,但触发伴随着args
		raise string,args,tb     # 触发字符串异常,但提供一个跟踪记录(traceback)对象tb供使用
		raise                    # 重新触发前一个异常,如果之前没有异常,触发TypeError
		
* 内建异常
		
		BaseException                # 所有异常的基类
		SystemExit                   # python解释器请求退出
		KeyboardInterrupt            # 用户中断执行
		Exception                    # 常规错误的基类
		StopIteration                # 迭代器没有更多的值
		GeneratorExit                # 生成器发生异常来通知退出
		SystemExit                   # python解释器请求退出
		StandardError                # 所有的内建标准异常的基类
		ArithmeticError              # 所有数值计算错误的基类
		FloatingPointError           # 浮点计算错误
		OverflowError                # 数值运算超出最大限制
		AssertionError               # 断言语句失败
		AttributeError               # 对象没有这个属性
		EOFError                     # 没有内建输入,到达EOF标记
		EnvironmentError             # 操作系统错误的基类
		IOError                      # 输入/输出操作失败
		OSError                      # 操作系统错误
		WindowsError                 # windows系统调用失败
		ImportError                  # 导入模块/对象失败
		KeyboardInterrupt            # 用户中断执行(通常是ctrl+c)
		LookupError                  # 无效数据查询的基类
		IndexError                   # 序列中没有此索引(index)
		KeyError                     # 映射中没有这个键
		MemoryError                  # 内存溢出错误(对于python解释器不是致命的)
		NameError                    # 未声明/初始化对象(没有属性)
		UnboundLocalError            # 访问未初始化的本地变量
		ReferenceError               # 若引用试图访问已经垃圾回收了的对象
		RuntimeError                 # 一般的运行时错误
		NotImplementedError          # 尚未实现的方法
		SyntaxError                  # python语法错误
		IndentationError             # 缩进错误
		TabError                     # tab和空格混用
		SystemError                  # 一般的解释器系统错误
		TypeError                    # 对类型无效的操作
		ValueError                   # 传入无效的参数
		UnicodeError                 # Unicode相关的错误
		UnicodeDecodeError           # Unicode解码时的错误
		UnicodeEncodeError           # Unicode编码时的错误
		UnicodeTranslateError        # Unicode转换时错误
		Warning                      # 警告的基类
		DeprecationWarning           # 关于被弃用的特征的警告
		FutureWarning                # 关于构造将来语义会有改变的警告
		OverflowWarning              # 旧的关于自动提升为长整形的警告
		PendingDeprecationWarning    # 关于特性将会被废弃的警告
		RuntimeWarning               # 可疑的运行时行为的警告
		SyntaxWarning                # 可疑的语法的警告
		UserWarning                  # 用户代码生成的警告

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

* 实例

	class MyException(Exception):   # 继承Exception异常的类,定义自己的异常
			pass
	try:                          # 监控这里的异常
			option=int(raw_input('my age:'))
			if option != 28:
					raise MyException,'a1'  #触发异常
	except MyException,a:         # 异常处理代码
			print 'MyExceptionaa'
			print a    # 打印异常处内容
	except:            # 捕捉所有其它错误
			print 'except'
	finally:           # 无论什么情况都会执行 关闭文件或断开连接等
		   print 'finally' 
	else:              # 无任何异常 无法和finally同用
			print 'no Exception'



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

