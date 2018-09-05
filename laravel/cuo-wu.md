# 错误

1. 修改了类后，无法使用命令行生成文件

```
In ClassLoader.php line 444:
```
解决方法：
```
composer dump-autoload
```