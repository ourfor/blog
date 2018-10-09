---
title: VPS搭建Shadowsocks实现科学上网
date: 2018-02-22 10:53:20
tags: [SSR]
categories: [VPS]
---
最近很多免费的vpn软件都失效了，之前有用过蓝灯、FreeVPN之类的科学上网的软件，这类软件虽然免费，但是安全性较低、连接速度比较慢。油管视频基本看不了，有时还连接失败。好在最近亚马逊云（AWS）、谷歌云（Google Cloud）等虚拟主机厂商都推出了免费VPS的活动，如果你有信用卡你可以去AWS和Google Cloud上面去看看，AWS提供一年的免费云主机，Google Clou赠送的金额足够你的VPS跑半年，然而由于信用卡的缘故，这两个我都没用，想想也不现实天底下哪有这么大免费午餐，不然别人还不得亏死，还是老老实实买个VPS吧，推荐搬瓦工和Vultr他家的VPS，这两家现在都支持支付宝付款，并且都比较便宜。   
<!--more-->  
## 选购云主机（VPS）  
- [搬瓦工](https://bandwagonhost.com/)
- [Vultr](https://www.vultr.com/?ref=7332767)  
目前` 搬瓦工 `最低的套餐-` $19.9/年 10G VPS `已经售坠了，` Vultr `最低套餐为` $2.50/月 `目前还有，通过我的邀请码注册` Vultr `应该会额外赠送$3,[Vultr](https://www.vultr.com/?ref=7332767)。如果你在搬瓦工上面购买VPS的话，它那里有KVM和OpenVZ两种类型的主机，选KVM，还是OpenVZ？这个问题对新手来说没有太大意义。一句话来说：想折腾的选KVM，想买便宜货的选OpenVZ，但从业界大趋势来看，建议购买虚拟化程度更高的KVM方案，而` Vultr `上面只有` KVM `类型的。 


### OpenVZ的优势：
- IPv6支持
- 更好的CPU性能

### KVM的优势：
- 完全虚拟化
- 自定义内核支持（BBR等）
- Docker支持
- 更好的隔离
- 提高网络吞吐量

（SSR加速可以使用BBR，迅雷远程下载等需要Docker）

都以最低配置进行比较：

||SSD|ECC RAM|带宽|中央处理器|价钱|
|:-:|:-:|:-:|:-:|:-:|:-:|
|Vultr|20 GB固态硬盘|512 MB|500 GB|1x Intel Xeon|$2.50/月|
|搬瓦工|10 GB固态硬盘|512 MB|500 GB|1x Intel Xeon|$19.9/年|   

其中` Vultr `是以每小时收费的，` 搬瓦工 `支持30天退款，

<img src="http://ozkg680jm.bkt.clouddn.com/VPS%E6%90%AD%E5%BB%BAShadowsocks%E5%AE%9E%E7%8E%B0%E7%A7%91%E5%AD%A6%E4%B8%8A%E7%BD%91-1.png" width=70% height=30%>

我是在` Vultr `上面的配置的主机，注册$10,关注官方` Twtter `获得` $3 `。  

<img src="https://www.vultr.com/media/banner_1.png" width=70% height=30%>    

选一个你认为合适的厂商购买云主机，部署地点最好选择美国西海岸距离中国近的，这样延迟比较低，比如` 洛杉矶 `这些地方，系统最好选择`CentOS` 、` Ubuntu `这两种，` CentOS `最好选择` 6 `，因为` 7 `有防火墙需要额外设置。下面我以` Vultr `上面的` CentOS 6 x64 `为例搭` Shadowsocks `.

## 开始搭建SSR

### ssh连接VPS  
- Windows下使用` xshell `或者` putty `来连接
- Linux和macOS下直接在终端连接，用法：` ssh root@ip_address `其中` root `是用户名，一般是` root `,端口不更改就是` 22 `,` ip_address `是主机的` 外网ip `

首先，更改` root `密码，ssh连接主机后输入以下命令：  

```bash
sudo passwd root
```

改好密码后下载` doub.io `的一键安装脚本，键入以下指令即可，

```bash
wget -N --no-check-certificate https://softs.fun/Bash/ssr.sh && chmod +x ssr.sh && bash ssr.sh
```

它会下载` ssr.sh `这个一键安装脚本，按照提示输入即可，之后如果你想查看用户信息，直接输入` bash ssr.sh `如果提示没有权限` chmod +x ssr.sh `加上运行权限就行了，你填写好参数后会在屏幕上面打印出` ss `和` ssr `链接地址。  

### SSR客户端下载  

无法到官网下载` Shadowsocks `(被墙)，可以去` github `上面下载。  

客户端下载：

- [Windows](https://letsgofree.net/ssr-download/ssr-win.zip)
- [Android](https://letsgofree.net/ssr-download/ssr-android.apk)
- [macOS](https://letsgofree.net/ssr-download/ssr-mac.dmg)
- IOS 需要在` App Store `购买` Potatso `或者` Shadowrocket `或者` Surge `

将之前的` ss `或者` ssr `地址复制，打开` shadowsocks `，点击` 添加 `选择` 从剪粘板导入 `即可。    




### 免费SSR分享  
当然也不是每个人都需要经常用到` google `,尽管` 百度 `在做` 外卖 `，` google `在做` AI `,抛开` 安全性 `和` 稳定性 `不提,免费的` SSR `还是有很多人分享的，只不过速度没有那么快罢了。

- https://www.letsgofree.net（需要注册，且每个月只有2G）
- https://doub.bid/sszhfx/


{% aplayer "没离开过" "张韶涵" "http://ozkg680jm.bkt.clouddn.com/%E5%BC%A0%E9%9F%B6%E6%B6%B5-%E6%B2%A1%E7%A6%BB%E5%BC%80%E8%BF%87.flac"  "https://gss0.bdstatic.com/94o3dSag_xI4khGkpoWK1HF6hhy/baike/c0%3Dbaike272%2C5%2C5%2C272%2C90/sign=6ed5142a95510fb36c147fc5b85aa3f0/8326cffc1e178a8231192533fd03738da977e878.jpg" "autoplay" %}














