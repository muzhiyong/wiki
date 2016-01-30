
cacti 中如果添加需要127.0.0.1 为ip address的主机时，会报错
搞定方法如下

vi add_device.php
注释掉验证，//就是注释。

```
    /* process ip */
    if (isset($addresses[$ip])) {
        //db_execute("update host set description = '$description' where id = " . $addresses[$ip]);
        echo "ERROR: This IP already exists in the database ($ip) device-id: (" . $addresses[$ip] . ")\n";
        exit(1);
    }


 变成全部注释掉

    /* process ip */
    /* disable the ip check
    if (isset($addresses[$ip])) {
        //db_execute("update host set description = '$description' where id = " . $addresses[$ip]);
        echo "ERROR: This IP already exists in the database ($ip) device-id: (" . $addresses[$ip] . ")\n";
        exit(1);
    }
    */

```

snmp
		

```
		snmptranslate .1.3.6.1.2.1.1.3.0    # 查看映射关系
		DISMAN-EVENT-MIB::sysUpTimeInstance
		snmpdf -v 1 -c public localhost                            # SNMP监视远程主机的磁盘空间
		snmpnetstat -v 2c -c public -a 192.168.6.53                # SNMP获取指定IP的所有开放端口状态
		snmpwalk -v 2c -c public 10.152.14.117 .1.3.6.1.2.1.1.3.0  # SNMP获取主机启动时间
		# MIB安装(ubuntu) 
		# sudo apt-get install snmp-mibs-downloader
		# sudo download-mibs
		snmpwalk -v 2c -c public 10.152.14.117 sysUpTimeInstance   # SNMP通过MIB库获取主机启动时间
```