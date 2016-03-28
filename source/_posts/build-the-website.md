title: 建站记
date: 2015-08-15 14:52:54
categories: programming
tags: web
---
## 沉淀
还是觉得干活之余需要沉淀，于是准备开一个博客和一个wiki。在调研了各种方案后，决定在Github上建三个repo。两个repo用于blog，分别存放src和publish；一个repo用于wiki。

## 博客
利用hexo建站。网上博客上建站的内容可以参考，但大多有些过时（教程中总有那么几小步并不适合于最新的版本）。看完摸清大致过程后去官网按[hexo](https://hexo.io/)官网给的步骤来做最靠谱。

### 修改主题
更换主题，我选择了icarus主题，按icarus主题的教程部署以后会有问题，需要修改根目录下`_config.yml`文件中的root，改为`/`

### deploy插件
在[这个教程](http://wsgzao.github.io/post/hexo-guide/)中间要求安装一堆插件，但没说明每个插件是干什么的，不过我感觉就那个deploy的插件比较好用。`npm install hexo-deployer-git --save`。在添加了这个deploy插件后，先配置好自己的github pages路径，每次更新完博客，就只需要`hexo d`就可以把博客内容同步更新到github上了。还有那几个生成tag之类的插件应该也是需要装的。

### 支持数学公式
使用[这位博主](http://catx.me/2014/03/09/hexo-mathjax-plugin/)开发的hexo-mathjax插件，安装方法：`npm install hexo-math --save`，具体参考[github](https://github.com/akfish/hexo-math)上的教程，而不要看博客中的，它已经过时了。使用时，要在用到公式的文章中，至少一处写成这样的形势。

加入Mathtag: $ \cos 2\theta = \cos^2 \theta - \sin^2 \theta $

测试Mathjax Blck：
$$ y = x $$
测试inline: $ y = x $

### 添加图片的问题
与传统的markdown添加图片方式有所不同，需要
1. 修改`_config.yml`，设置`post_assets_folder`为true，这样在添加新博文时就会新建一个博文对应的文件夹，然后把需要的资源放在那里就可以了。
2. 使用如`{ % asset_img slug [title] % }`的方式添加图片，请去掉“{”与“%”间的空格，另一边同理。

参考<https://hexo.io/docs/asset-folders.html>

### 搭建博客结束
这样，整个博客就搭建得差不多了。下面来搞定wiki。

## wiki的搭建
相对于博客，wiki搭建的参考资料就少了很多，似乎需要并不像博客那么旺盛。然而就像[这篇文章](http://www.yangzhiping.com/tech/gollum.html)中说的：`博客凸显创作，wiki适合整理`。很多东西并不适合放在博客上，但放在自己的wiki中却很有可能在下次碰到时省下不少时间；另外，自己对于知识体系的整理也更适合放在wiki中，总值，个人觉得wiki还是应该区别于博客存在的。

### 方案
采用Gollum，并与一个Github repo同步。

### wiki搭建过程
wiki的搭建几乎完全参考前面提到的[这篇文章](http://www.yangzhiping.com/tech/gollum.html)，装库的时候会有些问题，不过比较好解决。另外，上面这篇文章利用pow实现本地运行的部分在我这里并不成功，因此参考了[这篇](http://www.juliendesrosiers.com/2011/07/20/run-gollum-on-pow)。

### 又是数学公式
与Github的项目wiki同步后，数学公式是无法显示的。不过本地运行gollum时加上参数--mathjax就能渲染公式。pow配置mathjax参考了[这篇](http://msimav.net/2013/08/01/gollum-a-lightweight-wiki/)


#### 重新搭建博客
1. 安装node.js
2. 安装hexo
3. 安装next主题
以上都是参考next主题的文档完成的。选择next，一是因为这个主题很简洁，二是因为它有很好的文档支持，三是因为它在浏览文章时，有目录大纲的信息。

决定把src和public放在一个repo，方法就是修改_config.yml
记录一下原始文件，以
```tree
blog
├── node_modules
├── public
├── scaffolds
├── source
└── themes
```

下面是生成的文件
```tree
/Users/jason/Codes/my-github/blog/public
├── 2016
├── archives
├── css
├── images
├── js
└── vendors
```
以后可以到这里来区分
