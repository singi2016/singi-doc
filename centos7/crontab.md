# `crontab`

## `php`执行`crontab`命令
`cron [file]`

1.先生成`cron.txt`内容如下：

> `echo -e` 表示遇到`\n`会换行。

```
echo -e "0 * * * * curl --insecure https://www.example.com/admin.php/auction_crontab/add_cron_next\n
40 * * * * curl --insecure https://www.example.com/admin.php/auction_crontab/fresh\n
50 * * * * curl --insecure https://www.example.com/admin.php/auction_crontab/fresh\n
58 * * * * curl --insecure https://www.example.com/admin.php/auction_crontab/result\n" > cron.txt
```

2.然后`crontab cron.txt`

> 重启crontab `/etc/rc.d/init.d/crond restart`

> 查看crontab运行情况 `tail /var/log/cron`

## `https`
> `curl`访问`https`时，`--insecure`表示忽略`https`证书验证，否则访问会失败。

`curl --insecure https://www.addoom.com`