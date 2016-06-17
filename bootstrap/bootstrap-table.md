#[Bootstrap Table](http://issues.wenzhixin.net.cn/bootstrap-table/index.html)
>[Github](https://github.com/wenzhixin/bootstrap-table-examples/blob/master/welcome.html) [中文文档](http://bootstrap-table.wenzhixin.net.cn/zh-cn/documentation/)

##一个简单的例子demo

###html
```html
<table id="table"></table>
```
###js
```javascript
$('#table').bootstrapTable({
                url:"{:U('course/selectCourses')}",
                queryParams: function () {
                    return {
                        uid:uid,
                    };
                },
                pagination: true,
//                pageNumber:1,
//                pageSize:5,
                pageList: [5, 10, 20, 50],//分页步进值
                search: true,
//                sidePagination:"server",
//                dataType: "json",//期待返回数据类型
//                method: "get",//请求方式
//                searchAlign: "left",//查询框对齐方式
//                queryParamsType: "limit",//查询参数组织方式
//                showRefresh: true,//刷新按钮
//                showColumns: true,//列选择按钮
//                showPaginationSwitch: true,//
//                showHeader:'true',
//                showFooter:'true',
//                locale: "zh-CN",//中文支持,

                columns: [
                    {
                        field: 'id',
                        title: 'id',
                        visible: false
                    },
                    {
                        field: 'name',
                        title: '课程名',
                        align: 'center',
                        width: '',
                        valign: 'middle',
                        sortable: true
                    }, {
                        field: 'courseMinutes',
                        title: '课时长/分钟',
                        align: 'center',
                        width: '',
                        valign: 'top',
                        sortable: true
                    }, {
                        field: 'people',
                        title: '课程总人数/人',
                        align: 'center',
                        width: '',
                        valign: 'middle',
                        sortable: true
                    }, {
                        field: 'coach',
                        title: '教练',
                        align: 'center',
                        width: '',
                        valign: 'middle',
                        sortable: true
                    }, {
                        field: 'cost',
                        title: '教练费用/元',
                        align: 'center',
                        width: '',
                        valign: 'middle',
                        sortable: true
                    }],
                //单击某行时，执行函数，row为当前行的数据
                onClickRow: function (row) {
                    console.log(row);
                },
            });
```
