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
                sidePagination : 'server',//服务器端分页
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

---

##客户端分页

```js
const table = $('#table'),
                remove = $('#remove');

        //加载页面
        $('document').ready(function () {
            //加载文章列表
            table.bootstrapTable({
                pagination: true,//显示分页
                striped: true, //设置为 true 会有隔行变色效果
                responseHandler: function (res) { /*加载服务器数据之前的处理程序，可以用来格式化数据。 参数：res为从服务器请求到的数据。*/
                    console.log(res);
                    res.data.forEach(function (vo) {
                        const datetime = new Date(vo.createdAt).format('yyyy-MM-dd HH:mm:ss');
                        vo.createdAt = datetime;
                        vo.action = `<a href="{:U('Article/editArticle')}?id=${vo.objectId}">编辑</a> | <a href="#" onclick="del('${vo.objectId}')">删除</a> `
                    });
                    return res;
                },
                clickToSelect:true,//点击行自动选择
                search: true,//显示搜索框
                showHeader: true,//显示头
                showColumns: true,//显示行
                showRefresh: true,//显示刷新
                showToggle: true,//显示切换
                showPaginationSwitch: true,//显示选择每页显示多少行
                columns: [{
                    field: 'state',//字段名
                    checkbox: true,//多选框
                    halign: 'center',//首行居中
                    align: 'center'//内容居中
                }, {
                    field: 'title',
                    title: '标题',
                    sortable: true,
                    halign: 'center'
                }, {
                    field: 'createdAt',
                    title: '发布日期',
                    sortable: true,
                    halign: 'center',
                    align: 'center'
                }, {
                    field: 'action',
                    title: '操作',
                    halign: 'center',
                    align: 'center'
                }],
//                sidePagination : 'server',
                url: 'http://happyfit-medium-service.leanapp.cn/api/article/'//获取服务器数据
            });
        });

        //删除文章
        function del(id) {
            if (id) {
                layer.confirm('确定要删除吗?', function (index) {
                    //删除文章
                    $.ajax({
                        url: 'http://happyfit-medium-service.leanapp.cn/api/article/',
                        data: {articleId: id},
                        type: 'delete',
                        dataType: 'json',
                        beforeSend: function () {
                            $('#show_load').show();
                        },
                        success: function (data) {
                            console.log(data);
                            if (data.code != 200) return false;

                            //刷新表格
                            table.bootstrapTable('remove',{//删除表格中的这一行
                                field: 'objectId',//需要删除的字段
                                values: [id]//需要删除的字段值，是一个数组
                            })
//                            $('#article').bootstrapTable('refresh', {url: 'http://happyfit-medium-service.leanapp.cn/api/article/'});
                            layer.close(index);
                        },
                        complete: function () {
                            $('#show_load').hide();
                        }
                    });
                })
            } else {
                layer.alert('没有选择数据!');
                //刷新表格
                $('#article').bootstrapTable('refresh', {url: 'http://happyfit-medium-service.leanapp.cn/api/article/'});
            }
        }
        //选择多选框时，显示‘删除所选’按钮，没有多选框被选中时，‘删除所选’按钮不可点击
        table.on('check.bs.table uncheck.bs.table ' +
                'check-all.bs.table uncheck-all.bs.table', function () {
            remove.prop('disabled', !table.bootstrapTable('getSelections').length);
        });

        //删除所选的行
        remove.click(function () {
            const data = table.bootstrapTable('getSelections');
            console.log(data);
            const objectIds = $.map(data, function (v) {//将所有行数据中的objectId重新组成一个数组
                return v.objectId;
            })
            //删除数据库数据
            data.forEach(function (v) {
                $.ajax({
                    url: 'http://happyfit-medium-service.leanapp.cn/api/article/',
                    data: {articleId: v.objectId},
                    type: 'delete',
                    dataType: 'json',
                    beforeSend: function () {
                        $('#show_load').show();
                    },
                    success: function (data) {
                        console.log(data);
                        if (data.code != 200) {
                            layer.alert('服务器错误,将重新载入页面!');
                            location.reload();
                        } else {
                            //删除表格数据
                            table.bootstrapTable('remove', {
                                field: 'objectId',
                                values: objectIds
                            });
                        }
                    },
                    complete: function () {
                        $('#show_load').hide();
                    }
                });
            });
        });
```




