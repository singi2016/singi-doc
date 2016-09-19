# [PHPMailer](https://github.com/PHPMailer/PHPMailer)
###1. 安装phpmailer
```cmd
composer require phpmailer/phpmailer
```
###2. Github官方例子

```php
<?php
require 'PHPMailerAutoload.php';

$mail = new PHPMailer;

//$mail->SMTPDebug = 3;                               // Enable verbose debug output

$mail->isSMTP();                                      // Set mailer to use SMTP
$mail->Host = 'smtp1.example.com;smtp2.example.com';  // Specify main and backup SMTP servers
$mail->SMTPAuth = true;                               // Enable SMTP authentication
$mail->Username = 'user@example.com';                 // SMTP username
$mail->Password = 'secret';                           // SMTP password
$mail->SMTPSecure = 'tls';                            // Enable TLS encryption, `ssl` also accepted
$mail->Port = 587;                                    // TCP port to connect to

$mail->setFrom('from@example.com', 'Mailer');
$mail->addAddress('joe@example.net', 'Joe User');     // Add a recipient
$mail->addAddress('ellen@example.com');               // Name is optional
$mail->addReplyTo('info@example.com', 'Information');
$mail->addCC('cc@example.com');
$mail->addBCC('bcc@example.com');

$mail->addAttachment('/var/tmp/file.tar.gz');         // Add attachments
$mail->addAttachment('/tmp/image.jpg', 'new.jpg');    // Optional name
$mail->isHTML(true);                                  // Set email format to HTML

$mail->Subject = 'Here is the subject';
$mail->Body    = 'This is the HTML message body <b>in bold!</b>';
$mail->AltBody = 'This is the body in plain text for non-HTML mail clients';

if(!$mail->send()) {
    echo 'Message could not be sent.';
    echo 'Mailer Error: ' . $mail->ErrorInfo;
} else {
    echo 'Message has been sent';
}
```
###3. 准备发送邮件的服务器，这里选择QQ STMP 服务器。
登录QQ邮箱，设置->账户->POP3/IMAP/SMTP/Exchange/CardDAV/CalDAV服务，这一选项下，开通POP3/SMTP服务。需要发送短信生成授权码（0.1元/条），然后记住生成的授权码，后面需要用到。
###4. 编写自己的邮件发送函数
我使用的是thinkphp3.2.3，把phpmailer包下载下来，然后放在到Thinkphp/Library/Vendor/目录下，这时的路径为Thinkphp/Library/Vendor/phpmailer,然后在函数前面引入phpmailer，如下面代码所示，即可正常使用phpmailer。
> ####注意:自动加载文件是引入PHPMailerAutoload.php，不是autoload.php

```php
vendor('phpmailer.PHPMailerAutoload');

/**
 * 发送邮件
 * @param $subject //邮件主题
 * @param $body //邮件内容
 * @param $to_mail //发送到邮箱地址
 * @return bool
 */
function send_mail($subject,$body,$to_mail){
    date_default_timezone_set('PRC');//设置时区
    $mail->CharSet = 'UTF-8'; //设置邮件的字符编码，这很重要，不然中文乱码
    
    $mail = new \PHPMailer();
//  $mail->SMTPDebug = 3;                // 调试模式，有错误的情况下最好打开，便于查出错误
    $mail->isSMTP();                       // 使用 SMTP
    $mail->Host = 'smtp.qq.com';           // 使用 QQ的 SMTP 服务器
    $mail->SMTPAuth = true;                // 使用 SMTP 权鉴，必须
    $mail->Username = '发送邮件地址';        // SMTP username
    $mail->Password = '发送邮件QQ授权码';    // SMTP password,使用qq的话,是授权码,不是邮箱登录密码!!!
    $mail->SMTPSecure = 'ssl';             // Enable TLS encryption, `ssl` also accepted 加密
    $mail->Port = 465;                     // TCP port to connect to 链接端口:465或587

    $mail->setFrom('服务器邮箱地址', '别名');   //服务器邮箱地址，第二个参数是别名，从服务器邮箱发送到哪
    $mail->addAddress($to_mail, '别名');     // 接受邮箱地址,可以添加多个
//  $mail->addReplyTo('info@example.com', 'Information');
//  $mail->addCC('cc@example.com');
//  $mail->addBCC('bcc@example.com');

//  $mail->addAttachment('./admin.php');         // 添加附件，附件地址是服务器上的地址
//  $mail->addAttachment('./1464581020.jpg', 'new.jpg'); // 可以给附件设置别名，附件地址是服务器上的地址
    $mail->isHTML(true);                         // 发送 HTML格式的内容

    $mail->Subject = $subject;//邮件主题
    $mail->Body    = '<p>'.$body.'</p>';//邮件内容
//  $mail->AltBody = 'This is the body in plain text for non-HTML mail clients'; //纯文本邮件内容

    if(!$mail->send()) {
//        return $mail->ErrorInfo;//调试的时候返回错误信息，我这里测试成功了，就不返回了。
        return false;
    } else {
        return true;
    }
}
```
###5. 调用函数，发送邮件
在控制器中直接调用**send_mail($subject,$body,$to_mail)**函数，就可以成功向指定的邮箱发送邮件了。