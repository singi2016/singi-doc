# 百度编辑器 UEditor

> ### 标签：`thinkphp3.2.3`,`ueditor`,`qiniuyun`
> #### 应用场景：
> 使用UEditor上传图片，文件等到七牛云服务器，
> **结果：编辑器图片链接为七牛云链接**

### sdk资源准备
1. 七牛云 phpSDK 重命名为qiniuyun
2. UEditor [1.4.3.3 php] utf-8版 重命名为ueditor

### 集成到thinkphp3.2.3
因为`UEditor`已经帮我们写好了php代码，所以，后缀是.php的，这意味着在thinkphp中，这些文件属于外来的。那么这里就按照外来的文件对待。
直接将`UEditor`sdk和七牛云sdk一起复制到thinkphp3.2.3中的Public目录下面。
> 想放在别的目录也可以，但是这里不适合再用thinkphp的方法，请将思维转回到传统php来。所以，我才选择放在Pulick目录下面

目录结构如下图:
* Public
  * qiniuyun
  * ueditor
  
### 改造UEditor
> 这时的UEditor处理图片的方法是将图片上传到网址根目录下面。具体配置在`ueditor/php/config.json`文件中。



