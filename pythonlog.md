
思路

```
list.conf
10.10.76.76:/opt/soft/a.log:7
```

从数据库中取出，相应的参数。

新添加服务器第一次传送 crontab 文件。以后只更新


生成crontab配置文件 ，传送到 服务器 /etc/cron.d 固定不变，系统级别，在crontab -l 里看不到，以后不需要更改

增加 debug ，输入到日志，判断是否有错误

0 0 * * * root /usr/sbin/logrotate -f /data/muzy/logrotate/logrotate.conf  -d > /tmp/logrotate.log 2>&1 &

生成 lograte，传送到服务器，每次变更这个文件更新

执行更新


成功状态判断

```
/var/lib/logrotate.status
/tmp/logrotate.log
```

部分代码

```
#!/usr/bin/env python
import os

def start():
	for lines in open('list'):
		ip = lines.split(":")[0]
		log = lines.split(":")[1]
		day = lines.split(":")[2]
		#print ip+"-"+log+"-"+day
		#print log
		#print day
		Conf_File = CreateFile(str(ip))
		file_object = open(Conf_File,'a')
		cron = '* * * * * root /usr/sbin/logrotate -f /data/muzy/logrotate/%slogrotate.conf  -d > /tmp/logrotate.log 2>&1 &' %ip
		file_object.writelines(cron)
		file_object.close()

		logrotate_File = CreateFile(ip+logrotate)
		file_object = open(Conf_File,'a')


def CreateFile(filename):
    #ConfFile = '/Users/Mu/Documents/ops/upnagios/%s.cfg' %filename
    ConfFile = '/Users/Mu/Desktop/%s' %filename
    if os.path.exists(ConfFile):
        os.remove(ConfFile)
    return ConfFile


if __name__ == '__main__':
	start()

```