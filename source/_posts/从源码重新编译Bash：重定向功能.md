---
title: 从源码重新编译 Bash：重定向功能
date: 2022-04-20 13:09:20
tags: [Kali,虚拟机]
categories:
 - 虚拟机
 - Kali-Linux
index_img: https://cdn.jsdelivr.net/gh/noneSycamore/noneSycamore.github.io/2022/04/20/%E4%BB%8E%E6%BA%90%E7%A0%81%E9%87%8D%E6%96%B0%E7%BC%96%E8%AF%91Bash%EF%BC%9A%E9%87%8D%E5%AE%9A%E5%90%91%E5%8A%9F%E8%83%BD/bash.jpg
banner_img: https://cdn.jsdelivr.net/gh/noneSycamore/noneSycamore.github.io/2022/04/20/%E4%BB%8E%E6%BA%90%E7%A0%81%E9%87%8D%E6%96%B0%E7%BC%96%E8%AF%91Bash%EF%BC%9A%E9%87%8D%E5%AE%9A%E5%90%91%E5%8A%9F%E8%83%BD/bash.jpg
---
Kali 中预装的 bash 没有编译 重定向功能，所以要用到 -e 选项，需要重新编译 bash
<!-- more -->
## 重新编译 Bash 的原因
大部分 **Linux** 版本都已经 **预装了 bash**，
但是我的 **Kali** 虚拟机，貌似默认**没开 bash 的 网络重定向** 功能（ **-e** 不能使用），

而在尝试 **反弹 shell** 的时候，利用 **bash 反弹**的方法需要用到 **重定向**...

为了使用 bash 重定向的功能，大概只能 **从源码重新编译一遍 bash**

与直接编译不同的是，编译时需要加上 **`–enable-net-redirections`**
## 查看 Bash Shell 版本
因为 **Kali Linux** 用的 **Shell** 不是 **bash**，所以：
- 查看系统使用的 **Shell**：
	- `echo $SHELL`
	- 可以看到 Kali Linux 用的是 **zsh**：
![](https://cdn.jsdelivr.net/gh/noneSycamore/blog_pic_url/rebash2.png)

<br>
- 查看 **bash** 的版本：
	- `bash --version` 
![](https://cdn.jsdelivr.net/gh/noneSycamore/blog_pic_url/rebash1.png)

## 下载安装 Bash
**Linux** 下安装 **bash** 实际上有三种方式：
RPM 包安装、yum 安装、从源码安装。

但是，我的**目的**是，要加上 **`–enable-net-redirections` 编译 bash**，
所以 前两种方式都不那么直观（可能也可以？）
总而言之，这里只介绍第三种方式：**源码安装**

### 下载
- 我使用的 **版本** 的下载链接（5.1.16，与原来预装的一致）---> [传送门](https://ftp.gnu.org/gnu/bash/bash-5.1.16.tar.gz)
<br>
- 或者，去页面 [[Index of /gnu/bash]](https://ftp.gnu.org/gnu/bash/) 挑选下载的版本：
<br>
- 或者也可以，访问 **Bash** 的官方页面：[[Bash]](http://www.gnu.org/software/bash/bash.html)，自行挑选下载方式。

不管使用哪种方式，你都获得了需要的 **下载链接** 了，
然后你可以直接通过浏览器下载，或者使用 **wget**：
`wget https://ftp.gnu.org/gnu/bash/bash-5.1.16.tar.gz`
如图：
![](https://cdn.jsdelivr.net/gh/noneSycamore/blog_pic_url/rebash3.png)

### 解压
**解压**源码包 并 **进入**生成的目录：

解压：`tar zxvf bash-5.1.16.tar.gz `
解压后，会在当前目录下生成一个 **bash-** 目录：
![](https://cdn.jsdelivr.net/gh/noneSycamore/blog_pic_url/rebash4.png)

进入目录：`cd bash-5.1.16`

### 配置（configure）
`--prefix` 参数指定 **安装目录**，`--enable-net-redirections` 为 bash 添加 **重定向功能**

命令：`./configure --prefix=/usr/local/bash --enable-net-redirections`
![](https://cdn.jsdelivr.net/gh/noneSycamore/blog_pic_url/rebash5.png)

### 编译 & 安装
编译命令：`make`
![](https://cdn.jsdelivr.net/gh/noneSycamore/blog_pic_url/rebash6.png)

安装命令：`make install`
![](https://cdn.jsdelivr.net/gh/noneSycamore/blog_pic_url/rebash7.png)

## 更换使用
- 把新安装的 bash 添加到 `/etc/shells` 文件中：`echo "/usr/local/bash/bin/bash" >> /etc/shells`
- 更换 **Shell** ：`chsh -s /usr/local/bash/bin/bash`
- 重启：`reboot`

更换后，查看使用的 Shell ：
![](https://cdn.jsdelivr.net/gh/noneSycamore/blog_pic_url/rebash8.png)

成功！
