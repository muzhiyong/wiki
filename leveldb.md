leveldb

```
yum install -y  gcc-c++
wget http://10.10.76.79:81/muzy/software/leveldb-1.15.0.tar.gz
tar zxvf leveldb-1.15.0.tar.gz
cd leveldb-1.15.0
make
cp -r include/leveldb /usr/local/include
```