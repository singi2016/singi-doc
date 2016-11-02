### 微信支付PHP-SDK-v3

### 支付流程
1. 用户下单，调用*微信统一下单接口*
2. 调用微信支付页面，显示订单信息和*立即支付按钮*,以及支付完成之后跳转页面逻辑
3. 在回调notify中处理支付完成之后逻辑

### 微信公众号配置
1. 基本配置-服务器配置：成为开发者
2. 接口权限-网页授权：网页方式获取用户openid
3. 微信支付-开发配置-公众号支付-授权目录：支付授权目录(URL必须与服务器地址完全一致)

### WxpayController.class.php

```php


```

### jsapi.html
```html

<html>
<head>
    <meta http-equiv="content-type" content="text/html;charset=utf-8"/>
    <meta name="viewport" content="width=device-width, initial-scale=1"/>
    <title>微信支付样例-支付</title>
    <script type="text/javascript">
        //调用微信JS api 支付
        function jsApiCall() {
            WeixinJSBridge.invoke(
                    'getBrandWCPayRequest',
                    {$jsApiParameters},
                    function (res) {
                        WeixinJSBridge.log(res.err_msg);
                        if (res.err_msg == "get_brand_wcpay_request:ok") {
                            //支付成功后跳转到提示
                            window.location.href = '{$website}' + '__MODULE__/Order/index';
                        } else {
                            //支付失败
                            alert(res.err_code + res.err_desc + res.err_msg);
                        }
                    }
            );
        }

        function callpay() {
            if (typeof WeixinJSBridge == "undefined") {
                if (document.addEventListener) {
                    document.addEventListener('WeixinJSBridgeReady', jsApiCall, false);
                } else if (document.attachEvent) {
                    document.attachEvent('WeixinJSBridgeReady', jsApiCall);
                    document.attachEvent('onWeixinJSBridgeReady', jsApiCall);
                }
            } else {
                jsApiCall();
            }
        }
    </script>
    <script type="text/javascript">
        //获取共享地址
        function editAddress() {
            WeixinJSBridge.invoke(
                    'editAddress',
                    {editAddress},
                    function (res) {
                        var value1 = res.proviceFirstStageName;
                        var value2 = res.addressCitySecondStageName;
                        var value3 = res.addressCountiesThirdStageName;
                        var value4 = res.addressDetailInfo;
                        var tel = res.telNumber;

                        alert(value1 + value2 + value3 + value4 + ":" + tel);
                    }
            );
        }

        window.onload = function () {
            if (typeof WeixinJSBridge == "undefined") {
                if (document.addEventListener) {
                    document.addEventListener('WeixinJSBridgeReady', editAddress, false);
                } else if (document.attachEvent) {
                    document.attachEvent('WeixinJSBridgeReady', editAddress);
                    document.attachEvent('onWeixinJSBridgeReady', editAddress);
                }
            } else {
                editAddress();
            }
        };

    </script>
</head>
<body>
<br/>
<font color="#9ACD32"><b>该笔订单支付金额为<span style="color:#f00;font-size:50px">1分</span>钱</b></font><br/><br/>
<div align="center">
    <button style="width:210px; height:50px; border-radius: 15px;background-color:#FE6714; border:0px #FE6714 solid; cursor: pointer;  color:white;  font-size:16px;"
            type="button" onclick="callpay()">立即支付
    </button>
</div>
</body>
</html>
```