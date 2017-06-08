# 广告屏蔽插件监测

## js
```javascript
<script>(function(w,u){var d=w.document,z=typeof u;function g207(){function c(c,i){var e=d.createElement('i'),b=d.body,s=b.style,l=b.childNodes.length;if(typeof i!=z){e.setAttribute('id',i);s.margin=s.padding=0;s.height='100%';l=Math.floor(Math.random()*l)+1}e.innerHTML=c;b.insertBefore(e,b.childNodes[l-1])}function g(i,t){return !t?d.getElementById(i):d.getElementsByTagName(t)};function f(v){if(!g('g207')){c('<div class="alert alert-danger alert-dismissible fade in" role="alert"> <button type="button" class="close" data-dismiss="alert" aria-label="Close"><span aria-hidden="true">×</span></button> <strong>本网站监测到您启用了广告屏蔽插件，为了使本网站正常工作，请将本网站加入广告屏蔽插件白名单或暂时禁用广告屏蔽插件!</strong> </div>', 'g207')}};(function(){var a=['Adrectangle','PageLeaderAd','ad-column','advertising2','divAdBox','mochila-column-right-ad-300x250-1','searchAdSenseBox','ad','ads','adsense'],l=a.length,i,s='',e;for(i=0;i<l;i++){if(!g(a[i])){s+='<a id="'+a[i]+'"></a>'}}c(s);l=a.length;for(i=0;i<l;i++){e=g(a[i]);if(e.offsetParent==null||(w.getComputedStyle?d.defaultView.getComputedStyle(e,null).getPropertyValue('display'):e.currentStyle.display)=='none'){return f('#'+a[i])}}}());(function(){var t=g(0,'img'),a=['/adaffiliate_','/adops/ad','/adsales/ad','/adsby.','/adtest.','/ajax/ads/ad','/controller/ads/ad','/pageads/ad','/weather/ads/ad','-728x90-'],i;if(typeof t[0]!=z&&typeof t[0].src!=z){i=new Image();i.onload=function(){this.onload=z;this.onerror=function(){f(this.src)};this.src=t[0].src+'#'+a.join('')};i.src=t[0].src}}());(function(){var o={'http://pagead2.googlesyndication.com/pagead/show_ads.js':'google_ad_client','http://js.adscale.de/getads.js':'adscale_slot_id','http://get.mirando.de/mirando.js':'adPlaceId'},S=g(0,'script'),l=S.length-1,n,r,i,v,s;d.write=null;for(i=l;i>=0;--i){s=S[i];if(typeof o[s.src]!=z){n=d.createElement('script');n.type='text/javascript';n.src=s.src;v=o[s.src];w[v]=u;r=S[0];n.onload=n.onreadystatechange=function(){if(typeof w[v]==z&&(!this.readyState||this.readyState==="loaded"||this.readyState==="complete")){n.onload=n.onreadystatechange=null;r.parentNode.removeChild(n);w[v]=null}};r.parentNode.insertBefore(n,r);setTimeout(function(){if(w[v]!==null){f(n.src)}},2000);break}}}())}if(d.addEventListener){w.addEventListener('load',g207,false)}else{w.attachEvent('onload',g207)}})(window);</script>
```

## css
```
<style>
    #g207 {
        position:fixed;
        width:100%;
        left: 0;
        bottom:0;
        text-align:right;
        font-size: 1.4em;
    }
</style>
```