os模块

* 文件处理

		mkfifo()/mknod()       # 创建命名管道/创建文件系统节点
		remove()/unlink()      # 删除文件
		rename()/renames()     # 重命名文件
		*stat()                # 返回文件信息
		symlink()              # 创建符号链接
		utime()                # 更新时间戳
		tmpfile()              # 创建并打开('w+b')一个新的临时文件
		walk()                 # 遍历目录树下的所有文件名
	
* 目录/文件夹

		chdir()/fchdir()       # 改变当前工作目录/通过一个文件描述符改变当前工作目录
		chroot()               # 改变当前进程的根目录
		listdir()              # 列出指定目录的文件
		getcwd()/getcwdu()     # 返回当前工作目录/功能相同,但返回一个unicode对象
		mkdir()/makedirs()     # 创建目录/创建多层目录
		rmdir()/removedirs()   # 删除目录/删除多层目录
	
* 访问/权限

		saccess()              # 检验权限模式
		chmod()                # 改变权限模式
		chown()/lchown()       # 改变owner和groupID功能相同,但不会跟踪链接
		umask()                # 设置默认权限模式
		
* 文件描述符操作

		open()                 # 底层的操作系统open(对于稳健,使用标准的内建open()函数)
		read()/write()         # 根据文件描述符读取/写入数据 按大小读取文件部分内容
		dup()/dup2()           # 复制文件描述符号/功能相同,但是复制到另一个文件描述符
	
* 设备号

		makedev()              # 从major和minor设备号创建一个原始设备号
		major()/minor()        # 从原始设备号获得major/minor设备号
	

* os.path模块

		os.path.expanduser('~/.ssh/key')   # 家目录下文件的全路径

* 分隔

			basename()         # 去掉目录路径,返回文件名
			dirname()          # 去掉文件名,返回目录路径
			join()             # 将分离的各部分组合成一个路径名
			spllt()            # 返回(dirname(),basename())元组
			splitdrive()       # 返回(drivename,pathname)元组
			splitext()         # 返回(filename,extension)元组
		
* 信息

			getatime()         # 返回最近访问时间
			getctime()         # 返回文件创建时间
			getmtime()         # 返回最近文件修改时间
			getsize()          # 返回文件大小(字节)
		
* 查询

			exists()          # 指定路径(文件或目录)是否存在
			isabs()           # 指定路径是否为绝对路径
			isdir()           # 指定路径是否存在且为一个目录
			isfile()          # 指定路径是否存在且为一个文件
			islink()          # 指定路径是否存在且为一个符号链接
			ismount()         # 指定路径是否存在且为一个挂载点
			samefile()        # 两个路径名是否指向同一个文件

* 子进程

		os.fork()    # 创建子进程,并复制父进程所有操作  通过判断pid = os.fork() 的pid值,分别执行父进程与子进程操作，0为子进程
		os.wait()    # 等待子进程结束

* 相关模块

		base64              # 提供二进制字符串和文本字符串间的编码/解码操作
		binascii            # 提供二进制和ASCII编码的二进制字符串间的编码/解码操作
		bz2                 # 访问BZ2格式的压缩文件
		csv                 # 访问csv文件(逗号分隔文件)
		csv.reader(open(file))
		filecmp             # 用于比较目录和文件
		fileinput           # 提供多个文本文件的行迭代器
		getopt/optparse     # 提供了命令行参数的解析/处理
		glob/fnmatch        # 提供unix样式的通配符匹配的功能
		gzip/zlib           # 读写GNU zip(gzip)文件(压缩需要zlib模块)
		shutil              # 提供高级文件访问功能
		c/StringIO          # 对字符串对象提供类文件接口
		tarfile             # 读写TAR归档文件,支持压缩文件
		tempfile            # 创建一个临时文件
		uu                  # uu格式的编码和解码
		zipfile             # 用于读取zip归档文件的工具
		environ['HOME']     # 查看系统环境变量
	


* 跨平台os模块属性

		linesep         # 用于在文件中分隔行的字符串
		sep             # 用来分隔文件路径名字的字符串
		pathsep         # 用于分割文件路径的字符串
		curdir          # 当前工作目录的字符串名称
		pardir          # 父目录字符串名称
