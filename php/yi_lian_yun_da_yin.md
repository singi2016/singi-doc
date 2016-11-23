# 易联云打印

### phpsdk整合

### 微信支付模块notify方法中调用
```php
//易联云打印------ 数据准备 ----- $log['tid']为shopping3_order.id
  $sql_seller = 'SELECT * FROM ' . tablename('wechats') . ' WHERE `weid`=:weid';//商家信息;
  $seller = pdo_fetch($sql_seller,array(':weid'=>$log['weid']));

  $sql_order_info = 'SELECT * FROM ' . tablename('shopping3_order') . ' WHERE `id`=:id';//订单信息
  $order_info = pdo_fetch($sql_order_info,array(':id'=>$log['tid']));

  $sql_order_product_info = 'SELECT * FROM ' . tablename('shopping3_order_goods') . ' WHERE `orderid`=:orderid';//订单信息
  $order_product_info = pdo_fetchall($sql_order_product_info,array(':orderid'=>$order_info['id']));

  $sql_goods = 'SELECT * FROM ' . tablename('shopping3_goods') . ' WHERE `id`=:goodsid';//商品信息
  foreach($order_product_info as $k=>$v){
      //根据goodsid查询goods信息
      $goods = pdo_fetch($sql_goods,array(':goodsid'=>$v['goodsid']));
      $order_product_info[$k]['goods_info'] = $goods;
  }
  //----------准备打印
  $elind = new Yprint();
  $content = '<center>'.$seller['name'].$order_product_info['goodsid'].'</center>';//抬头数据
  $content .= '<table>';
  $content .= '<tr><td>名称</td><td>单价x数量</td><td>金额</td></tr>';//打印数据
  foreach($order_product_info as $v){
      $content .= '<tr><td>'.$v['goods_info']['title'].'</td><td>'.$v['goods_info']['marketprice'].'x'.$v['total'].'</td><td>'.$v['goods_info']['marketprice']*$v['total'].'</td></tr>';//商品数据
  }
  $content .= '@@2<tr><td>总价:</td><td></td><td>'.$order_info['totalprice'].'</td></tr>';//总价
  $content .= '</table>';
  $content .= '<right>'.date('Y-m-d H:i:s').'</right>';//时间

  $elind->action_print(6052,'4004512478',$content,'91ffdc1fb247310dae54f3c3d6f9b02531442f92','xi7k8er7bhxy');
  //----------打印结束
```