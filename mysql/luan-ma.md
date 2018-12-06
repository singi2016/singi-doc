# 写入数据库数据乱码

## 查看数据库字符是否设置正确

```
show variables like 'character%';
```

## 设置所有字符一致

> 找到my.ini文件,添加下面的代码

```
character_set_server=utf8 
init_connect='SET NAMES utf8'
```