---
title: Nginx以及私有云搭建
date: 2018-04-28 11:57:22
tags: [Nginx,ownCloud]
categories: "私有云" 
src: 
---
平时没事经常去GitHub看看开源的项目，昨天看见一个下载` Youtube ` 视频的项目，觉得很不错，国外网速快，4个G不到30s下好了，要是能VPS上面在线播放就好了，这不，Nginx就派上用场了，平时下载国外资源网速慢，可以先下载到服务器，再从服务器下载。回归正题，本文需要` LNMP ` 环境。
<!--more-->

## 一键安装LNMP
所谓的***LNMP***是指：
- [x] Linux系统
- [x] Nginx
- [x] mysql(数据库)
- [x] Php

下面使用一键安装脚本：
ssh连接VPS，使用` root ` 登录主机：
```bash
wget http://soft2.vpser.net/lnmp/lnmp1.4-full.tar.gz  #下载lnmp完整包
tar -xvf lnmp1.4-full.tar.gz      #解压
cd lnmp1.4-full                   #进入lnmp1.4-full文件夹
chmod +x install.sh                        #为安装脚本添加可执行权限，遇到确实执行权限，可以添加运行权限
```

- 安装` screen ` （可选）
因为编译时间比较长，大概半个小时左右，如果不慎关闭终端，那么远程服务器的操作就会终止，这时候使用` screen ` 来创建一个会话，这样即使断开本地终端与服务器的连接，安装操作也会继续进行，一般Linux预装了***screen***
如果没有安装的话，可以通过` yum install screen ` (centOS等),` apt-get install screen ` (Ubuntu等)

```bash
screen -S lnmp          #创建名为lnmp的对话窗口
bash install.sh         #执行安装脚本
```
安装过程我就不细说了，按照提示操作就可以了。


## 配置Nginx

- 通过源码编译安装Nginx
通过源码编译安装` Nginx ` 是为了能够使用` Nginx ` 的一些模块，这里为了美化Nginx的目录浏览，会安装` Fancy Index module ` ,[Nginx源码](http://nginx.org/en/download.html).下面我以` version=	1.14.0 ` 为例;

```bash
wget http://nginx.org/download/nginx-1.14.0.tar.gz      #你也可以选择使用curl下载
gunzip -c nginx-1.14.0.tar.gz | tar -xvf -         #解压源码压缩包到当前目录
git clone https://github.com/aperezdc/ngx-fancyindex.git ngx-fancyindex   #需要安装git
cd nginx-1.14.0              #进入目标文件夹
./configure --user=www --group=www --prefix=/usr/local/nginx \      #每条命令都要回车
--with-http_stub_status_module \ 
--with-http_ssl_module \
--with-http_v2_module \
--with-http_gzip_static_module \ 
--with-ipv6 \ 
--with-http_sub_module \
--add-module=../ngx-fancyindex              #添加Fancy Index module
make && sudo make install                   #编译并安装
```
安装好` Nginx ` 之后我们需要简单设置一下来开启` 目录浏览功能 ` 并启用` Fancy Index module ` ,在` /usr/local/nginx/conf/nginx.conf ` 中添加以下代码：

service字段中添加：
```bash
location / {
  fancyindex on;              # Enable fancy indexes.
  fancyindex_exact_size off;  # Output human-readable file sizes.
}
```
http字段中添加：
```bash
autoindex on;
include fancyindex.conf;
```

接下来执行如下命令：
```bash
git clone https://github.com/TheInsomniac/Nginx-Fancyindex-Theme.git /usr/local/nginx/fancyindex
```
效果预览：[@-@](https://file.ourfor.top)

主题项目地址：

- [TheInsomniac](https://github.com/TheInsomniac/Nginx-Fancyindex-Theme.git)
- [Naereen](https://github.com/Naereen/Nginx-Fancyindex-Theme.git)

## 安装` Youtube-dl `

- [youtube-dl](https://github.com/rg3/youtube-dl)

GitHub上面有详细的使用教程；按照上面的介绍，你可以在` Terminal ` 中键入：

```bash
sudo curl -L https://yt-dl.org/downloads/latest/youtube-dl -o /usr/local/bin/youtube-dl
sudo chmod a+rx /usr/local/bin/youtube-dl
```
嗯，就这样就安装好了，接下来你就可以去油管找你想下载的视频了。我就不详细介绍命令的用法了。

![youtube-dl](http://p5culcl8r.bkt.clouddn.com/youtube-dl.png)

分辨率最高的视频是不包含音频的，所以还要下载音频，最后用` ffmpeg ` 来将音频文件和视频文件合成新的视频文件。

![ffmpeg](http://p5culcl8r.bkt.clouddn.com/ffmpeg.png)













## ownCloud
- [ownCloud](https://owncloud.org/)

首先你得有一个域名，大部分域名还是很便宜的，像阿里云、腾讯云的新用户首年1元的域名还是很多的
添加一个虚拟主机目录：
```bash
lnmp vhost add
cloud.ourfor.top             #你的域名，同时将域名dns解析到服务器ip
```

进入网站更目录：
```bash
cd /home/wwwroot/cloud.ourfor.top
curl -L https://download.owncloud.org/download/community/owncloud-latest.zip -o oc.zip   #下载ownCloud源码，并重命名为oc.zip
unzip oc.zip    #解压源码压缩包
cp -R owncloud/* .      #递归拷贝文件到网站根目录
```
> 注意：ownCloud需要Php版本高于5.6.0，如果你的PHP版本比较低可以在lnmp文件夹下面执行` upgrade.sh ` 脚本升级Php

接下来打开你绑定的域名，设置一下就好了。


（未完待续）

