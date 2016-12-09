# image
> php图像处理

### 访问网页直接输出图像下载
```php
$file = 'monkey.gif';

if (file_exists($file)) {
    header('Content-Description: File Transfer');
    header('Content-Type: application/octet-stream');
    header('Content-Disposition: attachment; filename="'.basename($file).'"');
    header('Expires: 0');
    header('Cache-Control: must-revalidate');
    header('Pragma: public');
    header('Content-Length: ' . filesize($file));
    readfile($file);
    exit;
}
```
### 等比例缩小图片
> 原图被覆盖

```
function scaling($img,$width){
//因为PHP只能对资源进行操作，所以要对需要进行缩放的图片进行拷贝，创建为新的资源
$src=imagecreatefromjpeg($img);

//取得源图片的宽度和高度
$size_src=getimagesize($file_path);
$w=$size_src['0'];
$h=$size_src['1'];

//指定缩放出来的最大的宽度（也有可能是高度）
$max=$width;

//根据最大值为$width，算出另一个边的长度，得到缩放后的图片宽度和高度
if($w > $h){
    $w=$max;
    $h=$h*($max/$size_src['0']);
}else{
    $h=$max;
    $w=$w*($max/$size_src['1']);
}
//声明一个$w宽，$h高的真彩图片资源
$image=imagecreatetruecolor($w, $h);

//关键函数，参数（目标资源，源，目标资源的开始坐标x,y, 源资源的开始坐标x,y,目标资源的宽高w,h,源资源的宽高w,h）
imagecopyresampled($image, $src, 0, 0, 0, 0, $w, $h, $size_src['0'], $size_src['1']);

//告诉浏览器以图片形式解析
imagepng($img,$img);

//销毁资源
imagedestroy($image);

}
```