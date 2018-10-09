---
title: hexo个人博客
date: 2018-03-06 19:16:21
tags: [github,hexo,coding]
categories: "blog"
src: hexo+github.jpg
---
常见的博客系统有简书、新浪博客等等然而这些大多是使用官方域名，博客样式也比较单一，优点是容易上手，不必太注重编辑语法，缺点是博客的样式比较单一，无法使用自己的域名，同时也就意味访问量注定不高，随着QQ空间、微信朋友圈的流行，人们对博客的浏览也越来越少，然而QQ空间、微信朋友圈大多以生活记录、趣事分享为主，虽然微信公众号经常会发布一些资讯、技术帖，然而微信客户端的限制注定无法满足人们的需要，仅仅从经验分享、交流而言。博客还是有存在的必要的。
<!--more-->

## 胡说八道

> 我为什么搭建博客？为什么不是WordPress而是Hexo？   

21世纪是信息时代，这年头谁没有个QQ空间、微信朋友圈，你又是否觉得微信朋友圈、QQ空间并不是一个想说什么就能说的地方，QQ空间随处可见的广告，朋友圈的矫情，当浅尝辄止成为思维定式，急功近利成为文化景象，喧嚣肤浅成为人们喜闻乐见的行为方式时，人们势必难以用心而行，无法静下心来。浮躁是这个时代的集体病症，生活中充斥着QQ空间、微信朋友圈的无病呻吟。是否还能有一个地方能个静下心来研究高深之学问，我想大概就只有博客了吧。你可以用博客来分享经验、记录。总之，在这里你说了算。搭建个人博客系统，无需购买云主机，避免WordPress的繁琐与臃肿，0基础上手，(未完待续)

|type|advantages|disadvantages|
|:-:|:-:|:-:|
|WordPress|可以更加专注于写作，媒体资源可以储存在主机上|需要主机、公网IP以及LNMP/LAMP环境，同时具备一定的建站基础|
|Hexo|无需主机（相对而言）以及公网IP同时提供二级域名，比较稳定|使用MarkDown纯文本语法写作兼容HTML，媒体资源一般使用外链|

虽然你可以在路由器上面跑` WordPress `,前提是你对*Linux*比较熟悉同时有宽带运营商提供固定的公网IP，公网IP资源相对比较匮乏，直接购买比较昂贵，向宽带运营商索要是不错的选择。当然如果你经常使用` Shadowsocks `(酸酸乳)的话，直接搭载同一台主机上面就行了，这样不至于性能过剩。而Hexo搭建静态博客是使用了` Github `和` Coding `提供的***Pages***服务，这个是比较稳定的，***Github***作为全球最大的开源社区，安全性和稳定性肯定不用担心，我们使用的*Pages*服务仅仅是[Github](https://github.com/)的冰山一角而已，或许从搭建blog以后你就会感受到Github的魅力。   


## 必备组件  
- [Git](https://git-scm.com/) 
- [Node.js](https://nodejs.org/en/)   

> Notice: 根据你使用的操作系统下载安装对于的版本即可，Linux和macOS可以通过命令行安装，对于macOS，安装包管理软件之后就可以通过源安装，对于新手不推荐使用这种方式，因为可能会用到root权限，这样以后生成、部署就比较麻烦。如果从来没有用过命令行，建议了解一下通配符。   

#### Linux下安装`git`和`Node.js`
通过下面命令安装
```bash
sudo apt-get update      #检查更新
sudo apt-get install git    #安装Git
sudo apt-get install nodejs    #安装nodejs
```

估计用` Linux `的用户应该看看官方的说明文档就会了。所以下面以` Windows `和` macOS `为例。其中macOS可以安装包管理软件来安装必须组件，例如MacPorts，Homebrew，Fink。     

#### git、Node.js下载 
Windows、macOS通过下载安装包安装     
下面链接均为64位系统长期支持版本。32位系统[点击这里](https://nodejs.org/en/download/)       
> Node.js
* [macOS Installer (.pkg)](https://nodejs.org/dist/v8.10.0/node-v8.10.0.pkg)
* [Windows Installer (.msi)](https://nodejs.org/dist/v8.10.0/node-v8.10.0-x64.msi) 

> Git   
- [macOS](https://sourceforge.net/projects/git-osx-installer/files/git-2.16.2-intel-universal-mavericks.dmg/download?use_mirror=autoselect)
- [Windows](https://github.com/git-for-windows/git/releases/download/v2.16.2.windows.1/Git-2.16.2-32-bit.exe) 

#### macOS通过brew安装
macOS可以使用上面的方法下载安装包安装，而我更喜欢通过` brew `和` command line `安装，使用这种方法安装，你必须先安装包管理软件` brew `:


```bash
/usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
```
安装好` brew `后，键入以下命令：
```bash
brew install git         #安装git
brew install nodejs      #安装Node.js
```

## 安装Hexo   

```bash
npm install hexo-cli -g     #安装Hexo
hexo init blog              #初始化博客
cd blog                     #进入博客根目录
npm install                 #安装hexo到博客根目录
```
(未完待续)
## 高清重置

由于学习和工作的需要，大部分同学使用的是` Windows ` 操作系统，所以` Linux ` 和 ` macOS ` 就先不写了，我在虚拟机里面安装了` Windows10 ` 所以下面以` Windows ` 为例，来安装` hexo ` 搭建博客。

- [Node.js](https://file.ourfor.top/tools/node-v10.2.0-x64.msi)
- [git](https://file.ourfor.top/tools/Git-2.17.0-64-bit.exe)


你可以到官网下载，不过可能由于` GFW ` 的原因下载比较慢，所以我下载到了服务器，放在了` tools `这个目录里面。[🔧Here](https://file.ourfor.top).下载好这两个软件，安装的时候保存默认就好。

## 安装` hexo `


在` Windows10 ` 的搜索框中查找***Git bash***,或者点击Windows徽键，在最近添加中打开，在` Git bash `键入如下命令：
```bash
pwd                #print working directory显示当前路径。
cd ~/Desktop       #change directory,更改路径切换到桌面。如果提示找不到，那可能要把Desktop改成桌面
mkdir blog         #make directory 新建一个名为blog的文件夹，名字不一定叫blog可以根据你的喜好填写
npm install hexo-cli -g   #安装hexo
hexo -v                #检查是否成功安装hexo，并查看版本信息
hexo init blog         #初始化blog这个文件夹，这个文件夹就是第3条命令创建的文件夹，如果你使用的是其他名称，换成对应的名称即可。
cd blog                #进入blog这个文件夹，和上面一样
npm install            #安装必要插件
hexo generate          #简写hexo g,即渲染并生成HTML页面。
hexo server            #简写hexo s,本地计算机启动服务，如果此时出现nodejs提示的防火墙，允许即可

```

- ` hexo -v `出现如下信息则说明` hexo `安装好了。

```bash
hexo-cli: 1.1.0
os: Windows_NT 10.0.16299 win32 x64
http_parser: 2.8.0
node: 10.2.0
v8: 6.6.346.32-node.8
uv: 1.20.3
zlib: 1.2.11
ares: 1.14.0
modules: 64
nghttp2: 1.29.0
napi: 3
openssl: 1.1.0h
icu: 61.1
unicode: 10.0
cldr: 33.0
tz: 2018c
```



- ` hexo s `输出信息

```bash
INFO  Start processing
INFO  Hexo is running at http://localhost:4000/. Press Ctrl+C to stop.
INFO  Catch you later
```


 

<img src="http://p923bw9fi.bkt.clouddn.com/git_bash.PNG">
博客将会部署到本地，使用` 4000 ` 的端口，在浏览器中打开` http://localhost:4000/ ` 就可以查看博客了。自此我们的hexo就安装好了。

### 远程部署
你逗我的吧，` hexo `就弄好了？那我为什么外网访问不了呢？手机上面也打不开啊！
嗯，***hexo*** 确实已经安装好了，博客也确实安装好了，那么我要怎样才能在外网中访问它呢，同时我又能不能用自己喜欢的域名来访问我的博客呢？


- 什么是域名？
举个简单的例子：
当你在浏览器地址栏中输入` baidu.com `,你的浏览器就会自动打开百度官网，像***baidu.com***这一串就是一个顶级域名，比如我的域名` ourfor.top ` 也是一个顶级域名，而` file.ourfor.top `则是一个二级域名，它是` ourfor.top `的子域名，加了个` file. `，可以这样说只有一个` dot `的就是顶级域名，两个点` . `的就是二级域名，顶级域名拥有对其子域名的管理权。再举个例子,如果你在浏览器中输入` m.baidu.com `,你的浏览器将会访问百度的手机版页面，现在` google `要求强制使用` HTTPS `的协议，当你输入` http//:baidu.com `它会强制跳转到` https `，所以目前大部分网站` https `和` http `没什么区别，所以你在浏览器地址栏中输入网址不需要加协议（https://或者http://）就能打开。

- 说了半天我还是不懂，🤣🤣，好吧其实科普一下就OK，那么这个域名是干什么用的呢？
一般情况下计算机通过` ip `地址来访问服务器，但是通过` ipv4 `来访问网站这样太麻烦了，太难记忆了，极不方便，于是人们便想出通过一串字母（网址）来访问网站。同时使用` DNS `解析到服务器ip，这样当你输入网址后计算机就会访问域名解析的` ip `地址。

你可以按下` win + r(run)`,同时输入` cmd `来打开 ` 命令提示符 `(原谅我Windows的命令懂得不多，Linux和macOS还行😅😅)
```bash
ping baidu.com       #它会检测服务器的ip地址以及响应速度，按住Ctrl + c就可以停止
ping ourfor.top      #我用的是美国🇺🇸的服务器，服务器IP是144.202.15.107
ping file.ourfor.top  #这两个网站我放在同一个服务器上面的，所以IP地址是一样的。 
```

## 更新文章
博客安装好了，我要怎样写文章呢？
所以我们就有必要了解一下blog这个文件夹里面各个部分的作用了。

![blog文件夹🏠](http://p923bw9fi.bkt.clouddn.com/blog.png)
![source文件夹📂](http://p923bw9fi.bkt.clouddn.com/source.png)
![themes文件夹😝](http://p923bw9fi.bkt.clouddn.com/themes.png)

- 文章保存在` source/_posts `里面，是以` .md `结尾的文本文件，你可以用文本编辑器打开编辑它,不过我更推荐你用[Sublime Text 3](https://ourfor.top/2018/03/24/3/)，这个文本文件使用的是` MarkDown `这种轻量级的标记语法，同时兼容` HTML ` ，是***纯文本的***，不像` WordPress `和` PPT `那样，当然这是优点。

- 写第一篇文章
在` Git bash `(注意你得cd到博客根目录下面，即上文的blog文件夹下面) ，输入` hexo new 我的XX `(我的XX-是标题，自拟)
这时候你就可以在` blog/source/_posts `里面看到它，编辑这个文件就OK了。

- 博客部署到远程仓库

如何从外网访问博客呢？其实我们打开的` http://localhost:4000/ `这个网址它的网站根目录是在` blog/public `下面，你可以打开public这个文件夹看看，里面就是网站页面的源码，你可以打开这个` index.html `文件，是不是就是你的博客的主页。只是没有图片而已，所以我们只需要将这个文件夹里面的东西放到一个外网可以访问的地方就行了，好在` hexo `的配置文件里面已经有相关的设置了，我们只需要稍作更改就行了。

首先我们先去` github `或者` coding `注册一个账号。

- [GitHub](https://github.com/)
- [Coding](https://coding.net/)

由于` Github `主机在美国，访问速度可能有点慢，所以你也可以部署到` Coding `，下面以全球最大的开源社区` GitHub `为例(今年是GitHub十周年)。

#### 1.打开[GitHub官网](https://github.com/),点击右上角的` Sign up `注册一个账号。
![Sign up](http://p923bw9fi.bkt.clouddn.com/sing_up.png)
- ` Username `填一个简单一点的英文名，因为以后你的博客就通过` Username.github.io `来访问的，所以起一个好点的、不太长的名字就很有必要了，比如我的这个` Username `是` ourfor `,很短也很好记。

- ` Email address `填个QQ邮箱📮也是OK的啦

- ` Password `这个你懂得😳😳

- ` step2和step3 `这个由于我注册过了，我就没打开看了，你看着填吧。

#### 2.新建一个` Repository `，点击页面上面的` New repository `
![New repository](http://p923bw9fi.bkt.clouddn.com/new_repository.png)
- 这个` Repository name `填` username.github.io `,比如我的就填` ourfor.github.io `.你的根据你的` username `填。
- ` Public `就是这个，点击` Create repository `就可以完成创建。
- ` Description `可选，建议勾选☑️` Initialize this repository with a README `

这时候就会打开仓库主页，依次点击页面右侧的` Clone or download `、` Use SSH `复制框中的` Repo `地址，待会要用。

#### 3.修改配置文件` _config.yml `
用` Sublime Text 3 `或者其他文本编辑器打开博客根目录下面的` _config.yml `文件，在文件末尾，找到：
```bash
# Deployment
## Docs: https://hexo.io/docs/deployment.html
deploy:
  type:

```
改成：
```bash
# Deployment
## Docs: https://hexo.io/docs/deployment.html
deploy:
  type: git
  repo: 
       github: git@github.com:ourfor/ourfor.github.io.git,master
       #coding: git@git.coding.net:ourfor/ourfor.git,master
  branch: master     
  message: blog update
```
上面这个` git@github.com:ourfor/ourfor.github.io.git `是我的仓库的地址,你改成刚才复制的那个就行了，如果你用的是` coding `你可以把` github `这一行用` # `注释掉，去掉` coding `前面的` # `。最后保存更改。

### 4.添加部署密钥.
打开` Git bash `，输入` ssh-keygen -t rsa -C "2320813747@qq.com" `,这个邮箱地址换成你的。连续四次回车就生成了一对密钥。
```bash
Your identification has been saved in /c/Users/zip/.ssh/id_rsa.
Your public key has been saved in /c/Users/zip/.ssh/id_rsa.pub.
```
它会告诉你密钥生成在那个文件夹,上面是我的密钥生成路径，下面要相应替换成你的，使用` cat `来查看公钥内容：
```bash
cat /c/Users/zip/.ssh/id_rsa.pub
```
复制输出的内容，打开` GitHub `，点击页面右侧头像旁边的倒三角，打开` Settings `，在页面左侧的` Personal settings `下面定位到` SSH and GPG keys `这一栏,点击右侧的` New SSH key `来添加一个密钥，其中` Title `随意,` Key `填写上一步` Git bash `里面生成的那个。最后` Add SSH key `就行了。

> 当你写好文章之后,首先得使用` hexo g `来生成，而` hexo s `可以在本地查看实际效果，` hexo d `会自动` push `到远程仓库，你就可以在浏览器地址栏中输入` username.github.io `来访问你的博客` username `是你的***GitHub***用户名。



- 更换主题
是不是觉得默认的` landscape `太单调简洁了？不会前端设计？没关系，GitHub上面有很多开发者为` hexo `设计了许多精美的主题。诸如` Next `、` mellow `等等。
我个人比较喜欢这两个主题：
- [x] [Next](http://theme-next.iissnan.com/getting-started.html) 
- [x] [Mellow](https://github.com/codefine/hexo-theme-mellow/wiki)
上面都有详细的帮助文档，如果看不太懂😭，我们可以一起讨论交流。


- 绑定个性化域名
是不是觉得` username.github.io `这个难记而且那个(😝你懂的)，那么我要怎样获取我喜欢的域名呢？

获取免费域名: [freenom](http://www.freenom.com/)这个网站提供免费的顶级域名包括解析，只不过大多以` tk `结尾。

收费域名: 国内的阿里云、腾讯云啊都有域名服务，有一些域名首年只要` ￥1 `,每年续费好像是7到8元的样子。

```bash
 ____________
< Hello,World >
 ------------
       \   ,__,
        \  (oo)____
           (__)    )\
              ||--|| *


```


<details><summary>千万别看</summary>
![😳😳](http://p923bw9fi.bkt.clouddn.com/lp23.png)

</details>

附上我这篇博客文章的源码，了解一下该怎样写[Click Here](https://file.ourfor.top/ebook/hexo-github-coding%E6%90%AD%E5%BB%BA%E4%B8%AA%E4%BA%BA%E5%8D%9A%E5%AE%A2.md)

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
        src: 'http://p923bw9fi.bkt.clouddn.com/%E5%91%A8%E4%BA%8C%E7%8F%82%20-%20%E5%91%8A%E7%99%BD%E6%B0%94%E7%90%83.wav',
        poster: 'http://p923bw9fi.bkt.clouddn.com/%E5%91%A8%E4%BA%8C%E7%8F%82.jpg',
        name: '告白气球(翻唱)',
        artist: '周二珂'
      }
    ]
  })
</script>

(今晚继续写)

> 梦想是注定孤独的旅行
路上少不了质疑和嘲笑
但那又怎样
哪怕遍体鳞伤
也要活得漂亮
———陈欧



























