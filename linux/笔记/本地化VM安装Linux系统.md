###  一、安装虚拟机

### 二、配置网络

 1. 使用vi编辑`/etc/sysconfig/network-script/ifcfg-ens33`文件

    ```bash
    vi /etc/sysconfig/network-script/ifcfg-ens33
    ```

2. 这里我使用静态IP，修改 `BOOTPROTO` 为 static，`ONBOOT `为 on，并添加网络信息

   ```bash
   BOOTPROTO=static
   ONBOOT=on
   
   # 新增行，网络信息
   IPADDR=192.168.44.20
   NETMASK=255.255.255.0
   GATEWAY=192.168.44.1
   DNS1=8.8.8.8
   DNS2=114.114.114.114
   ```

3. [对vm虚拟机网络做一些配置](!另外一篇)

4. 重启网络

   ```bash
   systemctl restart network
   ```

5. 查看网卡信息

   ```
   ip addr
   ```

   如下信息，ens33已有静态IP，则网卡配置成功

   ```bash
   1: lo: <LOOPBACK,UP,LOWER_UP> mtu 65536 qdisc noqueue state UNKNOWN group default qlen 1000
       link/loopback 00:00:00:00:00:00 brd 00:00:00:00:00:00
       inet 127.0.0.1/8 scope host lo
          valid_lft forever preferred_lft forever
       inet6 ::1/128 scope host 
          valid_lft forever preferred_lft forever
   2: ens33: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc pfifo_fast state UP group default qlen 1000
       link/ether 00:0c:29:78:4c:30 brd ff:ff:ff:ff:ff:ff
       inet 192.168.44.20/24 brd 192.168.44.255 scope global noprefixroute ens33
          valid_lft forever preferred_lft forever
       inet6 fe80::b9b6:f6a1:e54a:1fb4/64 scope link noprefixroute 
          valid_lft forever preferred_lft forever
   ```

6. 测试是否能与内外网通信（这里我ping 我的笔记本以及百度）

   ```
   ping 192.168.44.2
   ```

   ```
   # 可以与局域网通信
   PING 192.168.44.2 (192.168.44.2) 56(84) bytes of data.
   64 bytes from 192.168.44.2: icmp_seq=1 ttl=128 time=0.724 ms
   64 bytes from 192.168.44.2: icmp_seq=2 ttl=128 time=0.473 ms
   64 bytes from 192.168.44.2: icmp_seq=3 ttl=128 time=0.358 ms
   ```

   ```bash
   ping baidu.com
   ```

   ```
   # 可以与外网通信
   PING baidu.com (39.156.69.79) 56(84) bytes of data.
   64 bytes from 39.156.69.79 (39.156.69.79): icmp_seq=1 ttl=128 time=47.0 ms
   64 bytes from 39.156.69.79 (39.156.69.79): icmp_seq=2 ttl=128 time=45.7 ms
   64 bytes from 39.156.69.79 (39.156.69.79): icmp_seq=3 ttl=128 time=45.5 ms
   ```

### 三、安装常用软件

1. 安装`vim`

   ```bash
   yum install vim -y
   ```

2. 安装`htop`，首先需要安装`企业版Linux附加软件包(EPEL)`Centos7的，这里不安装yum搜索不到htop

   ```bash
   yum install https://dl.fedoraproject.org/pub/epel/epel-release-latest-7.noarch.rpm
   ```

   然后安装

   ```9bash
   yum install htop -y
   ```

3. 安装网络工具(常用`ifconfig`命令)

   ```
   yum install net-tools -y
   ```

4. 安装`wget`

   ```bash
   yum install wget -y
   ```

   

