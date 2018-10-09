---
title: 开启hidpi
date: 2018-01-01 15:27:01
tags: [hidpi]
---
当你顺利安装好黑果之后是否感觉系统字体太小，而当你更改更低的分辨率是又无法忍受字体发虚、界面模糊。开启hidpi能够让你在使用低分辨率的同时能够享受高清。
<!--more-->
## 获取两个重要参数
### 获取DisplayVendorID和DisplayProductID
在Terminal中键入这两条命令：   

    ioreg -l|grep "DisplayVendorID"
    ioreg -l|grep "DisplayProductID"

<img src="http://ozkg680jm.bkt.clouddn.com/%E5%BC%80%E5%90%AFHidpi-2.png" width=70% height=30%>


此时屏幕上会输出两个十进制数，如图，我得到的两个十进制数分别是：` 2533 `和` 1719 `
接下来就是将这两个十进制数转化为十六进制数，我们可以使用计算器来转化，打开` 启动台 `-` 计算器 `
点击` 显示 `-` 编程型 `    
<img src="http://ozkg680jm.bkt.clouddn.com/%E5%BC%80%E5%90%AFHidpi-1.png" width=70% height=30%>
分别刚才获取的两个` ID `输入,然后点击16，就转化为十六进制了。  

<img src="http://ozkg680jm.bkt.clouddn.com/%E5%BC%80%E5%90%AFHidpi-3.png" width=70% height=30%>   
<img src="http://ozkg680jm.bkt.clouddn.com/%E5%BC%80%E5%90%AFHidpi-4.png" width=70% height=30%>   
记住这两个16进制数。接下来需要用到。

## 生成配置显示器文件
在` Terminal `中键入以下命令：   
```bash
cd ~/Desktop
mkdir DisplayVendorID-xxxx    //其中“xxxx”是DisplayVendorID的16进制值小写
cd DisplayVendorID-xxxx        //进入DisplayVendorID-xxxx目录
touch DisplayProductID-xxxx     //其中“xxxx”是DisplayProductID的16进制值小写
open .                          //Finder中打开
```

### 添加分辨率 

在线生成配置文件，添加分辨率，[在线网址](https://comsysto.github.io/Display-Override-PropertyList-File-Parser-and-Generator-with-HiDPI-Support-For-Scaled-Resolutions/)

<img src="http://ozkg680jm.bkt.clouddn.com/%E5%BC%80%E5%90%AFHidpi-5.png" width=70% height=30%>   

在右边填写配置信息，左边会生成相应的代码。   

 
- ` DisplayProductName `:可随意填写
- ` DisplayProductID `:之前获取的DisplayProductID的16进制数
- ` DisplayVendorID `:之前获取的DisplayVendorID的16进制数
- ` Scale Resolutions `:所有添加的分辨率
- ` hidpi `:勾选即开启该分辨率的hidpi


添加完毕后，复制左边的代码，编辑之前创建的没有后缀名的` DisplayProductID-xxxx `的文件（用文本编辑器打开即可）粘贴复制的代码保存，显示器的配置文件就配置好了，接下来只需要将这个文件夹` DisplayVendorID-xxxx `复制到` /System/Library/Displays/Contents/Resources/Overrides/ `下面（需要输入管理员密码）。     


### 打开hidpi
在` Terminal `中键入以下命令开启Hidpi   
```bash
sudo defaults write /Library/Preferences/com.apple.windowserver.plist DisplayResolutionEnabled -bool true
```
## 使用RDM切换   
github项目地址 [RDM](https://github.com/avibrazil/RDM)  
下载安装后，重启系统打开RDM就可以在状态栏切换分辨率了。

