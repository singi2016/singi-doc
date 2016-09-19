# summernote

###内容中的图片上传
> 默认是base64格式，现在需要上传七牛云，并改成七牛云链接格式

###前端
```js
$('#summernote').summernote({
                height: 300,                 // set editor height
                minHeight: null,             // set minimum height of editor
                maxHeight: null,             // set maximum height of editor
                focus: true,
                lang:'zh-CN',
                callbacks: {
                    onImageUpload: function(files) {
                        var data = new FormData(); //使用FormData对象上传
                        data.append('file', files[0]);
                        $.ajax({
                            url: '/Home/file/uploadQiNiu',
                            method: 'POST',
                            data: data,
                            processData: false,
                            contentType: false,
                            success: function(url) {
                                $('#summernote').summernote('insertImage', url);
                            }
                        });
                    }
                }
            });
```

###后端
```php
    /**
     * 上传七牛云
     */
    function uploadQiNiu(){
        if($_FILES['file']['tmp_name']){
            //上传七牛云
            $urlKey = time().$_FILES['fileup']['name'];
            $url = uploadQiniu($urlKey,$_FILES['fileup']['tmp_name']);
            $this->ajaxReturn(array('urlKey'=>$urlKey,'url'=>$url),'json');
        }
    }
```
