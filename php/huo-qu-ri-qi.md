# 本日本周本月

```
//本日
$today_start_int = strtotime(date('Y-m-d'));
$today_end_int = strtotime("+1 day");
//本周
$week_start_int = strtotime("this week Mon");
$week_end_int = strtotime("this week Sun");
//本月
$month_start_int = strtotime(date('Y-m-01'));
$month_end_int = strtotime(date('Y-m-01')." +1 month");
```