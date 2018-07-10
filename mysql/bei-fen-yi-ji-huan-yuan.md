# 备份以及还原

## 备份

```
mysqldump -uroot -p'password' --databases db_name > dump.sql
```

## 还原

```
mysql -uroot -p'password' < dump.sql
```