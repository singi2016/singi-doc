# php命令行执行sql

## sql.sh

```
mysql -uusername -p'pasword' -D'mysql' < path_to_sql_file/file.sql;

```

## file.sql

```
# create remote account for database
grant all on `database`.* to username@localhost identified by 'pasword';

flush privileges;
```