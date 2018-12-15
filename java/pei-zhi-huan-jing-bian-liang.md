# 配置环境变量

> 下载好`sdk`，并安装完成
> 以下操作在win10上进行

## 假设路径

```
F:\soft\javasdk  //sdk
F:\soft\javajre  //jre
```

## 打开环境变量

按快捷键`win+PauseBreak` => 高级系统设置 => 环境变量

## 配置环境变量

1. 在系统变量 => 新建 `JAVA_HOME`:`F:\soft\javasdk`
2. 在系统变量 => 编辑 `Path`，添加`F:\soft\javasdk`和`F:\soft\javasdk\jre\bin`
3. 在系统变量 => 新建 `CLASSPATH`,添加`.`,`F:\soft\javasdk\lib`,`F:\soft\javasdk\lib\dt.jar`和`F:\soft\javasdk\lib\tools.jar`

