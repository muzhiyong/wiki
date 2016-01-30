```
yum install libevent-devel
wget http://10.10.76.79:81/muzy/software/twemcache-2.5.0.tar.gz
tar zxvf twemcache-2.5.0.tar.gz
cd  twemcache-2.5.0

./configure --prefix=/opt/twemcache
make ;make install

/opt/twemcache/bin/twemcache -d -m4096 -p30001 -u root -P /opt/twemcache/tw_30001.pid -X /opt/twemcache/cmd_30001.log -l 10.10.68.160
```