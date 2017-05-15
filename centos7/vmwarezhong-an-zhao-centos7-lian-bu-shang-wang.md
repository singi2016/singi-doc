# vmware中按照centos7连不上网

> 有线网卡没有激活

## 1. 获得管理员权限，编辑`ifcfg-enoxx`文件,`xx`这里的数字是随机的,我这里是`32`。
```
su
cd /etc/sysconfig/network-scripts/
ls 
vi ifcfg-eno32
```
编辑
`ONBOOT="yes"`
