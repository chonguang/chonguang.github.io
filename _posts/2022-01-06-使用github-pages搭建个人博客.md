---
title: 使用github pages搭建个人博客
date: 2022-01-06 23:09:40 +0800
category: 个人博客
tags: GitHub
excerpt: 在github上搭建个人博客
---

## 使用github pages搭建个人博客

无意中发现了github pages这个功能，仔细了解了一下发现使用github repo可以存放静态网页代码，所以可以用其来搭建自己的博客，最主要这个零成本啊，不需要买服务器:smiley:，那么在github中搭建博客着实不错。

> github pages官方网站：<https://pages.github.com/>
>
> 官方推荐jeklly主题框架，因此在github中找到了这个主题：<https://github.com/showzeng/Minimalism>，感觉不错，就把它clone下来上传到自己的github

### 1.准备步骤

> 新建一个repo，仓库名字为`xxx.github.io`，其中xxx为你github的username
>
> 在这里由于我已经创建过这个仓库了，所以提示已经存在

![image-20220106232956203](https://gitee.com/chonguang/picture-bed/raw/master/imgs-typora/202201062329275.png)

### 2.clone主题

> 把自己想要的主题clone下来，示例代码：
>
> ```shell
> git clone https://github.com/showzeng/Minimalism.git
> ```

![image-20220106233351777](https://gitee.com/chonguang/picture-bed/raw/master/imgs-typora/202201062333827.png)

### 3.clone仓库

> 把刚才新建的repo克隆下来，示例代码：
>
> ```shell
> git clone http://github.com/chonguang/chonguang.github.io.git
> ```

![image-20220106233833877](https://gitee.com/chonguang/picture-bed/raw/master/imgs-typora/202201062338923.png)

### 4.使用主题文件搭建博客

> 把主题文件夹中除了.git文件夹全部复制到自己仓库所在的文件夹

![image-20220106234345898](https://gitee.com/chonguang/picture-bed/raw/master/imgs-typora/202201062343968.png)

![image-20220106234450949](https://gitee.com/chonguang/picture-bed/raw/master/imgs-typora/202201062344012.png)

> 更改配置文件

- _config.yml文件：

```yml
excerpt_separator: <!--more-->

defaults:
  -
    scope:
      path: ""
      type: "posts"
    values:
      layout: "post"
  -
    scope:
      path: "assets/img"
    values:
      image: true

# --- 网站信息设置 ---
# 下面填写你的博客标题
title: 标题
# 下面填写你的网络常用名
name: 常用名
# 下面填写你的座右铭或者是个性签名
description: 个性签名
# 你博客的 url 地址，比如：https://showzeng.github.io 或者是自定义的域名
url: https://showzeng.github.io 
# 在页尾的版权时间信息，比如：2016-2018，默认是 2018 年
copyright_time: 2018
# 标签页的 logo 及博客的头像，如果你想引用网络图片资源，就取消下面的注解，并填写图片资源的 url 地址
# 或者，推荐的做法是将这两个图片资源下载到本地的 /assets/img/ 文件夹下，且图片名必须命名为 favicon 和 avatar
# favicon:
# avatar:
# --- 网站信息设置 ---


# --- 文章列表页 ---
# 文章列表是否显示摘要
show_excerpt: true
# --- 文章页 ---


# --- 社交链接 ---
# 取消下面的注解，并填写相应的你要开启的社交链接
#twitter: https://twitter.com/showzeng
weibo: https://weibo.com/u/978967865/
github: https://github.com/xxx
# 邮件地址前面带上 mailto:
email: mailto:123456789@qq.com
# RSS 订阅
rss: true
# --- 社交链接 ---


# --- 版权声明 ---
# 禁止复制 (注：启用后仅文章页和关于页禁止复制)
# lock_copy: true
# 禁止右键菜单 (注：为全局设置，启用后所有页面均无法使用右键菜单)
# lock_menu: true
# 复制文本末尾添加版权声明 (注：启用后仅文章页和关于页复制添加版权声明)
# copy_with_declaration: true
# --- 版权声明 ---


# --- 打赏设置 ---
# 开启打赏，取消下面一行注解，并将微信和支付宝的收款二维码放置在 /assets/img/ 文件夹下
# 同时图片的文件名必须为 alipay 和 wechat
reward: true
# 打赏的推广语
reward_description: 推广语
# --- 打赏设置 ---



# theme: jekyll-theme-minimalism
remote_theme: showzeng/Minimalism

exclude:
  - new

```

- about.md

```markdown
---
layout: about
title: 关于
reward: false
---

这里定制自己的关于页面
```

> 图片在assets\img下，可以替换自己的头像、ico图标以及打赏收款码
>
> 在仓库根目录下建`_posts`文件夹，博客文章需放在这个文件夹里
>
> 博客文章类型为Markdown文件，为了实现摘要、归档、分类和标签功能需在每篇文章开头插入元数据块，Typora 支持[YAML Front Matter](https://jekyllrb.com/docs/front-matter/)。输入`---`在文章的顶端然后按下`Enter`键就会采用或者从菜单中插入一个元数据块，具体格式为：
>
> ```markdown
> ---
> title: 使用github pages搭建个人博客
> date: 2022-01-06 23:09:40 +0800
> category: 个人博客
> tags: GitHub
> excerpt: 在github上搭建个人博客
> ```

