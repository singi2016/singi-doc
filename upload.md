# file upload

### 1. 前台上传图片自动预览

```php
<?php echo form_open_multipart('user/edit',array('class'=>'form-horizontal'));?>
<?php echo form_hidden('id',set_value('id'));?>
<div class="form-group">
    <label for="name" class="col-sm-2 control-label">用户名</label>
    <div class="col-sm-10">
        <input type="text" required class="form-control" name="name" value="<?php echo set_value('name');?>" id="name" placeholder="用户名">
        <span class="text-danger"> <?php echo form_error('name');?> </span>
    </div>
</div>
<div class="form-group">
    <label for="avatar" class="col-sm-2 control-label">头像</label>
    <div class="col-sm-10">
        <button class="btn btn-default">
            <input type="file" required style="position:absolute;left:0;top:0;opacity:0;font-size:40px;" width="100%" height="100%" name="avatar" id="avatar">
            上传头像
        </button>
        <span class="text-danger">
            <?php echo $this->upload->display_errors();?>
        </span>
    </div>
</div>
<div class="form-group" hidden id="show_img">
    <label class="col-sm-2 control-label">图片预览</label>
    <div class="col-sm-10">
        <img src="" id="avatar_img" alt="" width="200px">
    </div>
</div>
<div class="form-group">
    <div class="col-sm-offset-2 col-sm-10">
        <button type="submit" class="btn btn-success col-sm-offset-4 col-sm-4">确定</button>
    </div>
</div>

</form>

<script>
    /*
     * 本地上传文件并预览
     * */
    $("#avatar").change(function(e) {
        console.log(11);
        for (var i = 0; i < e.target.files.length; i++) {
            var file = e.target.files.item(i);
            var freader = new FileReader();
            freader.readAsDataURL(file);
            freader.onloadend = function(e1) {
                var src = e1.target.result;
                $('#show_img').show();
                $("#avatar_img").attr("src",src);
            };
        }
    });
</script>
```

### 2. 后台处理方法

```php
function edit(){
        $data['title'] = '首页';
        $data['sub_title'] = '用户信息编辑';

        $this->form_validation->set_rules('name','name','required',array('required'=>'用户名不能为空'));

        if($this->form_validation->run() == FALSE){
            $this->load->view('tpl/header',$data);
            $this->load->view('user/edit',$data);
            $this->load->view('tpl/footer');
        }else{
            if ( ! $this->upload->do_upload('avatar'))
            {
                $this->load->view('tpl/header',$data);
                $this->load->view('user/edit',$data);
                $this->load->view('tpl/footer');
            }
            else
            {
                //删除旧头像
                $old_avatar = $this->user_model->getField('avatar');
                $old_avatar['avatar'] = '.'.$old_avatar['avatar'];
                if($old_avatar['avatar']) unlink($old_avatar['avatar']);
                //保存新头像
                $avatar_path = strstr($this->upload->data('full_path'),'/public');
                $this->user_model->save($avatar_path);
                $this->load->view('tpl/jump',array('url'=>site_url('user/editShow').'/'.$this->input->post('id')));
            }
        }
    }
```

> 删除图片时，如果是相对路径，路径前面需要加上`.`；例如`/public/avatar/me.jpg` =&gt; `./public/avatar/me.jpg`



