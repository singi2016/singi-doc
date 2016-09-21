# 百度编辑器 UEditor

> ### 标签：`thinkphp3.2.3`,`ueditor`,`qiniuyun`
> #### 应用场景：
> 使用UEditor上传图片，文件等到七牛云服务器，
> **结果：编辑器图片链接为七牛云链接**

### sdk资源准备
1. 七牛云 phpSDK 重命名为qiniuyun
2. UEditor [1.4.3.3 php] utf-8版 重命名为ueditor

### 集成到thinkphp3.2.3
因为`UEditor`已经帮我们写好了php代码，但后缀是.php的，这意味着在thinkphp中，这些文件属于外来的。那么这里就按照外来的文件对待。
直接将`UEditor`sdk和七牛云sdk一起复制到thinkphp3.2.3中的Public目录下面。
> 想放在别的目录也可以，但是这里不适合再用thinkphp的方法，请将思维转回到传统php来。所以，我才选择放在Pulick目录下面

目录结构如下图:
* Public
  * qiniuyun
  * ueditor
  
### 改造UEditor
> 这时的UEditor处理图片的方法是将图片上传到网址根目录下面。具体配置在`ueditor/php/config.json`文件中。

下面将以上传图片为例：
1. 修改`ueditor/php/config.json`配置如下：
```php
"imageUrlPrefix": "http://o7atl50ri.bkt.clouddn.com/", /* 图片访问路径前缀，七牛云域名 */
"imagePathFormat": "{time}{rand:6}", /* 上传保存路径,可以自定义保存路径和文件名格式，七牛云图片名称 */
```
> 这里的配置会返回七牛云链接`http://o7atl50ri.bkt.clouddn.com/文件名`，并插入到`UEditor`内容中去。

2. 修改`ueditor/php/Uploader.class.php`如下:

  在`Uploader`类开始处引入七牛云`SDK`
  ```php
  require_once 'qiniuyun/autoload.php';
  ```
  增加七牛云上传方法`uploadQiniu`:
```php
/**
     * 上传七牛云
     * @param $key 七牛云文件名
     * @param $filePath $_FILE[]['tmp_name']
     * @return mixed
     * @throws Exception
     */
    private function uploadQiniu($key, $filePath){
        $auth = new \Qiniu\Auth('RYyqdPimpYxIUJl4KVcJ6APplN90d5CEpU1kZ-a6','mOQ5hXi3OVLMA4uy346lYq3cDvSCdKNeGLDwv8UE');
        // 要上传的空间
        $bucket = 'gymfile'; 

        // 生成上传 Token
        $token = $auth->uploadToken($bucket);

        // 初始化 UploadManager 对象并进行文件的上传
        $uploadMgr = new \Qiniu\Storage\UploadManager();

        // 调用 UploadManager 的 putFile 方法进行文件的上传
        list($ret, $err) = $uploadMgr->putFile($token, $key, $filePath);

        if ($err !== null) {
            return false;
        } else {
            return true;
        }
    }
```
  修改`Uploader`类中文件上传方法,最后几行如下:
  
  原来方法是上传到网址根目录，这里修改成直接上传到七牛云。
  ```php
        //移动文件,上传到七牛云
        $res = $this->uploadQiniu($this->fullName, $file["tmp_name"]); //此处修改
        if (!($res)) { //移动失败 此处修改
            $this->stateInfo = $this->getStateInfo("ERROR_FILE_MOVE");
        } else { //移动成功
            $this->stateInfo = $this->stateMap[0];
        }
  ```

> 到这里改造结束。如果还想提取编辑器内容中的图片链接，请往下看

### 提取编辑器中所有图片链接

```php
  $content = I('post.editorValue');
  preg_match_all('<img.*?src="(.*?)">',ltgt($content),$match);
  $files = $match[1];
```
> `$match[1]`中即为编辑器中所有图片链接

提取`$match[1]`中，所有七牛云文件名:
```php
      $urlKey = array();
      foreach($files as $k=>$v){
         $urlKey[$k] = substr(strrchr($v, '/'),1);
      }
```
> `$urlKey`和`$match[1]`中的数据一一对应，文件名:文件地址

### UEditor常用配置
```php
,charset:"utf-8"  //针对getAllHtml方法，会在对应的head标签中增加该编码设置。
,initialFrameHeight:500  //初始化编辑器高度,默认320
,textarea:'editorValue' // 提交表单时，服务器获取编辑器提交内容的所用的参数，多实例时可以给容器name属性，会将name给定的值最为每个实例的键值，不用每次实例化的时候都设置这个值
,initialContent:'欢迎使用ueditor!'    //初始化编辑器的内容,也可以通过textarea/script给值，看官网例子
```

