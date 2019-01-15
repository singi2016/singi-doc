# vmware中按照centos7连不上网

> 有线网卡没有激活

## 获得管理员权限，编辑`ifcfg-enoxx`文件,`xx`这里的数字是随机的,我这里是`32`。
```
su
cd /etc/sysconfig/network-scripts/
ls 
vi ifcfg-eno32
```
编辑`ONBOOT="yes"`然后`:wq`保存退出
## 重启有限网卡
`service network restart`

## 如果还不能正常上网。那么请检查下面事项
1. 打开虚拟机存储的目录，用记事本打开`.vmx`配置文件，检查`ethernet0.virtualDev = "e1000"`是否存在，如果没有，就加进去保存
2. 虚拟机网卡模式设置成`NAT`连接

## 本地与虚拟机中主机无法互相ping,但可以ping通外网

1. 查看本地ip和虚拟机主机ip是否在同一网段,本地`ipconfig /all`,虚拟机 `ip addr`
2. 如果不一致,打开虚拟机 `编辑/虚拟网络编辑器` 设置`VMnet8`为NAT模式,`ip`段为本地`ip`段相同