# curl

###post 
```php
    $ch = curl_init();
    $header = array();
    $header[] = 'Content-Type: application/json;charset:utf-8'; //设置编码
    $header[] = 'Content-Length:' . strlen($data); //传输数据长度
    $header[] = "AppKey: ".C('netease_vcloud_appKey');
    $header[] = "Nonce: ".C('netease_vcloud_nonce');
    $header[] = "CurTime: ".$time;
    $header[] = "CheckSum: ".sha1(C('netease_vcloud_appSecret').C('netease_vcloud_nonce').$time);

    curl_setopt($ch, CURLOPT_URL, $api);
    curl_setopt($ch, CURLOPT_POST, 1); //类型post
    curl_setopt($ch, CURLOPT_CONNECTTIMEOUT, 60); //链接时长
    curl_setopt($ch, CURLOPT_HTTPHEADER, $header); //heander头内容
    curl_setopt($ch, CURLOPT_POSTFIELDS , $data); //post数据
    curl_setopt($ch, CURLOPT_RETURNTRANSFER, 1);

    $output = curl_exec($ch);

    return $output;

    curl_close($ch);
```

