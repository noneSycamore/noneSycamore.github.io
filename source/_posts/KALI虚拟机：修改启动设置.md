---
title: KALI虚拟机：修改启动设置
date: 2022-03-23 15:13:52
tags: [Kali,虚拟机]
categories: 
 - 虚拟机
 - Kali-Linux
index_img: https://res.cloudinary.com/sycamore/image/upload/v1704033144/Typera/2023/12/b7ea9d1222bacb7781961d44117c400f.jpg
banner_img: https://res.cloudinary.com/sycamore/image/upload/v1704033144/Typera/2023/12/b7ea9d1222bacb7781961d44117c400f.jpg
---
对 kali 启动设置的几种懒人向的优化
<!-- more -->

**起因**是，在写 [LINUX 后门复现环境搭建](https://blog.sycamore.top/2022/03/21/LINUX%E5%90%8E%E9%97%A8%E5%A4%8D%E7%8E%B0%E7%8E%AF%E5%A2%83%E6%90%AD%E5%BB%BA/) 的时候，总是需要 `reboot` 重启 kali 虚拟机，
然后我就发现：**每次**登录输密码啥的，实在是**太麻烦了**...
所以就有了这篇文章 O(∩_∩)O

总而言之就是，对 kali 启动设置的几种**懒人向**的优化


## 允许 root 用户登录
（初次安装 Kali 记得**最好**先进 root 模式，然后 `passwd root` 命令设置 root 密码）

最新的几版 Kali ，默认把直接**用 root 用户登录**给关了，
也就是说，你在这个 ↓ 界面，用户名 **root** ，密码也**正确**，还是进不去的。
![](https://res.cloudinary.com/sycamore/image/upload/v1704010452/Typera/2023/12/a402df1a20b236ddcbcf1eee3e254813.png)
我们需要经过设置才能以 root 身份登录 Kali ：

1. 启动 kali 虚拟机，在下图所示的**引导页面**，按 **e** 进入编辑模式：
![](https://res.cloudinary.com/sycamore/image/upload/v1704010455/Typera/2023/12/ee9e095803026b6734c0a8c908209e6f.png)
2. 修改以下红框内容（`ro quite splash`）为 `rw init=/bin/sh splash`，然后按 **Ctrl + X** 退出编辑模式，重启系统
修改前：![](https://res.cloudinary.com/sycamore/image/upload/v1704010458/Typera/2023/12/511e5615a8474f12b4de12e701c32d67.png)
修改后：![](https://res.cloudinary.com/sycamore/image/upload/v1704010528/Typera/2023/12/2711dc66462686c032f9aaa47489fe83.png)

现在，就可以用 root **直接登陆**了







## 跳过登录页面直接进
因为总是需要重启 **Kali** 虚拟机，然后**每次重启**都要输一遍账号密码。。。
实在是太**麻烦**了，我就想着该怎么**跳过登录页面**，直接进（释放双手）

1. 打开 Termial，输入命令：`vim /etc/lightdm/lightdm.conf`
编辑 **lightdm.conf** 文件（因为 **Kali** 的登录界面就是 **LightDM** 的）
<br>
2. 找到 **[Seat:*]** 这一行，在它的**下方**添加下面两行代码，或者**取消**这两行代码的**注释**
（一定要是 **Seat**下面，因为它的**前面**有**一样的**，被注释的代码，别搞错了）
![](https://res.cloudinary.com/sycamore/image/upload/v1704010461/Typera/2023/12/3d4b0b74cf92beadd8ecd4dfd9f9907c.png)
添加的代码：
`autologin-user=root`（用 **root** 用户登录，如果你想用**其他的用户**，改成对应的就行）
`autologin-user-timeout=0`
如图所示：
![](https://res.cloudinary.com/sycamore/image/upload/v1704010465/Typera/2023/12/79cd91f5f023cbad0cc14f46c39d0119.png)
保存退出：`Esc`+`:wq`
<br>
3. 修改pam相关的验证文件，输入命令：`vim /etc/pam.d/lightdm-autologin`，
注释掉`auth required pam_succeed_if.so user != root quiet_success`这一行，完成~
![](https://res.cloudinary.com/sycamore/image/upload/v1704010468/Typera/2023/12/2d63a7f739e8266cde13b950dfe93f9b.png)
<br>
4. 重启查看效果：`reboot`






## 启动跳过5s引导界面
就是这个：
![](https://res.cloudinary.com/sycamore/image/upload/v1704010471/Typera/2023/12/7bf93978563fcf67505a8dc94ac19443.png)
改了 **跳过登录页面** 之后，感觉这个**引导界面**又有点**多余**了（反正要用的时候再改回来)
因为要等的话，要等 **5s** ，不想等的话，还得按个**回车键**跳过~
那我为了**释放双手**，自然得去掉这玩意

1. 打开 Termial，输入命令：`vim /etc/default/grub	`
编辑 grub 文件，因为 **Kali** 用的启动引导程序就是 **GRUB**
<br>
2. 将 **GRUB_TIMEOUT** 设置成 **0**（就是你**等待的时间**），保存退出：`Esc`+`:wq`
![](https://res.cloudinary.com/sycamore/image/upload/v1704010474/Typera/2023/12/df74a7f1e325b85e1e40d39e1520b6d9.png)
3. 命令：`update-grub` 更新文件，然后重启查看效果：`reboot`
![](https://res.cloudinary.com/sycamore/image/upload/v1704010480/Typera/2023/12/cc110976411f12bcacdd0c9fa001c7d6.png)
<br>
到这里，就**改完了**，以后就能**直接进 root** ，而且**启动登录Kali**全程能够**释放双手**了~

## 补充：关闭自动锁屏
有没有遇到一种情况，你在等待 Kail 完成某项长时间的操作，于是就先去干手头上一些其他的事情了，
然后等你回来的时候，发现 Kali **已经锁屏**了。。。
所以，你还要再输一遍用户密码，那为什么不**干脆关闭锁屏**呐？

1. 打开电源设置 Power manager settings：
![](https://res.cloudinary.com/sycamore/image/upload/v1704010479/Typera/2023/12/0759d1a59a1f52034cc9405a21936f9c.png)
2. 点击 Security，取消勾选这个选项，就能关闭锁屏：
![](https://res.cloudinary.com/sycamore/image/upload/v1704010483/Typera/2023/12/5d4bcd7102648ae38c3565ddc0802b9c.png)
然后直接关闭设置就行，Kali 里面没有**保存确定**之说
