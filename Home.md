*[markdown语法参考](markdown)*  |  *[sample](samplemarkdown)*


[python](python)  | [django](django) | [w3c](w3c)

[java](java)

[linux](linux) | [shell](shell)

进一步整理
[apache](apache)| [mysql](mysql) | [nginx](nginx)| [php](php) |[lvs](lvs)

[zookeeper](zookeeper) 

[leveldb](leveldb) | [kestrel](kestrel) |[twemcache](twemcache) |[redis](redis)

数据库
[mysql](mysql)|[mongodb](mongodb)


存储
[nsq](nsq)

工具类软件
[git](git) | [svn](svn) |[maven](maven)|[wiki](wiki) | [jira](jira) 

监控
[nagios](nagios)|[cacti](cacit)|[zabbix](zabbix)

[mac](mac)


- 开发语言带的简易模块
    - python ：$ python -m SimpleHTTPServer
    - php: $ php -S localhost:8000
    - ruby: $ ruby -run -e httpd . -p 5000

切换用户启动程序

`su rabbitmq -s /bin/sh -c /usr/lib/rabbitmq/bin/rabbitmq-server`

nohup  远程启动的方法

`ssh $ip "cd /opt/nsq ; nohup ./start_nsqd.sh >/opt/nsq/nohup.out < /dev/null 2>&1"`
