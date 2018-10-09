---
title: MIUI Theme
date: 2018-04-07 10:10:34
tags: [Theme,MIUI]
---
最近闲的没事，改了改手机上的主题。虽然主题商店里面有不少精美的主题的，但是这些主题都不够完美，有些图标精致，有些锁屏强大，所以总能勾起修改的欲望。接触主题制作这么久了，***主题商店***还仅仅上架过一款主题，说实话我PS弄得一般般，所以这款唯一上架的主题也仅仅分成了10多块大洋，设计不太会，代码还是懂一点的，主题描述文件是遵循` xml `语法的，所以就借用其他主题的素材，修改部分代码，东拼西凑了一下，最后效果还不错。（仅限自用，请勿上传到主题商店）

<!--more-->
### 效果预览
![主屏](http://p5culcl8r.bkt.clouddn.com/autojump_0.png)
这个` AT&T `是在手机的` 设置-状态栏-运营商 `这里修改。而这个` Love you %d days `是修改了主题的状态栏描述文件，这个数字就是电池实时电量的百分比。

![Time](http://p5culcl8r.bkt.clouddn.com/autojump_1.png)

时间设置成` 星期+日期|时间 `也在主题的描述文件里面设置的，图标则是使用了***H2SO***的图标。

![Tips](http://p5culcl8r.bkt.clouddn.com/autojump_2.png)

### 时间居中
状态栏时间居中是在解锁System后使用` MiUI Statusbar Pro `设置的，当然你也可以反编译` system/priv-app/miuisystemui `里的` miuisystemui.apk `,这同样需要*root*权限。

相关教程[下载](http://p5culcl8r.bkt.clouddn.com/%E7%8A%B6%E6%80%81%E6%A0%8F%E5%B8%83%E5%B1%80%E8%AF%A6%E7%BB%86%E6%95%99%E7%A8%8B%EF%BC%88%E4%BF%AE%E8%AE%A2%E7%89%88%EF%BC%89.pdf)

### 应用主题
下载地址：
[v1.0](http://p5culcl8r.bkt.clouddn.com/H2OS.mtz)(仅限自用，请勿上传到主题商店)
[v2.0](http://p5culcl8r.bkt.clouddn.com/H2OS_2.0.mtz)

[MIUI Theme Editor](http://p5culcl8r.bkt.clouddn.com/com.mixapplications.miuithemeeditor.apk)

我使用的是星空的官改rom，由于这手机平时用得着，所以就退出体验版内测了，估计大部分人用的是官方的开发版或者稳定版，没更新过系统的话，用` MIUI Theme Editor `（不需要root）注入主题，就可以在主题里面应用，只不过这个软件第一次使用需要下载大概60m的数据文件，需要翻墙下载。

# 免破解个性化状态栏
首先，请确保您已经完成下述工作：
- 获取` root ` 权限
- 解锁` system ` 分区,推荐使用[syslock](http://p923bw9fi.bkt.clouddn.com/com.lerist.syslock.apk),改软件可在酷安下载。
- 安装` RE文件管理器 `(其他具有相同功能的软件也行,当然终端也是可以的)

## Step 1
下载你喜欢的主题包,在此分享一个简单的方法:1.在` MIUI主题商店 `免费试用主题 2.在主题商店没有下载完成主题包之前,打开系统自带` 下载管理 `,暂停当前下载主题的任务. 3.点击查看之前暂停的下载任务详细，复制下载地址，删除暂停下载的主题包，新建一个下载任务。

## Step 2
找到下载好的主题包` mtz `文件，将后缀名改为` zip `。
![theme_unzip](http://p923bw9fi.bkt.clouddn.com/theme_unzip.png)
接下来找到` com.android.systemui `,添加后缀` zip `,同样解压。主题资源文件在` res `下面。

相关文件夹说明：
- ***raw-xxhdpi***:电池变化的状态和图标保存在这里
- ***drawable-xxhdpi***:状态栏的` 网速、WiFi等 `图标以及` 通知栏背景 `存放在该文件夹下面

进入` drawable-xxhdpi `文件夹删除所有后缀名为` .9.png `的文件，可以自行删除,也可以在终端中用命令` rm -rf *.9.png `。

## Step 3
打开手机上面的` RE文件管理器 `(需要root权限),提取复制该路径下面的` /system/priv-app/MiuiSystemUI/ `的***MiuiSystemUI.apk***文件(注意备份该文件),发送到电脑,在` Windows `下右键该apk文件，使用` RAR `打开查看:(可以先改后缀名apk为zip,记得最后改回来;也可以在打开方式里面找到RAR的安装位置打开)

- 将` step 2中res/drawable-xxhdpi/ `下面的所有文件复制,然后粘贴到 ` MiuiSystemUI.apk\res\drawable-xxhdpi-v4\ `,在` RAR `的查看界面按下` Ctrl + v `点击确认即可。
- 将` step 2中res/raw-xxhdpi/ `按下` Ctrl + c `复制,在RAR中定位到` MiuiSystemUI.apk\res\raw-xxhdpi-v4\ `，按下` Ctrl + v `替换即可。
![查看,不需要解压](http://p923bw9fi.bkt.clouddn.com/rar.png)

(注意保证文件名为` MiuiSystemUI.apk `)

## Step 4
将修改后的状态栏文件替换原来的文件,同时修复权限为:` rw-r--r-- `
![权限](http://p923bw9fi.bkt.clouddn.com/%E6%9D%83%E9%99%90.png)
![修复权限](http://p923bw9fi.bkt.clouddn.com/%E4%BF%AE%E5%A4%8D%E6%9D%83%E9%99%90.png)

## 懒人版
- 删除点9文件的主题资源[res](http://p923bw9fi.bkt.clouddn.com/res.zip)
- miui 10.8.6.6已修改[MiuiSystemUI.apk](http://p923bw9fi.bkt.clouddn.com/MiuiSystemUI.apk)
(note:OTA升级前确保` System `分区上锁,否则增量包升级会翻车)


{% dplayer "url=http://file.ourfor.top/youtube/Army1.mp4" "api=http://dplayer.daoapp.io" "pic=http://img0.c.yinyuetai.com/artist/fan/150810/0/-M-70f069427cca50778df6b121a8bf5a8a_0x0.jpg" "id=9E2E3368B56CDBB4" "loop=yes" "theme=#FADFA3" "autoplay=false" "token=tokendemo" %}
