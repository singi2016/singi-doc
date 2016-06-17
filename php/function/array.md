# 数组
## 二位数组转一维数组-array_column()
```php
array array_column ( array $input , mixed $column_key [, mixed $index_key ] )
```
###input
需要取出数组列的多维数组（或结果集）

###column_key
需要返回值的列，它可以是索引数组的列索引，或者是关联数组的列的键。 也可以是NULL，此时将返回整个数组（配合index_key参数来重置数组键的时候，非常管用）

###index_key
作为返回数组的索引/键的列，它可以是该列的整数索引，或者字符串键值。

####个人理解
>**实际上就是从二维数组中取一列返回，默认选择的一列作为value值，当然也可以设置第三个参数，再从二维数组中取一列，作为返回一维数组的key值。**