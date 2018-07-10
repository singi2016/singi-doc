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