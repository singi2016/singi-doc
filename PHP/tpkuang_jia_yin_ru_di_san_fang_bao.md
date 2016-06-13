# thinkphp3.2.3框架引入第三方包
> ##注意是引入以.php结尾的

###1. 下载需要引入的第三方包，然后拷贝到Think/Library/Vendor/目录下
###2. 在需要引入的控制器、模型、函数等地方，使用vendor()方法引入第三包即可
###3. 示例：引入七牛云SDK
####3.1 下载七牛云SDK,拷贝到Think/Library/Vendor/目录下，此时的路径是Think/Library/Vendor/qiniuyun。
####3.2 在控制器中引入七牛云，就可以使用了。
```php
//引入七牛云SDK
vendor('qiniuyun.autoload');
```