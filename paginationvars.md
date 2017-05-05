

# 分页-多参数

## 1配置

```php

    function fund($offset=0,$limit=2){
        $pay_where = array(
            'p_from_u_id'=>$this->session->userdata('s_id'),
            'p_to_u_id'=>$this->session->userdata('s_id'),
        );
        $total_count = $this->pay_model->getCount($where);//数据总条数
        // 基本设置
        $config['base_url'] = site_url('finance/fund').'/';
        $config['uri_segment'] = count($this->uri->segments)-1;//倒数第二个是偏移量
        $config['total_rows'] = $total_count;
        $config['per_page'] = $limit;
        $config['num_links'] = 3;
        // 外观设置
        $config['cur_tag_open'] = '<li class="btn btn-white active"> <a href="#"> ';
        $config['cur_tag_close'] = '</a></li>';
        // 初始化分页
        $this->pagination->initialize($config);
        // --- 分页end ---
        
        // 其他逻辑
        
        }
```

## 2前台调用分页条

```php
<?php echo $this->pagination_singi->create_links();?>
```