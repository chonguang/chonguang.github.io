---
title: IntelliJ IDEA添加jar包
date: 2022-03-12 23:59:36 +0800
category: 后端技术
tags: [IDEA，jar包]
excerpt: IntelliJ IDEA添加jar包的三种方式（适用于idea的web项目）
---



## IntelliJ IDEA添加jar包

> 虽说现在主流都是maven项目，不过偶尔还是需要手动导包，本文介绍适用于 `idea的web项目` 的导包方式

### 直接复制

> 在 `web/WEB-INF` 目录下新建 `lib文件夹` (位置不能错)，将需要导入的jar包复制进lib文件夹，右键选中jar包点击添加为库(Add as Library)即可完成导包操作

![image-20220313004646016](https://gitee.com/chonguang/picture-bed/raw/master/imgs-typora/202203130046813.png)

![Snipaste_2022-03-13_00-51-52](https://gitee.com/chonguang/picture-bed/raw/master/imgs-typora/202203130052537.png)

![Snipaste_2022-03-13_00-50-13](https://gitee.com/chonguang/picture-bed/raw/master/imgs-typora/202203130050132.png)

> 只是把jar包复制进lib文件夹是没有用的，注意看在添加为库之后jar包出现了箭头，即代表jar包可用

![image-20220313005650956](https://gitee.com/chonguang/picture-bed/raw/master/imgs-typora/202203130056996.png)

---

### 库和模块

> 先准备好jar包库，也就是一个内含jar包的文件夹，一个jar包库可用于多个项目
>
> 进入项目结构设置(Project Structure)，依次选择

![image-20220313012808662](https://gitee.com/chonguang/picture-bed/raw/master/imgs-typora/202203130128806.png)

> 点击进入文件管理，选择你准备好的文件夹，单击确定

![image-20220313013131714](https://gitee.com/chonguang/picture-bed/raw/master/imgs-typora/202203130131817.png)

> 在接下来的弹窗中选择确定

![image-20220313013359426](https://gitee.com/chonguang/picture-bed/raw/master/imgs-typora/202203130136529.png)

> 最后在Artifacts界面Available Elements框下项目名上单击右键选择Put into Output Root，以后只需要将jar包复制进你选择的文件夹即可完成导入，很适合一个项目一个库文件夹的方式

![image-20220313021754678](https://gitee.com/chonguang/picture-bed/raw/master/imgs-typora/202203130217742.png)

> 至此jar包已被导入

![image-20220313014859888](https://gitee.com/chonguang/picture-bed/raw/master/imgs-typora/202203130148958.png)

---

### 全局库

> 在idea中设置一个文件夹为全局库(Global Libraries)，全局库设置之后可以在所有项目中直接导入

![image-20220313015708386](https://gitee.com/chonguang/picture-bed/raw/master/imgs-typora/202203130157421.png)

> 在项目结构设置(Project Structure)中按序点击，选择文件夹，这里选择的文件夹即为以后的全局库，要求jar包直接存在此文件夹中，不能有二级目录

![image-20220313020020664](https://gitee.com/chonguang/picture-bed/raw/master/imgs-typora/202203130200716.png)

>设置好了全局库之后，在任何项目中导入全局库需如下操作：

![image-20220313020416302](https://gitee.com/chonguang/picture-bed/raw/master/imgs-typora/202203130204356.png)

![image-20220313020706324](https://gitee.com/chonguang/picture-bed/raw/master/imgs-typora/202203130207375.png)

> 最后添加到根目录

![image-20220313021107005](https://gitee.com/chonguang/picture-bed/raw/master/imgs-typora/202203130211101.png)

>至此完成添加

![image-20220313021212541](https://gitee.com/chonguang/picture-bed/raw/master/imgs-typora/202203130212577.png)

---

### 写在后面

#### 普通idea项目添加jar包

> 1.直接复制：
>
> > 将需要导入的jar包复制进项目的lib文件夹下，右键选中jar包点击添加为库(Add as Library)即可完成导包操作
> >
> > ![image-20220313030007432](https://gitee.com/chonguang/picture-bed/raw/master/imgs-typora/202203130300497.png)
>
> 2.通过Modules的Dependencies添加：
>
> > 打开 File -> Project Structure，单击 Modules -> Dependencies，点击添加选择 Jars or directories
> >
> > ![image-20220313023017942](https://gitee.com/chonguang/picture-bed/raw/master/imgs-typora/202203130230004.png)
> >
> > 选择要添加的jar包，接下来点击 Apply -> OK
>
> 3.通过Libraries添加：
>
> >打开 File -> Project Structure，单击 Libraries，点击添加选择Java， 选择需要导入的jar包文件
> >
> >![image-20220313024014479](https://gitee.com/chonguang/picture-bed/raw/master/imgs-typora/202203130240513.png)
> >
> >![image-20220313024456385](https://gitee.com/chonguang/picture-bed/raw/master/imgs-typora/202203130244413.png)
> >
> >在弹出的方框中点击Cancel，取消将其添加到Module中
> >
> >![image-20220313024740523](https://gitee.com/chonguang/picture-bed/raw/master/imgs-typora/202203130247550.png)
> >
> >回到Modules菜单，点击 Dependencies，点击添加选择 Library
> >
> >![image-20220313025346085](https://gitee.com/chonguang/picture-bed/raw/master/imgs-typora/202203130253139.png)
> >
> >选择建好的Libraries，点击 Add Selected
> >
> >![image-20220313025531227](https://gitee.com/chonguang/picture-bed/raw/master/imgs-typora/202203130255265.png)
> >
> >最后点击 Apply -> OK
>
> 图标区别：添加在项目lib目录下的jar包的图标像文件夹，在其他目录添加的jar包的图标像柱状图

---

#### idea打jar包

>打开 File -> Project Structure，单击 Artifacts，点击添加选择 jar -> from modules with dependencies

![image-20220313031536487](https://gitee.com/chonguang/picture-bed/raw/master/imgs-typora/202203130315537.png)

> 在弹出的配置窗口配置完成后点击OK
>
> >Main Class：选择包含main方法的类
> >
> >JAR files form libraries：选择第一个是把依赖的包打进一个包中，选择第二个则是打包时不包含依赖的包
> >
> >Directory for META-INF/MANIFEST.MF：默认就可以，不用关心
> >
> >Include tests：是否连测试代码一起打包，默认不需要

![image-20220313032058692](https://gitee.com/chonguang/picture-bed/raw/master/imgs-typora/202203130320735.png)

>菜单：Build -> Build Artifacts，导出jar包

![image-20220313032623775](https://gitee.com/chonguang/picture-bed/raw/master/imgs-typora/202203130326807.png)

![image-20220313032659967](https://gitee.com/chonguang/picture-bed/raw/master/imgs-typora/202203130326996.png)

> 在输出目录里可以看见刚打的jar包

![image-20220313033111775](https://gitee.com/chonguang/picture-bed/raw/master/imgs-typora/202203130331809.png)

---

