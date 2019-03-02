# 步骤

> 这里以`fileinfo`为例
> lnmp1.4

1. 登录[`pecl`](http://pecl.php.net)搜索需要的`fileinfo`
2. `wget 'http://pecl.php.net/get/Fileinfo-1.0.4.tgz'`
3. `tar -zxvf Fileinfo-1.0.4.tgz`
4. `cd Fileinfo-1.0.4`
5. `/usr/local/php/bin/phpize` #phpize
6. `./config --with-php-config=/usr/local/php/bin/php-config`
7. `make && make install`

## 遇到错误

- `reinstall the libmagic ...`
> `yum install -y file-devel`