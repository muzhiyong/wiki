*[常见错误合集](errors)*

    
抓取

提炼html元素 pyquery




[help](#help)
[pip](#pip)




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