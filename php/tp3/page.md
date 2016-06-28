# 分页

###分页方法
```php

protected function page($total_size = 1, $page_size = 0, $current_page = 1, $listRows = 2, $pageParam = 'page', $pageLink = '', $static = FALSE) {
        if ($page_size == 0) {
            $page_size = C("PAGE_LISTROWS");
        }

        if (empty($pageParam)) {
            $pageParam = C("VAR_PAGE");
        }

        $Page = new \Think\Page($total_size, $page_size, $current_page, $listRows, $pageParam, $pageLink, $static);
        $Page->SetPager('Admin', '{prev}&nbsp;{liststart}{list}{listend}&nbsp;{next}', array("listlong" => "9", "prev" => "<", "next" => ">", "list" => "*", "disabledclass" => "active"));
        $Page->SetPager('AdminShop', '{prev}{next}', array("prev" => "<", "next" => ">","disabledclass" => "active"));
        return $Page;
    }
```
###查询数据
```php
$count = M('admin')->field('id,username,trueName,email,tel')->where('status=1')->count();
$page = $this->page($count,5);
$data = M('admin')->field('id,username,trueName,email,tel')->order('id')->where('status=1')->limit($page->firstRow.','.$page->listRows)->select();
foreach($data as &$v){
   $v['password'] = S('pwd');
}
$this->assign('data',$data);
$this->assign('count',$count);
$this->assign('page', $page->show('Admin'));
$this->display('Admin/registerCheck');
```