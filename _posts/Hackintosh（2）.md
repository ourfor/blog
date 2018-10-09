---
title: Hackintosh（2）
date: 2017-10-12 16:01:10
category: "PC"  #
tags: [Hackintosh,系统]  #
---
## 黑苹果安装教程之开始安装
##  已经制作好的安装优盘
如果你按照之前的教程成功制作了黑苹果原版系统安装优盘，那么你会发现你进入Mac安装界面无法格式化Mac安装分区，如果没有制作好安装优盘，那么分区和调整系统esp引导分区依旧是很有必要的，这不仅有利于我们安装Mac，同时也为我们启动多系统提供了便利，相信有不少读者都安装了我们喜爱的Linux的发行版Ubuntu.  
<!-- more -->
##  Mac系统安装分区  
关闭安全启动可以看看大佬的帖子
首先，我们要给mac系统分出一个安装盘，进入Windows10系统，打开文件管理，右键我的电脑，打开管理；  
<img src="http://img02.sogoucdn.com/app/a/100520146/95ff9fd401e906499548f90e6ca041c7" width="70%" height="30%" />
单击磁盘工具，右键c盘，

选择压缩卷，我输入压缩空间量60G，你们可以自行调整;  
<img src="http://img04.sogoucdn.com/app/a/100520146/1c39d2f400c227cc9c14d2255873a6e6" width="70%" height="30%" />
之后打开工具Paragon Hard Disk Manage，将压缩出来的分区格式转化为Apple HFS。软件下载地址：  
[https://pan.baidu.com/s/1geYjoDd](https://pan.baidu.com/s/1geYjoDd](https://pan.baidu.com/s/1geYjoDd](https://pan.baidu.com/s/1geYjoDd "下载地址") 
<img src="http://img03.sogoucdn.com/app/a/100520146/b7b4fc939461deac70620c82deaeb8f6" width="70%" height="30%" />  
<img src="http://img01.sogoucdn.com/app/a/100520146/e9f3b83f5f5c11b4a8cfdca0822a6408" width="70%" height="30%" />
这样mac安装盘就分好了，接下来进入苹果安装界面，选择磁盘工具，将我们分好的苹果分区抹掉，格式我是选择APFS或者HFS，如果抹除不成功，一般是笔记本的esp分区太小了，应该要300m以上，如何扩大esp分区，可以看看论坛大佬的贴子，安装教程就到这里，不要忘了把系统的esp分区下的文件夹替换成我的efi文件夹里的，这样的话就不用每次进mac系统前借助优盘的四叶草引导跑代码了，如果不会替换，建议多爬爬贴，论坛里有教程￼￼￼，当然这只是安装好了，只是完成了三分之一，后续更新驱动安装和四叶草界面美化 


小米笔记本驱动下载：
https://pan.baidu.com/s/1skAjk8d
这些驱动按照需要安装，安装调节分辨率的软件后在上面状态栏选择调节分辨率，亮度调节也是这样。
<img src="http://img01.sogoucdn.com/app/a/100520146/4473dadc91a6c4aa4fb70e452f6203e9" width="70%" height="30%" />

建议先搞一个pe，以防不测，其次如果要将，efi替换需要使用软件easyuefi为四叶草引导添加启动项，并把四叶草引导调为首选启动项，或者合拼efi分区

可以看看这些大佬的帖子：  
http://www.miui.com/thread-7419826-1-1.html  
http://www.miui.com/thread-7601066-1-1.html  
http://www.miui.com/thread-7574042-1-1.html  
女帝镇楼：  

<img src="http://img01.sogoucdn.com/app/a/100520146/d813b2df31168428eca4bb9d33be0066" wedth="70%"
height="30%">  




