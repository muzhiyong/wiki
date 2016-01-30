zookeeper 连接数查询

`netstat -na | grep 2181 | awk {'print $5'} | awk -F: {'print $1'} | sort | uniq -c | sort -rn`