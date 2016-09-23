# 字符串处理场景

### 从字符串中获取指定字符
```php
/**
 * @param $str
 * @param $separator
 * @return string
 */
function get($str,$separator){
    return substr(strrchr($str,$separator),1);
}
```
Example：根据七牛云地址获取七牛云Key

`getEndBySeparator('http://ob0ci39pv.bkt.clouddn.com/1474613744女03前弓步-动作要领.mp4','/')`

`input` : `http://ob0ci39pv.bkt.clouddn.com/1474613744女03前弓步-动作要领.mp4`

`output` : `1474613744女03前弓步-动作要领.mp4`
