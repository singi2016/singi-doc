# curl

###post请求 
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
    curl_setopt($ch, CURLOPT_POST, 1); //会发送 POST 请求，类型为：application/x-www-form-urlencoded，是 HTML 表单提交时最常见的一种。
    curl_setopt($ch, CURLOPT_CONNECTTIMEOUT, 60); //在尝试连接时等待的秒数。设置为0，则无限等待。
    curl_setopt($ch, CURLOPT_TIMEOUT, 120);
    curl_setopt($ch, CURLOPT_HTTPHEADER, $header); //设置 HTTP 头字段的数组。格式： array('Content-type: text/plain', 'Content-length: 100')
    curl_setopt($ch, CURLOPT_POSTFIELDS , $data); //post数据
    curl_setopt($ch, CURLOPT_RETURNTRANSFER, 1); //将curl_exec()获取的信息以字符串返回，而不是直接输出。

    $output = curl_exec($ch);

    return $output;

    curl_close($ch);
```

