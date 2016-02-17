监控nagios自身

```
!/bin/sh
source /etc/profile
flag=`tail /usr/local/nagios/var/nagios.log |grep 'SIGSEGV'`
con="nagios is down"
if [ -n "$flag" ];then
        python /opt/scripts/mail/python/sendmail.py shuyiguo@sohu-inc.com,zhiyongmu@sohu-inc.com "nagios server maybe down"
        /usr/bin/wget -q -O /dev/null "http://10.10.76.79:8800/sms/send/?NUM=18810423928&conn=${con}"
fi
echo -n "`date +%F-%T` "
/etc/init.d/nagios start
chmod 777 /usr/local/nagios/var/rw/nagios.cmd
```