##监控


 #检查url 状态码

```
check=`curl -o /dev/null -s -m 10 --connect-timeout 10 -w %{http_code}  192.168.99.14:9010/server/login.jsp`
if [ "$check" == "200" ]
then
    echo "ok"
fi
```


 #检查端口并重启
```
#!/bin/sh

a=`/usr/local/nagios/libexec/check_tcp -H 10.13.81.220 -p 8088| grep "OK"`
if [ "$a" == "" ]
then
    echo "influxdb is down"
    /etc/init.d/influxdb restart 
fi
```