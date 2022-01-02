---
title: kolla与OpenStack
date: 2021-10-03 14:44:26 +0800
category: 云计算
tags: 云计算
excerpt: kolla与OpenStack的爱情
---



## kolla与OpenStack

### 1. 下载iso镜像

   链接：https://pan.baidu.com/s/1MsL-NW9CGcrkAbX2tOt5LQ
   提取码：g6h4 
   （过期请留言）

### 2. 创建一个搭建OpenStack的虚拟机

   ![1](https://gitee.com/chonguang/picture-bed/raw/master/imgs-typora/202201021344856.png)
   ![2](https://gitee.com/chonguang/picture-bed/raw/master/imgs-typora/202201021338870.png)
   ![3](https://gitee.com/chonguang/picture-bed/raw/master/imgs-typora/202201021338908.png)
   ![4](https://gitee.com/chonguang/picture-bed/raw/master/imgs-typora/202201021344820.png)
   ![5](https://gitee.com/chonguang/picture-bed/raw/master/imgs-typora/202201021338117.png)
   ![6](https://gitee.com/chonguang/picture-bed/raw/master/imgs-typora/202201021344899.png)
   ![7](https://gitee.com/chonguang/picture-bed/raw/master/imgs-typora/202201021344230.png)
   ![8](https://gitee.com/chonguang/picture-bed/raw/master/imgs-typora/202201021344187.png)
   ![9](https://gitee.com/chonguang/picture-bed/raw/master/imgs-typora/202201021344182.png)
   ![10](https://gitee.com/chonguang/picture-bed/raw/master/imgs-typora/202201021339333.png)
   ![11](https://gitee.com/chonguang/picture-bed/raw/master/imgs-typora/202201021339533.png)
   ![12](https://gitee.com/chonguang/picture-bed/raw/master/imgs-typora/202201021339780.png)
   ![13](https://gitee.com/chonguang/picture-bed/raw/master/imgs-typora/202201021344712.png)
   ![14](https://gitee.com/chonguang/picture-bed/raw/master/imgs-typora/202201021344871.png)
   ![15](https://gitee.com/chonguang/picture-bed/raw/master/imgs-typora/202201021344770.png)
   ![16](https://gitee.com/chonguang/picture-bed/raw/master/imgs-typora/202201021344950.png)

>以上的环境配好之后，先不要启动，开始配置网卡

   ![17](https://gitee.com/chonguang/picture-bed/raw/master/imgs-typora/202201021344179.png)
   ![18](https://gitee.com/chonguang/picture-bed/raw/master/imgs-typora/202201021344037.png)

>配置两个虚拟网卡的ip

   ![19](https://gitee.com/chonguang/picture-bed/raw/master/imgs-typora/202201021344571.png)

>完成上面的配置之后完成，配置windows的网卡

   ![20](https://gitee.com/chonguang/picture-bed/raw/master/imgs-typora/202201021344578.png)
   ![21](https://gitee.com/chonguang/picture-bed/raw/master/imgs-typora/202201021344128.png)
   ![22](https://gitee.com/chonguang/picture-bed/raw/master/imgs-typora/202201021344328.png)
   ![23](https://gitee.com/chonguang/picture-bed/raw/master/imgs-typora/202201021344660.png)

>启动虚拟机

   ![24](https://gitee.com/chonguang/picture-bed/raw/master/imgs-typora/202201021344425.png)
   ![25](https://gitee.com/chonguang/picture-bed/raw/master/imgs-typora/202201021344583.png)

>这一步比较慢，耐心等待

   ![26](https://gitee.com/chonguang/picture-bed/raw/master/imgs-typora/202201021340182.png)

>到这一步就完成虚拟机的安装，登录名：kolla，密码：kollapass

   ![27](https://gitee.com/chonguang/picture-bed/raw/master/imgs-typora/202201021344272.png)

>到这一步不要以为就奥利给了

   ![28](https://gitee.com/chonguang/picture-bed/raw/master/imgs-typora/202201021344992.png)

### 3. 配置openstack

   - kolla安装的命令

   ```Xml
 # 切换到root用户
 sudo -s
 # 切换到根目录
 cd
 # 查看编译
 kolla-ansible
 # 预先检查阶段 无failed=0表示安装成功
 kolla-ansible prechecks
 # 安装 无failed=0表示安装成功
 kolla-ansible deploy
 # 查看启动的命令
 docker ps
 # 生成src文件
 kolla-ansible post-deploy
 ## cp rc.sh文件到当前目录（根目录）
 cp /etc/kolla/admin-openrc.sh .
 # 查看启动的服务
 source admin-openrc.sh
 # 开启临时容器
 openstack
 # 查看服务
 service list
 # ctrl+d退出，然后查看ip
 ip addr
   ```

   - 查看密码

   ```Cmd
cat admin-openrc.sh
   ```

   >使用xshell连接，复制密码
   >ip使用的是10.10.10.2，账号：kolla，密码：kollapass
   >
   >```Cmd
   ># 连接成功之后，切换到root用户
   >sudo -s
   ># 切换到存放admin-openrc.sh文件的目录下，这里我是放在根目录下的
   ># cd直接到根目录
   >cd
   ># 查看密码
   >cat admin-openrc.sh
   >```
   >
   >![29](https://gitee.com/chonguang/picture-bed/raw/master/imgs-typora/202201021344462.png)
   >
   > - 在浏览器输入10.10.10.254显示如下
   >   ![30](https://gitee.com/chonguang/picture-bed/raw/master/imgs-typora/202201021340516.png)

   >账号：admin，密码是在xshell中cat后的那段复制粘贴，然后登录

   ![31](https://gitee.com/chonguang/picture-bed/raw/master/imgs-typora/202201021340793.png)

   - 下载所需的文件地址，文件不全或未更新到，也可以到其他的地方下载

   >download.cirros-cloud.net

   ![32](https://gitee.com/chonguang/picture-bed/raw/master/imgs-typora/202201021340982.png)