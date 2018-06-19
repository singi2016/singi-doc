# function

## php 基础函数应用


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

