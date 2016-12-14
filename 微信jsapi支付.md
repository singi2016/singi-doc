# 微信jsapi支付

### 后端
```php
    //下单，写入vip_order表
    $post = $_POST;
    $post['uniacid'] = $uniacid;
    $post['openid'] = $openid;
    $post['total_fee'] = 598.00;
    $post['created'] = date('Y-m-d H:i:s');

    pdo_insert('vip_order',$post);

    //-------------------签名start
    //签名步骤一：按字典序排序参数
    $time = time();
    $sort_data = array(
        'appid'=>$_W['account']['jssdkconfig']['appId'],
        'openid'=>$openid,
        'attach'=>'haihong_vip',
        'body'=>'海弘会员',
        'mch_id'=>$_W['cache']['unisetting:75']['payment']['wechat']['mchid'],
        'nonce_str'=>$_W['account']['jssdkconfig']['nonceStr'],
        'notify_url'=>$_W['siteroot'] . "addons/ewei_shop/payment/wechat/notify.php",
        'out_trade_no'=>md5($time),
        'spbill_create_ip'=>$_W['setting']['cloudip']['ip'],
        'total_fee'=>1,
        'trade_type'=>'JSAPI',
    );
    ksort($sort_data);

    $buff = "";
    foreach ($sort_data as $k => $v) {
        if ($k != "sign" && $v != "" && !is_array($v)) {
            $buff .= $k . "=" . $v . "&";
        }
    }
    $buff = trim($buff, "&");
    $string = $buff;
    //签名步骤二：在string后加入KEY
    $string = $string . "&key=" . $_W['cache']['unisetting:75']['payment']['wechat']['signkey'];
    //签名步骤三：MD5加密
    $string = md5($string);
    //签名步骤四：所有字符转为大写
    $result = strtoupper($string);
    //------------------end

    //调用统一下单接口 start
    $data = '<xml>
       <appid>'.$sort_data['appid'].'</appid>
       <openid>'.$sort_data['openid'].'</openid>
       <attach>'.$sort_data['attach'].'</attach>
       <body>'.$sort_data['body'].'</body>
       <mch_id>'.$sort_data['mch_id'].'</mch_id>
       <nonce_str>'.$sort_data['nonce_str'].'</nonce_str>
       <notify_url>'.$sort_data['notify_url'].'</notify_url>
       <out_trade_no>'.$sort_data['out_trade_no'].'</out_trade_no>
       <spbill_create_ip>'.$sort_data['spbill_create_ip'].'</spbill_create_ip>
       <total_fee>'.$sort_data['total_fee'].'</total_fee>
       <trade_type>'.$sort_data['trade_type'].'</trade_type>
       <sign>'.$result.'</sign>
    </xml>';

    $url = 'https://api.mch.weixin.qq.com/pay/unifiedorder';
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
    //------------------统一下单 end

    //json 返回jsapi调用支付接口信息
    //将XML转为array
    //禁止引用外部xml实体
    libxml_disable_entity_loader(true);
    $retData = json_decode(json_encode(simplexml_load_string($output, 'SimpleXMLElement', LIBXML_NOCDATA)),true);

    //JSAPI 吊起支付参数

    //1. 参数签名
    $jsapi_data = array(
        'appId'=>$_W['account']['jssdkconfig']['appId'],
        'package'=>'prepay_id='.$retData['prepay_id'],
        'nonceStr'=>$_W['account']['jssdkconfig']['nonceStr'],
        'timeStamp'=>time(),
        'signType'=>'SHA1'
    );
    ksort($jsapi_data);
    $jsapi_buff = "";
    foreach ($jsapi_data as $k => $v) {
        if ($k != "sign" && $v != "" && !is_array($v)) {
            $jsapi_buff .= $k . "=" . $v . "&";
        }
    }
    $jsapi_buff = trim($jsapi_buff, "&");
    $jsapi_string = $jsapi_buff;
    //签名步骤二：在string后加入KEY
    $jsapi_string = $jsapi_string . "&key=" . $_W['cache']['unisetting:75']['payment']['wechat']['signkey'];
    //签名步骤三：MD5加密
    $jsapi_string = md5($jsapi_string);
    //签名步骤四：所有字符转为大写
    $jsapi_result = strtoupper($jsapi_string);
    //完成参数拼接
    $jsapi_data['paySign'] = $jsapi_result;

    exit(json_encode($jsapi_data));
```

### 前段
```js
//ajax post
        $.post('/fenxiao/app/index.php?i=75&c=entry&do=shop&m=ewei_shop&op=vip_pay_ajax',ajax_data,function(data){
            //调用微信JS api 支付
            WeixinJSBridge.invoke(
                    'getBrandWCPayRequest',
                    data,
                    function (res) {
                        WeixinJSBridge.log(res.err_msg);
                        if (res.err_msg == "get_brand_wcpay_request:ok") {
                            //支付成功后跳转到提示
                            alert('支付成功');
                            window.location.href = '/fenxiao/app/index.php?i=75&c=entry&do=shop&m=ewei_shop&winzoom=1';
                        } else {
                            //支付失败
                            console.log(res.err_code + res.err_desc + res.err_msg);
                        }
                    }
            );
        },'json');
```


