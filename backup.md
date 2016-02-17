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
BACKUPDIR=/opt/backup
APPS_FILE=$BACKUPDIR/cacti_`date +%y%m%d`.tar.gz
back_server=10.13.81.46
tar zcvf $APPS_FILE samba
ssh  root@${back_server} 'find /data/backup/10.10.76.79/samba/ -name "samba*.gz" -ctime +30 -exec rm -f {} \;'
rm -f /data/smaba$Date7.tar.gz
```

 #备份多台服务器的多个目录指定类型文件
```
while read line
do
    ip=`echo $line|awk -F ':' '{print $1}'`
    path_list=`echo $line|awk -F ':' '{print $2}'`
    mkdir -p /data/Backup_data/$ip/ 
    ssh -n $ip 'find '$path_list' -type f  -name "*.sh" -or -name "*.ctl" -or -name "*.tpl" -or -name "*.py" -or -name "*.plx" -or -name "*.pl" -or -name "*.perl" -or -name "*.pm"  |xargs tar zcf /tmp/data_backup.tar.gz '
    scp $ip:/tmp/data_backup.tar.gz /data/Backup_data/$ip/data_backup`date +%Y%m%d`.tar.gz
done < /opt/scripts/backup_data/data_path.conf
```

 #备份nagios cacti
```
#!/bin/sh

####add by muzy    backup nagios  and cacti ####
BACKUPDIR=/opt/backup
###############
APPS_FILE=$BACKUPDIR/cacti_`date +%y%m%d`.sql.gz
mysqldump -uroot  cacti | gzip > $APPS_FILE
#APPS_FILE1=$BACKUPDIR/resin_`date +%y%m%d`.sql.gz
#mysqldump -uroot  resin | gzip > $APPS_FILE1

scp $APPS_FILE root@10.13.81.46:/data/backup/10.10.76.79/nagios_cacti
cd  $BACKUPDIR
find $BACKUPDIR -name "*.gz" -ctime +5 -exec rm -f {} \;

tar zcvf $BACKUPDIR/nagios_`date +%y%m%d`.tar.gz /usr/local/nagios
scp $BACKUPDIR/nagios_`date +%y%m%d`.tar.gz root@10.13.81.46:/data/backup/10.10.76.79/nagios_cacti


tar zcvf $BACKUPDIR/cacti_`date +%y%m%d`.tar.gz /opt/cacti
scp $BACKUPDIR/cacti_`date +%y%m%d`.tar.gz root@10.13.81.46:/data/backup/10.10.76.79/nagios_cacti

ssh  10.13.81.46 'find /data/backup/10.10.76.79/nagios_cacti -name "*.gz" -ctime +25 -exec rm -f {} \;'
```