# autoload

###自动引入PHP文件

####目录结构

myphp为最外层文件夹,autoload.php与src平级，将所有的`.php`文件都放在src文件夹内即可，然后使用下面的代码。
* |--myphp
*  --autoload.php
*  --src

####文件名保存为autoload.php

文件具体代码如下：

```php
function classLoader($class)
{
    $path = str_replace('\\', DIRECTORY_SEPARATOR, $class);
    $file = __DIR__ . '/src/' . $path . '.php';

    if (file_exists($file)) {
        require_once $file;
    }
}
spl_autoload_register('classLoader');
```
####示例：
#####1、在thinkphp中使用

在控制器中使用下面方法引用即可
```php
//引入myphp
vendor('myphp.autoload');
```

##参考
* 来自七牛云PHP-SDK的自动引入。