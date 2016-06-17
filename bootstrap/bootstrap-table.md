#[Bootstrap Table](http://issues.wenzhixin.net.cn/bootstrap-table/index.html)
>[Github](https://github.com/wenzhixin/bootstrap-table-examples/blob/master/welcome.html) [中文文档](http://bootstrap-table.wenzhixin.net.cn/zh-cn/documentation/)

##一个简单的例子demo（基于thinkphp3.2.3）

###html
```html
<link href="path/css/bootstrap-table.min.css" rel="stylesheet">
<script src="path/js/bootstrap-table.min.js"></script>
<script src="path/js/bootstrap-table-zh-CN.min.js"></script>

<table id="table"></table>
```
###js
```javascript
$('#table').bootstrapTable({
                url:"{:U('course/selectCourses')}",//请求数据url
                queryParams: function () {
                    return {
                        uid:uid,//自定义的数据,会跟在url后面传到服务器
                    };
                },
                pagination: true,//分页
                pageList: [5, 10, 20, 50],//分页步进值
                search: true,//显示搜索框
                //表格的列
                columns: [
                    {
                        field: 'id',//域值
                        title: 'id',//标题
                        visible: false//false表示不显示
                    },
                    {
                        field: 'name',
                        title: '课程名',
                        align: 'center',//水平居中对齐
                        width: '',//列宽
                        valign: 'middle',//垂直居中对齐
                        sortable: true//启用排序
                    }, {
                        field: 'courseMinutes',
                        title: '课时长/分钟',
                        align: 'center',
                        width: '',
                        valign: 'top',
                        sortable: true
                    }],
                //单击某行时，执行函数，row为当前行的数据
                onClickRow: function (row) {
                    console.log(row);
                },
            });
```
###php(服务器端)
```php
         $uid = I('get.uid');
         $per_page = I('get.per_page');
         $page = I('get.page');
         $offset = ($page-1)*$per_page;
         $today = date('Y-m-d H:i:s',time());//当前时间
         $map['courseDate'] = array('gt',$today);//获取大于当前时间的数据
         $map['uid'] = $uid;
         $res = M('course')->field('id,name,courseMinutes')->where($map)->limit($offset,$per_page)->select();
         $this->ajaxReturn($res, 'json');
```

>###服务器返回的json值需要跟表格定义的列的域值一致。
