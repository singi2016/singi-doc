# function

##HTML实体 转换为 html字符串
```js
        //HTML实体 转换为 html字符串 htmlspecialchars_decode
        function htmlspecialchars_decode(str) {
            str = str.replace(/&amp;/g, '&');
            str = str.replace(/&lt;/g, '<');
            str = str.replace(/&gt;/g, '>');
            str = str.replace(/&quot;/g, '"');
            str = str.replace(/&#039;/g, "'");
            return str;
        }
````        