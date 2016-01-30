<h5 id="crontab">crontab</h5> 

>
* 如果发现您的系统里没有这个命令,请安装下面两个软件包 vixie-cron,crontabs
* /var/spool/cron,每个用户一个文件,可以直接编辑,用puppet等进行管理
	
		crontab -e               # 编辑周期任务
		#分钟  小时    天  月  星期   命令或脚本
		1,30  1-13/2    *   *   *      命令或脚本  >> file.log 2>&1   # 每天的1点到13点每两个小时的1分钟和30分钟时执行
		echo "40 7 * * 2 /root/sh">>/var/spool/cron/root    # 直接将命令写入周期任务
		crontab -l                                          # 查看当前用户下的cron任务
		crontab -e                                          # 编辑当前用户的定时任务
		crontab -r                                          # 删除自动周期性任务
		crontab -u  scm  -e                                 # 编辑用户scm的定时任务
		cron.deny和cron.allow                               # 禁止或允许用户使用周期任务
		service crond start|stop|restart                    # 启动自动周期性服务





基本格式 :
*　　*　　*　　*　　*　　command
分　时　日　月　周　命令

第1列表示分钟1～59 每分钟用*或者 */1表示
第2列表示小时1～23（0表示0点）
第3列表示日期1～31
第4列表示月份1～12
第5列标识号星期0～6（0表示星期天）
第6列要运行的命令


注意 :

1. 当程序在你所指定的时间执行后，系统会寄一封信给你，显示该程序执行的内容，若是你不希望收到这样的信，请在每一行空一格之后加上 > /dev/null 2>&1 即可
2. cmd要运行的程序，程序被送入sh执行，这个shell只有USER,HOME,SHELL这三个环境变量

例子：
```
30 21 * * * /usr/local/etc/rc.d/lighttpd restart
上面的例子表示每晚的21:30重启apache。

45 4 1,10,22 * * /usr/local/etc/rc.d/lighttpd restart
上面的例子表示每月1、10、22日的4 : 45重启apache。

10 1 * * 6,0 /usr/local/etc/rc.d/lighttpd restart
上面的例子表示每周六、周日的1 : 10重启apache。

0,30 18-23 * * * /usr/local/etc/rc.d/lighttpd restart
上面的例子表示在每天18 : 00至23 : 00之间每隔30分钟重启apache。

0 23 * * 6 /usr/local/etc/rc.d/lighttpd restart
上面的例子表示每星期六的11 : 00 pm重启apache。

* */1 * * * /usr/local/etc/rc.d/lighttpd restart
每一小时重启apache

* 23-7/1 * * * /usr/local/etc/rc.d/lighttpd restart
晚上11点到早上7点之间，每隔一小时重启apache

0 11 4 * mon-wed /usr/local/etc/rc.d/lighttpd restart
每月的4号与每周一到周三的11点重启apache

0 4 1 jan * /usr/local/etc/rc.d/lighttpd restart
一月一号的4点重启apache

● 0 */2 * * * /sbin/service httpd restart  意思是每两个小时重启一次apache

● 50 7 * * * /sbin/service sshd start  意思是每天7：50开启ssh服务

● 50 22 * * * /sbin/service sshd stop  意思是每天22：50关闭ssh服务

● 0 0 1,15 * * fsck /home  每月1号和15号检查/home 磁盘

● 1 * * * * /home/bruce/backup  每小时的第一分执行 /home/bruce/backup这个文件

● 00 03 * * 1-5 find /home "*.xxx" -mtime +4 -exec rm {} /;  每周一至周五3点钟，在目录/home中，查找文件名为*.xxx的文件，并删除4天前的文件。
● 30 6 */10 * * ls  意思是每月的1、11、21、31日是的6：30执行一次ls命令

#每天早上7点执行一次 /bin/ls :

0 7 * * * /bin/ls

在 12 月内, 每天的早上 6 点到 12 点中，每隔3个小时执行一次 /usr/bin/backup :

0 6-12/3 * 12 * /usr/bin/backup

周一到周五每天下午 5:00 寄一封信给 alex@domain.name :

0 17 * * 1-5 mail -s "hi" alex@domain.name < /tmp/maildata

每月每天的午夜 0 点 20 分, 2 点 20 分, 4 点 20 分....执行 echo "haha"

20 0-23/2 * * * echo "haha"

#每天早上6点10分

10 6 * * * date

#每两个小时

0 */2 * * * date

#晚上11点到早上8点之间每两个小时，早上8点

0 23-7/2，8 * * * date

#每个月的4号和每个礼拜的礼拜一到礼拜三的早上11点

0 11 4 * mon-wed date

#1月份日早上4点

0 4 1 jan * date

```