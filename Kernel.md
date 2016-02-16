####修改内核临时端口范围

1.显示当前临时端口的范围：

一般情形下：linux临时端口号范围是(32768，61000)

`      sysctl  net.ipv4.ip_local_port_range`

或 

`    cat /proc/sys/net/ipv4/ip_local_port_range`

2.暂时性修改临时端口的范围：

`# echo 1024 65535 > /proc/sys/net/ipv4/ip_local_port_range`

注意以上命令是在root用户时执行的！！

或者 

`sudo sysctl -w net.ipv4.ip_local_port_range="1024 64000"`

3.永久性修改

修改文件 /etc/sysctl.conf

键入如下语句：

`net.ipv4.ip_local_port_range = 1024 65535`