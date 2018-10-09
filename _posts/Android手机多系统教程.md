---
title: Android手机多系统教程
date: 2018-05-12 20:20:40
tags: [Android,Dual Boot Patcher]
categories: "玩机"
src: sw1.jpg
---
其实在小米4之前的每一代小米手机都可以安装双系统，这是由于MIUI的频繁更新而设置的一种保护机制,不过之后就取消了,目前Android手机多系统教程,是通过软件` Dual Boot Patcher ` 来实现的,顾名思义就是可以在一部手机上面安装多个基于UI,比如国内基于安卓系统的UI-` MIUI、Flyme、Mokee这些 `，安卓系统使用的是Linux的内核，这个多系统只是借助了***chroot***而已.网上关于这款软件有很多教程，但是很多教程写的都不够详细，对新手不够友好，也没有做到详略得当，所以我就把我安装多系统的过程记录下来。

<!--more-->

***名词释义***
- chroot
chroot命令用来在指定的根目录下运行指令。chroot，即` change root directory ` （更改 root 目录）。在 linux 系统中，系统默认的目录结构都是以/，即是以根 (root) 开始的。而在使用` chroot ` 之后，系统的目录结构将以指定的位置作为/位置。

- UI
即` user interface ` (用户界面)

效果预览：

![mokee](desktop.png)
![miui](interface.png)
![mokee_app](interface_mokee.png)
![miui_app](interface_miui.png)



### 用到工具

记得老师总说，做题就像做菜一样，首先要把原料准备好，这里我们主要用到的工具有：
- [Dual Boot Patcher](https://dbp.noobdev.io/) [Android下载](https://dbp.noobdev.io/files/9.3.0.r493.g32c14fd5/Android/DualBootPatcherAndroid-9.3.0.r493.g32c14fd5-snapshot.apk)

- [MT工具箱](http://p5culcl8r.bkt.clouddn.com/bin.mt.plus-2.5.0-18042700-21048.apk)

- [files]()

#### 要求
- 获取root权限
- 解锁system分区
- 解密data分区

#### 注意事项及常见问题

- 刷入系统后，先不要重启，复制内部存储下的` multiboot `文件夹📁下的启动文件到root分区，注意是root分区，不是boot分区，这样做是为了保证当data未解密时仍然能够通过recovery刷入boot镜像切回主系统，路径：` /storage/emulated/0/multiboot/ `下面的所有文件夹复制到根目录的root分区
- 解密` data `分区，使用twrp中的解密data，然后刷入supersu，防止data加密
- 刷入` recovery `，推荐刷入T W R P，使用一键刷入recovery工具包
- 处理刷机包，选择刷入分区，建议都安装在data分区
- 下载刷机包，使用MT工具箱文本编辑，删除基带验证。
- 带BL锁的，要先解BL锁。
- 刷入` Supersu `，获取ROOT权限，同时还能防止data再次加密
- 使用` syslock `解锁system分区，从而获取完整root权限，针对MIUI从官方下载root包获取的权限，如果使用Supersu获取的话可以忽略。
- 刷入位置：推荐data分区，其他位置一般刷入失败的概率比较大，填写ID时，根据个人喜好填写，仅仅只是为了区分系统安装的位置而已。
- 文件乱码，内部存储无读写权限：这种情况属于未解密data分区，可以在recovery中刷入你想启动的系统的boot.img文件，即可切回主系统。
- 解密` data `会清空所有数据，所以提前备份好重要数据，推荐使用小米云服务备份。
- 由于` 8.x `系统分区结构改变，并且会自动加密data分区，dual boot patcher作者尚未更新，所以8.x系统大部分不能用作副系统。
- 为除` 主系统 `外的其他系统刷入Supersu以及xposed都需要处理，处理方式与刷入系统方式相同，同时安装位置要与待安装到的系统位置相同，即填写id标识与系统相同。
- 设置锁屏密码;刷入其他系统后，最多只能有一个系统设置锁屏密码，并且只有最后一次设置的密码能够解锁对应系统，其他系统均会出现密码错误。
- 密码错误，无法解密:此时只需要在TWRP自带的Terminal下面删除锁屏密码保存的文件即可，锁屏密码锁在路径，系统的相对路径(系统安装位置)假设为～，密码保存文件位于：` ~/data/system/ `，以主系统为例 ` cd /data/system `,查看文件` ls `,其他后缀名为 ***key***的就是要删除的文件,` rm *.key `同样的，因为密码错误无法进入系统也可以删除对应的密码保存文件。

### 刷机指南



#### 通过` Recovery ` 卡刷
#### 通过` Fastboot ` 线刷

（未完待续...）
<div id="app"></div>
<!-- 加载 cplayer 脚本 -->
<script src="https://cdn.jsdelivr.net/gh/MoePlayer/cPlayer/dist/cplayer.js"></script>
<script>
  let player = new cplayer({
    element: document.getElementById('app'),
    autoplay: true,
    showPlaylist: true,
    playlist: [
      {
        src: 'http://ozkg680jm.bkt.clouddn.com/%E6%A3%AE%E6%B0%B8%E7%9C%9F%E7%94%B1%E7%BE%8E-Mermaid%20girl%20%28Extended%20RRver.%29.flac',
        poster: 'http://ozkg680jm.bkt.clouddn.com/Mermaid%20girl%20%28Extended%20RRver.%29.jpg',
        name: 'Mermaid girl (Extended RRver.)',
        artist: '森永真由美'
      },
      {
        src: 'http://ozkg680jm.bkt.clouddn.com/%E6%A3%AE%E6%B0%B8%E5%8D%83%E6%89%8D-%E3%83%9F%E3%83%81%E3%83%8E%E3%83%81%E3%83%A2%E3%82%B7%E3%83%BC%E3%82%AD%E3%83%9F%E3%83%8E%E3%82%AD%E3%83%A2%E3%83%81%20%28%E8%B7%AF%E4%B8%8A%E7%9A%84%E7%8C%AB%E5%B0%BE%E8%8D%89%20%E4%BD%A0%E7%9A%84%E5%BF%83%E6%83%85%29.mp3',
        poster: 'http://ozkg680jm.bkt.clouddn.com/%E3%83%9F%E3%83%81%E3%83%8E%E3%83%81%E3%83%A2%E3%82%B7%E3%83%BC%E3%82%AD%E3%83%9F%E3%83%8E%E3%82%AD%E3%83%A2%E3%83%81%20%28%E8%B7%AF%E4%B8%8A%E7%9A%84%E7%8C%AB%E5%B0%BE%E8%8D%89%20%E4%BD%A0%E7%9A%84%E5%BF%83%E6%83%85%29.jpg',
        name: '路上的猫尾草 你的心情',
        artist: '森永千才'
      },
      {
        src: 'http://ozkg680jm.bkt.clouddn.com/%E5%AD%99%E9%9C%B2-%E6%9B%BE%E7%BB%8F%E7%88%B1%E8%BF%87%E8%B0%81.flac',
        poster: 'http://ozkg680jm.bkt.clouddn.com/%E6%9B%BE%E7%BB%8F%E7%88%B1%E8%BF%87%E8%B0%81.jpg',
        name: '曾经爱过谁',
        artist: '孙露'

      },
      {
        src: 'http://ozkg680jm.bkt.clouddn.com/%E8%B5%B5%E7%B4%AB%E9%AA%85-%E5%8F%AF%E4%B9%90.mp3',
        poster: 'http://ozkg680jm.bkt.clouddn.com/%E5%8F%AF%E4%B9%90-%E8%B5%B5%E7%B4%AB%E9%AA%85.jpg',
        name: '可乐',
        artist: '赵紫骅',
        lyric: '[ti:可乐]\n[ar:赵浴辰]\n[al:可乐]\n[by:]\n[offset:0]\n[00:00.10]可乐 - 赵紫骅\n[00:00.20]词：赵紫骅\n[00:00.30]曲：赵紫骅\n[00:00.40]\n[00:31.20]可惜在遇见我那天你并不快乐\n[00:36.42]\n[00:38.20]可能是因为我们相遇的太晚了\n[00:44.47]\n[00:45.62]可是我要走了\n[00:48.51]\n[00:49.34]可温暖要走了\n[00:52.18]\n[00:53.08]可否有另一个我在你身后给予快乐\n[00:59.54]\n[01:01.37]可当我牵着你的手傻乎乎的乐\n[01:06.33]\n[01:08.17]渴望的爱情终于在我生命出现了\n[01:14.57]\n[01:15.65]可时间倒数了\n[01:18.55]\n[01:19.23]可你的答案停住了\n[01:22.49]\n[01:23.10]可想到你的脸我还是很快乐\n[01:30.16]可能你不快乐\n[01:33.39]\n[01:34.09]可惜你不快乐\n[01:36.89]\n[01:37.74]可能是我的爱情它来的太晚了\n[01:44.66]\n[01:45.64]可他给了你些什么\n[01:49.82]你是不是真快乐\n[01:53.50]可要听我的话别再为他犯傻了\n[02:00.16]可能你不快乐\n[02:03.93]可我要你快乐\n[02:07.37]\n[02:07.94]可能是我的爱情它来的太晚了\n[02:14.99]\n[02:15.68]可我只想对你说\n[02:19.40]我绝对不退出了\n[02:23.16]可以让你快乐是我的快乐\n[02:32.58]\n[02:42.46]可当我牵着你的手傻乎乎的乐\n[02:47.64]\n[02:49.43]渴望的爱情终于在我生命出现了\n[02:55.87]\n[02:56.96]可时间倒数了\n[03:00.00]\n[03:00.58]可你的答案停住了\n[03:03.82]\n[03:04.39]可想到你的脸我还是很快乐\n[03:11.04]\n[03:11.72]可能你不快乐\n[03:15.15]可惜你不快乐\n[03:18.51]\n[03:19.16]可能是我的爱情它来的太晚了\n[03:26.26]\n[03:26.91]可他给了你些什么\n[03:30.52]\n[03:31.09]你是不是真快乐\n[03:34.82]可要听我的话别再为他犯傻了\n[03:41.40]可能你不快乐\n[03:45.16]可我要你快乐\n[03:49.22]可能是我的爱情它来的太晚了\n[03:56.96]可我只想对你说\n[04:00.65]我绝对不退出了\n[04:04.45]可以让你快乐是我的快乐\n[04:16.24]\n[04:24.76]不快乐\n[04:25.87]\n[04:26.60]可惜你不快乐\n[04:29.42]\n[04:30.55]可能是我的爱情它来的太晚了\n[04:38.19]可他给了你些什么\n[04:41.92]\n[04:42.44]你是不是真快乐\n[04:46.04]可要听我的话别再为他犯傻了\n[04:52.72]可能你不快乐\n[04:56.35]可我要你快乐\n[04:59.81]\n[05:00.44]可能是我的爱情它来的太晚了\n[05:08.16]可我只想对你说][05:11.39][05:11.91]我绝对不退出了[05:15.09][05:15.63]可以让你快乐是我的快乐'
      }
    ]
  })
</script>


