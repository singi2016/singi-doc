# yum按照软件提示被锁

> 提示原文`Another app is currently holding the yum lock; waiting for it to exit...`

> 有其他yum进程在运行，找到并清除

## 强制移除yun进程
`rm -f /var/run/yum.pid`

> `ps kill <pid>`无用