# 无限分级

### 使用
```php
            $rules = M('rule')->order('sortid')->select();
            $list = list_to_tree($rules, 'id', 'pid');
            $this->assign('rules', $list);
```
