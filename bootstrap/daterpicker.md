# bootstrap-daterpicker

## 引入`js`和`css`

## `html`
```
<form action="#" method="post" class="form-horizontal">
    <div class="form-group">
        <label class="col-sm-2 control-label">*报名开始时间</label>
        <div class="col-sm-6">
            <input type="text" class="form-control form_datetime" readonly>
        </div>
    </div>
    <div class="form-group">
        <div class="col-sm-8 col-sm-push-4">
            <button type="submit" class="btn btn-primary">确定</button>
        </div>
    </div>
</form>
```

## 配置`js`
```
var today = new Date();
$(".form_datetime").datetimepicker({
    format: "yyyy-mm-dd hh:ii:00",
    startDate:today,
    autoclose:true,
    startView:'month',
    todayBtn:true,
    todayHighlight:true,
    language:'zh-CN'
});
```
