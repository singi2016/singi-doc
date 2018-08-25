# hjly168

# 采用技术

- `laravel-5.5.*`
- `bootstrap 3.3.6` 
- `encore/laravel-admin "1.5.*"`

# 需求

1. 我的包裹CURD
2. 我的订单(1:n=我的包裹)，CURD
3. 用户设置
4. FAQ

## 数据库

### 我的包裹 packages

字段|类型|备注
-|-|-
uid|int:10|用户id
order_id|int|订单id
express_no|varchar:255|快递单号
goods_name|varchar:255|货物品名
goods_type|tinyint:1|货物类型,1普货2带电3食品4其他
goods_count|int:10|货物数量
note|text|备注
is_reached|tinyint:1|1已到库2未到库

### 我的订单

字段|类型|备注
-|-|-
uid|int:10|用户id
order_time|timestamp|下单时间
order_no|varchar:255|订单编号,自动生成HJLY+YdmHis+rand:6
order_transport_no|varchar:255|转单号
weight|int:10|重量
cost|int:10|费用
is_pay|tinyint:1|1已支付2未支付



