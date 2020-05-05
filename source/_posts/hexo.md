---
layout: post
title: "基于hexo创建自己的博客"
date: 2020-05-05 08:23
comments: true
tags:
    - hexo
    - git
    - 博客
    - markdown
---
写博客的初衷大概就是分享和共同进步吧。
网络上有很多博客网站，像比较出名的[简书](https://www.jianshu.com/)，[CSDN](https://www.csdn.net/)，[博客园](https://www.cnblogs.com/)等等，我们注册账号就可以在里面写自己的博客文章，这些文章常常都会在我们查阅资料，查找难题的解决方法时会参考到。
但是，这些网站因为需要维护和经营，所以除了一些代币，小广告也是漫天飞，而且结构单一，是别人建好的固有框架，我们何不自己的博客自己做主，拥有"root权限"呢！

<!--more-->

## 什么是Hexo

[Hexo](https://hexo.io/zh-cn/) 是一个快速、简洁且高效的博客框架。

## 准备

* 安装node环境
* 安装git
* markdown语法基础

## 快速搭建

打开命令行，输入以下命令，全局安装hexo

```bash
npm install hexo -g
```

初始化项目，并在本地运行

```bash
hexo init blog // 初始化博客项目
cd blog
npm install // 安装依赖
hexo server // 本地运行
```

浏览器输入：`localhost:4000`运行成功的界面如下：
![Alt 'hexo_local.png'](/assets/blogImg/hexo_local.png "hexo_local.png")


## 部署到GitHub Pages访问

首先在git上创建一个和自己github账号名一样的私有仓库`<user-name>.github.io`，注意小写，比如我这里创建的是这样的：
![Alt 'create_repo.png'](/assets/blogImg/create_repo.png "create_repo.png")

在刚创建的仓库的`setting`中下拉，可以看见GitHub Pages的访问地址：
![Alt 'github_pages.png'](/assets/blogImg/github_pages.png "github_pages.png")

然后，在hexo项目目录下找到`_config.yml`这个文件，在`deploy`下，配置自己之前创建的仓库，如下配置：
![Alt 'deploy_config.png'](/assets/blogImg/deploy_config.png "deploy_config.png")

接着，安装`hexo-deployer-git`库，安装成功后命令行运行`hexo clean && hexo deploy`即可发布到GitHub Pages，浏览器输入`<user-name>.github.io`即可防问到你的博客。效果如下：
![Alt 'github_pages_show.png'](/assets/blogImg/github_pages_show.png "github_pages_show.png")


## 丰富我的博客内容

写一篇博客文章，可以运行命令`hexo new [layout] title`，其中`layout`是只创建什么风格的博客文章，实际作用是指在那个目录下，`title`就是博客文章的标题。比如命令行输入`hexo new [post] 你真好看`，执行结果：
![Alt 'new_page_command.png'](/assets/blogImg/new_page_command.png "new_page_command.png")

打开`source/_posts/你真好看.md`，
![Alt 'new_page.png'](/assets/blogImg/new_page.png "new_page.png")

你可以开始你的写作，当然`hexo`支持[markdown](https://www.runoob.com/markdown/md-tutorial.html)语法,所以你得有markdown的语法知识唷！
推荐一款markdown编辑器，[Typora](https://www.typora.io/)，简洁明了，免费。
写好后，同样的命令`hexo clean && hexo deploy`，发布到你的GitHub Pages。

加入评论系统，博客文章一般发表一些观点，那么肯定有的访客会评论一些自己的看法，讨论才会产生更完美的方案。那么需要给我们的博客接入评论功能。
评论插件有很多，下面是`gitalk`的接入效果👇：
![Alt 'comments_show.png'](/assets/blogImg/comments_show.png "comments_show.png")

添加一些装饰，比如右下角的`lived2d`动漫人物，还有背景音乐，打赏功能，置顶功能等等，详情留意后续博客文章，👇是一些效果：
![Alt 'live2d_wanko.png'](/assets/blogImg/live2d_wanko.png "live2d_wanko.png")

## 结语

写博客是对自己的知识和生活的提炼，总结和分享。虽然耗费时间，但坚持下来，受益匪浅。