# laravel-5.5.28生成器

## 参考链接

[laravelgenerator](http://labs.infyom.com/laravelgenerator/docs/5.5/getting-started)

## 遇到的问题


### 1 failed to open stream: No such file or directory

---

运行`php artisan infyom.publish:layout`时,报错:

  ```php
  In LayoutPublishCommand.php line 86:

  file_get_contents(C:\laragon\www\scaffold.singiblog.top\app\routes/web.php): failed to open stream: No such file or directory

  ```
  
解决方法:
  打开`/vendor/infyomlabs/laravel-generator/src/Commands/Publish/LayoutPublishCommand.php`
  
  `$path = config('infyom.laravel_generator.path.routes', app_path('routes/web.php'));`
  =>`$path = config('infyom.laravel_generator.path.routes', ('routes/web.php'));`
  
  [Support for Laravel 5.4 #382](https://github.com/InfyOmLabs/laravel-generator/issues/382)
  
---


