# 猜一个数字

## 需求描述

猜一个整数，如果错了，系统提示大了还是小了，直到才对为止。结果显示，猜的总次数和正确答案。

## 程序实现

> `PHP`,再命令行下运行

```
$min = 0;
$max = 100;
$answer = rand($min,$max);
$i = 1;
$count = 0;
while($i){
    fwrite(STDOUT,"请猜一个数({$min}-{$max})：");
    $count += 1;
    $in = fgets(STDIN);
    if($in > $answer){
        fwrite(STDOUT,"您输入的数过大\n");
    }elseif($in < $answer){
        fwrite(STDOUT,"您输入的数过小\n");
    }else{
        fwrite(STDOUT,"您猜对了\n您共猜了{$count}次，答案是{$answer}!\n");
        $i = 0;
    }
}
```