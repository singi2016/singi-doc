# 备份以及还原

## 备份

1. 备份所有数据库

```
mysqldump -uroot -p'password' --all-databases > dump.sql

```

2. 备份某些数据库

```
mysqldump -uroot -p'password' --databases db_name [db2_name]> dump.sql
```

## 还原

```
mysql -uroot -p'password' < dump.sql
```

## shell脚本

> 每天01:00备份数据库,备份保留30天

1. `backup.sh`

```
#!/bin/bash
date_str=`date +%Y%m%d%H%M%S`
mysqldump -uroot -p'password' --all-databases > /root/db_backup/db_backup_${date_str}.sql
```

2. `delete_backup.sh`

> 删除30天以前的sql文件

```
rm -rf $(find /root/db_backup/ -mtime +30 -name "*.sql")
```
