
 #rsync
```
date
rsync -avlprz /opt/atlassian --exclude=log --exclude=logs 10.13.81.46:/data/backup/10.10.76.79/wiki/
```

 #时间
```
Today=`date +%Y-%m-%d`
Date7=`date -d "7 days ago" +%Y-%m-%d`
```

 #删除
```
back_server=10.13.81.46
tar zcvf samba`date +%y%m%d`.tar.gz samba
ssh  root@${back_server} 'find /data/backup/10.10.76.79/samba/ -name "samba*.gz" -ctime +30 -exec rm -f {} \;'
rm -f /data/smaba$Date7.tar.gz
```