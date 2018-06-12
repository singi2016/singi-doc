# 数据库用户添加,权限分配

## b2b

> 特指在服务器登录数据库的账号(不允许远程登录数据库)

* root
  * 所有权限 all privileges
* 系统管理员 b2b_admin
  * 表[增删改查],数据库[增改减]索引 insert,select,delete,update,create,alter,drop,index
* 应用管理员 b2b_app
  * 增删改查 insert,select,delete,update
* 运维管理员 b2b_opt
  * 查 select

## 实际操作

> 假设操作的数据库为 `conzhu.com` , 表为 `company`

### 一般流程

1 创建用户并赋予权限

```
# 赋予b2b_admin用户conzhu.com数据库的所有表的 表[增删改查],数据库[增减]索引 权限
grant insert,select,delete,update,create,alter,drop,index on `conzhu.com`.* to b2b_admin@localhost identified by 'Admin2018';
```

2 刷新权限

```
flush privileges;
```

### 命令参考

#### 使用shell脚本执行sql

```
mysql -uroot -p'password' -D'db_name' < /path_to_sql/create_db_role.sql;
```

#### 查看用户权限

1. 查看某用户权限

```
SHOW GRANTS FOR 'b2b_admin'@'localhost';
```

2. 查看当前用户权限
 
```
SHOW GRANTS FOR CURRENT_USER;
```

#### 删除用户和权限

```
drop user b2b_admin@localhost;
flush privileges;
```

#### 修改密码

```
update mysql.user set password=password('Admin2018new') where User="b2b_admin" and Host="localhost";
flush privileges;
```