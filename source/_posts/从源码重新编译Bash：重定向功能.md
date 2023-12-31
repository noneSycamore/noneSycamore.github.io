---
title: 从源码重新编译 Bash：重定向功能
date: 2022-04-20 13:09:20
tags: [Kali,虚拟机]
categories:
 - 虚拟机
 - Kali-Linux
index_img: https://res.cloudinary.com/sycamore/image/upload/v1704033693/Typera/2023/12/3ea0ff03af3b42b348eeb0416d6a28d1.jpg
banner_img: https://res.cloudinary.com/sycamore/image/upload/v1704033693/Typera/2023/12/3ea0ff03af3b42b348eeb0416d6a28d1.jpg
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
	<img src="https://res.cloudinary.com/sycamore/image/upload/v1704011789/Typera/2023/12/a6dc5cf7a829a5a6097d237405661fca.png" style="zoom: 50%;" />

<br>
- 查看 **bash** 的版本：
	- `bash --version` 
	<img src="https://res.cloudinary.com/sycamore/image/upload/v1704011798/Typera/2023/12/72468c0ebb118510e769b5b84090330a.png" style="zoom: 50%;" />

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
<img src="https://res.cloudinary.com/sycamore/image/upload/v1704011808/Typera/2023/12/34cc060cd5b5566b1e3199248a5d1b9d.png" style="zoom:50%;" />

### 解压
**解压**源码包 并 **进入**生成的目录：

解压：`tar zxvf bash-5.1.16.tar.gz `
解压后，会在当前目录下生成一个 **bash-** 目录：
<img src="https://res.cloudinary.com/sycamore/image/upload/v1704011821/Typera/2023/12/f735c3f744f1c15416e9ed316c072c5e.png" style="zoom: 50%;" />

进入目录：`cd bash-5.1.16`

### 配置（configure）
`--prefix` 参数指定 **安装目录**，`--enable-net-redirections` 为 bash 添加 **重定向功能**

命令：`./configure --prefix=/usr/local/bash --enable-net-redirections`
<img src="https://res.cloudinary.com/sycamore/image/upload/v1704011834/Typera/2023/12/56ff26d1b92b96426325dc707626d147.png" style="zoom:50%;" />

### 编译 & 安装
编译命令：`make`
<img src="https://res.cloudinary.com/sycamore/image/upload/v1704011840/Typera/2023/12/06946af30cebfad1df042a0913409994.png" style="zoom:50%;" />

安装命令：`make install`
<img src="https://res.cloudinary.com/sycamore/image/upload/v1704011843/Typera/2023/12/071576989e4ab50a87b4319ab34c6adc.png" style="zoom:50%;" />

## 更换使用
- 把新安装的 bash 添加到 `/etc/shells` 文件中：`echo "/usr/local/bash/bin/bash" >> /etc/shells`
- 更换 **Shell** ：`chsh -s /usr/local/bash/bin/bash`
- 重启：`reboot`

更换后，查看使用的 Shell ：
<img src="https://res.cloudinary.com/sycamore/image/upload/v1704011845/Typera/2023/12/04a9e7185976fdfa19a6a6f9dec41af1.png" style="zoom:50%;" />

成功！
