# mysql

### 连接mysql
```
mysql -uroot -proot //-u后面是用户名，-p后面是密码
```

### 常用命令

> mysql命令最后需要加`;`

```
show databases; //显示所有数据库
use user;//选择要操作的数据库
show tables;//显示所有表
describe tables;//显示表结构

select * from tables;
insert tables (name) values ('singi');
update tables set name = 'singi' where id = 1;
delete from tables where id = 1;
```
### 修改数据库表结构

1. 新增1列

```
alter table table_name add column_name tinyint(1) unsigned default 0 comment '备注' not null;
```

### 授权访问用户操作
```
/*
 database授权操作的数据库名称
 username用户名
 host主机ip
 passwd密码
 */
grant create,drop,select,insert,update,delete on database.* to username@host identified by 
passwd; //创建

revoke select,insert,update,delete on *.* from username@host; //删除
flush privileges;//刷新权限
```