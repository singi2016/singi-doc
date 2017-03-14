### 网页下载

#### 1 下载压缩文件

```php
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

#### 2 下载excel文件

```php
        $this->load->library('PHPExcel');//ci 导入PHPExcel
        //创建表格对象
        $objPHPExcel = new PHPExcel();
        //读取数据

        //初始化表格内容 [文档](https://github.com/PHPOffice/PHPExcel/blob/develop/Documentation/markdown/Overview/07-Accessing-Cells.md)
        $objPHPExcel->getSheet()->setCellValue('A1', 'PHPExcel');
        //准备网页输出
        $objWriter = new PHPExcel_Writer_Excel2007($objPHPExcel);

        header('Content-type: application/vnd.ms-excel');
        header('Content-Disposition: attachment; filename="资金交易记录.xlsx"');
        $objWriter->save('php://output'); //向网页中输出excel
```