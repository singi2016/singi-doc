# str
##str 扩展
###
```js
//除去字符串头部特定字符
String.prototype.trimStart = function(trimStr){  
    if(!trimStr){return this;}  
    var temp = this;  
    while(true){  
        if(temp.substr(0,trimStr.length)!=trimStr){  
            break;  
        }  
        temp = temp.substr(trimStr.length);  
    }  
    return temp;  
};  
//除去字符串尾部特定字符
String.prototype.trimEnd = function(trimStr){  
    if(!trimStr){return this;}  
    var temp = this;  
    while(true){  
        if(temp.substr(temp.length-trimStr.length,trimStr.length)!=trimStr){  
            break;  
        }  
        temp = temp.substr(0,temp.length-trimStr.length);  
    }  
    return temp;  
};  
//除去字符串头尾部特定字符
String.prototype.trim = function(trimStr){  
    var temp = trimStr;  
    if(!trimStr){temp=" ";}  
    return this.trimStart(temp).trimEnd(temp);  
}; 
```
