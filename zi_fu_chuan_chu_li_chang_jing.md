# 字符串处理场景

#### 查找指定字符在字符串中的最后一次出现,并返回指定字符之后的所有字符（不包括指定字符本身）
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
**例子**：根据七牛云文件地址获取七牛云文件名

`调用` : `getEndBySeparator('http://ob0ci39pv.bkt.clouddn.com/1474613744女03前弓步-动作要`领.mp4','/')`

`输出` : `1474613744女03前弓步-动作要领.mp4`
