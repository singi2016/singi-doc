# [七牛云SDK](http://developer.qiniu.com/code/v7/sdk/php.html)
##thinkphp3.2.3集成七牛云SDK
###1. 安装七牛云SDK，然后引入（请参考[thinkphp3.2.3引入第三方包](./tpkuang_jia_yin_ru_di_san_fang_bao.md)）
###2. 配置七牛云参数
```php
//七牛云配置
    'accessKey' => 'XXX',//秘钥
    'secrectKey' => 'XXX',//秘钥
    'domain' => 'o7atl50ri.bkt.clouddn.com',//域名，这里是七牛云提供的测试域名
    'bucket' => 'XX',//'<空间名称>',
```
###3. 改写七牛云SDK
```php
  class FileController extends Controller
{ 
    /**
     * 获得七牛云权鉴
     */
    public function getAuthQiniu()
    {
        $auth = new \Qiniu\Auth(C('accessKey'), C('secrectKey'));
        return $auth;
    }

    /**
     * 获取单个文件信息
     */
    public function getFile($key)
    {
        //初始化Auth状态
        $auth = $this->getAuthQiniu();

        //初始化BucketManager
        $bucketMgr = new \Qiniu\Storage\BucketManager($auth);

        //你要测试的空间， 并且这个key在你空间中存在
        $bucket = C('bucket');

        //获取文件的状态信息
        list($ret, $err) = $bucketMgr->stat($bucket, $key);
        if ($err !== null) {
            return $err;
        } else {
            return $ret;
        }
    }

    /**
     * 获取文件列表,默认为10个,没有过滤条件
     */
    public function listFiles()
    {
        $auth = $this->getAuthQiniu();
        $bucketMgr = new \Qiniu\Storage\BucketManager($auth);

        // 要列取的空间名称
        $bucket = C('bucket');

        // 要列取文件的公共前缀
        $prefix = '';

        $marker = '';
        $limit = 10;

        list($iterms, $marker, $err) = $bucketMgr->listFiles($bucket, $prefix, $marker, $limit);
        if ($err !== null) {
            return $err;
        } else {
            return $iterms;
        }
    }

    /**
     * 删除文件
     */
    public function delete($key)
    {
        //初始化Auth状态
        $auth = $this->getAuthQiniu();

        //初始化BucketManager
        $bucketMgr = new \Qiniu\Storage\BucketManager($auth);

        //你要测试的空间， 并且这个key在你空间中存在
        $bucket = C('bucket');

        //删除$bucket 中的文件 $key
        $err = $bucketMgr->delete($bucket, $key);
        if ($err !== null) {
            return $err;
        }
    }

    /**
     * 修改文件MIME类型
     *
     */
    public function putMime($key, $mime)
    {
        // 构建鉴权对象
        $auth = $this->getAuthQiniu();

        // 空间
        $bucket = C('bucket');

        $bucketMgr = new \Qiniu\Storage\BucketManager($auth);

        $err = $bucketMgr->changeMime($bucket, $key, $mime);

        if ($err !== null) {
            return $err;
        }
    }

    /**
     * 修改文件名
     *
     */
    public function rename($key, $newKey)
    {
        // 构建鉴权对象
        $auth = $this->getAuthQiniu();

        // 指定空间
        $bucket = C('bucket');

        $bucketMgr = new \Qiniu\Storage\BucketManager($auth);

        $err = $bucketMgr->rename($bucket, $key, $newKey);

        if ($err !== null) {
            return $err;
        }
    }

    /**
     * 复制文件
     */
    public function copy($bucket, $key, $bucket2, $key2)
    {
        //初始化Auth状态
        $auth = $this->getAuthQiniu();

        //初始化BucketManager
        $bucketMgr = new \Qiniu\Storage\BucketManager($auth);

        $err = $bucketMgr->copy($bucket, $key, $bucket2, $key2);
        if ($err !== null) {
            return $err;
        }
    }

    /**
     * 移动文件
     */
    public function move($bucket, $key, $bucket2, $key2)
    {
        //初始化Auth状态
        $auth = $this->getAuthQiniu();

        //初始化BucketManager
        $bucketMgr = new \Qiniu\Storage\BucketManager($auth);


        $err = $bucketMgr->move($bucket, $key, $bucket2, $key2);

        if ($err !== null) {
            return $err;
        }
    }

    /**
     * 上传,客户端直传七牛云
     */
    public function uploadQiniu($filePath, $key)
    {

        // 构建鉴权对象
        $auth = $this->getAuthQiniu();

        // 要上传的空间
        $bucket = C('bucket');

        // 生成上传 Token
        $token = $auth->uploadToken($bucket);

        // 初始化 UploadManager 对象并进行文件的上传
        $uploadMgr = new \Qiniu\Storage\UploadManager();

        // 调用 UploadManager 的 putFile 方法进行文件的上传
        list($ret, $err) = $uploadMgr->putFile($token, $key, $filePath);
        if ($err !== null) {
            return $err;
        } else {
            return $ret;
        }
    }

    /**
     * 下载文件URL
     * $attname=false 如果希望浏览器的动作是下载而不是打开(显示图片).默认false表示打开,true表示直接下载.
     *
     * imageView2=0 限定缩略图的长边最多为<LongEdge>，短边最多为<ShortEdge>，进行等比缩放，不裁剪.从应用场景来说，模式0适合移动设备上做缩略图
     * imageView2=1 限定缩略图的宽最少为<Width>，高最少为<Height>，进行等比缩放，居中裁剪
     * imageView2=2 限定缩略图的宽最多为<Width>，高最多为<Height>，进行等比缩放，不裁剪.模式2适合PC上做缩略图
     * imageView2=3 限定缩略图的宽最少为<Width>，高最少为<Height>，进行等比缩放，不裁剪.你可以理解为模式1是模式3的结果再做居中裁剪得到的。
     * imageView2=4 限定缩略图的长边最少为<LongEdge>，短边最少为<ShortEdge>，进行等比缩放，不裁剪。这个模式很适合在手持设备做图片的全屏查看（把这里的长边短边分别设为手机屏幕的分辨率即可），生成的图片尺寸刚好充满整个屏幕（某一个边可能会超出屏幕）。
     * imageView2=5 限定缩略图的长边最少为<LongEdge>，短边最少为<ShortEdge>，进行等比缩放，居中裁剪。同上模式4，但超出限定的矩形部分会被裁剪。
     *
     * $format      新图的输出格式.取值范围：jpg，gif，png，webp等，默认为原图格式。
     * $interlace   是否支持渐进显示 取值范围：1 支持渐进显示，0不支持渐进显示(默认为0)。 适用目标格式：jpg 效果：网速慢时，图片显示由模糊到清晰。
     * $q           新图的图片质量 取值范围是[1, 100]，默认75。 七牛会根据原图质量算出一个修正值，取修正值和指定值中的小值。 注意： ● 如果图片的质量值本身大于90，会根据指定值进行处理，此时修正值会失效。 ● 指定值后面可以增加 !，表示强制使用指定值，如100!。 ● 支持图片类型：jpg。
     * $ignore_error 可选 取值：1 ● 未设置此参数时，正常返回处理结果。 ● 设置了此参数时，若图像处理的结果失败，则返回原图。 ● 设置了此参数时，若图像处理的结果成功，则正常返回处理结果。
     *
     * @param $key
     * @param bool $attname
     * @param int $imageView2
     * @param int $w
     * @param $h
     * @param $format
     * @param int $interlace
     * @param int $q
     * @param int $ignore_error
     * @return string
     */
    public function getDownloadUrl($key,$attname=false,$imageView2,$w,$h,$format,$interlace=1,$q=75,$ignore_error=1)
    {
        // 构建鉴权对象
        $auth = $this->getAuthQiniu();

        //baseUrl构造成私有空间的域名/key的形式
        $domain = C('domain');
        //拼接URL(还未签名)$domain和$key为必须
        $baseUrl = 'http://' . $domain . '/'.$key.'?';
        //调用了imageView2接口,才拼接imageView2的处理参数
        if($imageView2){
            $baseUrl .= 'imageView2/'.$imageView2;
            if($w){ $baseUrl .= '/w/'.$w; }
            if($h){ $baseUrl .= '/h/'.$h; }
            if($format){ $baseUrl .= '/format/'.$format; }
            if($interlace){ $baseUrl .= '/interlace/'.$interlace; }
            if($q){ $baseUrl .= '/q/'.$q; }
            if($ignore_error){ $baseUrl .= '/ignore-error/'.$ignore_error; }
        }

        if($attname){ $baseUrl = $baseUrl.'&attname='.$key; }

        $authUrl = $auth->privateDownloadUrl($baseUrl);//下载链接有效期3600秒
        return $authUrl;
    }
}
```