# 微信工具类

### notify
```php
/**
     * 微信支付回调
     */
    function notify()
    {
        //获取通知的数据
        $xml = $GLOBALS['HTTP_RAW_POST_DATA'];
        //将XML转为array
        //禁止引用外部xml实体
        libxml_disable_entity_loader(true);
        $retData = json_decode(json_encode(simplexml_load_string($xml, 'SimpleXMLElement', LIBXML_NOCDATA)), true);

        /**
         * 处理订单支付完成后逻辑
         * $retData为php数组
         */
         
        echo 'success';
    }
```

### curl_post
```
function curl_post($url, $data)
    {
        //创建一个新cURL资源
        $curl = curl_init();
        //设置URL和相应的选项
        curl_setopt($curl, CURLOPT_SAFE_UPLOAD, false);
        curl_setopt($curl, CURLOPT_URL, $url);
        if (!empty($data)) {
            curl_setopt($curl, CURLOPT_POST, 1);
            curl_setopt($curl, CURLOPT_POSTFIELDS, $data);
        }
        curl_setopt($curl, CURLOPT_RETURNTRANSFER, 1);
        curl_setopt($curl, CURLOPT_SSL_VERIFYPEER, FALSE);
        curl_setopt($curl, CURLOPT_SSL_VERIFYHOST, FALSE);//严格校验
        //执行curl，抓取URL并把它传递给浏览器
        $output = curl_exec($curl);
        //关闭cURL资源，并且释放系统资源
        curl_close($curl);
        return son_decode($output,true);
    }
```

### curl_get
```
function curl_get($url)
    {
        //初始化
        $curl = curl_init();
        //设置抓取的url
        curl_setopt_array($curl, array(
            CURLOPT_URL => $url,
            CURLOPT_RETURNTRANSFER => true,
            CURLOPT_ENCODING => "",
            CURLOPT_MAXREDIRS => 10,
            CURLOPT_TIMEOUT => 30,
            CURLOPT_HTTP_VERSION => CURL_HTTP_VERSION_1_1,
            CURLOPT_CUSTOMREQUEST => "GET",
            CURLOPT_SSL_VERIFYPEER => FALSE,
            CURLOPT_SSL_VERIFYHOST => FALSE,
        ));

        $response = curl_exec($curl);
        $err = curl_error($curl);

        curl_close($curl);

        if ($err) {
            return $err;
        } else {
            return json_decode($response, true);
        }
    }
```

### xml2Arr
```
function xml2Arr($xml){
   //禁止引用外部xml实体
   libxml_disable_entity_loader(true);
   return json_decode(json_encode(simplexml_load_string($xml, 'SimpleXMLElement', LIBXML_NOCDATA)), true);
}
```
### arr2Xml
```
function arr2Xml(){
  
}
```
