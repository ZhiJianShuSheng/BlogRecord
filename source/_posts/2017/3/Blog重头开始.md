---
title: Blog重头开始
notag: false
toc: true
author: wesly
comment: false
date: 2017-03-31 18:31:56
description: 
categories:
- Blog
tags:
- Hexo 
- Git
permalink:
thumbnail: http://upload-images.jianshu.io/upload_images/664334-6a635025e0c104d7.png
---
　自从上次博客从hexo+github迁移到简书后，再也没有捣鼓相关的内容了。今天无意中看到了hexo的主题[Material Theme](https://material.viosey.com/)，再次燃起兴趣......
<!-- more -->

## 重头开始
这里完全重头搭建一个gitpage+Hexo的静态博客。所以看完这篇文章之后，你完全可以自己弄一个玩一玩。虽然这些内容完全可以通过官网全部找到，这里也就相当于一个总结吧！

## 一切源头
[GitHub](https://github.com/)

- Node.js
	- [Node.js GitHub地址](https://github.com/nodejs/node)
	- [Node.js 文档](https://nodejs.org/en/)
- Hexo
	- [Hexo GitHub 地址](https://github.com/hexojs/hexo)
	- [Hexo 文档](https://hexo.io/)
	- [Hexo 中文文档](https://hexo.io/zh-cn/)
- Git
	- [Git GitHub 地址](https://github.com/git/git)
	- [Git 使用教程- 这里推荐中版](http://www.liaoxuefeng.com/wiki/0013739516305929606dd18361248578c67b8067c8c017b000)
- Hexo Theme
	- [hexo-theme-material GitHub 地址](https://github.com/viosey/hexo-theme-material)
	- [material 主题文档](https://material.viosey.com/)

一下操作步骤，其实在上面的文档中能够全部找到。目前网上流传所谓的教程其实最开始也是从这些官方文档获得的。**所以如果时间充裕，最好从官方文档入手！**

## 安装node
直接打开官方地址[node](https://nodejs.org/en/)，下载安装包即可。

![](http://upload-images.jianshu.io/upload_images/664334-450f0bf96d56c348.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

## 安装Hexo
同样打开官方地址[hexo](https://hexo.io/)

![](http://upload-images.jianshu.io/upload_images/664334-7906f95f92b239fc.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

在终端执行其中的命令即可。

## 登录GitHub创建项目
![](http://upload-images.jianshu.io/upload_images/664334-f50d3d356a202614.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

填写项目名，**这里一定要注意项目名称需要用用户名+github.io结尾**

![](http://upload-images.jianshu.io/upload_images/664334-41acbd8d7acb0b4e.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

创建完成之后拖到下面会有关于gitpage的介绍。选择个主题再返回就启用了。
![](http://upload-images.jianshu.io/upload_images/664334-6ff6d02ebe0a17ac.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

接下来的事情就是将Hexo生成的静态页面push到这个仓库中就可以了。然后访问提示的这个链接就可以看到内容。

## 自动发布到GitHub
虽然经过上面的不走，勉勉强强能写点东西并且能够发布了。但是还有很多事情需要做，比如：

1. 主题的选择，一般情况下hexo的默认主题不会让你满意。
2. 自动部署，每次写了新的文章都用git命令操作一遍，很费时间。
3. 添加一些本地或者google搜索。
4. 支持评论等
5. ......

上面的3、4、5在选用三方主题的时候基本上简单配置一下就可以的。所以不难。

**自动部署在官方文档中也用说明。[自动部署中文版](https://hexo.io/zh-cn/docs/deployment.html)**

- 安装[ hexo-deployer-git](https://github.com/hexojs/hexo-deployer-git)：
	- 在当前hexo生成的目录下执行：`npm install hexo-deployer-git --save`
- 配置deploy内容：比如我这样设置的

	```
	deploy:
  type: git
  repo: git@github.com:****/***.github.io.git
  branch: master
```
 这里repo后面的内容可以直接复制你仓库中的地址：
![](http://upload-images.jianshu.io/upload_images/664334-3bc95bffac2f1955.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

### 给github账号添加ssh
经过上面的过程依然还不能push到仓库，还没设置ssh。如果你执行了`hexo  d`会报403的错误。

设置Github的用户名和邮箱

```
git config --global user.name "你在Github上的昵称"
git config --global user.email "你在Github上的邮箱"
```

这里是全局设置的用户账号，考虑到某些仓库不能用这个账号，可以具体的仓库中使用如下：

```
git config user.name "用户名" 
git config user.email "邮箱"
```
设置

### 公钥私钥
接下来就是生产公钥私钥：

```
ssh-keygen -t rsa -C "你在Github上的邮箱"
// 多账号情况下：（多个git使用）
ssh-keygen -t rsa -f ~/.ssh/名称 -C "邮箱"
```

- -t 指定密钥类型，默认是 rsa ，可以省略。
- -f 指定密钥文件存储文件名。

添加密钥

```
ssh-add id_rsa
```

执行后，会填写保存两种密钥的文件夹，和passphrase。这里是指的密码尽量简单点，因为后面会在添加私钥的时候用到。**全部可以按enter。然后执行ls来查看生成后的文件。**

- id_rsa和id_rsa.pub分别是私有密钥和公有密钥。
- 我们指定的文件名就是id_rsa.github，这时~/.ssh目录下会多出id_rsa.github和id_rsa.github.pub两个文件，id_rsa.github里保存的就是我们要使用的key。

### 有多个git账号怎么办（常见问题）
- 创建：touch ~/.ssh/config
- 添加内容：例如

	```
	#gitlab
Host ****
HostName ****
RSAAuthentication yes
IdentityFile ~./ssh/id_rsa_gitlab
#github
Host****
HostName ****
RSAAuthentication yes
User ****
IdentityFile ~./ssh/github_id_rsa
#github
Host github
HostName github.com
RSAAuthentication yes
User 你的登录邮箱
IdentityFile ~./ssh/github_id_rsa
```

### 添加公钥到github账号ssh
- 打开github账号的设置界面
- 新建一个SSH Key

然后将打开公钥文件，把内容粘贴到
![](http://upload-images.jianshu.io/upload_images/664334-cf6211149269298f.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

测试是否成功`ssh -T git@github.com`

如果显示：

```
Are you sure you want to continue connecting (yes/no)?
```

输入yes。
然后就可以看到

```
Hi yourusername! You've successfully authenticated, but GitHub does not
provide shell access.
```

## 设置主题
这部分看着文档走就可以了，没什么难度。当然第一次创建一个比较有感觉的博客还是需要花一些时间的。这里我大致弄了一个模板。如果嫌麻烦可以直接用这个项目生成。地址[后期补上]()


## THE END

## 扩展阅读
[生成ssh公钥并连接到github](http://www.jianshu.com/p/0d7038102cd6)
[Mac里添加多个git ssh](http://blog.csdn.net/diamont1001/article/details/51822803)










