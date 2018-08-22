# 安装

> 配置好`/eccube_install.php`文件中的`DBUSER`,`DBPASS`和`ROOTPASS`

```
php eccube_install.php mysql
```

# 使用的技术

1. Silex
2. Symfony2(表单类型引用和验证器引用)
3. Doctrine ORM
4. twig
5. composer

# 目录结构

```
/app/ 配置文件和日志文件等,插件和模板
    config/eccube 配置文件
/html 公共资源文件（css和图像文件）
/src 应用程序的主体，一般不允许直接修改这里面内容

```

# 调试

将`/index_dev.php`改为`/index.php`,再访问首页即可进入调试模式 

# 缓存

> 根目录下

```
php app/console cache:clear //清除缓存
```

# 开发

> 将`Resource/template/default`下的对应文件复制到`app/template/default`下修改即可

1. ECCUBEROOT/app/template/[template_code]
2. ECCUBEROOT/src/Eccube/Resource/template/[template_code]
3. ECCUBEROOT/app/Plugin

