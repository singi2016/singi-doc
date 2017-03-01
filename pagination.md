# pagination bootstrap style

### 1. 配置文件

```php
/*
 * bootstrap 风格的分页样式
 * */

$config['full_tag_open'] = '<ul class="pagination">';
$config['full_tag_close'] = '</ul>';

$config['first_tag_open'] = '<li>';
$config['first_tag_close'] = '</li>';

$config['prev_tag_open'] = '<li>';
$config['prev_tag_close'] = '</li>';

$config['cur_tag_open'] = '<li class="active"> <a href="#"> ';
$config['cur_tag_close'] = '</a></li>';

$config['num_tag_open'] = '<li>';
$config['num_tag_close'] = '</li>';

$config['next_tag_open'] = '<li>';
$config['next_tag_close'] = '</li>';

$config['last_tag_open'] = '<li>';
$config['last_tag_close'] = '</li>';
```

### 2. 后台调用分页

```php
/**
     * 显示所有记录
     */
    function index($p = 1){
         $length = 10;
         $data['title'] = '我的博客';
         $data['blog'] = $this->blog_model->getAll($p,$length);


         $config['base_url'] = site_url('blog/index');
         $config['total_rows'] = $this->db->count_all('blog');
         $config['per_page'] = $length;
         $this->pagination->initialize($config);

         $this->load->view('tpl/header',$data);
         $this->load->view('blog/index',$data);
         $this->load->view('tpl/footer');
    }
```

### 3. 前台显示分页

```php
<?php echo $this->pagination->create_links();?>
```



