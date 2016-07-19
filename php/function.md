# function

## php 基础函数应用


###stdClass类转array
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

