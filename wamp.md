# WampServer 绑定域名，添加虚拟主机

### 启用虚拟主机配置文件
安装wamp,然后点击wamp小图标，选择apache->httpd.conf;
查找 Virtual hosts  去掉下面include行前面的# 修改为
```
#Virtual hosts
Include conf/extra/httpd-vhosts.conf
```
这样就在配置文件中引入了httpd-vhosts.conf文件。

### 配置虚拟主机

在Apache安装目录的confextra目录下，比如我的是D:\wamp\bin\apache\apache2.2.22\conf\extra，用记事本打开httpd-vhosts.conf，最最底部你会看到２个虚拟主机样例，将其中一个修改为类型下面的，删除多余的样例：
```
<VirtualHost *:80>
 ServerAdmin singi
 DocumentRoot "C:/xampp/htdocs/bannuo/"
 ServerName bannuo.com
 ErrorLog "logs/bannuo.com-error.log"
 CustomLog "logs/bannuo.com-access.log" common
</VirtualHost>
```

### 重启apache
### 添加host记录
用记事本打开 c:\windows\system32\drivers\etc 目录下hosts文件，在最下面添加一行： 
127.0.0.1 bannuo.com 
### 访问浏览器
在浏览器下输入bannuo.com,可以看到通过http已经访问到本机下 d:\wamp\www\bannuo 目录，以后你只要将这个网站的文件放在这个目录即可。 
### 如果你要添加多个虚拟主机，重复上面的操作即可。