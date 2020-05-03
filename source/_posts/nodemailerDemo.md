---
layout: post
title: "使用nodemailer模块，来发送一封邮件"
date: 2019-12-04 23:02:00
comments: true
tags:
    - nodemailer
    - SMTP
    - QQ邮件
---

有时候呢，我们需要定时发送一封邮件的，比如我已经把每个人的生日都记下来(骗纸)，创建一个定时任务，然后在生日当天给对应的小姐姐发送生日祝福邮件，发送时间点也可以挑哦。

开个玩笑，😊，其实，今天做到关于节假日的功能需求，这个有个坑爹的是，你不知道2021年的放假安排，所以需要到前一年12月份左右（这个时候明年放假安排已经出来了），比如当下，发送一封邮件给运维，提醒一下，该翻日历了，把节假日的那份文件更新下！

于是乎，我们使用到了[nodemailer](https://nodemailer.com/about/)这个模块。

<!--more-->

<img src='/assets/blogImg/nodemailerIcon.png'>

不要以为度数加深了，官方图片就是这么糊！😂

## 开始正题
安装nodemailer:
```
cnpm install nodemailer -s
```
Tip: 未配置cnpm的用npm来安装。

我的运行环境:
nodejs版本`v10.17.0` nodemailer版本`v6.4.0`

新建一个文件nodeMailerDemo.js，编辑。
引入模块:
```javascript
const nodemailer = require('nodemailer');
```

创建一个transporter,它将发送我们的邮件:
```javascript
let transporter = nodemailer.createTransport({
    host: 'smtp.qq.com', // 主机名
    port: 587, // 端口
    scure: false, // 是否使用tls
    auth: {
        user: '1429190569@qq.com', // qq邮箱
        pass: 'xxxx' // 使用smtp客户端凭证 在qq邮箱设置里面可获得
    }
});
```

配置我们需要发送的内容:
```javascript
let data = {
    from: '1429190569@qq.com', // 发送邮件的人
    to: '1429190569@qq.com', // 收邮件的人 ps:可以自己发给自己
    subject: 'Hello World', // 邮件主题
    text: '我也不知道这是做什么的', // 纯文本
    html: '<h5>你好呀，世界！</h5>',// html字符串 收到邮件会被渲染显示出来
    attachments: { // 附件
        filename: '', // 文件名
        path: '' // 路径
    }
};
```

发送邮件:
```javascript
transporter.sendMail(data, (err, info) => {
    console.log('err, info:', err, info);
})
```
然后，我们打开终端，cd到nodeMailerDemo.js所在的目录
```bash
node nodeMailerDemo.js
```
打开你的QQ邮箱，即发现收到一封自己给自己发送的邮件。
如下：
![Alt 'testMail.jpeg'](/assets/blogImg/testMail.jpeg "testMail.jpeg")

因为我们的附件没有写文件名和地址，所以收到了一个0B的默认文件。

再看看nodeMailer模块的源码，data中的Mail Options 不止这些：
![Alt 'mailoptions.png'](/assets/blogImg/mailoptions.png "mailoptions.png")
感兴趣可以去研究啦，不同的邮件客户端支持的选项也有所差异。