### 网页下载

```
// 1 获取下载内容
$tmp_name = time();
$filename = BASEPATH . "public/zip/".$tmp_name.".zip";
$ouput_name = '订单号：616565116.zip';
$img = '素材图片地址';
$content = 'txt内容';
// 2 组织数组输出
$zip = new ZipArchive();
if ($zip->open($filename, ZIPARCHIVE::CREATE)!==TRUE) { //创建压缩文件
exit("无法打开压缩文件！");
}
$zip->addFromString("设计要求.txt",$content); //添加内容文件
$zip->addFile(BASEPATH . "public/zip/avatar.jpg",'素材1.jpg'); //添加文件
$zip->close();
header('Content-type: application/zip');
header('Content-Disposition: attachment; filename="'.$ouput_name.'"');
readfile($filename); //读取文件，再网页中下载
unlink($filename); //删除生成的压缩文件
```