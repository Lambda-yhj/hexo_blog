---
layout: post
title: "Express快速搭建自己的个人网站"
date: 2020-05-02 23:01
comments: true
tags: 
    - express
    - node
    - 个人网站
    - web服务器
---

​平时我们会使用手机去浏览网页信息，各种形色不一的网站，不乏有设计巧妙，简洁清新的网页，如[豆瓣FM](https://douban.fm/)等等，浏览起来极度舒适。它们有的是分享知识和音乐，有的是个性网站，分享生活，说的我都想搭建一个自己的个人网站了。那么就开始吧！我们使用[**Express**](https://www.expressjs.com.cn/)框架来快速搭建一个个人网站！

## 认识Express

什么是Express？

Express - 基于[**Nodejs**](https://nodejs.org/en/)平台，快速，开放，极简的web开发框架。

<!--more-->

## 安装

因为是基于node的嘛，所以先得安装node环境，戳[✈️](https://nodejs.org/en/)，找到适合自己电脑的node版本，下载安装，运行`node -v`，安装成功则可以查看node版本。

```bash
> node -v
v10.17.0
```

之后就是安装Express，新建文件夹**myWebsite**，打开命令行窗口输入`npm install express --save`，等待安装完成。
![Alt "express_install.png"](/assets/blogImg/express_install.png "express_install.png")

## 创建自己的个人网站

在命令行输入`npx express-generator`，执行完成。这时我们的个人网站已经建成，安装依赖`npm install`，会将package.json里面配置的运行需要依赖的库安装到本地，然后运行它`DEBUG=mywebsite:* npm start`，也可以到**./bin**目录下`node www`！

打开浏览器，地址栏输入`localhost:3000`，即可看到默认的网页。
![Alt "express_hello.png"](/assets/blogImg/express_hello.png "express_hello.png")

接下来就需要你扎实的`html + css + javascript`基础来设计丰富自己的网页了，可以借鉴他人，然后慢慢的写出有自己个性的网页。加油！特种兵。

## 认识Express框架

目录结构：

![Alt "express_frame.png"](/assets/blogImg/express_frame.png "express_frame.png")

* `bin`下`www`文件是启动文件，里面内容是创建一个http还是https的服务。

* `public`目录一般被设置成一个公共的静态资源库，在网络上可以直接访问其目录下的内容，

  一些分享的文件我们可以上传到这个目录，但是重要的私密文件可别放这。

```javascript
app.use(express.static(path.join(__dirname, 'public'))); // 将public目录设置为静态资源文件夹
```

* `routes`目录下是一些路由文件，我们从浏览器访问时，会根据url中的**path**路由到对应的

  接口。比如：浏览器访问`http://localhost:3000/users`就会路由到users.js这个文件`/users`这个接口，因为我们在app.js中配置了。

```javascript
var usersRouter = require('./routes/users');
app.use('/users', usersRouter);
```

* `views`目录下放的是网页文件，`.jade`是文件是Express引用了`jade`前段模版引擎。模版引擎可以是你的网页变成可配置，动态更新和可扩展性。
* `app.js`主模块，这里可以引用很多成熟好用的中间键来扩展你的应用功能，也可以过滤访问的IP等，保护网站系统等。

```javascript
app.use(express.json()); // 解析json格式的请求参数
app.use(express.urlencoded({ extended: false })); // 解析application/x-www-form-urlencode的请求参数
app.use(cookieParser()); // 方便操作客户端中的cookie值，比如账号密码信息
```

* `package-lock.json`将你初始化应用是安装的库的信息，保存在这个文件，因为后面可能安装其他库来扩展应用，而这个文件只记录你第一次`npm install`所安装的库。
* `package.json`框架依赖的库信息配置，别人可以通过`npm install`来安装你的应用运行所需要的所有库。

## 加入数据操作等逻辑

我们创建的Express应用是一个web服务器，浏览器访问时，服务器会将数据发给浏览器，浏览器渲染成我们看到的页面。web页面中有很多按钮，可以触发点击事件，提交表单数据等，这些有的就会请求到我们的服务器，经过一些逻辑和数据操作，将浏览器需要的数据返回。

* 使用mongodb来保存一些页面数据，比如访问记录等

* 编辑一些逻辑脚本，来处理请求，返回结果

## 网站安全

一些长使用到的方法：

* 配置IP白名单，限制单位时长访问次数

* 加密请求/应答数据，使用令牌

* 常见web攻击的预防，如http头部信息，Cookie信息，SQL注入等，可以看下这篇博客[✈️](https://www.cnblogs.com/qingmingsang/articles/10397870.html)

## 结语

我们可以使用express框架的web服务器，丰富个人网站的功能，而不是仅仅是页面浏览，和服务器交互的过程比静态页面更符合我们的期望。