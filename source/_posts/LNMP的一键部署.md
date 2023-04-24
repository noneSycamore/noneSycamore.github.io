---
title: LNMP的一键部署
date: 2022-03-14 13:26:36
tags: 
- 云服务器
categories:
- 云服务器
index_img: https://cdn.jsdelivr.net/gh/noneSycamore/noneSycamore.github.io/2022/03/14/LNMP%E7%9A%84%E4%B8%80%E9%94%AE%E9%83%A8%E7%BD%B2/1.jpg
banner_img: https://cdn.jsdelivr.net/gh/noneSycamore/noneSycamore.github.io/2022/03/14/LNMP%E7%9A%84%E4%B8%80%E9%94%AE%E9%83%A8%E7%BD%B2/1.jpg
---
**详细教程**：两种简单方法部署LNMP，包括宝塔面板的安装（小白向，不想麻烦的就进来看吧）
<!-- more -->
## 前言~
提供服务器上部署lnmp的两个简单的方法，个人推荐第二种，宝塔面板实在是太香了！
顺便安上本人安装lnmp的选择
（emm...确实，我两个方法都安装过(°ー°〃)）
## 方式一：使用官网lnmp一键安装包
贴上官网上的安装教程：[https://lnmp.org/install.html](https://lnmp.org/install.html)
有问题可以自行查询，大部分应该没啥问题，若是还有问题没解决就直接用宝塔吧~
### 准备
先要装个远程命令窗口，推荐Xshell，还附带个文件传输的功能Xftp；putty也可以，小巧精简
选一个用就行了~
放个[Xshell](https://blog.csdn.net/qq_33173608/article/details/106757749 "Xshell")的安装教程...
### 安装lnmp稳定版
就是无人值守安装，无人值守安装是一个新增的功能，可以预设好相关参数自动进行安装，不需要按提示一个一个的选择，适合批量安装部署；
如果需要使用无人值守安装，请使用[无人值守命令生成工具](https://lnmp.org/auto.html "无人值守命令生成工具")，或查看[无人值守说明](https://lnmp.org/faq/v1-5-auto-install.html "无人值守说明")，获得无人值守安装的命令
### 一般方法
执行命令：`wget http://soft.vpser.net/lnmp/lnmp1.8.tar.gz -cO lnmp1.8.tar.gz && tar zxf lnmp1.8.tar.gz && cd lnmp1.8 && ./install.sh lnmp`

然后你会看到这个：

![](https://cdn.jsdelivr.net/gh/noneSycamore/whitzard_cdn/wp-content/uploads/2021/09/lnmp1.5-install-1.png)

让我们选择MySQL的版本，本人选择了4，
要注意的是：MySQL 5.6,5.7及MariaDB 10必须在1G以上内存的更高配置上才能选择

然后要我们输入数据库的密码：![](https://cdn.jsdelivr.net/gh/noneSycamore/whitzard_cdn/wp-content/uploads/2021/09/lnmp1.5-install-2.png)

如果你不小心输错了密码，你可以按住Ctrl再按Backspace键进行删除

再然后， 询问是否需要启用MySQL InnoDB：

![](https://cdn.jsdelivr.net/gh/noneSycamore/whitzard_cdn/wp-content/uploads/2021/09/lnmp1.5-install-3.png)

InnoDB引擎默认为开启，一般建议开启，直接回车或输入 y ，
如果确定确实不需要该引擎可以输入 n，(MySQL 5.7+版本无法关闭InnoDB),输入完成，回车进入下一步

让我们选择PHP版本：

![](https://cdn.jsdelivr.net/gh/noneSycamore/whitzard_cdn/wp-content/uploads/2021/09/lnmp1.5-install-4.png)

这里需要考虑到：选择PHP 7+版本时需要自行确认PHP版本是否与自己的程序兼容， 不过还是建议7+版本，至少目前wordpress网站已经不支持5.5以下的php版本安装了
所以我选了8 (。＾▽＾)

下一步选择是否安装内存优化

![](https://cdn.jsdelivr.net/gh/noneSycamore/whitzard_cdn/wp-content/uploads/2021/09/lnmp1.5-install-5.png)

回车不安装就可以了，想要安装的话就在2，3中选，Jemalloc或者TCMalloc，想要深入了解的可以戳[这里](https://www.cnblogs.com/cthon/p/10563946.html "这里")

再就等待它装好就可以了，时间要很久，大概半个小时左右吧，可以先做其他事情...
就像这样：
![](https://cdn.jsdelivr.net/gh/noneSycamore/whitzard_cdn/wp-content/uploads/2021/09/lnmp1.5-install-success.png)

- 显示Nginx: OK，MySQL: OK，PHP: OK，
- 并且Nginx、MySQL、PHP都是running，80和3306端口都存在，
- 提示了安装使用的时间且最后出现Install lnmp V1.6 completed! enjoy it.

那就说明你安装成功了!
如果安装失败，问题不大，可以卸载lnmp后重新安装：
进入lnmp安装目录，输入./uninstall.sh回车即可 ，命令如下：
`cd lnmp1.4`
`ls`
`./uninstall.sh`
后续内容可以参考[这里](https://lnmp.org/faq/lnmp-vhost-add-howto.html)，这篇博客就不再赘述了，毕竟是LNMP的安装教程，而且本人也没去尝试后续开虚拟主机的内容

## 方式二：宝塔一键安装

### 安装宝塔面板
#### **安装要求：**
内存：512M以上，推荐768M以上（纯面板约占系统60M内存）
硬盘：300M以上可用硬盘空间（纯面板约占20M磁盘空间）
系统：CentOS 7.1+ (Ubuntu16.04+.、Debian9.0+)，确保是干净的操作系统，没有安装过其它环境带的Apache/Nginx/php/MySQL/pgsql/gitlab/java（已有环境不可安装）
架构：x86_64（主流服务器均是此架构），ARM不完整兼容（面板环境安装慢，部分软件可能安装不上）

系统兼容性顺序：Centos7.x > Debian10 > Ubuntu 20.04 > Cenots8.x > Ubuntu 18.04 > 其它系统
（所以建议服务器采用Cento7.x版本的，反正租的都是一个价不是吗(ง •_•)ง）
#### 关于开端口的问题
emm...宝塔面板需要服务器放行安全组，(ps: 这个很重要!)
就根据自己租的服务器点击下方链接，然后照做就行，操作简单的：
阿里、腾讯、华为
开好了就直接从下面选对应的安装就可以了
#### **Linux面板7.7.0安装命令：**
Centos安装命令：
`yum install -y wget && wget -O install.sh http://download.bt.cn/install/install_6.0.sh && sh install.sh`
试验性Centos/Ubuntu/Debian安装命令，独立运行环境（py3.7），可能存在少量兼容性问题
`curl -sSO http://download.bt.cn/install/install_panel.sh && bash install_panel.sh`
Ubuntu/Deepin安装命令：
`wget -O install.sh http://download.bt.cn/install/install-ubuntu_6.0.sh && sudo bash install.sh`
Debian安装命令：
`wget -O install.sh http://download.bt.cn/install/install-ubuntu_6.0.sh && bash install.sh`
Fedora安装命令:
`wget -O install.sh http://download.bt.cn/install/install_6.0.sh && bash install.sh`
Linux面板7.7.0升级命令：curl `http://download.bt.cn/install/update6.sh|bash`

#### 安装成功!
![](https://cdn.jsdelivr.net/gh/noneSycamore/whitzard_cdn/wp-content/uploads/2021/09/QQ截图20210908143811.png)

不要关！注意要保存这里圈出来的内容，这是宝塔后台地址和账号密码
我们可以复制到记事本保存一下...
### 宝塔安装LNMP
在浏览器上打开上面保存的地址，登入宝塔面板（输入你上面保存的账号密码），面板会自动推荐你安装环境套件，
这里有两种选择，第一种是LNMP套件，第二种是LAMP套件：

![](https://cdn.jsdelivr.net/gh/noneSycamore/whitzard_cdn/wp-content/uploads/2021/09/btlnmp.png)

在这里你可以选择LNMP的版本，php版本的问题之前已经提到过：
选择PHP 7+版本时需要自行确认PHP版本是否与自己的程序兼容，不过还是建议7+版本，至少目前wordpress网站已经不支持5.5以下的php版本安装了，不过这里给出的配置也没什么问题，后续也可以更新版本...

要注意的一点是，安装方式的选择：
为确保后期程序运行的稳定性，请选择编译安装！极速安装主要用体验和测试使用，正常情况下应当避免使用极速安装！

然后点击一键安装就行了，会自动跳入任务列表（没有的话就在左上角那里），界面上会显示程序的安装进度，时间大概十几分钟吧。列表上都显示安装成功就大功告成了！

## ps

- 宝塔面板当然你也可以选择安装LAMP，不过我之所以选择LNMP，因为nginx具有的特点是，并发能力强并且占用内存小，所以更推荐安装这个(/▽＼)
- 之所以推荐宝塔面板来安装，因为宝塔对网站的后续建设也很方便，wordpress等建站系统也可以一键部署，还有Https设置，自动定期备份等，所以强推哦(ง •_•)ง
- 本文完成于2021/9/8，请核对时间，部分内容可能因为时间关系与实际不符！X﹏X
