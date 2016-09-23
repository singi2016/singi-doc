# 字符串处理场景

### 从字符串中获取指定字符
```php
/**
 * 根据七牛云地址获取七牛云Key
 * @param $qUrl
 * @return string
 */
function getUrlKey($qUrl){
    return substr(strrchr($qUrl,'/'),1);
}
```
