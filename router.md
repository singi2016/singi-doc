# 路由配置-`URI`

配置文件位置：`application/config/routes.php`
格式：`rootpath/class/method/param`
例如：`http://ci/news/1`表示新闻id为1的记录。

再`router.php`配置如下：

`$route['news/(:num)'] = 'news/$1';`
其中`(:num)`表示任何数字，等同`[0-9]+`,`$1`表示`(:num)`

对照下面理解
`$route['news/(:num)/(:any)'] = 'news/$1/$2';`
其中`(:any)`表示任何字符（除了 '/' 字符，因为它是段与段之间的分隔符）,`$1`表示`(:num)`即第一个参数，`$2`表示`(:any)`,即第二个参数。

