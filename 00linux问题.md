





/etc/sysconfig/network-scripts/ifcfg-enp0s3





service network restart







/etc/sysconfig/network





## 修改IP地址

vi /etc/sysconfig/network-scripts/ifcfg-eth0

## 修改主机名

vi /etc/sysconfig/network

cat /etc/udev/rules.d/70-persistent-net.rules 

## 删除文件

rm -rf /etc/udev/rules.d/

## 

# 安装vim 命令

yum -y install vim*

## 安装rsync

yum -y install rsync

## 远程拷贝命令

rsync -av 192.168.10.102:/home/soft/tar/ /home/soft



rsync -av 192.168.10.102:/home/soft/tar/ /home/soft







find 目录名  -name 文件名

/etc/resolv.conf





find 目录名 -name 文件名 





find / -name xsync