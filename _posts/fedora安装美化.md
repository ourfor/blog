---
title: Fedora安装美化
date: 2018-10-07 21:24:56
tags: [Linux,Fedora]
src: //i.loli.net/2018/10/07/5bba1390d7003.jpg
---
上操作系统的课，这老师非得装Linux，说起Linux,从初三那年我有一台笔记本开始，那笔记本安装Windows，真是没意思😞️，我就装了ubuntu，那时候Linux的distribution都玩遍了，那时候觉得deepin和elementory os的ui还可以，后来我才明白那时候是真的傻啊。不过玩了这么久的linux，还是只喜欢RPM系的和gnome这个桌面。好久没用没在笔记本💻️上面装linux了，是觉得OS X和Windows以及一台Fedora的服务器已经够用了。

<!--more-->
![稳定强大](https://i.loli.net/2018/10/07/5bba12ea4c4d9.png)

# 下载安装镜像
- [官网](https://getfedora.org/zh_CN/)下载

![Fedora 28](https://i.loli.net/2018/10/07/5bba12ea4ffcb.png)

# 将安装镜像刷入到u盘

## 烧录镜像到u盘
- 使用dd命令(macOS和Linux)
插入😎️U盘，查看分区` diskutil list `,如图，我的u盘被系统挂载到了***/dev/disk3***,现在要先卸载它，不然等下写盘的时候会提示设备忙的，` diskutil unmountDisk /dev/disk3 `,好了，准备好你的镜像文件，键入如下命令：

```bash
sudo dd if=/path/to/imagefile of=/dev/disk3 bs=4m  #注意if是input file 的意思，of是out put 的意思，这里在键入if=后，将你的镜像文件拖入终端，of=后面接你要操作的磁盘，即我们的u盘
```
![卸载磁盘并烧录镜像](https://i.loli.net/2018/10/09/5bbcb0535c3f6.png)
由于没用加参数，所以在整个写入过程中不会有任何提示
![写入完毕](https://i.loli.net/2018/10/09/5bbcb01f4efb9.png)

- 使用第三方工具
这里推荐使用开源软件` etcher `,它支持的平台范围很广，包括` OS X `、` Linux `和` Windows `,[官网地址](https://etcher.io)

## 免u盘安装(仅Windows下)
- (免u盘)新建分区，fat32，将镜像文件解压到该分区，添加引导

# 开始安装，设置挂载点

- 设置引导分区
- 设置根分区

>注意：但凡有修改源安装软件的在操作,在修改源之后都需要使用` sudo dnf update `更新,不然包管理工具会找不到软件的.

# 装机必备软件

首先，更新下系统(建议)
![Update System](https://i.loli.net/2018/10/09/5bbcb11ed94c8.png)
如果太大了，也没必要安装。
![更新](https://i.loli.net/2018/10/09/5bbcb1775d11a.png)
保持一颗平常心，你需要耐心等待。
![喝杯茶，回来](https://i.loli.net/2018/10/09/5bbcb1baec65a.png)

- some useful software
```bash
sudo dnf install vim git zsh curl screen wget nmap -y
```
![常用软件](https://i.loli.net/2018/10/09/5bbcb21d09cca.png)

- google-chrome
```bash
sudo dnf install fedora-workstation-repositories
sudo dnf config-manager --set-enabled google-chrome
sudo dnf update
sudo dnf install google-chrome-stable #如果找不到包，退出当前shell重试安装
```

![最好的浏览器，没有之一](https://i.loli.net/2018/10/09/5bbcb65c583db.png)

# 安装主题管理器
- gnome tweak tool
```bash
sudo yum -y install gnome-tweak-tool
```

# 图标主题更改
- paper图标
```bash
sudo dnf config-manager --add-repo https://download.opensuse.org/repositories/home:snwh:paper/Fedora_25/home:snwh:paper.repo
sudo dnf install paper-icon-theme
```

- papirus图标
```bash
wget -qO- https://raw.githubusercontent.com/PapirusDevelopmentTeam/papirus-icon-theme/master/install.sh | sh
```

![papirus icon](https://i.loli.net/2018/10/09/5bbcb248b346d.png)
- materia主题 
```bash
sudo dnf copr enable tcg/themes
sudo dnf install materia-theme
```

![materia theme](https://i.loli.net/2018/10/09/5bbcb3ce63367.png)

在优化(gnome-tweak)中应用图标和主题
![应用图标和主题](https://i.loli.net/2018/10/09/5bbcb34e27dd1.png)

# 更换Shell
- Zsh
自带的` bash `功能没有那么强大，这里推荐安装zsh，` zsh `不仅功能强大，而且插件丰富，主题也特别多。
```bash
sh -c "$(curl -fsSL https://raw.githubusercontent.com/robbyrussell/oh-my-zsh/master/tools/install.sh)"
```

- powerline

```bash
git clone https://github.com/jeremyFreeAgent/oh-my-zsh-powerline-theme.git powerline-theme
cd powerline-theme;./install_in_omz.sh
```

powerline还可以，不过感觉没powerlevel9k功能强大

- powerlevel9k
作为一款` zsh `的主题，自定义功能极强，在github上面收获6k+的小星星。

![powerlevel9k](https://i.loli.net/2018/10/09/5bbcb7febebc3.png)
![Fedora更换Terminal字体](https://i.loli.net/2018/10/09/5bbcb4f5a0893.png)


桌面环境美化后的效果。
![最终美化效果](https://i.loli.net/2018/10/09/5bbcb553bf1a9.png)
# Vim插件安装
- Airline
- 插件管理系统

# 更换引导程序
- clover引导

![Clover引导](https://i.loli.net/2018/10/07/5bba0b1c88f57.png)
![OS X](https://i.loli.net/2018/10/07/5bba0b1b776d3.png)
![没有fedora的图标，我换成freebsd的图标了](https://i.loli.net/2018/10/07/5bba0b1bcdd74.png)

<!--
https://i.loli.net/2018/10/07/5bba0b1b776d3.png
https://i.loli.net/2018/10/07/5bba0b1bcdd74.png
https://i.loli.net/2018/10/07/5bba0b1c88f57.png
https://i.loli.net/2018/10/07/5bba12ea4c4d9.png
https://i.loli.net/2018/10/07/5bba12ea4ffcb.png
https://i.loli.net/2018/10/07/5bba1390d7003.jpg


-->





