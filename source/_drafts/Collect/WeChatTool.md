title: 微信小程序开发环境搭建
date: 2015-12-25 18:29:00
description: 
categories:
- Report
tags:
- Report
toc: true
author:
comments:
original:
permalink: 
---

　　**自用笔记：**最近微信小程序，这么一火，确实让不少人重视了前端的发展。
<!-- more -->
人类的智慧还是伟大的，短短的几天时间，微信小程序就破解出来了。我也来上手试试。

## 环境搭建：
![demo的动态图](http://img.blog.csdn.net/20160923011211416)

下载：
[【应用号】IDE + 破解 + Demo](https://github.com/gavinkwoe/weapp-ide-crack)

由于新版本的微信开发程序，取消了登录的界面。所以我们要先用0.7版本的登录后，覆盖安装0.9版本的程序。

分别找到下面三个目录替换对应文件即可
进入程序目录后，替换以下文件（只需要替换0.9版本里的，0.7版本用来登陆）：

Windows：
\package.nw\app\dist\components\create\createstep.js
\package.nw\app\dist\stroes\projectStores.js
\package.nw\app\dist\weapp\appservice\asdebug.js

Mac：
/Resources/app.nw/app/dist/components/create/createstep.js
/Resources/app.nw/app/dist/stroes/projectStores.js
/Resources/app.nw/app/dist/weapp/appservice/asdebug.js


[]( "")
[首个微信小程序开发教程](http://gold.xitu.io/entry/57e34d6bd2030900691e9ad7/view "")
[微信小程序：不得不学的 js 技巧之关键字 this](http://gold.xitu.io/post/57e48c0075c4cd2d9f3485f1?utm_source=gold_browser_extension "")
[[博卡君]微信应用号「小程序」开发教程首发第二弹！](http://mp.weixin.qq.com/s?__biz=MzIyMDM2Mjg2Nw==&mid=2247484440&idx=1&sn=d612c592324a20b4240de0a0b98feee5&chksm=97cc6504a0bbec1297b5116dbc051dbcb8b7a6165fd3392dabd1a3ef0a38e8b452a64092f8af&scene=1&srcid=0923opn6Lqe2D6yaowz4RNco#rd "")
[微信小程序开发资源汇总](https://github.com/justjavac/awesome-wechat-weapp "")
[首个微信小程序开发教程！](http://gold.xitu.io/entry/57e34d6bd2030900691e9ad7 "")
[](https://zhuanlan.zhihu.com/p/22574282 "")
[微信小程序剖析【下】：运行机制](http://mp.weixin.qq.com/s?__biz=MjM5Mjg4NDMwMA==&mid=2652974093&idx=1&sn=0570a243304ea8bb7d1b636624886fb1#rd "")
[微信小程序，一个有局限的类似 React Native 轮子！](http://www.jianshu.com/p/060c6f3dd4e8# "")
[微信小程序Doc](http://wxopen.notedown.cn/ "")

注意：
1. 找不到所要替换的文件
问题原因：开发工具版本不正确，老版本不支持
解决方案：确保下载的程序版本在0.9.092100以上

1. Failed to load resource: net::ERR_NAME_NOT_RESOLVED http://1709827360.appservice.open.weixin.qq.com/appservice
问题原因：通常是由于系统设置了代理如Shadowsocks等。
解决方案：关闭代理，或者依次点击工具栏“动作”-"设置"，选择“不使用任何代理，勾选后直连网络”。

1. 修复asdebug.js报错
问题原因：TypeError: Cannot read property 'MaxRequestConcurrent' of undefined
解决方案：替换 /Resources/app.nw/app/dist/weapp/appservice/asdebug.js

1. 扫码登录失败
问题原因：please bind your wechat account to the appid first
解决方案：先使用0.7版本的进行扫码登陆，登陆成功后，再用0.9的版本打开就直接进入了。
0.7版本地址：http://dldir1.qq.com/WechatWebDev/release/0.7.0/wechat_web_devtools_0.7.0.dmg

## 代码逻辑：