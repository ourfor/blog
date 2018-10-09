---
title: Markdown插入视频音频
date: 2018-02-20 13:46:24
tags: [Markdown]
categories:
---
对于部署在代码托管网站上面的静态博客，我们使用Markdown语法编辑文章，对于插入图片、视频和音频，我们不能安装WordPress或者Office办公套件里面那套来，因为这个Markdown写的文章是纯文本的，同样我们也不能把图片、视频音频这些文件放在Github、Coding等代码托管网站（因为容量太小了），所以我们可以利用各大音乐、视频网站的外链播放器，当然有些歌曲视频由于版权问题无法生成外链，我们可以将视频、音频的源文件放在七牛云这类网站的对象存储中，生成外链来播放。  
<!--more-->   
## 利用网易云音乐  
[网易云音乐](https://music.163.com/)中选一首你喜欢的歌，点击生产外链播放器，比如我选的这首李玉刚-刚好遇见你，看了下网址：https://music.163.com/#/song?id=439915614 ，以及生成的外链播放器：

```bash
<iframe type="music" frameborder="no" border="0" marginwidth="0" marginheight="0" width=330 height=86 src="//music.163.com/outchain/player?type=2&id=439915614&auto=1&height=66"></iframe>
```

每首歌的区别在于这个` id `,有些歌曲当你点击生成外链播放器时它提示` 由于版权保护，无法生成外链。 `这时候你就可以替换这个` id `来打破这个限制。    

<iframe type="music" frameborder="no" border="0" marginwidth="0" marginheight="0" width=330 height=86 src="//music.163.com/outchain/player?type=2&id=440241144&auto=1&height=66"></iframe>  

## 安装插件  
Audio： [hexo-tag-aplayer](https://github.com/grzhan/hexo-tag-aplayer)
Video： [hexo-tag-dplayer](https://github.com/NextMoe/hexo-tag-dplayer)

进入博客根目录，打开Terminal或者cmd，使用npm安装：  

```bash
npm install hexo-tag-aplayer
npm install hexo-tag-dplayer
```



### Audio  
根据github项目的说明用法是将下面的代码粘贴到博客文章中你想出现音乐播放器的地方。


```bash
{% aplayer title author url [picture_url, narrow, autoplay, width:xxx, lrc:xxx] %}
```

说明：    
- ` title ` : music title
- ` author `: music author
- ` url `: music file url
- ` picture_url `: optional, music picture url
- ` narrow `: optional, narrow style
- ` autoplay `: optional, autoplay music, not supported by mobile browsers
- ` width:xxx `: optional, prefix width:, player's width (default: 100%)
- ` lrc:xxx: ` optional, prefix lrc:, LRC file url      

{% aplayer "Lovey-Dovey" "T-ara" "http://ozkg680jm.bkt.clouddn.com/T-ara-Lovey-Dovey.flac"  "http://img0.c.yinyuetai.com/artist/fan/150810/0/-M-70f069427cca50778df6b121a8bf5a8a_0x0.jpg" %}   

### Video
方法和Audio的一样也是粘贴在博客文章中。格式用法：     

```bash
{% dplayer key=value ... %}
```

github项目上介绍的：  
key can be    

```bash
dplayer options:
    'autoplay', 'loop', 'screenshot', 'hotkey', 'mutex', 'dmunlimited' : bool options, use "yes" "y" "true" "1" "on" or just without value to enable
    'preload', 'theme', 'lang', 'logo', 'url', 'pic', 'thumbnails', 'vidtype', 'suburl', 'subtype', 'subbottom', 'subcolor', 'subcolor', 'id', 'api', 'token', 'addition', 'dmuser' : string arguments
    'volume', 'maximum' : number arguments
container options:
    'width', 'height' : string, used in container element style
other:
    'code' : value of this key will be append to script tag

```

以及例子： 

```bash
{% dplayer "url=http://devtest.qiniudn.com/若能绽放光芒.mp4" "addition=https://dplayer.daoapp.io/bilibili?aid=4157142" "api=http://dplayer.daoapp.io" "pic=http://devtest.qiniudn.com/若能绽放光芒.png" "id=9E2E3368B56CDBB4" "loop=yes" "theme=#FADFA3" "autoplay=false" "token=tokendemo" %}
{% dplayer "url=http://devtest.qiniudn.com/若能绽放光芒.mp4" "addition=https://dplayer.daoapp.io/bilibili?aid=4157142" "api=http://dplayer.donot.help/dplayerpy" "pic=http://devtest.qiniudn.com/若能绽放光芒.png" "id=2622668" "loop=yes" "theme=#FADFA3" "autoplay=false" "width=233px" %}
{% dplayer 'url=some.mp4' "id=someid" "api=https://api.prprpr.me/dplayer/" "addition=/some.json" 'code=player.on("loadstart",function(){console.log("loadstart")})' "autoplay" %} 
```

{% dplayer "url=http://ozkg680jm.bkt.clouddn.com/T-ara%20-%20TIAMO.mp4" "api=http://dplayer.daoapp.io" "pic=http://img0.c.yinyuetai.com/artist/fan/150810/0/-M-70f069427cca50778df6b121a8bf5a8a_0x0.jpg" "id=9E2E3368B56CDBB4" "loop=yes" "theme=#FADFA3" "autoplay=false" "token=tokendemo" %}   

{% dplayer "url=http://ozkg680jm.bkt.clouddn.com/T-ara%20-%20%E1%84%8B%E1%85%AA%E1%86%AB%E1%84%8C%E1%85%A5%E1%86%AB%20%E1%84%86%E1%85%B5%E1%84%8E%E1%85%A7%E1%86%BB%E1%84%82%E1%85%A6%20%28So%20Crazy%29.mp4" "api=http://dplayer.daoapp.io" "pic=http://img0.c.yinyuetai.com/artist/fan/150810/0/-M-70f069427cca50778df6b121a8bf5a8a_0x0.jpg" "id=9E2E3368B56CDBB4" "loop=yes" "theme=#FADFA3" "token=tokendemo" %}
