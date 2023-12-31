---
title: LINUX后门复现环境搭建
date: 2022-03-21 21:36:37
tags: [Kali,后门,虚拟机]
categories:
 - 虚拟机
 - Kali-Linux
 - 后门
index_img: https://cdn.jsdelivr.net/gh/noneSycamore/noneSycamore.github.io/2022/03/21/LINUX%E5%90%8E%E9%97%A8%E5%A4%8D%E7%8E%B0%E7%8E%AF%E5%A2%83%E6%90%AD%E5%BB%BA/kali.png
banner_img: https://cdn.jsdelivr.net/gh/noneSycamore/noneSycamore.github.io/2022/03/21/LINUX%E5%90%8E%E9%97%A8%E5%A4%8D%E7%8E%B0%E7%8E%AF%E5%A2%83%E6%90%AD%E5%BB%BA/kali.png
---
采用虚拟机（**kali**-Linux）作为目标服务器，从 Windows 主机通过 **ssh** （Xshell）连接虚拟机，模拟getshell场景。
<!-- more -->

## VMware创建Kali虚拟机
如何创建 **Kali** 虚拟机就不多说了，网上的教程很多很多，

如果你懒得用 iso 镜像源一步一步来，这里放一个官网**配置好的虚拟机镜像文件**：[链接](https://kali.download/virtual-images/kali-2022.1/kali-linux-2022.1-vmware-amd64.7z)
（**VMware**的，因为我用的就是VMware搭的虚拟机）

如果你是**Virtual Box**，我也给你放一个好了：[链接](https://kali.download/virtual-images/kali-2022.1/kali-linux-2022.1-virtualbox-amd64.ova)

都是**kali**的，所以这篇文章对于 Debian 的应该都适用
## Xshell安装和会话创建
> 安装。。。懒得写了，所以 Xshell 就不提这个了，这篇[博客](https://www.jianshu.com/p/4716cc35750f)就很不错

要想**通过 Xshell 连接到Kali虚拟机**，我们需要在 Xshell 中新建一个会话

打开Xshell -> 文件 -> 新建，你就能看到下图所示的窗口，按照图片的标注填好信息：


![](https://res.cloudinary.com/sycamore/image/upload/v1704010995/Typera/2023/12/ec0e3b63c1b6407381f5fc198204b88b.png)


其中，会话的**名称**随意，**端口号**用默认的 22 就够了，唯一有疑问的，估计就是服务器（即虚拟机）的 **ip** 怎么写了。

其实很简单，运行虚拟机，在 **Terminal** 窗口中输入 `ifconfig` 命令就能查看到虚拟机的 ip 了：

![](https://res.cloudinary.com/sycamore/image/upload/v1704011010/Typera/2023/12/03de79df0a7a5f15066393d8b3fdc732.png)

比如上图中，我的 ip 就是 **192.168.168.128** ，把在这个填入表里就可以了。

## Kali配置SSH连接（问题汇总）
创建完会话就能成功连接了吗？

嘿嘿，你大概率会是这样的：
![](https://res.cloudinary.com/sycamore/image/upload/v1704011009/Typera/2023/12/44ad2149c5ece1467cd8f0dee447a105.png)

下面说一下该怎么解决。


### 开启

如果你这时候直接尝试，是连接不通的。
因为 kali **默认关闭了 ssh**，所以，我们还要**打开ssh服务**：`service ssh start`，
然后**查看ssh的状态**：`service ssh status`，
![](https://res.cloudinary.com/sycamore/image/upload/v1704011014/Typera/2023/12/bf8774117739cb26e9767cc0b5a1f9f5.png)
如果是这样 ssh 服务就成功开启了

然后，我们还可以设置一下，ssh **开机自启**：`sudo systemctl enable ssh`
如果想**关闭**开机自启的话：`sudo systemctl disable ssh`

最后，你可以~(￣▽￣)~*重启系统：`reboot`

### ping 不通吧

> 嘿嘿，你开启了 ssh ，重启了 kali 虚拟机，然后再次尝试从 Xshell 连接...
你可能会发现，还是和上面一样，**连接不上**。（因为有**可能不会**出现这个错误）

尝试 ping 一下虚拟机 ip：
![](https://res.cloudinary.com/sycamore/image/upload/v1704011015/Typera/2023/12/c72106aee3f1d8b7ac9a24d572b59b36.png)
总而言之就是还连接不上。

**原因可能有很多种：**
这里只说我遇到的问题，
其他的，可能是网关不太对、 VMnet8网络适配器IP不对等等原因（活用搜索吧...），
因为实在太多了，咱们得具体问题具体分析，所以就只说我的了 (/▽＼)

**解决方案是**：

- 打开VMware -> 编辑 -> **虚拟网络编辑器** -> 右下角**更改设置**（不点的话操作不了）-> 选中 **Vmnet8**那一项 -> 勾选**将主机虚拟连接到此网络**
（如果**已经勾上了**，重启一下这个服务：取消勾选，应用，然后再勾选一次，再应用即可）![](https://res.cloudinary.com/sycamore/image/upload/v1704011019/Typera/2023/12/97fccc2c2ee041cbd1e6feb5cacbf47d.png)
现在应该就能连上了。（不怕麻烦的话，就先这样吧)
<br><br>

上述方法**确实可行**，但是，我在后续使用时**发现**：
如果我**重启**了电脑，这个操作得**重来**过，才能连上 ssh 。。。

这对于我来说，每次来，实在是有点**麻烦**啊！！
所以我开始**活用搜索**了 (oﾟvﾟ)ノ，然后发现了这样**几个解决方案**，就记录一下：

- **配置端口转发**（对我没用） 
但一般用 **NAT** 连虚拟机网络的，大概都是这种：
**NAT** 模式使用虚拟机的一个虚拟网卡做**网关**，然后在网关上配 dhcp ，或者直接用静态地址。
这就相当于形成了一个虚拟的局域网 VLAN 。
这时候虚拟机能够访问外网（**向外通信没问题**），但主机想要访问虚拟机就**会出问题**。
所以我们需要在 NAT 的网卡上做**端口转发**就行（具体咋做CSDN上一堆）
<br>
- ...
（我这种还没找到解决方法，但上面的第一种可行）

### SSH服务拒绝密码
如果你 ping 通了，可能还会遇到我的这个问题：

![](https://res.cloudinary.com/sycamore/image/upload/v1704011024/Typera/2023/12/4a17b7f6085ed11e25581ad4af01ad96.png)

你输入的密码是正确的，但是提示：**SSH服务器拒绝了密码，请再试一次**

**解决方法：**
修改 ssh 针对服务器端的配置文件`vim /etc/ssh/sshd_config`
如下图所示：
![](https://res.cloudinary.com/sycamore/image/upload/v1704011028/Typera/2023/12/8900184ed3d063762a64a4307d9111e0.png)
总而言之改成这样，有注释的取掉注释

重启 ssh ：`systemctl restart sshd`
重启虚拟机：`reboot`

重新连接 Xshell：成功！
![](https://res.cloudinary.com/sycamore/image/upload/v1704011029/Typera/2023/12/bc8a0d69bbf2c5972d1bb2864e8e36f7.png)