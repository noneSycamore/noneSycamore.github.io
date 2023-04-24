---
title: 利用3CDaemon搭建FTP服务
date: 2022-04-09 21:13:52
tags: [虚拟机,FTP]
categories: 
 - 虚拟机
index_img: https://cdn.jsdelivr.net/gh/noneSycamore/noneSycamore.github.io/2022/04/09/%E5%88%A9%E7%94%A83CDaemon%E6%90%AD%E5%BB%BAFTP%E6%9C%8D%E5%8A%A1/3CDaemon.jpg
banner_img: https://cdn.jsdelivr.net/gh/noneSycamore/noneSycamore.github.io/2022/04/09/%E5%88%A9%E7%94%A83CDaemon%E6%90%AD%E5%BB%BAFTP%E6%9C%8D%E5%8A%A1/3CDaemon.jpg
---
因为安装 Win7 虚拟机，被迫搞出来的 FTP 服务
<!-- more -->


## bibibi~
吐槽一下写这篇文章的原因（可越过本节）。

起因是要搞 Windows 的**渗透测试**，所以就要整一个 Win7 的虚拟机。
然后 Win7 镜像下好了，安装也安好了，基本上就剩下安装 **Vmware-Tools** 了。
结果来了一堆 **报错**~~~

害，然后网上一搜，大概是 **Win7** 用的**驱动程序签名算法**，太 **low**了，只支持 **SHA1**，

然后我用的又是，最新的 **VMware Workstation Pro 16**，
盲猜 **Vmware-Tools** 用的是 **SHA2**，那这指定通不过验证嘛~

所以，我需要下载安装补丁 kb4474419 来支持 SHA2 算法，
> 补丁传送门-----> ([Microsoft Update Catalog](https://www.catalog.update.microsoft.com/Search.aspx?q=kb4474419))

然后，就是重点了。。。
我没装 **Vmware-Tools** ，那 **Win7** 连不上网，也么的**共享文件夹**好用，
思来想去也就只有搭个 **FTP** 了啊！

再然后，由于嫌 自己布置 ftp 太麻烦 ~，所以就有了 **3CDaemon**

## 简单介绍 3CDaemon
**3CDaemon** 是一个好用的**简易服务器工具**，包含 **TFTP** 服务器、**FTP** 服务器、**Syslog** 服务器 和 **TFTP** 客户机 **四**个功能。
**3CDaemon** 使用方便，面板简洁，可以让我们的 **主机** 快速变成一个 **FTP客户端**，
让我们能够在**无外网**连接的情况下，在内网中快速地**传递文件**。

（这篇文章仅包含**利用 3CDaemon 搭建 FTP 服务**）

**图标：**
<img src="https://cdn.jsdelivr.net/gh/noneSycamore/blog_pic_url/3CDaemon1.png " width=200 height=200 />

**界面：**
<img src="https://cdn.jsdelivr.net/gh/noneSycamore/blog_pic_url/3CDaemon2.png " width=600 />

**中文版下载**： -----> [下载地址](https://github.com/noneSycamore/blog_pic_url/raw/main/3CDaemon.EXE)
（亲测**可用无毒**，要用官方英文版的就自行搜索吧）
## 主机配置 3CDaemon
打开下载好的 **3CDaemon** 软件，在左侧栏中，点开 **FTP 服务器**，按照下图步骤完成 **FTP** 登录**用户**的设置：
![](https://cdn.jsdelivr.net/gh/noneSycamore/blog_pic_url/3CDaemon3.png)
（反正是自用，用户权限就全给上了）

## 虚拟机开启 FTP 服务
**Win7** 默认是**没有**开启 **FTP** 服务的，所以我们要手动打开（在 **Win10** 也是差不多的操作）：

1. 打开控制面版：
![](https://cdn.jsdelivr.net/gh/noneSycamore/blog_pic_url/3CDaemon4.png)
<br>
2. 单击 **程序** 进入设置：
![](https://cdn.jsdelivr.net/gh/noneSycamore/blog_pic_url/3CDaemon5.png)
<br>
3. 进入 **打开或关闭 Windows 功能**，找到 **Internet 信息服务**，图中对应项**打勾**：
![](https://cdn.jsdelivr.net/gh/noneSycamore/blog_pic_url/3CDaemon6.png)
<br>
4. 等待一段时间后，跟随提示重启电脑
<img src="https://cdn.jsdelivr.net/gh/noneSycamore/blog_pic_url/3CDaemon7.png" width=300 />  <img src="https://cdn.jsdelivr.net/gh/noneSycamore/blog_pic_url/3CDaemon8.png" width=300 />

## 虚拟机连接 FTP 服务器
首先确定虚拟机和主机之间能够**相互ping** 通，并且虚拟机已开启 **21** 端口（**关闭防火墙**也行）
![](https://cdn.jsdelivr.net/gh/noneSycamore/blog_pic_url/3CDaemon9.png)

虚拟机打开 **CMD 窗口** ，输入：`ftp 主机IP`；
按下图所示，依次输入**之前添加**的用户名、密码。
![](https://cdn.jsdelivr.net/gh/noneSycamore/blog_pic_url/3CDaemon10.png)
连接成功！

## 如何简单地用FTP 传接文件
先找到之前设置的，主机共享文件的目录，
当我们在**虚拟机**中登录到 **FTP** 的时候，就是在这个**主机**的共享文件**目录**下。

1. 在主机共享目录下，随便放一个文件：
<img src="https://cdn.jsdelivr.net/gh/noneSycamore/blog_pic_url/3CDaemon11.png " width=600 />
<br>
2. 虚拟机 **CMD** 终端输入 `dir` 命令查看共享目录下的文件：
<img src="https://cdn.jsdelivr.net/gh/noneSycamore/blog_pic_url/3CDaemon12.png" width=600 />
<br>
3. 使用 `get 文件名` 下载对应文件
（如无意外，文件保存在 **进入FTP时所在的路径下**）
<img src="https://cdn.jsdelivr.net/gh/noneSycamore/blog_pic_url/3CDaemon13.png" width=600 />
<br>
4. 输入 `by`，退出 **FTP**，关闭 **221** 服务
![](https://cdn.jsdelivr.net/gh/noneSycamore/blog_pic_url/3CDaemon14.png)

**完成 ~~~**
