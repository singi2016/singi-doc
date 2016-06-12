# MAMP

###在mac系统中的MAMP下扩展mongo(和mongodb)

####具体步骤如下
1. 将MAMP的/bin目录添加到mac执行目录$PATH下，在cmd中运行下面的命令：
```cmd
export PATH=/Applications/MAMP/bin/php/php5.x.x/bin:$PATH
```
 **注意:**把php5.x.x中的x换成具体的数字（在MAMP存在的版本），例如5.6.7，这时整条命令如下：

 ```cmd
export PATH=/Applications/MAMP/bin/php/php5.6.7/bin:$PATH
```

2. 去下载对应的**[php包](http://www.php.net/downloads.php )**，将文件夹里面的所有文件复制到下面的路径中。
  ```cmd
  /Applications/MAMP/bin/php/php5.x.x/include/php(如果/include/php不存在，就手动创建include和php文件夹)
  ```
  然后执行
  ```cmd
  cd /Applications/MAMP/bin/php/php5.x.x/include/php
  ./configure
  ```
  
3. 安装mongo执行
 ```cmd
cd /Applications/MAMP/bin/php/php5.x.x/bin
sudo pecl install mongo（如果报错尝试：sudo ./pecl install mongo）
```
安装mongodb执行
 ```cmd
cd /Applications/MAMP/bin/php/php5.x.x/bin
sudo pecl install mongodb（如果报错尝试：sudo ./pecl install mongodb）
```

4. 在php.ini中加上`extension=mongo.so`，MAMP可以在file->Edit Template->PHP中找到对应的php.ini。
5. 重启MAMP,打印phpinfo看到mongo或mongodb扩展安装的信息，就安装成功了。


> 以上方法来自[这里](http://lukepeters.me/blog/setting-up-mongodb-with-php-and-mamp)


