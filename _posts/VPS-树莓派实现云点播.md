---
title: VPS/树莓派实现云点播
date: 2018-03-01 08:50:37
tags: [Xware,Docker,Emby]
categories: "云播"
---
本文将介绍如何使用下载工具*Xware*（迅雷远程下载）以及Emby来实现云点播，下载工具万万千千，为什么我们要用*Xware*？大家熟知的下载神器除了迅雷还有*Aria2*、*Transmission*；其实这些也是可以用的，只不过个人感觉` 迅雷 `下载快一点，同样对于媒体服务而言除了*Emby*还有*Plex*，只不过这个` Plex `安卓端播放是需要会员的，因此这里使用` Xware `和` Emby `如果你有个开发板或者VPS，接下来就开始折腾。   
<!--more-->       

## Install Xware   
安装*Xware*之前，我们需要安装*Docker*，而Docker只能安装在64位的电脑上面，这里我的VPS使用的是` CentOS6 x64 `，输入以下命令安装：    

```bash
curl -sSL https://get.daocloud.io/docker | sh      #安装Docker
```

树莓派直接使用该命令` sudo apt-get install docker.io `安装*Docker*，安装好` Docker `之后，我们来下载*Xware*的镜像，这些镜像你可以在[DaoCloud](www.daocloud.io)上面下载，对于VPS使用这个镜像` caiguai/docker-xware `树莓派使用这个` zxq1002/docker-thunder-xware `镜像  

### caiguai/docker-xware
在终端中依次输入以下命令：     

拉取最新镜像：
```bash
docker pull caiguai/docker-xware:latest
```

创建一个下载目录. 用于挂载卷   
```bash
mkdir data
```

运行
```bash
docker run -d \
        --name=xware \
        --net=host \
        -v $(pwd)/data:/xware/TDDOWNLOAD \
        caiguai/docker-xware
```

查看日志(激活码)/到迅雷增加设备   
```bash
docker logs xware
```   
```bash
// output:
killall: ETMDaemon: no process killed
killall: EmbedThunderManager: no process killed
killall: vod_httpserver: no process killed
initing...
try stopping xunlei service first...
setting xunlei runtime env...
port: 9000 is usable.

YOUR CONTROL PORT IS: 9000

starting xunlei service...
Connecting to 127.0.0.1:9000 (127.0.0.1:9000)
setting xunlei runtime env...
port: 9000 is usable.

YOUR CONTROL PORT IS: 9000

starting xunlei service...

getting xunlei service info...

THE ACTIVE CODE IS: xxx                   //激活码

go to http://yuancheng.xunlei.com, bind your device with the active code.
finished.
```
打开网站[迅雷远程下载](http://yuancheng.xunlei.com)，输入激活码绑定就可以下载了。

### zxq1002/docker-thunder-xware
在终端中依次输入以下命令：     

拉取最新镜像：
```bash
docker pull zxq1002/docker-thunder-xware:latest
```

创建一个下载目录. 用于挂载卷   
```bash
mkdir data
```

运行
```bash
docker run -d \
         --name=xware \
         --net=host \
         -v $(pwd)/data:/app/TDDOWNLOAD \
         zxq1002/docker-thunder-xware
```
剩下的步骤和上面的一样。

### 添加开机启动
输入` docker ps `可以查看正在运行的容器，` docker ps -l `用于查看所有容器，输入命令查看`  `.
修改启动脚本` /etc/rc.local `

```bash
sudo vi /etc/rc.local
```
按` i `进入编辑状态，在` exit 0 `之前加上这一句` sudo docker start xxxxxxxx(Docker容器CONTAINER ID） `,之后按` Esc `进入命令输入状态输入` :wq `,注意` : `需要在英文状态下按住` Shift `输入。

迅雷远程下载官网的影视搜索里面有资源下载的网站，这里推荐一个下载动漫的网站：
- [动漫花园](share.dmhy.org)

## Install Emby

- [Emby官网](https://emby.media/)

` Emby服务端 `在<https://emby.media/linux-server.html> 


<img src="http://ozkg680jm.bkt.clouddn.com/install%20Emby%20service.png" width=70% height=30%>

*右键*Download后面的安装包，选择复制*下载地址（链接）*，服务器安装` wget `下载工具，当然你也可以电脑下载好之后通过*ftp/scp*上传到VPS或者树莓派。这里树莓派选择` Armhf `架构的安装包。    

树莓派输入` sudo apt-get install wget `,VPS输入` yum install wget `安装*wget* 

以树莓派为例，输入以下命令下载` Emby `   
```bash
wget https://github.com/MediaBrowser/Emby/releases/download/3.3.0.3/emby-server-deb_3.3.0.3_armhf.deb
```

由于伟大的中国长城防火墙（GFW）de缘故，可能官网提供的下载地址下载没有速度，我这里上传到七牛云。版本均为` 3.3.0.3 `

下面的` deb安装包 `仅支持Debian系的（包括Ubuntu）系统，而Redhat系的（包括CentOS）则使用docker镜像，因为官网没有提供` rpm安装包 `

树莓派:` wget http://ozkg680jm.bkt.clouddn.com/emby-server-deb_3.3.0.3_armhf.deb `
VPS:` wget http://ozkg680jm.bkt.clouddn.com/emby-server-deb_3.3.0.3_amd64.deb `

由于下载的是安装包，安装时肯定存在依赖问题。VPS需要安装` dpkg `，` apt install dpkg `

尝试安装：   

树莓派：` dpkg -i emby-server-deb_3.3.0.3_armhf.deb `
Debian系VPS：` dpkg -i emby-server-deb_3.3.0.3_amd64.deb `

如果安装失败，解决依赖问题：  

树莓派：` sudo apt-get install -f `
Debian系VPS：` sudo apt-get install -f `

修复依赖后再次安装就行来。  

Redhat系的（包括CentOS）：     
拉取镜像：   

```bash
docker pull emby/embyserver:latest
```

运行：

```bash
docker run -d \
    --volume /path/to/programdata:/config \ # This is mandatory
    --volume /path/to/share1:/mnt/share1 \ # To mount a first share
    --volume /path/to/share2:/mnt/share2 \ # To mount a second share
    --device /dev/dri/renderD128 \ # To mount a render node for VAAPI
    --publish 8096:8096 \ # To expose the HTTP port
    --publish 8920:8920 \ # To expose the HTTPS port
    --env UID=1000 \ # The UID to run emby as (default: 2)
    --env GID=100 \ # The GID to run emby as (default 2)
    --env GIDLIST=100 \ # A comma-separated list of additional GIDs to run emby as (default: 2)
    emby/embyserver:latest
```
升级
```bash
docker pull emby/embyserver:latest
```
当然你也可以使用第三方镜像



安装完毕后，打开` http://localhost:8096 `,这里的` localhost `是ip地址，VPS填写公网IP，树莓派填写局域网IP。











