# wamp

##配置自定义域名
安装wamp,然后点击wamp小图标，选择apache->httpd.conf;
查找 Virtual hosts  去掉下面include行前面的# 修改为
```
#Virtual hosts
Include conf/extra/httpd-vhosts.conf
```
这样就在配置文件中引入了httpd-vhosts.conf文件。
