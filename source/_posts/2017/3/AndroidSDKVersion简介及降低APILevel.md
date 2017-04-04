---
title: Andriod SDK Version及API Level
notag: false
toc: true
author: wesly
comment: false
date: 2017-04-01 14:17:56
description: 
categories:
- Android
tags:
- Android 
- SDK
permalink:
thumbnail: http://upload-images.jianshu.io/upload_images/664334-13697e5797e706d1.png
---
　抽空打开了Android Studio准备研究一下开源项目代码，没想到运行不了。总的来说还是自己对Android开发不是太熟，这里简单总结一下遇到的一些坑！
<!-- more -->

## SDK Version简单介绍
一切源于向前兼容，用户在升级到新版 Android 的时候，用以前版本的 SDK 构建的应用不会出问题。这就是 compileSdkVersion, minSdkVersion 和 targetSdkVersion 的作用：他们分别控制可以使用哪些 API ，要求的 API 级别是什么，以及应用的兼容模式。

### Compile Sdk Version
compileSdkVersion 告诉 Gradle 用哪个 Android SDK 版本编译你的应用。使用任何新添加的 API 就需要使用对应 Level 的 Android SDK。

修改 compileSdkVersion 不会改变运行时的行为。当你修改了 compileSdkVersion 的时候，可能会出现新的编译警告、编译错误，但新的 compileSdkVersion 不会被包含到 APK 中：它纯粹只是在编译的时候使用。

在开发中最常见的就是总是使用最新的 SDK 进行编译。在现有代码上使用新的编译检查可以获得很多好处，避免新弃用的 API ，并且为使用新的 API 做好准备。Android Stuido默认是用最新的，所以一般不怎么改compileSdkVersion。

### Min Sdk Version
如果 compileSdkVersion 设置为可用的最新 API，那么 minSdkVersion 则是应用可以运行的最低要求。minSdkVersion 是 Google Play 商店用来判断用户设备是否可以安装某个应用的标志之一。

在开发时 minSdkVersion 也起到一个重要角色：lint 默认会在项目中运行，**它在你使用了高于 minSdkVersion  的 API 时会警告你，帮你避免调用不存在的 API 的运行时问题。**如果只在较高版本的系统上才使用某些 API，通常使用运行时检查系统版本的方式解决。

**注意：当使用第三方库可能有他们自己的 minSdkVersion 。你的应用设置的 minSdkVersion 必需大于等于这些库的 minSdkVersion 。**

### Target Sdk Version
targetSdkVersion 是 Android 提供向前兼容的主要依据，在应用的 targetSdkVersion 没有更新之前系统不会应用最新的API变化。这允许你在适应新的API变化之前就可以使用新的 API。

### 关系
三者需要满足`minSdkVersion <= targetSdkVersion <= compileSdkVersion`。但是最为理想的状态应该是`minSdkVersion (lowest possible) <=  targetSdkVersion == compileSdkVersion (latest SDK)`用较低的 minSdkVersion 来覆盖最大的人群，用最新的 SDK 设置 target 和 compile 来获得最好的外观和行为。

## API Level  与 Version
有了上面的基础知识，于是为了学习更为牛逼的代码，于是去GitHub上下载了几个项目的源码。一切都没问题，在连上真机的时候突然报错。提示：![](http://upload-images.jianshu.io/upload_images/664334-3cdba0423c0ef161.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)。

于是瞎捣鼓了一下才明白，原来每一个Android版本对应一个API  level。报错的原因就是真机的系统版本低于项目设定的版本。

在官网上找到了一张图标，能够彻底说明这个问题。[Codenames, Tags, and Build Numbers](http://source.android.com/source/build-numbers.html)

![](http://upload-images.jianshu.io/upload_images/664334-c290eec12f54f4af.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

### 降低API Level
为了让项目在真机上运行起来，不得不降低项目的API level。**虽然我这里报错是minSDK,但我这里演示的是所有更改所有sdk，比如comiple,target,misdk的情况。具体更改根据报错信息修改对应的选项即可。**

这里有两种方式解决。

1. 图形化操作
	- 1.1 修改 compile Sdk Version
		![](http://upload-images.jianshu.io/upload_images/664334-7cb1d57138e8cf19.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
	- 1.2 修改Target Sdk Version
		![](http://upload-images.jianshu.io/upload_images/664334-f3332ccd2e6ba093.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
	- 1.3修改完之后，IDE会自动修改build.grade的内容。
		![](http://upload-images.jianshu.io/upload_images/664334-bcb9adf7bab225fd.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)


2. 修改build.gradle：上面提到的这些sdk内容，全部在build.gradle文件里找到。我们可以直接修改相应的内容即可。比如：
	![](http://upload-images.jianshu.io/upload_images/664334-3cd0cfd5755f9a5b.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
	
## 问题
由较高的API Level转至较低的API Level，有时候会出现兼容上的问题。比如较低版本的API Level不支持某些特性。

## 扩展阅读
[Picking your compileSdkVersion, minSdkVersion, and targetSdkVersion](https://medium.com/google-developers/picking-your-compilesdkversion-minsdkversion-targetsdkversion-a098a0341ebd)

[如何选择 compileSdkVersion, minSdkVersion 和 targetSdkVersion](http://chinagdg.org/2016/01/picking-your-compilesdkversion-minsdkversion-targetsdkversion/)


