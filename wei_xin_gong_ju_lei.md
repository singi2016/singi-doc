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

### xml2Arr
```
function xml2Arr($xml){
   //禁止引用外部xml实体
   libxml_disable_entity_loader(true);
   return json_decode(json_encode(simplexml_load_string($xml, 'SimpleXMLElement', LIBXML_NOCDATA)), true);
}
```