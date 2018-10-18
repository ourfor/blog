---
title: 初尝Typecho
date: 2018-07-20 16:34:37
tags: [VPS,Typoche]
categories: "Blog"
---
昨天笔记本重装10.13不小心把博客的源代码删了，虽然我有保存有多个副本，但是最近的一次副本保存在机械硬盘里面的，而这机械硬盘我放在宿舍没拿回家，所以我就暂时没有去碰服务器和Coding上面的` HTML源码 `，但是我也不能闲着啊，毕竟有两个月的时间在家，除了平时的笔记push到` Github `仓库之外，我还会把一些东西记录下来，也是一个偶然的机会发现了 ***Typecho***，原本是在应用商店里面看` Rime输入法 `，无意中点进去一个博客，发现底部的博客框架是` Typecho `，点进去就来到了[Typecho官网](http://typecho.org/),反正我也闲来无事，就搭一个耍耍，顺便记录下来，可能会帮到搭建遇到问题的人。
<!--more-->



# 初识Typecho
- 这` Typecho `究竟是什么博客框架？
这个博客框架和` WordPress `一样属于动态博客框架，之前有看过我写的[hexo+github/coding搭建个人博客](https://blog.ourfor.top/2018/03/06/hexo-github-coding%E6%90%AD%E5%BB%BA%E4%B8%AA%E4%BA%BA%E5%8D%9A%E5%AE%A2/)就知道这二者的区别。

其实二者最本质的区别就是对[编辑语法]的支持以及[环境的依赖]。如果你跟喜欢Word文档或者Powerpoint式的写作，那么我并不推荐你使用静态博客，也就是` HTML语法 `的网页，` PHP语法 `更适合你。所以二者环境的区别就是是否需要安装` Php `和` Mysql数据库 `，这里不深入展开讨论，回归正题，` Typecho `有哪些优点呢？官网首页这样写到：

- 轻量高效 仅仅 7 张数据表，加上不足 400KB 的代码，就实现了完整的插件与模板机制。超低的 CPU 和内存使用率，足以发挥主机的最高性能。

- 先进稳定 原生支持 Markdown 排版语法，易读更易写。支持 BAE/GAE/SAE 等各类云主机，即使面对突如其来的高访问量，也能轻松应对。

- 简洁友好 精心打磨过的操作界面，依然是你熟悉的面孔，更多了一份成熟与贴心。每一个像素的剪裁，都只为离完美更进一步。

我补充几点：

- 丰富的主题及插件 你可以上` Github `上面搜索 ***Typecho***,你就会发现很多精美的开源主题和异常丰富的插件，此外原生支持评论，这类动态博客都可以这web端随时随地管理，同样缺点也很明显，文章不利于保存，还得拥有一台有公网IP的主机。

- 用户量还算比较多 据说有500,000 用户。

>建议还算适当的掌握 ***MarkDown语法*** 和一些简单的 ***HTML语法***，虽然此框架不要求。

# 搭建环境

昨天我在Vultr上面的服务器上面搭建好了，今天我就以` 树莓派 `上面的` CentOS `为例，下面👇🏻贴出我的详细配置：

```bash
Last login: Fri Jul 20 15:40:12 2018 from 192.168.1.174
Nice To Meet You!
                 ..                    root@localhost.localdomain
               .PLTJ.                  --------------------------
              <><><><>                 OS: CentOS Linux 7 (Core) armv7l
     KKSSV' 4KKK LJ KKKL.'VSSKK        Host: Raspberry Pi 3 Model B
     KKV' 4KKKKK LJ KKKKAL 'VKK        Kernel: 4.14.52-201.el7.armv7hl
     V' ' 'VKKKK LJ KKKKV' ' 'V        Uptime: 12 hours, 22 mins
     .4MA.' 'VKK LJ KKV' '.4Mb.        Packages: 468 (rpm)
   . KKKKKA.' 'V LJ V' '.4KKKKK .      Shell: zsh 5.0.2
 .4D KKKKKKKA.'' LJ ''.4KKKKKKK FA.    Terminal: /dev/pts/0
<QDD ++++++++++++  ++++++++++++ GFD>   CPU: Generic DT based system (4)
 'VD KKKKKKKK'.. LJ ..'KKKKKKKK FV     Memory: 173MiB / 974MiB
   ' VKKKKK'. .4 LJ K. .'KKKKKV '
      'VK'. .4KK LJ KKA. .'KV'
     A. . .4KKKK LJ KKKKA. . .4
     KKA. 'KKKKK LJ KKKKK' .4KK
     KKSSA. VKKK LJ KKKV .4SSKK
              <><><><>
               'MKKM'
                 ''
```
首先安装` lnmp环境 `，由于安装` lnmp `并不是本文的重点，你可以去官网下载源码编译安装，也可以在仓库安装，为了节约时间，这里使用一键安装脚本。
一键安装脚本[官网](https://lnmp.org/download.html),这里提供` version=1.5 `的在线安装脚本[下载链接](http://soft.vpser.net/lnmp/lnmp1.5.tar.gz)

ssh接入服务器，键入如下命令：
```bash
wget http://soft.vpser.net/lnmp/lnmp1.5.tar.gz
tar -xvf lnmp1.5.tar.gz     #解压压缩文件，会生成一个名为lnmp1.5的目录，可以通过ls查看
cd lnmp1.5          #进入解压后的文件夹
yum install -y screen   #安装screen，让脚本后台安装
screen -S Install_lnmp  #创建一个名为Install_lnmp的session。
./install.sh   #执行安装脚本
```

执行安装脚本后它会提示你安装哪个版本，你可以直接回车，当然🙄️也可以按照自己的喜好安装，不过安装Mysql时会让你创建数据库` root `用户的密码，记住此密码待会有用到。此时你只需要等待它安装完毕即可。

```bash
PHP: OK
PHP-FPM: OK
Clean src directory...
+------------------------------------------------------------------------+
|          LNMP V1.5 for CentOS Linux Server, Written by Licess          |
+------------------------------------------------------------------------+
|           For more information please visit https://lnmp.org           |
+------------------------------------------------------------------------+
|    lnmp status manage: lnmp {start|stop|reload|restart|kill|status}    |
+------------------------------------------------------------------------+
|  phpMyAdmin: http://IP/phpmyadmin/                                     |
|  phpinfo: http://IP/phpinfo.php                                        |
|  Prober:  http://IP/p.php                                              |
+------------------------------------------------------------------------+
|  Add VirtualHost: lnmp vhost add                                       |
+------------------------------------------------------------------------+
|  Default directory: /home/wwwroot/default                              |
+------------------------------------------------------------------------+
|  MySQL/MariaDB root password: 2320813747                          |
+------------------------------------------------------------------------+
+-------------------------------------------+
|    Manager for LNMP, Written by Licess    |
+-------------------------------------------+
|              https://lnmp.org             |
+-------------------------------------------+
nginx (pid 24643 24642 24641 24640 24639) is running...
php-fpm is runing!
 SUCCESS! MySQL running (25190)
Active Internet connections (only servers)
Proto Recv-Q Send-Q Local Address           Foreign Address         State
tcp        0      0 127.0.0.1:25            0.0.0.0:*               LISTEN
tcp        0      0 0.0.0.0:3306            0.0.0.0:*               LISTEN
tcp        0      0 0.0.0.0:80              0.0.0.0:*               LISTEN
tcp        0      0 0.0.0.0:22              0.0.0.0:*               LISTEN
tcp6       0      0 :::22                   :::*                    LISTEN
Install lnmp takes 162 minutes.
Install lnmp V1.5 completed! enjoy it.​
```
显示此信息就说明安装完毕，其中上面的` 0.0.0.0:3306 `中的 ***3306*** 是Mysql默认监听的端口，` 0 0.0.0.0:80 `中的` 80 `是` Nginx `占用的端口。如后续使用` Caddy `就可以停用` Nginx `。

## 网站根目录
这里安装的` lnmp `是默认把` /home/wwwroot `作为主机的目录。以后添加目录以后都会在这里相应的创建文件夹方便管理。

- 添加虚拟主机

使用命令` lnmp vhost add `添加虚拟主机目录，其中：

|Q|A|
|:-:|:-:|
|Please enter domain(example: www.lnmp.org): |填写你的域名，同时dns解析到服务器ip|
|Enter more domain name(example: lnmp.org .lnmp.org):|保存默认，回车即可|
|Default directory: /home/wwwroot/share.ourfor.top:|回车|
|Allow Rewrite rule? (y/n)|y|
|Enable PHP Pathinfo? (y/n)|y|
|Allow access logs (y/n)|y|
|Add SSL Certificate (y/n)|y|
|1.: Use your own SSL Certificate and Key 2.: Use Let's Encrypt to create SSL Certificate and Key|建议使用2，自动添加https证书|


接下来它会自动开始配置，当提示此信息我们就可以进行下一步了。

```bash
================================================
Virtualhost infomation:
Your domain: share.ourfor.top
Home Directory: /home/wwwroot/share.ourfor.top
Rewrite: other
Enable log: yes
Create database: no
Create ftp account: no
Enable SSL: yes
  =>Let's Encrypt
================================================
```
>如果你使用的是VPS，这里忽略


其中由于现在我用的是树莓派，没有做内网穿透，没有公网ip，所以我得修改nginx的配置才能在局域网中访问树莓派。
使用 ***find***命令搜索🔍️配置文件` find / -name nginx.conf `,搜索结果显示我的配置文件在:` /usr/local/nginx/conf/nginx.conf `,使用vi编辑` vi /usr/local/nginx/conf/nginx.conf `将其中的:
```bash
listen 80 default_server;
         #listen [::]:80 default_server ipv6only=on;
         server_name _;
         index index.html index.htm index.php;
         root  /home/wwwroot/default;
```
改为：
```bash
listen 80 default_server;
         #listen [::]:80 default_server ipv6only=on;
         server_name _;
         index index.html index.htm index.php;
         root  /home/wwwroot/share.ourfor.top;
```
其中` /home/wwwroot/share.ourfor.top `就是上文我们添加的网站目录，按照你添加的修改，使用` lnmp restart `重启***Nginx***使配置生效，那么接下来我们就可以去官网下载源码了。

---

### 开始安装


- 下载源码
```bash
wget http://typecho.org/downloads/1.1-17.10.30-release.tar.gz&&tar -xvf 1.1-17.10.30-release.tar.gz
```
- 移动到网站根目录
```bash
mv build/* /home/wwwroot/share.ourfor.top/ #也就是上文的网站根目录，按照实际情况修改
```

- 创建一个名为typecho的数据库
```bash
mysql -u root -p   #回车，接下来输入之前创建root用户所设置的密码
#password
create DATABASE typecho; #创建名为typecho的数据库
exit  #退出，保存。
```

接下来就可以打开域名或者局域网ip(树莓派)了，这时候如果打开Dashboard(控制面板)出现没有权限或者` Not Found `的话，就需要修改` php.ini `,同样使用find命令搜索` find / -name php.ini `,使用vi编辑，键入` /cgi.fix_pathinfo `，查找字符，将` cgi.fix_pathinfo=0 `改为` cgi.fix_pathinfo=1 `,随后重启php,` lnmp restart `


- 常见问题：[官方帮助文档](http://docs.typecho.org/faq)
---

- 未监听9000端口
在php配置文件（一般应该是叫` php-fpm.conf `）中添加：
```bash
listen = /tmp/php-cgi.sock  #一般有，这一段不用添加，只是定位
listen = 127.0.0.1:9000
```

使用` Caddy `代替` Nginx `作为 ***Http*** 服务器(推荐)，相比之前的步骤，使用` Caddy `则相对比较简单，首先去官网下载` Caddy `，
- [Caddy](https://caddyserver.com/)优势：
  - [x] 自动签发 HTTPS
  - [x] 目录浏览界面美观强大
  - [x] 容易上手，插件众多，官方文档介绍详细

这里我选择了几个实用的插件：
1. http.cache
2. http.filemanager
3. http.filter
4. http.git 
5. http.jekyll 
6. http.locale   
7. http.login  
8. http.upload 
9. http.webdav  
10. tls.dns.vultr

按照自己的需要选择，这里将` caddy `下载解压后的文件放到` /home/wwwroot `下，方便管理网站，并在该目录下创建一个名为` Caddyfile `的文件

```bash
blog.ourfor.top:443 {
	root /home/wwwroot/blog.ourfor.top/
	timeouts 10m
        gzip
        fastcgi / 127.0.0.1:9000 php
	tls 2320813747@qq.com
}
```

#### 说明

- ` blog.ourfor.top:443 `域名以及端口，其中` http为80 `而` https为443 `
- ` root /home/wwwroot/blog.ourfor.top/ `网站根目录路径



---
主题推荐：
- [life](https://github.com/WeicMa/Typecho-Theme-Life)
- [pinghsu](https://github.com/chakhsu/pinghsu.git)
- [lpisme](https://github.com/chakhsu/lpisme.git)
- [next](https://github.com/zgq354/typecho-theme-next)
- [jianshu](https://github.com/jiangmuzi/jianshu.git)



插件推荐：



<link rel="stylesheet" href="https://cdn.jsdelivr.net/npm/aplayer@1.10/dist/APlayer.min.css">
<script src="https://cdn.jsdelivr.net/npm/aplayer@1.10/dist/APlayer.min.js"></script>

<div class="aplayer"
    data-id="4220599045"
    data-server="tencent"
    data-type="playlist">
</div>

<script src="https://cdn.jsdelivr.net/npm/meting@1.2/dist/Meting.min.js"></script>

















# 相关文档
- [最快的 Hexo 博客搭建方法](https://blog.coding.net/blog/CS-Hexo?utm_source=newsletter&utm_medium=email&utm_campaign=monthly&utm_content=2018-04)

>这个是Coding发给我的电子邮件里面附上的，很少用` Cloud Studio `，不过看了它的教程似乎还行，当然仅作参考

- [Cloud Studio 部署 WordPress 示例](https://coding.net/help/cloud-studio/wordpress)

>这个可以在` 最快的 Hexo 博客搭建方法 `里面找到

- [hexo+github/coding搭建个人博客](https://blog.ourfor.top/2018/03/06/hexo-github-coding%E6%90%AD%E5%BB%BA%E4%B8%AA%E4%BA%BA%E5%8D%9A%E5%AE%A2/)

>😥️这个是我写的
