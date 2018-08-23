# 微信订阅号

## 回复

1. 关键字回复,具体的直接回复链接，其他的回复图文消息

## 菜单

菜单链接到页面模板，页面模板包含以系列图文消息

例如 图书菜单=>图片页面模板< python图书,java图书,php图书,... >

> 每日群发一篇文章


## 微信内网页分享显示LOGO

```
$.post('{:url("home/api/get_wechat_sign")}',{'wechat_key':'{$Think.session.wechat_key}','url':encodeURIComponent(location.href.split("#")[0])},function(res){
            console.log(res);
            wx.config({
                debug: true,
                appId: res.appId,
                timestamp: res.timestamp,
                nonceStr: res.nonceStr,
                signature: res.signature,
                jsApiList: [
                    'onMenuShareTimeline',
                    'onMenuShareAppMessage',
                    'onMenuShareQQ'
                ]
            });
            wx.ready(function () {
                var shareData = {
                    title: $('title').text(),
                    desc: location.href,
                    link: location.href,
                    imgUrl: 'https://www.conzhu.com/public/images/wechat_share_logo_300x300.jpg'
                };
                wx.onMenuShareAppMessage(shareData);//分享给朋友
                wx.onMenuShareTimeline(shareData);//分享到朋友圈
                wx.onMenuShareQQ(shareData);//分享到QQ
            });
            wx.error(function (res) {
                console.log(res);
            });
        },'json');
```

