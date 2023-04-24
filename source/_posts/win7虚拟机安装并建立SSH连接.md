---
title: win7虚拟机安装并建立SSH连接
date: 2022-04-09 18:10:52
tags: [Windows,虚拟机]
categories: 
 - 虚拟机
 - Windows
index_img: https://cdn.jsdelivr.net/gh/noneSycamore/noneSycamore.github.io/2022/04/09/win7%E8%99%9A%E6%8B%9F%E6%9C%BA%E5%AE%89%E8%A3%85%E5%B9%B6%E5%BB%BA%E7%AB%8BSSH%E8%BF%9E%E6%8E%A5/7.jpg
banner_img: https://cdn.jsdelivr.net/gh/noneSycamore/noneSycamore.github.io/2022/04/09/win7%E8%99%9A%E6%8B%9F%E6%9C%BA%E5%AE%89%E8%A3%85%E5%B9%B6%E5%BB%BA%E7%AB%8BSSH%E8%BF%9E%E6%8E%A5/7.jpg
---
Win7 虚拟机搭建的 二三事
<!-- more -->

因为要搞 **Windows** 的**渗透测试**，所以就要整一个 Win7 的虚拟机。

这篇文章就记录一下 **折腾** 的过程，一共包含：
1. **VMware Workstation Pro 16** 安装 **Windows 7** 虚拟机，
2. 安装 **VMware-Tools** 工具，解决**安装出错**的问题。
3. 创建 **win7** 共享文件夹
4. 安装建立和主机的 **SSH** 连接。

## 下载安装 win7 镜像
### 镜像下载（挑选)
照常，在 **MSDN** 上下载需要的 win7 镜像：
（[**MSDN** 传送门](https://msdn.itellyou.cn/)）

> 愿意挑的，进入链接后，按下图步骤 **下载镜像**（一定要选带 **SP1** 的，否则后续安装将会**失败**）：![](https://cdn.jsdelivr.net/gh/noneSycamore/blog_pic_url/win7vm1.png)

> 懒得挑的， 这里是本文镜像的 **磁力链接**：
> ```
> ed2k://|file|cn_windows_7_enterprise_with_sp1_x64_dvd_u_677685.iso|3265574912|E9DB2607EA3B3540F3FE2E388F8C53C4|/
> ```

### 安装 win7 虚拟机
1. `Ctrl + N`，或者 `文件 -> 新建虚拟机` 打开窗口：![](https://cdn.jsdelivr.net/gh/noneSycamore/blog_pic_url/win7vm2.png)
<br>
2. 选择 **典型**，下一步：
![](https://cdn.jsdelivr.net/gh/noneSycamore/blog_pic_url/win7vm3.png)
<br>
3. 选择安装的 **iso** 文件，按下图操作：
![](https://cdn.jsdelivr.net/gh/noneSycamore/blog_pic_url/win7vm4.png)
<br>
4. 填写 虚拟机 简易安装所需的**相关信息**：
![](https://cdn.jsdelivr.net/gh/noneSycamore/blog_pic_url/win7vm5.png)
若 **未填** 产品密钥，则**无需理会**这个提示：
![](https://cdn.jsdelivr.net/gh/noneSycamore/blog_pic_url/win7vm6.png)
另附，本文镜像（**win7** 企业版）的产品密钥：`33PXH-7Y6KF-2VJC9-XBBR8-HVTHH`，
若激活失败，方法如下：
> 1.  以管理员身份启动cmd
> 2.  `slmgr /skms kms.03k.org`
> 3.  `slmgr /ipk 33PXH-7Y6KF-2VJC9-XBBR8-HVTHH`
> 4. `slmgr /ato`

5. 填写虚拟机 名称、安装目录：
![](https://cdn.jsdelivr.net/gh/noneSycamore/blog_pic_url/win7vm7.png )
6. 填写磁盘容量：
![](https://cdn.jsdelivr.net/gh/noneSycamore/blog_pic_url/win7vm8.png)
> 默认即可，**无需理会** 空间分配得 是否 **过大**，
> 毕竟虚拟机不可能一下子把这些空间全用上，反而后续再**扩容** 才是**麻烦事**

8. 一路默认，完成安装，等待即可：
![](https://cdn.jsdelivr.net/gh/noneSycamore/blog_pic_url/win7vm9.png)![](https://cdn.jsdelivr.net/gh/noneSycamore/blog_pic_url/win7vm10.png)

进入 win7 桌面后，安装完成！
## 安装 VMware-Tools
这时候的虚拟机，是**没有安装 VMware-Tools** 的（Windows 的都得手动安装）

### 完全没有问题的 手动安装步骤
当然，完全**没有问题**的**手动安装**很简单，步骤如下：
1. 开启 **安装向导**
> `虚拟机 -> 安装 VMware-Tools`，耐心等待后，将**自动**开启安装，
> 若等待时间太长，按下图所示操作（只有点击`安装 VMware-Tools`选项后，才会挂载上**正确**的 D 盘）
> ![](https://cdn.jsdelivr.net/gh/noneSycamore/blog_pic_url/win7vm20.png)
> 
2. 点击运行 **运行 setup64.exe** ，出现一路弹窗
![](https://cdn.jsdelivr.net/gh/noneSycamore/blog_pic_url/win7vm15.png)![](https://cdn.jsdelivr.net/gh/noneSycamore/blog_pic_url/win7vm16.png)![](https://cdn.jsdelivr.net/gh/noneSycamore/blog_pic_url/win7vm17.png)![](https://cdn.jsdelivr.net/gh/noneSycamore/blog_pic_url/win7vm18.png)
成功开启 **安装向导**~
![](https://cdn.jsdelivr.net/gh/noneSycamore/blog_pic_url/win7vm19.png)
3. 下一步 -> 选择**典型安装** -> 下一步 -> 安装 -> 安装成功！
![](https://cdn.jsdelivr.net/gh/noneSycamore/blog_pic_url/win7vm21.png)
![](https://cdn.jsdelivr.net/gh/noneSycamore/blog_pic_url/win7vm30.png)
### 错误处理
但是，现实总是有 **各种意外**，总会有很多 **问题** 出现：
（每步都会有！）
#### 选项`安装 VMware-Tools` 为 灰色
如下图所示，这个安装选项是 **灰色** 的：
![](https://cdn.jsdelivr.net/gh/noneSycamore/blog_pic_url/win7vm11.png)
**解决办法：**
1. 关闭虚拟机：
![](https://cdn.jsdelivr.net/gh/noneSycamore/blog_pic_url/win7vm12.png)
2. 打开虚拟机设置 -> 选中软盘 -> 移除 -> 确定：
![](https://cdn.jsdelivr.net/gh/noneSycamore/blog_pic_url/win7vm13.png)
3. 启动虚拟机

可以看到，现在可以点击 `安装 VMware-Tools` 选项了：
![](https://cdn.jsdelivr.net/gh/noneSycamore/blog_pic_url/win7vm14.png)
#### Windows 无法验证此驱动程序软件的发布者
按照正常步骤启动 **安装向导** 后，提示：**Windows 无法验证此驱动程序软件的发布者**：
![](https://cdn.jsdelivr.net/gh/noneSycamore/blog_pic_url/win7vm22.png)

也不用做啥**无谓**的挣扎，这就是**报错**，可以直接退出了，后续报错如下：

![](https://cdn.jsdelivr.net/gh/noneSycamore/blog_pic_url/win7vm23.png)![](https://cdn.jsdelivr.net/gh/noneSycamore/blog_pic_url/win7vm24.png)

**原因：**
活用搜索之后，我有了大致的了解：

> 大概是 **Win7** 用的**驱动程序签名算法**，只支持 **SHA1**，
然后我用的又是：最新的 **VMware Workstation Pro 16**，
大概 **Vmware-Tools** 用的是 **SHA2**，所以通不过验证

**解决方法：**
1. 下载安装 **补丁kb4474419** 来支持SHA2算法。
[下载地址](https://www.catalog.update.microsoft.com/Search.aspx?q=kb4474419)
选择**符合的版本**下载（本文用的是 企业版的 **x64** ，也不是啥 **服务器** 版本，直接下载最后的即可）：
![](https://cdn.jsdelivr.net/gh/noneSycamore/blog_pic_url/win7vm25.png)
<br>
2. 利用 **FTP** 传入虚拟机
因为没有安装 **VMwarae-Tools**，所以虚拟机里 **没有网络连接**，也不能搞**共享文件夹**，只能使用 **FTP** 把补丁传进去。
推荐 **工具+文章**：[利用3CDaemon搭建FTP服务](https://blog.sycamore.top/2022/04/09/%E5%88%A9%E7%94%A83CDaemon%E6%90%AD%E5%BB%BAFTP%E6%9C%8D%E5%8A%A1/)（工具轻量便捷，当然你也可以自己搭 **FTP**）
<br>
3. 传入后，双击**运行** 补丁文件 即可（选择默认）：
<img src="https://cdn.jsdelivr.net/gh/noneSycamore/blog_pic_url/win7vm26.png" width=300 height=150 /><img src="https://cdn.jsdelivr.net/gh/noneSycamore/blog_pic_url/win7vm27.png" width=300 /><img src="https://cdn.jsdelivr.net/gh/noneSycamore/blog_pic_url/win7vm28.png" width=300 height=200 /><img src="https://cdn.jsdelivr.net/gh/noneSycamore/blog_pic_url/win7vm29.png" width=300 height=200 />
<br>
4. 重启后，可**正常**安装

## 创建 win7 共享文件夹
已经安装了 **VMware-Tools**，创建 **共享文件夹** 的动作就简单多了。
### VMware 虚拟机设置中添加
1. 打开虚拟机设置：
![](https://cdn.jsdelivr.net/gh/noneSycamore/blog_pic_url/win7vm31.png)
<br>
2. 按下图顺序操作，进入 **添加共享文件夹向导**：
![](https://cdn.jsdelivr.net/gh/noneSycamore/blog_pic_url/win7vm32.png)
<br>
3. 下一步 -> 填写 **主机路径** 和 虚拟机中显示的**名称** -> 完成！
![图 1](https://cdn.jsdelivr.net/gh/noneSycamore/blog_pic_url/win7vm33.png)![图 3](https://cdn.jsdelivr.net/gh/noneSycamore/blog_pic_url/win7vm35.png)![图 2](https://cdn.jsdelivr.net/gh/noneSycamore/blog_pic_url/win7vm34.png)
### win7 虚拟机中 映射网络驱动器
1. 打开 **控制面板** -> **网络和 internet** -> **网络和共享中心**，更改网络为：家庭 / 工作![](https://cdn.jsdelivr.net/gh/noneSycamore/blog_pic_url/win7vm36.png)
<br>
2. 选中 **计算机** -> 选择 **映射网络驱动器** -> **浏览**（等待搜索完毕） -> `vmware-host \ Shared Folders \ 共享文件夹名` -> 确定 -> 完成 ！
![](https://cdn.jsdelivr.net/gh/noneSycamore/blog_pic_url/win7vm37.png)

可以看到，完成 **映射** 后，在驱动器(Z:)下，出现了之前**设置**里添加的 **共享文件夹**：
![](https://cdn.jsdelivr.net/gh/noneSycamore/blog_pic_url/win7vm38.png)
## 安装建立 SSH 连接
虽然有了 **共享文件夹**，文件传输变得非常方便，
但是终究还是 **Xshell** 和 **Xftp** 香啊。

### bibi ~ 两句缘由
因为除 **Win7** 之外，我还有很多其他的虚拟机，
尤其是学习**渗透**测试的时候，总会遇到需要 **两个虚拟机** 之间来回倒的情况。

如果每次切换，都要在 **图形界面** 折腾半天，实在是太麻烦了。
而且，如果间隔时间**拿捏**得好一点，还可能会出现：每次切换都得 **输一遍密码** 的情况，
这就有点离谱了……

而 **Xshell** 界面简洁，不同会话之间**切换方便**，就**完全没有**这样的担忧。
当然不是说可以 **舍弃** 图形界面了，该用的时候，还是得去用的。

不管怎么说，对我而言，整个 **SSH** 很重要，可以让我的学习方便不少。

### 下载 安装 配置 OpenSSH
#### 下载：
[**Github** 源码下载地址](https://github.com/PowerShell/Win32-OpenSSH/releases)
![](https://cdn.jsdelivr.net/gh/noneSycamore/blog_pic_url/win7vm39.png)
下哪个都行，瞅准 64 / 32 位的版本问题就行。

#### 安装：
我下的 Zip 文件，由 **共享文件夹** 传入虚拟机，然后解压到 `C:\Program Files`目录：
![](https://cdn.jsdelivr.net/gh/noneSycamore/blog_pic_url/win7vm40.png)
这样 SSH 就好了，后续**配置完成**就可以使用了

<br>

**安装 sshd 服务：**

以**管理员**身份运行 **cmd**，
**cd** 到安装目录，输入命令：`powershell.exe -ExecutionPolicy Bypass -File install-sshd.ps1`
![](https://cdn.jsdelivr.net/gh/noneSycamore/blog_pic_url/win7vm45.png)

#### 配置：
- **1. 添加到环境变量:**
计算机右键 -> 属性 -> 高级系统设置 -> 环境变量—系统变量—Path -> 双击编辑 **Path**，添加：`;C:\Program Files\OpenSSH-Win64`（即：`;安装目录`）
![](https://cdn.jsdelivr.net/gh/noneSycamore/blog_pic_url/win7vm41.png) ![](https://cdn.jsdelivr.net/gh/noneSycamore/blog_pic_url/win7vm42.png)![](https://cdn.jsdelivr.net/gh/noneSycamore/blog_pic_url/win7vm43.png)
**CMD** 输入：`ssh` 验证，成功添加！
![](https://cdn.jsdelivr.net/gh/noneSycamore/blog_pic_url/win7vm44.png)
成功安装！
<br>
- **2. 配置sshd服务:**<br>
**配置开机自启sshd服务：**
命令：`sc config sshd start= auto`
![](https://cdn.jsdelivr.net/gh/noneSycamore/blog_pic_url/win7vm46.png)<br>
**开启 sshd 服务：**
命令：`net start sshd`
![](https://cdn.jsdelivr.net/gh/noneSycamore/blog_pic_url/win7vm47.png)<br>
**开启 22 端口**
（已关闭防火墙的不用执行）
命令：`netsh advfirewall firewall add rule name=sshd dir=in action=allow protocol=TCP localport=22`
![](https://cdn.jsdelivr.net/gh/noneSycamore/blog_pic_url/win7vm48.png)
#### Xshell 连接试验
1. 命令：` ipconfig`，获取当前 Win7 虚拟机的 **IP 地址** ：192.168.158.135
![](https://cdn.jsdelivr.net/gh/noneSycamore/blog_pic_url/win7vm49.png)

2. **Xshell** 建立新会话：
![](https://cdn.jsdelivr.net/gh/noneSycamore/blog_pic_url/win7vm50.png)
3. 接收保存 Win7 虚拟机 SSH **密钥**：
![](https://cdn.jsdelivr.net/gh/noneSycamore/blog_pic_url/win7vm51.png)
4. 输入正确的 **用户名**、**密码** 后，成功登录 Win7：
![](https://cdn.jsdelivr.net/gh/noneSycamore/blog_pic_url/win7vm52.png)


