# excel

### 导入phpexcel

### 后台代码
```php
$objPHPExcel = new\ PHPExcel();
$orderModel = new OrderModel();
$list = $orderModel - > order('id') - > selectByState(array('orderState' => 1)); //要插入到表格中的数据 
//表格设置 
$objActSheet = $objPHPExcel->getActiveSheet(); $objActSheet->getColumnDimension('B')->setAutoSize(true); //内容自适应 
$objActSheet->getColumnDimension('C')->setAutoSize(true); //内容自适应 
$objActSheet->getColumnDimension('D')->setAutoSize(true); //内容自适应 
$objActSheet->getColumnDimension('E')->setAutoSize(true); //内容自适应 
$objActSheet->getColumnDimension('F')->setAutoSize(true); //内容自适应 
$objActSheet->getColumnDimension('G')->setAutoSize(true); //内容自适应 
//设置行头 
$objPHPExcel->getActiveSheet()->setCellValue('A' . 1, '序列');//这里是设置A1单元格的内容 
$objPHPExcel->getActiveSheet()->setCellValue('B' . 1, '订单号');//这里是设置B1单元格的内容 
$objPHPExcel->getActiveSheet()->setCellValue('C' . 1, '粉丝电话号码');//这里是设置C1单元格的内容 
$objPHPExcel->getActiveSheet()->setCellValue('D' . 1, '粉丝姓名');//这里是设置D1单元格的内容
$objPHPExcel->getActiveSheet()->setCellValue('E' . 1, '下单时间');//这里是设置E1单元格的内容 
$objPHPExcel->getActiveSheet()->setCellValue('F' . 1, '商品名称');//这里是设置F1单元格的内容 
$objPHPExcel->getActiveSheet()->setCellValue('G' . 1, '商品分类名');//这里是设置G1单元格的内容
$objPHPExcel->getActiveSheet()->setCellValue('H' . $i, convertUTF8('商品图片'));//这里是设置F1单元格的内容
$objDrawing = new \PHPExcel_Worksheet_Drawing();
//给单元格添加图片 
foreach ($list as $key => $value) { $i = $key + 2;//表格是从第2行开始的 
$objPHPExcel->getActiveSheet()->setCellValue('A' . $i, $value['id']);//里是设置A1单元格的内容 
$objPHPExcel->getActiveSheet()->setCellValue('B' . $i, $value['orderId']);//这里是设置B1单元格的内容
$objPHPExcel->getActiveSheet()->setCellValue('C' . $i, $value['phoNumber']);//这里是设置C1单元格的内容 
$objPHPExcel->getActiveSheet()->setCellValue('D' . $i, $value['fanName']);//这里是设置D1单元格的内容 
$objPHPExcel->getActiveSheet()->setCellValue('E' . $i, $value['orderTime']);//这里是设置E1单元格的内容 
$objPHPExcel->getActiveSheet()->setCellValue('F' . $i, $value['goodsName']);//这里是设置F1单元格的内容 
$objPHPExcel->getActiveSheet()->setCellValue('G' . $i, $value['category']);//这里是设置G1单元格的内容 
//添加图片// $objDrawing->setName($value['goodsName']);
// $objDrawing->setDescription($value['goodsName']);
// $objDrawing->setPath('/Public/upload/20161014/2.jpg'); 
//图片引入位置
// $objDrawing->setCoordinates('H'.$i); //图片添加位置
// $objDrawing->setOffsetX(210);
// $objDrawing->setRotation(25);
// $objDrawing->setHeight(36);
// $objDrawing->getShadow()->setVisible(true);
// $objDrawing->getShadow()->setDirection(45); }; 
$objWriter = new \PHPExcel_Writer_Excel5($objPHPExcel);//保存excel—2007格式 
$name = '未发货订单表-' . date('Ymd'); 

header('Content-Type: application/vnd.ms-excel'); 
header('Content-Disposition: attachment;filename="' . $name . '.xls"'); 
header('Cache-Control: max-age=0'); 
$objWriter->save('php://output');
```

