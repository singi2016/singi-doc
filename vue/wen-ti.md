# 问题

1. vue cli 3.x.x 热重载失败

```

```

> 解决方法

在`package.json`中添加下列参数

```
"resolutions": {
    "webpack-dev-server": "3.1.10"
  }
```