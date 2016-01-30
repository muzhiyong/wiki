

<h5 id="yum">yum</h5> 

>
* -y 参数代表不需要输入yes
* \* 匹配

		yum list php*                # 查找所有php开头的包
		yum install -y 包名          # 安装包和依赖包
		yum -y update            # 升级所有包版本,依赖关系，系统版本内核都升级
		yum -y update 软件包名   # 升级指定的软件包
		yum -y upgrade           # 不改变软件设置更新软件，系统版本升级，内核不改变
		yum search mail          # yum搜索相关包
		yum grouplist            # 软件包组
		yum -y groupinstall "Virtualization"   # 安装软件包组
		yum clean all            # 清除缓存，一般在更换rpm源时使用
		


* yum扩展源

>包下载地址:http://download.fedoraproject.org/pub/epel   # 选择版本


```
		wget http://download.fedoraproject.org/pub/epel/5/i386/epel-release-5-4.noarch.rpm
		rpm -Uvh epel-release-5-4.noarch.rpm
```
    *mysql源*
```
		wget http://dev.mysql.com/get/mysql-community-release-el7-5.noarch.rpm
		rpm -ivh mysql-community-release-el7-5.noarch.rpm
```

* 自定义yum源

```
		find /etc/yum.repos.d -name "*.repo" -exec mv {} {}.bak \;
		
		vim /etc/yum.repos.d/yum.repo
		[yum]
		#http
		baseurl=http://10.0.0.1/centos5.5
		#挂载iso
		#mount -o loop CentOS-5.8-x86_64-bin-DVD-1of2.iso /data/iso/
		#本地
		#baseurl=file:///data/iso/
		enable=1

		#导入key
		rpm --import  /etc/pki/rpm-gpg/RPM-GPG-KEY-CentOS-5
```
