# 自动跳转提示页

### 1. jump.php

```php
<!DOCTYPE html>
<html lang="zh-CN">
<head>
    <meta charset="utf-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1">
    <!-- 上述3个meta标签*必须*放在最前面，任何其他内容都*必须*跟随其后！ -->
    <title>跳转页面</title>

    <!-- Bootstrap -->
    <link href="//cdn.bootcss.com/bootstrap/3.3.7/css/bootstrap.min.css" rel="stylesheet">

    <!-- HTML5 shim and Respond.js for IE8 support of HTML5 elements and media queries -->
    <!-- WARNING: Respond.js doesn't work if you view the page via file:// -->
    <!--[if lt IE 9]>
    <script src="https://cdn.bootcss.com/html5shiv/3.7.3/html5shiv.min.js"></script>
    <script src="https://cdn.bootcss.com/respond.js/1.4.2/respond.min.js"></script>
    <![endif]-->
</head>
<body>
<div class="container">
        <h1><?php echo isset($msg) ? $msg : '操作成功';?></h1>
        <p>还有 <strong id="time" class="text-warning"></strong> 跳转！</p>
        <p>没有跳转请 <a href="<?php echo isset($url)?$url:$_SERVER["REQUEST_URI"];?>">点击</a></p>
</div>
<!-- jQuery (necessary for Bootstrap's JavaScript plugins) -->
<script src="https://cdn.bootcss.com/jquery/1.12.4/jquery.min.js"></script>
<!-- Include all compiled plugins (below), or include individual files as needed -->
<script src="//cdn.bootcss.com/bootstrap/3.3.7/js/bootstrap.min.js"></script>

<script>
    var url = '<?php echo isset($url) ? $url : $_SERVER["REQUEST_URI"];?>';
    var time = <?php echo isset($time) ? $time : 3;?>;
    $(document).ready(function () {
        $('#time').text(time);
        var sid = setInterval(function(){
            if(time == 0){
                clearInterval(sid);
                location.href = url;
            }else{
                time --;
                $('#time').text(time);
            }
        },1000);
    })

</script>
</body>
</html>
```

### 2. 使用方法

```php
$this->load->view('tpl/jump');
```

> $this-&gt;load-&gt;view\('tpl/jump',\[array\]\);`array('msg'=>'','url'=>'','time'=>'')`



