---
title: Maven安装与创建Maven工程
date: 2022-03-03 11:08:06 +0800
category: 后端技术
tags: Maven
excerpt: 安装Maven与使用IDEA集成Maven并创建Maven工程
---



## Maven安装与创建Maven工程

### 关于Maven

#### 概述

-  **`Maven`** 充分运用了面向对象的思想，对项目进行模型抽象，是可以通过一小段描述信息来管理项目的构建，报告和文档的软件项目管理工具。 **`Maven`** 除了以程序构建能力为特色之外，还提供高级项目管理工具，由于 **`Maven`** 的缺省构建规则有较高的可重用性，所以常常用两三行 `Maven构建脚本` 就可以构建简单的项目。
- **Maven是由Apache开发的一个工具** ，用来管理 **java项目( `依赖(jar)管理`，`项目构建` ，`分模块开发` ，`管理项目的生命周期` )** 。

#### Maven的作用

- 依赖管理：maven对项目的第三方构件`(jar包)`进行统一管理。向工程中加入jar包不需要手工从其它地方拷贝，通过maven定义jar包的坐标，自动从maven仓库中去下载到工程中。


- 项目构建：maven提供一套对项目生命周期管理的标准，开发人员和测试人员统一使用maven进行项目构建。

  > 项目生命周期管理：编译、测试、打包、部署、运行

- maven对工程分模块构建，提高开发效率。

#### Maven的仓库

| 仓库名称 | 作用                                                         |
| -------- | ------------------------------------------------------------ |
| 本地仓库 | 相当于缓存，工程第一次会从远程仓库(互联网)去下载 `jar包` ，将 `jar包` 存在本地仓库，第二次不需要从远程仓库去下载，先从本地仓库找，如果找不到再去远程仓库找。 |
| 中央仓库 | 仓库中 `jar` 由专业团队( `maven团队` )统一维护。中央仓库的地址：http://repo1.maven.org/maven2/ |
| 远程仓库 | 是开发人员自己定制仓库，包含了所需要的代码库或者其他工程中用到的 `jar文件` ，例如在公司内部架设一台私服，其它公司架设一台仓库，对外公开。 |

#### Maven的坐标

- Maven的一个核心的作用就是管理项目的依赖，引入工程所需的各种 `jar包` 等。为了能自动化的解析任何一个 `java构件` ，Maven必须将这些 `jar包` 或者其他资源进行唯一标识，这是管理项目的依赖的基础，也就是我们要说的坐标。包括我们自己开发的项目，也是要通过坐标进行唯一标识的，这样才能在其它项目中进行依赖引用，坐标的定义元素如下：

  > groupId：项目组织唯一的标识符，实际对应JAVA的包的结构，一般写公司的组织名称
  >
  > - eg：com.baidu，com.alibaba
  >
  > artifactId：项目的名称
  >
  > version：定义项目的当前版本

  - 注：[maven坐标搜索网站](https://mvnrepository.com/ '点击链接前往')

例如：要引入 `druid` ，只需要在 `pom.xml` 配置文件中配置引入 `druid` 的坐标即可：

```xml
<dependecies>
	<!--druid连接池-->
	<dependency>
  		<groupId>com.alibaba</groupId>
  		<artifactId>druid</artifactId>    
  		<version>1.0.9</version>  
	</dependency>
    <dependency>
    	<groupId>mysql</groupId>
        <artifactId>mysql-connector-java</artifactId>
        <version>5.1.6</version>
    </dependency>
</dependecies>
```

---

### Maven的安装

#### 下载Maven

<img src="https://gitee.com/chonguang/picture-bed/raw/master/imgs-typora/202203031554935.png" alt="image-20220303155425084"  />

> 下载地址：<http://maven.apache.org/>
>
> Windows电脑下载 `-bin.zip` 格式的安装包

---

####  安装Maven

>将Maven压缩包解压，即安装完毕

![image-20220303155750656](https://gitee.com/chonguang/picture-bed/raw/master/imgs-typora/202203031557704.png)

---

####  Maven目录介绍

![43](https://gitee.com/chonguang/picture-bed/raw/master/imgs-typora/202203031559349.png)

---

#### 配置环境变量

- 进入环境变量

  ![tu_5](https://gitee.com/chonguang/picture-bed/raw/master/imgs-typora/202203031600440.png)

- 配置 `MAVEN_HOME` 和 `Path` 

  ![image-20220303160143463](https://gitee.com/chonguang/picture-bed/raw/master/imgs-typora/202203031601540.png)

  <img src="https://gitee.com/chonguang/picture-bed/raw/master/imgs-typora/202203031603695.png" alt="image-20220303160344647"  />

---

#### 配置本地仓库

> 在maven安装目录中的 `conf/ settings.xml` 文件这里配置本地仓库
>
> 将 `<localRepository>/path/to/local/repo</localRepository>` 移出注释，选择自己仓库的位置即可

```xml
<settings xmlns="http://maven.apache.org/SETTINGS/1.2.0"
          xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
          xsi:schemaLocation="http://maven.apache.org/SETTINGS/1.2.0 https://maven.apache.org/xsd/settings-1.2.0.xsd">
  <!-- localRepository
   | The path to the local repository maven will use to store artifacts.
   |
   | Default: ${user.home}/.m2/repository
  <localRepository>/path/to/local/repo</localRepository>
  -->
  <localRepository>D:\repository</localRepository>
```

>检验本地仓库是否已经设置成功
>
>保存 `settings.xml` 后控制台输入 `mvn help:system` 

![1858147-20210117223002155-140318163](https://gitee.com/chonguang/picture-bed/raw/master/imgs-typora/202203032049247.png)

> 打开本地仓库后，发现里面生成文件，说明修改成功
>
> > 首次执行 `mvn help:system` 命令，Maven相关工具自动帮助到Maven中央仓库下载缺省的或者Maven中央仓库更新的各种配置文件和类库(jar包)到Maven本地仓库中
> >
> > 下载完各种文件后， `mvn help:system` 命令会打印出所有的Java系统属性和环境变量

![image-20220303181725232](https://gitee.com/chonguang/picture-bed/raw/master/imgs-typora/202203031817277.png)

---

> 修改maven的源地址为阿里源
>
> 打开Maven的配置文件(windows机器一般在maven安装目录的 `conf/settings.xml` )，在 `<mirrors></mirrors>` 标签中添加 `mirror` 子节点

```xml
<mirror>
    <id>aliyunmaven</id>
    <mirrorOf>*</mirrorOf>
    <name>阿里云公共仓库</name>
    <url>https://maven.aliyun.com/repository/public</url>
</mirror>
```

---

#### 测试Maven安装成功

>打开cmd本地控制台，输入 `mvn -version` ，如下图表示成功：

![image-20220303160909268](https://gitee.com/chonguang/picture-bed/raw/master/imgs-typora/202203031618654.png)

---

### IDEA集成Maven

#### 配置Maven

- 配置Maven![7](https://gitee.com/chonguang/picture-bed/raw/master/imgs-typora/202203031625429.png)

- 配置参数(解决创建慢的问题)  `-DarchetypeCatalog=internal` 

  ![tu_8](https://gitee.com/chonguang/picture-bed/raw/master/imgs-typora/202203031626785.png)

- 然后新创建project，注意不要使用原来的project，第一次使用maven创建项目的时候一定要联网

---

#### 使用IDEA创建Maven工程

##### 创建javaweb工程

- 创建javaweb工程在选择Maven骨架时，选择 `maven-archetype-webapp` 即可：![image-20220303163535404](https://gitee.com/chonguang/picture-bed/raw/master/imgs-typora/202203031635455.png)![image-20220303163918975](https://gitee.com/chonguang/picture-bed/raw/master/imgs-typora/202203031639066.png)

---

- 创建好的javaweb工程如下：

  ![image-20220303164256582](https://gitee.com/chonguang/picture-bed/raw/master/imgs-typora/202203031645938.png)

---

- 手动创建 `java目录` 与 `resources目录` ：

  ![image-20220303164847736](https://gitee.com/chonguang/picture-bed/raw/master/imgs-typora/202203031648773.png)

  ![image-20220303164916994](https://gitee.com/chonguang/picture-bed/raw/master/imgs-typora/202203031649022.png)

  ![image-20220303165109445](https://gitee.com/chonguang/picture-bed/raw/master/imgs-typora/202203031651476.png)

---

- 需要 `main/java` 文件夹变成源码的目录(存放java源码)

  ![image-20220303165457960](https://gitee.com/chonguang/picture-bed/raw/master/imgs-typora/202203031654037.png)

- 创建 `resources` 目录, 变成资源的目录

  ![image-20220303165714355](https://gitee.com/chonguang/picture-bed/raw/master/imgs-typora/202203031657425.png)

---

##### 发布javaweb工程

![image-20220303165958961](https://gitee.com/chonguang/picture-bed/raw/master/imgs-typora/202203031659994.png)

![image-20220303170035870](https://gitee.com/chonguang/picture-bed/raw/master/imgs-typora/202203031700964.png)

![image-20220303170059566](https://gitee.com/chonguang/picture-bed/raw/master/imgs-typora/202203031700659.png)

![image-20220303170423395](https://gitee.com/chonguang/picture-bed/raw/master/imgs-typora/202203031704524.png)

---

##### 浏览器访问效果

![image-20220303170339058](https://gitee.com/chonguang/picture-bed/raw/master/imgs-typora/202203031703173.png)

---

### 写在后面

> 如果是社区版的IDEA并没有Tomcat的直接选项，可以使用Maven配置Tomcat，也可以使用插件(`Smart Tomcat`)
>
> 具体方法请参考：
>
> - [IDEA社区版tomcat配置教程](https://blog.csdn.net/zhoukun1314/article/details/88910242 '点击链接前往')
> - [问题解决：idea社区版添加tomcat](https://www.cnblogs.com/zhizhiyin/articles/9089736.html '点击链接前往')

