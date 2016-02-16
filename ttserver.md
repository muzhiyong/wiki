10.11.152.43

执行命令，备份10.11.152.44上的数据文件，带时间点

```
tcrmgr copy -port 11201 10.11.152.44 '@/opt/backup.sh'
tcrmgr copy -port 11202 10.11.152.44 '@/opt/backup.sh'
tcrmgr copy -port 11203 10.11.152.44 '@/opt/backup.sh'
```

10.11.152.44

请确认产生casket.tch.xxxxx类似的文件名，xxxxx代表时间戳。

```
cd /opt/tt_data/data
scp ***** 10.11.152.43:/opt/tt_data/data
```

10.11.152.43

```
ls
echo xxxxx >ttserver.rts
cp casket.tch.xxxxx casket.tch

ttserver -host 10.11.152.43 -port 11201 -mhost 10.11.152.44 -mport 11201 -pid /opt/tt_data/twitter_A.pid -dmn -le -ulog /opt/tt_data/logs/4405/ -sid 4401 -rts /opt/tt_data/data/4401.rts -ulim 128m -ext /home/lightcloud/extensions/our.lua -thnum 6 -tout 5 /opt/tt_data/data/4401.tch#bnum=1000000#fpow=13#opts=ld

ttserver -host 10.11.152.43 -port 11202 -mhost 10.11.152.44 -mport 11202 -pid /opt/tt_data/twitter_B.pid -dmn -le -ulog /opt/tt_data/logs/4402/ -sid 4402 -rts /opt/tt_data/data/4402.rts -ulim 128m -ext /home/lightcloud/extensions/our.lua -thnum 6 -tout 5 /opt/tt_data/data/4402.tch#bnum=1000000#fpow=13#opts=ld

ttserver -host 10.11.152.43 -port 11203 -mhost 10.11.152.44 -mport 11203 -pid /opt/tt_data/twitter_C.pid -dmn -le -ulog /opt/tt_data/logs/4403/ -sid 4403 -rts /opt/tt_data/data/4403.rts -ulim 128m -ext /home/lightcloud/extensions/our.lua -thnum 6 -tout 5 /opt/tt_data/data/4403.tch#bnum=1000000#fpow=13#opts=ld
```

运行后，ttserver将会以此时间戳进行同步。

2. 条数

`tcrmgr inform -port 11205 10.11.152.44`

3. 写入数据

`tcrmgr put -port 11201 10.11.152.44 test1 value1`

4. 读取数据

`tcrmgr get -port 11201 10.11.152.44 test1`

5. 删除数据

`tcrmgr out -port 11201 10.11.152.44 test1`

6. 查看所有的key

`tcrmgr list -port 11201 10.11.152.44`


```
 ttserver -host 10.11.152.43 -port 11203 -mhost 10.11.152.44 -mport 11203 -pid /opt/tt_data/twitter_C.pid -dmn -le -ulog /opt/tt_data/logs/4303/ -sid 4303 -rts /opt/tt_data/data/4303.rts -ulim 128m -ext /home/lightcloud/extensions/our.lua -thnum 6 -tout 5 /opt/tt_data/data/4303.tch#bnum=1000000#fpow=13#opts=ld
```



