[常见错误](#error)


<h5 id="rpm">rpm</h5> 


		rpm -ivh lynx          # rpm安装
		rpm -e lynx            # 卸载包
		rpm -e lynx --nodeps   # 强制卸载
		rpm -qa                # 查看所有安装的rpm包
		rpm -qa | grep lynx    # 查找包是否安装
		rpm -ql                # 软件包路径
		rpm -Uvh               # 升级包
		rpm --test lynx        # 测试
		rpm -qc                # 软件包配置文档
		rpm --import  /etc/pki/rpm-gpg/RPM-GPG-KEY-CentOS-6     # 导入rpm的签名信息

<h5 id="error">error</h5> 

```
rpmdb: unable to join the environment

error: db4 error(11) from dbenv->open: Resource temporarily unavailable
error: cannot open Packages index using db3 - Resource temporarily unavailable (11)
error: cannot open Packages database in /var/lib/rpm
no packages
```
原因，可能和升级内核有关
这次的问题好像不是，解决方法：
解决方法  cd /var/lib/rpm/

```
rm  -f  __db.001
rpm --rebuilddb
```