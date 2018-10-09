---
title: 个性化clover启动项
date: 2018-01-13 09:51:03
category: "clover"  #
tags: [clover]  #
---
clover启动时会有一些启动项，有些我们不常用，可以编辑clover的配置文件` config.plist `（/ESP/EFI/CLOVER/config.plist）来隐藏，可能你想个性化这些启动项的名称和图标，或者默认启动哪个Volumes，期待这篇文章对你有所帮助。
<!-- more --> 
  首先用` clover configurator `或者diskutil挂载ESP引导分区，同时用这个` clover configurator `打开/ESP/EFI/CLOVER/config.plist  

<img src="http://ozkg680jm.bkt.clouddn.com/%E4%B8%AA%E6%80%A7%E5%8C%96clover%E5%90%AF%E5%8A%A8%E9%A1%B9-clover%20configurator.png" width="70%" height="30%" />

打开就行了，在工具的左边，找到` boot `选项卡，其中` Default boot volume `是默认启动分区，你可以填写分区的名称或者其他的类似` LastBootedVolume `（这些在clover的帮助文档中找到）
勾选` NoearlyProgress `可以关机clover的欢迎界面  

<img src="http://ozkg680jm.bkt.clouddn.com/%E4%B8%AA%E6%80%A7%E5%8C%96clover%E5%90%AF%E5%8A%A8%E9%A1%B9-boot%20volume.png" width="70%" height="30%" />

在左边的` GUI `选项卡中，` Hide Volume `中填写你想隐藏的启动项；   
<img src="http://ozkg680jm.bkt.clouddn.com/%E4%B8%AA%E6%80%A7%E5%8C%96clover%E5%90%AF%E5%8A%A8%E9%A1%B9-hide%20volume.png" width="70%" height="30%" />  
在` Custom Entries `中添加：  
<img src="http://ozkg680jm.bkt.clouddn.com/%E4%B8%AA%E6%80%A7%E5%8C%96clover%E5%90%AF%E5%8A%A8%E9%A1%B9-macOS.png" width="70%" height="30%" />  
其中macOs中只要在` Volume `中选择macOS安装分区，类型选择OS X就行，而Windows和Ubuntu则不同，` Volume `中选择Esp分区，` Path `中填写启动项的绝对路径，类型选择对应的Windows和Ubuntu。   
<img src="http://ozkg680jm.bkt.clouddn.com/%E4%B8%AA%E6%80%A7%E5%8C%96clover%E5%90%AF%E5%8A%A8%E9%A1%B9-ubuntu.png" width="70%" height="30%" />     
<img src="http://ozkg680jm.bkt.clouddn.com/%E4%B8%AA%E6%80%A7%E5%8C%96clover%E5%90%AF%E5%8A%A8%E9%A1%B9-windows.png" width="70%" height="30%" />    

勾选` Title `，填写的名称就是你想个性化的启动项的名称，` Image `中填写图标的绝对路径，如果不想个性化启动项图标可以不用管它，个性化教程大概就是这样，如果有疑问可以联系我。   

一首周二珂的告白气球：

<iframe type="music" frameborder="no" border="0" marginwidth="0" marginheight="0" width=330 height=86 src="//music.163.com/outchain/player?type=2&id=440241144&auto=1&height=66"></iframe>  
