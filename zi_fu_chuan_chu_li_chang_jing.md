# 字符串处理场景

### 从字符串中获取指定字符
`input` : `http://ob0ci39pv.bkt.clouddn.com/1474613744女03前弓步-动作要领.mp4`

`output` : `1474613744女03前弓步-动作要领.mp4`
```php
/**
 * 根据七牛云地址获取七牛云Key
 * @param $qUrl
 * @return string
 */
function getUrlKey($qUrl,$separator){
    return substr(strrchr($qUrl,'$separator'),1);
}
```
