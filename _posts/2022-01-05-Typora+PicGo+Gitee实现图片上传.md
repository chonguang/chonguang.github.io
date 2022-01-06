---
title: Typora+PicGo+Gitee图床实现图片上传
date: 2022-01-05 21:19:57 +0800
category: 图床
tags: [Typora，PicGo，Gitee]
excerpt: Typora+PicGo+Gitee图床，打造图片上传，本地显示功能
---



## Typora+PicGo+Gitee图床实现图片上传

### 前言

为什么要实现这样一个功能呢？拿Markdown写笔记的人应该深有体会，插入图片实际上是在引用图片，并没有把图片插入到文件中去，那么这样就会有两种引用的方式，一种是插入本地的图片，另一种就是插入URL地址，而插入本地图片的话就有些不友好，因为迁移性有点差，当你拷贝你的笔记到别的主机上时文件中的图片引用链接失效，图片就会显示失败。当然可以让图片使用相对路径，然后把笔记和图片放在同一文件夹下，如有迁移需要，直接迁移整个文件夹即可，但这样显然还是有点不太简洁，毕竟多了个把图片放到文件夹的步骤，相对而言网络图片就相当友好，使用URL地址插入图片不管笔记怎么复制只要有网就能看。你可以找个免费的图床网站,将自己的图片传上去，图床网返回给你一个地址，插入图片时使用这个地址即可，但是这样操作也不是很简洁，那么能不能直接将图片插入笔记中，编辑器将图片上传到云端,云端url插入本地呢？答案是可以的，这就是这次要说的东西。

### Typora

[Typora](https://typora.com.cn/ "点击链接前往中文官网")没什么好说的，一款跨平台Markdown编辑器，简单美观，以前也免费，写数学公式画流程图插入表格很舒适，支持动态预览，在你书写的时候会实时渲染，所见即所得，自行下载安装即可（版本<=0.11.8免费）。

### Gitee图床

#### 建立 [Gitee](https://so.csdn.net/so/search?q=Gitee) 图床

> 注册 gitee 账号并创建一个仓库当图床

##### 1.注册或登陆 Gitee

Gitee 官网网址：https://gitee.com/

注册账号在这里就不细说了，注册好账号之后登陆 Gitee。

##### 2.新建仓库当图床

![image-20220105223242253](https://gitee.com/chonguang/picture-bed/raw/master/imgs-typora/202201052232063.png)

> 然后填写仓库信息

![image-20220105223928730](https://gitee.com/chonguang/picture-bed/raw/master/imgs-typora/202201052239809.png)

> 因为我已经建立了 PictureBed 这个仓库，所以提示已经存在
>
> 要选择开源仓库，如果私有的话可以上传照片但是无法在网络上查看照片
>
> Readme文件是自述文件，这是每个仓库应该有的

#### 生成私人令牌

点击设置里的私人令牌，点击生成私人令牌。

![image-20220105224517083](https://gitee.com/chonguang/picture-bed/raw/master/imgs-typora/202201052245173.png)

![image-20220105224700848](https://gitee.com/chonguang/picture-bed/raw/master/imgs-typora/202201052247904.png)

>点击提交即可，记得复制令牌，稍后在 Gitee 图床配置中会用到
>
>令牌只会显示一次，如果不复制的话，就只能重新修改令牌，步骤：修改-->重新生成令牌

### PicGo

#### 安装 PicGo

PicGo是一款图片上传的工具，目前支持微博图床，七牛图床，腾讯云，又拍云，GitHub，Gitee等图床，在这里，我们使用 Gitee 作为图床。

> 下载链接：<https://github.com/Molunerfinn/PicGo/releases>
>
> 选个自己喜欢的版本，点击进入，找到后缀 `.exe` 的，点击后自动下载。或者直接使用最新版。

![image-20220105230344467](https://gitee.com/chonguang/picture-bed/raw/master/imgs-typora/202201052303535.png)

#### PicGo 配置 Gitee 图床

##### 1.下载 Gitee 插件

> 注：若没有安装 node.js ，则会安装不了插件，因为插件下载需要使用到 node.js 的 npm
>
> node.js 官网下载链接：<https://nodejs.org/zh-cn/>
>
> 详细安装过程可参考：<https://www.runoob.com/nodejs/nodejs-install-setup.html>

安装好之后，打开 PicGo 软件，点击插件设置，搜索 gitee，选择第一个即可，别的插件也可以，配置过程也差不多。

![image-20220105231021762](https://gitee.com/chonguang/picture-bed/raw/master/imgs-typora/202201052310837.png)

##### 2.配置 Gitee 图床

> 首先在 PicGo 设置中选择 Gitee 图床。

![image-20220105231736933](https://gitee.com/chonguang/picture-bed/raw/master/imgs-typora/202201052317000.png)

>然后在图床设置中进行配置 Gitee 图床

![image-20220105232316498](https://gitee.com/chonguang/picture-bed/raw/master/imgs-typora/202201052323563.png)

点击确定，就可以使用了，如果只想上传图片，到这一步就可以了，不过咱们的目的是在Typora中自动上传填写URL地址，这样真的很提高开发效率！

> 注：这一步经常出错的就是repo填错，这个仓库名指的是仓库访问URL地址，可以进入仓库，点击管理查看
>
> ![image-20220105233059987](https://gitee.com/chonguang/picture-bed/raw/master/imgs-typora/202201052331072.png)

### Typora 配置 Gitee 图床

>打开进入 Typora，点击上方目录：文件-->偏好设置-->图像，然后配置图床

![image-20220105234012509](https://gitee.com/chonguang/picture-bed/raw/master/imgs-typora/202201052340607.png)

设置完之后点击验证图片上传选项，若成功则如下图：

<img src="https://gitee.com/chonguang/picture-bed/raw/master/imgs-typora/202201052343819.png" alt="image-20220105234321768" style="zoom: 50%;" />

> 注：这里有时会出现一个错误，就是上传地址和 PicGo 中的上传地址不一致导致上传失败
>
> typora上传地址：
>
> <img src="https://gitee.com/chonguang/picture-bed/raw/master/imgs-typora/202201052352866.png" style="zoom:50%;" />
>
> 到 PicGo 中去验证：点击 PicGo 设置-->设置 Sever，若和 Typora 中图片上传地址不一样，改成 Typora 中的监听端口即可，然后确认。
>
> ![image-20220105235539648](https://gitee.com/chonguang/picture-bed/raw/master/imgs-typora/202201052355708.png)

### 写在后面

> 可能有人按照上面步骤全部配置完还是上传图片失败，那么请检查检查你的PicGo:smile:
>
> 虽然这个操作很迷，但我第一次弄的时候图片老是上传失败，直到无意中把这个Gitee图床选中，一切问题迎刃而解

![image-20220106000409829](https://gitee.com/chonguang/picture-bed/raw/master/imgs-typora/202201060004891.png)

