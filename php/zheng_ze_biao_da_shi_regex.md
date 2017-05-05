# 正则表达式regex

### 从html中获取img的src值

```php
preg_match_all('<img.*?src="(.*?)">',ltgt($content),$match);
$files = $match[1];
```

`$match`中的数据如图：

```php
array(2) {
  [0] => array(4) {
    [0] => string(63) "img src="http://o7atl50ri.bkt.clouddn.com/1474440683670594.jpg""
    [1] => string(63) "img src="http://o7atl50ri.bkt.clouddn.com/1474440683631464.jpg""
    [2] => string(63) "img src="http://o7atl50ri.bkt.clouddn.com/1474440683615514.jpg""
    [3] => string(63) "img src="http://o7atl50ri.bkt.clouddn.com/1474440328898781.png""
  }
  [1] => array(4) {
    [0] => string(53) "http://o7atl50ri.bkt.clouddn.com/1474440683670594.jpg"
    [1] => string(53) "http://o7atl50ri.bkt.clouddn.com/1474440683631464.jpg"
    [2] => string(53) "http://o7atl50ri.bkt.clouddn.com/1474440683615514.jpg"
    [3] => string(53) "http://o7atl50ri.bkt.clouddn.com/1474440328898781.png"
  }
}
```



