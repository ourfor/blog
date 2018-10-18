---
title: 安装配置WordPress
date: 2018-10-18 13:01:10
tag: [Linux,php,WordPress]
categories: "Blog"
src: //i.loli.net/2018/10/18/5bc8476d6fa28.png
---
好久没玩过` WordPress `了，最近同学搞了个技术网站，顺便想搭个博客，同学不太熟悉` MarkDown `和` HTML `，我目前的这些网站绝大部分是静态的页面，之前也用过` WordPree `和` Typecho `，用不习惯，昨天搭了一下，还是那些常见的问题，随手记录一下。
<!--more-->

# 安装LNMP环境
[WordPress](https://wordpress.org)是使用` PHP `语言开发的博客平台，对于` .php `浏览器无法直接打开，这就需要服务器有` PHP `的语言环境了，同时访客在站点的资料和信息会保存到数据库里面，在互联网中要访问到该站点还得用到http服务软件。

需要安装的软件：
- [x] PHP环境(php)
- [x] 数据库(Mysql)
- [x] http服务软件(Nginx或Caddy)

> P、M、N都有了，那L是指什么？**L**就是Linux啊😥️

安装LNMP环境，为了避免不必要的麻烦，这里我在` Vultr `新开一台机房位于` 洛杉矶 `的服务器：
![系统选择的是CentOS 7](https://i.loli.net/2018/10/18/5bc8186a14543.png)
等待系统安装好以后，我们就可以查看主机的详细信息了
![主机信息](https://i.loli.net/2018/10/18/5bc81938298cc.png)
有几项关键信息：
- 主机` IP `(也就是公网ip)
- ROOT用户的密码
在连接主机之前，我们先来测试下访问主机的速度，打开` Terminal `或着` 命令提示符 `，使用如下命令:
```bash
ping 207.246.108.54 #ping后面接你主机的ip地址
```
此处略过一些特殊问题，比如ping不通等等，与本教程无关，不参与讨论
---

下面就是连接我们的主机了，` SSH `连接服务器，` Windows `下面建议使用` XShell `的家庭版(免费的)，` Unix/Linux `不需要而外安装软件，` Android `的话建议使用` Termux `安装***openssh***

- 在` Terminal `下面连接🔗️主机

```bash
ssh root@207.246.108.54 #用法 ssh 用户名@ip地址
sudo passwd root  #更改root密码，这vultr的密码设的也太复杂了吧

```
![更改root密码](https://i.loli.net/2018/10/18/5bc81ccd6bf66.png)
安装一些常用的软件和编译器

```bash
sudo yum install -y git make curl wget vim nmap screen vim gcc 
```

由于使用源码编译安装，安装时间比较长，使用` screen `开启一个` session `这样即使退出终端，服务器的编译安装也会继续进行：
```bash
screen -S install_lnmp #创建名为install_lnmp的session
```

这里使用一键安装脚本简化安装教程：
```bash
wget http://soft.vpser.net/lnmp/lnmp1.5.tar.gz
tar -xvf lnmp1.5.tar.gz
cd lnmp1.5
./install.sh
```
这时候你就可以断开与服务器的连接了，约莫1个小时左右的样子，就能安装好。

约莫过了50分钟了，我看看服务器编译安装好了没有。***ssh***连接服务器后：
```bash
screen -r install_lnmp
```
当你看到下图显示的信息的时候就说明，我们的` LNMP `已经安装好了
![安装完毕](https://i.loli.net/2018/10/18/5bc8313e29c51.png)
按下` Ctrl + c `退出。


> 如果你已经安装好了` PHP环境 `和` MySql数据库 `的话，那么就可以跳过此部分

# 下载安装WordPress
- [WordPress](https://cn.wordpress.org/)
```bash
wget https://cn.wordpress.org/wordpress-4.9.4-zh_CN.tar.gz #下载最新简体中文版
tar -xvf wordpress-4.9.4-zh_CN.tar.gz   #解压
mkdir /home/wwwroot  #在home目录下面创建一个网站的根目录，方便管理
mv wordpress /home/wwwroot/  #将博客网站的根目录一到wwwroot目录下
```

# 安装Caddy作为http服务软件
Q: 你为什么不用` Nginx `或者` Apache `这些老牌的***http***软件呢？
A: 主要是我懒，懒得配置这两个软件了，还有就是，` caddy `还是有很多优势的，体积小，很方便的

Q: 我就要用` Nginx `或许` Apache `，你用的这个软件和我的软件会冲突的吧，一个端口只能有一个守护进程吧，那这个软件怎么工作呢？
A: 我只是搭着玩一玩，我配置下` Caddy `不占用***443***和***80***这两个端口不就🐷️好了。

1. 安装` Caddy `
- 可以去官网下载二进制文件，不过` YUM `源里面有这个软件，直接通过源安装。

```bash
sudo yum install -y caddy vim #vim等下要用到
```

接下来就是配置我们的` caddy `了。首先我们切换到` /home/wwwroot `目录下，新建一个配置文件的目录。
```bash
cd /home/wwwroot
mkdir caddy_config
cd caddy_config
vim Caddyfile      #按下i插入字符
```

Caddyfile内容：
```bash
207.246.108.54:1018 {
	root /home/wwwroot/wordpress
	timeouts 10m
    gzip
    fastcgi / 127.0.0.1:9000 php
	tls ourfor@foxmail.com  #公网ip这一行不要
}
```
- ` 207.246.108.54 `是你的公网ip
- root ` /home/wwwroot/wordpress `是我们网站根目录的路径，注意，wordpress下面一定是一些` .php `的文件
- ` 1018 `是你想打开的端口，如果有其他进程占用此端口，你更换一个就是了
- tls ` ourfor@foxmail.com `是你想申请***SSL***证书的邮箱，如果是公网ip，那么这一行就别填了

粘贴进Caddyfile后，按下` ESC `，键入` ZZ `保存退出

接下来，我们就可以来部署` WordPress `了。

---
首先我们为` WordPress `创建一个数据库，为方便管理我就起名为` wordpress `.
```bash
mysql -u root -p  #接下来会让你输入命令
create DATABASE wordpress;  #注意有个分号，这是一条语句
exit   #退出
```
![创建数据库](https://i.loli.net/2018/10/18/5bc834cf05557.png)

接下来我们还要让` PHP `监听` 9000 `端口，这个` 9000 `端口我们在caddy的配置文件里面有用到，区别你网站占用的端口。

首先我们来查找一下` php-fpm `的配置文件：
```bash
find / -name "php-fpm.conf" #我这里是在/usr/local/php/etc/这个目录下面
vim /usr/local/php/etc/php-fpm.conf
```
光标移动到这一行
```bash
listen = /tmp/php-cgi.sock
```
按下` o `,在下面添加这一行：
```bash
listen = 127.0.0.1:9000
```
同样按下` ESC `后，使用大写的` ZZ `保存退出。更改了配置文件，需要重启下php：
```bash
systemctl restart php-fpm
```
![重启php-fpm](https://i.loli.net/2018/10/18/5bc8393a9cb1a.png)

接下来我们就得来打开http服务软件了。我们先来放行我们博客占用的端口，你关闭下防火墙也行。

- 关闭防火墙吧，这个简单😿️

```bash
systemctl stop firewalld
```
- 打开` caddy `

```bash
cd /home/wwwroot/caddy_config   #进入我们为caddy配置的目录
caddy 
```
不出意外，我们打开终端显示的网站，就能看到` WordPress `的设置页面。
![WordPress](https://i.loli.net/2018/10/18/5bc83bfeed7f1.png)
按照之前我们配置的填写就行了。
![配置信息](https://i.loli.net/2018/10/18/5bc83c37b31ed.png)
不出意外，它会来到这个页面。这是由于这个目录权限的问题，需要手动操作一下。
按下` Ctrl + z `，暂停我们的caddy，来到博客的根目录下(即wordpress下面)。
```bash
vim wp-config.php
```
按下` i `插入，将提示的信息粘贴，保存退出(方法同上)。使用` fg %1 `来恢复我们的caddy。

安装成功了，会出现下面的图片。
![安装成功了](https://i.loli.net/2018/10/18/5bc83f426da7c.png)

到这里，你以为就成功了？
我们还得添加一个` ftp `的账户，用来安装主题插件。使用之前的一键安装脚本下面的`pureftpd.sh `来安装

```bash
wget http://soft.vpser.net/lnmp/lnmp1.5.tar.gz
tar -xvf lnmp1.5.tar.gz
cd lnmp1.5
./pureftpd.sh
```
![目录最好填博客的根目录](https://i.loli.net/2018/10/18/5bc84407af56f.png)

填上你的帐号密码;
![ftp](https://i.loli.net/2018/10/18/5bc8444bc6b3b.png)

更改一下` wp-content `这个目录的权限，让` WordPress `可以写入。
```bash
chomd -R 777 wp-content  #在wordpress目录下执行
```

最后就是用screen为caddy创建一个` session `就可以断开和服务器的连接了。

<h1> Enjoy it !


