# 错误

1. 修改了类后，无法使用命令行生成文件

```
In ClassLoader.php line 444:
```

解决方法：
```
composer dump-autoload
```

2. npm run dev 报错


解决方法:
[laravel5.5](https://github.com/laravel/laravel/blob/5.5/package.json)更新该文件,再`npm install`
