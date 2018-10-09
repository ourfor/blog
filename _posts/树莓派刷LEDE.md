---
title: 树莓派刷LEDE
date: 2018-01-23 17:50:57
tags: [树莓派]
comments: ture
---
树莓派是一个卡片大小的微型电脑，价格在100~300以内，之前再小米商城看了看最新款的小米路由器和小米盒子（小米盒子和小米路由器确实不错）不过我手头有一个树莓派3B，最近闲来无事，就去OpenWrt上面看了看，好像还没有正式适配树莓派3B，不过它的衍生系统LEDE，于是乎就开始刷LEDE了。
<!--more-->
# Raspberry pi 3B刷LEDE
## 下载最新开源镜像
### LEDE项目官网
https://lede-project.org/zh/start
你可以下载源码自己编译，也可以下载编译好的固件。LEDE也是有不少优点的：
* 可扩展性
* 高安全性
* 高性能、高稳定性
* 强大的社区支持
* 开源/无额外支出
### 支持的硬件
https://lede-project.org/toh/start
<img src="http://ozkg680jm.bkt.clouddn.com/Raspberry%20pi%203b%E5%88%B7LEDE-1.png" width="70%" height="30%" />
目前小米路由器有三款可以刷LEDE，不过似乎没有必要，因为小米路由器的系统本身就是基于OpenWrt定制的，并且配合小米WIFI客户端使用体验还是非常棒的。树莓派目前所有的型号都支持LEDE，不过如果你真要用树莓派做路由器使用，建议你买几个USB网卡，不然这自带的无线网卡发射的信号可没那么强。    


|0|型号|WiKi网址|
|:-:|:-:|:-:|
|1|Xiaomi mini|https://wiki.openwrt.org/toh/xiaomi/mini|
|2|Xiaomi   MiWiFi Nano|https://wiki.openwrt.org/toh/xiaomi/nano|
|3|Xiaomi   MiWiFi 3G||
|4|Raspberry Pi A|https://wiki.openwrt.org/toh/raspberry_pi_foundation/raspberry_pi|
|5|Raspberry Pi B|https://wiki.openwrt.org/toh/raspberry_pi_foundation/raspberry_pi|
|6|Raspberry Pi 3B ||
|7|Raspberry Pi B+|https://wiki.openwrt.org/toh/raspberry_pi_foundation/raspberry_pi|
|8|Raspberry Pi 2B|https://wiki.openwrt.org/toh/raspberry_pi_foundation/raspberry_pi|
|9|Raspberry Pi Zero W|https://wiki.openwrt.org/toh/raspberry_pi_foundation/raspberry_pi|

    
LEDE支持的设备的固件都可以在这里下载：https://lede-project.org/toh/views/toh_fwdownload
由于我用的是树莓派3B，所以这里提供最新（20180123）的固件：https://downloads.lede-project.org/releases/17.01.4/targets/brcm2708/bcm2710/lede-17.01.4-brcm2708-bcm2710-rpi-3-ext4-sdcard.img.gz
这个固件大小为8.5m，在macOS中双击打开会得到一个大小为297.8m后缀名为img的镜像文件；在Windows下面用RAR解压打开也是如此
<img src="http://ozkg680jm.bkt.clouddn.com/Raspberry%20pi%203b%E5%88%B7LEDE-2.png" width="70%" height="30%" />


## 烧写镜像到SD卡
### Windows平台
Windows下面可以用诸如软碟通,Refuse等软件一键烧写，方法比较简单，这里就不详细介绍了。提供几个优质软件的官方网站：
Refuse（Windows，Ubuntu）：http://rufus.akeo.ie
Etcher（Windows，Linux，macOS）：https://etcher.io
### Linux,macOS平台
#### dd命令烧写镜像
在Linux/macOS中打开Terminal（终端），下面以macOS为例，在Dock中找到启动台-其他-终端。
步骤：1,卸载SD卡
     2,烧写镜像
在终端中输入：
    
```bash
diskutil list  #列出当前系统挂载的存储设备
```    
<img src="http://ozkg680jm.bkt.clouddn.com/Raspberry%20pi%203b%E5%88%B7LEDE-3.png" width="70%" height="30%" />
卸载SD卡的所有分区：
    
```bash
diskutil unmountDisk diskx   #diskx是系统挂载SD卡的路径
```     
烧写镜像，任何情况下你都可以将文件直接拖到Terminal中，Terminal将会输出文件的绝对路径 ，例如我将文件放在桌面，将它拖进终端，那么它显示的路径就会是       
     
```bash
/Users/zip/Desktop/lede-17.01.4-brcm2708-bcm2710-rpi-3-ext4-sdcard.img
```     
dd命令用法：Ubuntu和macOS中在更改系统设置时要加sudo，回车后需要输入用户密码，这样即使没有超级用户的权限，你也可以执行一些或者全部的权限
   
```bash
sudo dd if=<...> of=<...> bs=1m
```     
- if（input file）=输入文件、设备的绝对路径；
- of（output file）=输出文件、设备的绝对路径；
- bs（block size）=1m 一个操作周期的大小；

我输入的命令是：

```bash
 sudo dd if=/Users/zip/Desktop/lede-17.01.4-brcm2708-bcm2710-rpi-3-ext4-sdcard.img of=/dev/disk4 bs=1m
```

<img src="http://ozkg680jm.bkt.clouddn.com/Raspberry%20pi%203b%E5%88%B7LEDE-4.png" width="70%" height="30%" />
回车输入管理员密码，回车确认就开始烧写，在烧写过程中系统不会有任何提示。
<img src="http://ozkg680jm.bkt.clouddn.com/Raspberry%20pi%203b%E5%88%B7LEDE-5.png" width="70%" height="30%" />
看到上面提示说明烧写完成了。


## 使用开源软件Etcher
如果你觉得上面的命令比较麻烦，这里倒是有一些软件可以帮你一键刷写磁盘镜像，优点就是简洁、安全、美观和快捷，缺点就是效率比较低，而且只能烧写整个磁盘。
Etcher官网：https://etcher.io
Etcher支持主流PC平台
<img src="http://ozkg680jm.bkt.clouddn.com/Etcher.png" width="70%" height="30%" />
左边选择镜像，右边点击就可以烧写镜像了。

## 设置树莓派
由于LEDE默认不开启WiFi，这时候我们可以用网线将树莓派和电脑连接。
* step1 
确保电脑与树莓派通过网线连接好，打开` 浏览器 `在地址栏输入` 192.168.1.1 `进入路由器的web管理界面，默认root用户是没有密码的，直接登录，登录后会要求你设置密码，等你设置完密码后，你就可以通过ssh登录树莓派了。
* step2
打开WiFi
* step3
安装中文语言包

## 关于树莓派（Raspberry pi）
Raspberry Pi是一款针对电脑业余爱好者、教师、小学生以及小型企业等用户的迷你电脑，预装Linux系统，体积仅信用卡大小，搭载ARM架构处理器，运算性能和智能手机相仿。
在接口方面，Raspberry Pi提供了可供键鼠使用的USB接口，此外还有快速以太网接口、SD卡扩展接口以及1个HDMI高清视频输出接口，可与显示器或者TV相连

我的是Raspberry 3b。
<img src="http://ozkg680jm.bkt.clouddn.com/%E6%A0%91%E8%8E%93%E6%B4%BE1.jpg" width="70%" height="30%" />
<img src="http://ozkg680jm.bkt.clouddn.com/%E6%A0%91%E8%8E%93%E6%B4%BE2.jpg" width="70%" height="30%" />
<img src="http://ozkg680jm.bkt.clouddn.com/%E6%A0%91%E8%8E%93%E6%B4%BE3.jpg" width="70%" height="30%" />
## 关于OpenWrt
鉴于开源软件在国内的发展态势，目前国内有基于OpenWRT改进而来的OpenWRT-DreamBox。
开发Dreambox的lintel之后开发了基于Barrier Breaker的PandoraBox。
这个版本的OpenWRT集成了很多常用功能（包括脱机下载等），使用了改进过的较为稳定的硬件驱动，通过这个版本的OpenWRT可以把路由器的功能发挥得淋漓尽致，同时也保证路由器的稳定运行。
## 更多系统支持
树莓派除了可以当路由器来用，还可以当盒子（影音中心）、计算机来用
官网也提供了不少系统下载
Raspberry pi官网：https://www.raspberrypi.org

