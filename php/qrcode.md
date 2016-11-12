# QRcode
### 二维码生成

> 生成二维码的路径前不用加`/`,表示的是网站根目录，各路径代表的文件夹必须存在，否则创建失败，因为`QRcode()`不会自动创建对应的目录，只能生成文件.

```
$url = 'http://' . $_SERVER['SERVER_NAME'] . ':' . $_SERVER['SERVER_PORT'] . __CONTROLLER__ . '/extension_user_register?pid=' . $user['id'];
$qrcode = 'Public/customer_qrcode/qrcode.png';
//更新用户的用户二维码
\QRcode::png($url, $qrcode);
```