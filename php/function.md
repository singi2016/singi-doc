# function

## php 基础函数应用

### Json对象转成php可以识别的Json格式(json_decode可以使用的字符串)

```
function JsObjToJsonDecodeEnableStr($js_obj_str){
    return preg_replace(["/([a-zA-Z_]+[a-zA-Z0-9_]*)\s*:/", "/:\s*'(.*?)'/"], ['"\1":', ': "\1"'], $js_obj_str);
}
```

### 1. stdClass类转array
```php
    /** 
      * stdClass类转array 
      * @param $obj 
      * @return mixed 
      */
    function object_to_array($obj){ 
        $_arr = is_object($obj) ? get_object_vars($obj) : $obj; 
        foreach ($_arr as $key => $val) { 
            $val = (is_array($val) || is_object($val)) ? object_to_array($val) : $val; $arr[$key] = $val; 
        } 
        return $arr;
}
```

### 2. 中文星期几
```php
/** 
 * 中文星期几 
 * @param $date 
 * @return mixed 
*/
function cnWeek($date){ 
    $arr = array('天','一','二','三','四','五','六'); 
    return $arr[date('w',strtotime($date))];
} 
```

### 获取客户端真实IP地址

```php
function get_proxy_ip(){

        $arr_ip_header = array(
            'HTTP_CDN_SRC_IP',
            'HTTP_PROXY_CLIENT_IP',
            'HTTP_WL_PROXY_CLIENT_IP',
            'HTTP_CLIENT_IP',
            'HTTP_X_FORWARDED_FOR',
            'REMOTE_ADDR',
        );
        $client_ip = 'unknown';
        foreach ($arr_ip_header as $key)
        {
            if (!empty($_SERVER[$key]) && strtolower($_SERVER[$key]) != 'unknown')
            {
                $client_ip = $_SERVER[$key];
                break;
            }
        }
        return $client_ip;
    }
```

### 二位数组转一维数组-array_column()

### 二维数组去重
```php
function unique_arr($array2D,$stkeep=false,$ndformat=true)
{
    // 判断是否保留一级数组键 (一级数组键可以为非数字)
    if($stkeep) $stArr = array_keys($array2D);
    // 判断是否保留二级数组键 (所有二级数组键必须相同)
    if($ndformat) $ndArr = array_keys(end($array2D));
    //降维,也可以用implode,将一维数组转换为用逗号连接的字符串
    foreach ($array2D as $v){
        $v = join(",",$v); 
        $temp[] = $v;
    }
    //去掉重复的字符串,也就是重复的一维数组
    $temp = array_unique($temp); 
    //再将拆开的数组重新组装
    foreach ($temp as $k => $v)
    {
        if($stkeep) $k = $stArr[$k];
        if($ndformat)
        {
            $tempArr = explode(",",$v); 
            foreach($tempArr as $ndkey => $ndval) $output[$k][$ndArr[$ndkey]] = $ndval;
        }
        else $output[$k] = explode(",",$v); 
    }
    return $output;
}
```

### 二维数组排序
> 将两个数组合并，并排序

```php
      $data = array_merge($data1,$data2);
      // 取得列的列表
      foreach ($author_hot as $key => $row) {
          $volume[$key]  = $row['id'];
      }
      // 将数据根据 volume 降序排列,把 $data 作为最后一个参数，以通用键排序
      array_multisort($volume, SORT_DESC,$data);
```
