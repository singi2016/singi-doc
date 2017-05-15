# vmware中按照centos7连不上网

> 有线网卡没有激活

## 1. 获得管理员权限，编辑`ifcfg-enoxx`文件,`xx`这里的数字是随机的,我这里是`32`。
```
su
cd /etc/sysconfig/network-scripts/
ls 
vi ifcfg-eno32
```
编辑`ONBOOT="yes"`然后`:wq`保存退出
## 2. 重启有限网卡
`service network restart`

## 3. 如果还不能正常上网。那么请检查下面事项
1. 打开虚拟机存储的目录，用记事本打开`.vmx`配置文件，检查`ethernet0.virtualDev = "e1000"`是否存在，如果没有，就加进去保存
2. 虚拟机网卡模式设置成`NAT`连接