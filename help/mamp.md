# MAMP

###在mac系统中的MAMP下扩展mongo(暂不适用扩展mongodb)

####具体步骤如下
1. 将MAMP的/bin目录添加到mac执行目录$PATH下，在cmd中运行下面的命令：
```cmd
export PATH=/Applications/MAMP/bin/php/php5.x.x/bin:$PATH
```
 **注意:**把php5.x.x中的x换成具体的数字，例如5.6.7，这时整条命令如下：

 ```cmd
export PATH=/Applications/MAMP/bin/php/php5.6.7/bin:$PATH
```
设置完成之后，进入到这个目录：
 ```cmd
cd /Applications/MAMP/bin/php/php5.x.x/bin
```

2. 去下载对应的**[php包](http://www.php.net/downloads.php )**，将文件夹里面的所有文件复制到下面的路径中。
```cmd
/Applications/MAMP/bin/php/php5.x.x/include/php
(如果/include/php不存在，就手动创建include和php文件夹)
```
然后进入
```cmd
cd /Applications/MAMP/bin/php/php5.x.x/include/php
```
3. 