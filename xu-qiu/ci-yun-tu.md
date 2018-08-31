# 词云图 tag-cloud

> [antV G2](https://antv.alipay.com/zh-cn/g2/3.x/demo/other/word-cloud-mask.html)

# 代码

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width,height=device-height">
    <title>带图片遮罩的词云</title>
    <style>::-webkit-scrollbar{display:none;}html,body{overflow:hidden;height:100%;margin:0;}</style>
</head>
<body>
<div id="mountNode"></div>
<script>/*Fixing iframe window.innerHeight 0 issue in Safari*/document.body.clientHeight;</script>
<script src="https://gw.alipayobjects.com/os/antv/pkg/_antv.g2-3.2.7/dist/g2.min.js"></script>
<script src="https://gw.alipayobjects.com/os/antv/pkg/_antv.data-set-0.8.9/dist/data-set.min.js"></script>
<script>
function getTextAttrs(cfg) {
  return _.assign({}, {
    fillOpacity: cfg.opacity,
    fontSize: cfg.origin._origin.size,
    rotate: cfg.origin._origin.rotate,
    text: cfg.origin._origin.text,
    textAlign: 'center',
    fontFamily: cfg.origin._origin.font,
    fill: cfg.color,
    textBaseline: 'Alphabetic'
  }, cfg.style);
}
// 给point注册一个词云的shape
G2.Shape.registerShape('point', 'cloud', {
  drawShape: function drawShape(cfg, container) {
    var attrs = getTextAttrs(cfg);
    return container.addShape('text', {
      attrs: _.assign(attrs, {
        x: cfg.x,
        y: cfg.y
      })
    });
  }
});
function createTagCloud(data,img){
var dv = new DataSet.View().source(data);
  var range = dv.range('value');
  var min = range[0];
  var max = range[1];
  var imageMask = new Image();
  imageMask.crossOrigin = '';
  imageMask.src = img;
  imageMask.onload = function() {
    dv.transform({
      type: 'tag-cloud',
      fields: ['name', 'value'],
      imageMask: imageMask,
      font: 'Verdana',
      size: [window.innerWidth, window.innerHeight], // 宽高设置最好根据 imageMask 做调整
      padding: 0,
      timeInterval: 5000, // max execute time
      rotate: function rotate() {
        var random = ~~(Math.random() * 4) % 4;
        if (random == 2) {
          random = 0;
        }
        return random * 90; // 0, 90, 270
      },
      fontSize: function fontSize(d) {
        return (d.value - min) / (max - min) * (32 - 8) + 8;
      }
    });
    var chart = new G2.Chart({
      container: 'mountNode',
      width: window.innerWidth, // 宽高设置最好根据 imageMask 做调整
      height: window.innerHeight,
      padding: 0
    });
    chart.source(dv, {
      x: {
        nice: false
      },
      y: {
        nice: false
      }
    });
    chart.legend(false);
    chart.axis(false);
    chart.tooltip({
      showTitle: false
    });
    chart.coord().reflect();
    chart.point().position('x*y').color('text').shape('cloud');
    chart.render();
  };
}
var data = [{"value":9,"name":"AntV"},{"value":19,"name":"AntV"},{"value":59,"name":"AntV"},{"value":689,"name":"AntV"}];
var img = 'n.jpg';
createTagCloud(data,img);
</script>
</body>
</html>

```



