---
title: Aix run on qemu
tags: Aix
---



---

---

  qemu运行虚拟IBM系统，多数教程都有问题，qemu版本8.0.2。安装依赖：

```
yum -y install gcc gcc-c++ automake libtool zlib-devel glib2-devel bzip2-devel libuuid-devel spice-protocol spice-server-devel usbredir-devel libaio-devel wget python3 bzip2 i gmake make
```

安装ninja及依赖：

- wget https://github.com/skvadrik/re2c/releases/download/3.0/re2c-3.0.tar.xz
- cd re2c-3.0/ & autoreconf -i -W all
- ./configure && make && make install
- mkdir .build && cd .build && ../configure && make && make install
- git clone https://ghproxy.com/https://github.com/ninja-build/ninja.git && cd ninja
- /configure.py --bootstrap

qemu官方下载解压后即可源码安装。请根据官方文档自行操作。

为虚拟机添加网络：本地执行

1. ip tuntap add dev tap0 mode tap echo 1 > /proc/sys/net/ipv4/conf/tap0/proxy_arp
2.  cat /proc/sys/net/ipv4/conf/tap0/proxy_arp
3.  echo 1 > /proc/sys/net/ipv4/conf/ens33/proxy_arp
4.  ip addr add 192.168.100.4 dev tap0
5.   ip link set up tap0
6.  ip link set up dev tap0 promisc on
7.   ip route add 192.168.100.151 dev tap0
8.   arp -Ds 192.168.100.151 ens33 pub
9. arp -Ds 192.168.100.151 ens33 pub

可以用如下命令启动虚拟机。

```
qemu-system-ppc64 -smp 2 -m 2G -serial mon:stdio -drive file=hdisk0.qcow2,if=none,id=drive-virtio-disk0 -device virtio-scsi-pci,id=scsi -device scsi-hd,drive=drive-virtio-disk0 -drive format=raw,media=cdrom,readonly=on,file=aix_7200-04-02-2027_1of2_072020.iso -drive format=raw,media=cdrom,readonly=on,file=aix_7200-04-02-2027_2of2_072020.iso -prom-env "boot-command=boot cdrom:" -nographic

```

启动时间很漫长，请耐心等待。





---

