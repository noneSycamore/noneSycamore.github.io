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

> 愿意挑的，进入链接后，按下图步骤 **下载镜像**（一定要选带 **SP1** 的，否则后续安装将会**失败**）：![](https://res.cloudinary.com/sycamore/image/upload/v1704011056/Typera/2023/12/732bbc1c86ae1a240189d78f76323dde.png)

> 懒得挑的， 这里是本文镜像的 **磁力链接**：
> ```
> ed2k://|file|cn_windows_7_enterprise_with_sp1_x64_dvd_u_677685.iso|3265574912|E9DB2607EA3B3540F3FE2E388F8C53C4|/
> ```

### 安装 win7 虚拟机
1. `Ctrl + N`，或者 `文件 -> 新建虚拟机` 打开窗口：![](https://res.cloudinary.com/sycamore/image/upload/v1704011056/Typera/2023/12/9f57f4f5c20651c0c7345d6525ab8705.png)
<br>
2. 选择 **典型**，下一步：
![](https://res.cloudinary.com/sycamore/image/upload/v1704011059/Typera/2023/12/f6dc889e5b91bffc0f7c7a09001cd10a.png)
<br>
3. 选择安装的 **iso** 文件，按下图操作：
![](https://res.cloudinary.com/sycamore/image/upload/v1704011062/Typera/2023/12/73142fdc9301d5fc842da5723fd1884d.png)
<br>
4. 填写 虚拟机 简易安装所需的**相关信息**：
![](https://res.cloudinary.com/sycamore/image/upload/v1704011066/Typera/2023/12/53ac1d29ff5046b17161e7d8c8686b21.png)
若 **未填** 产品密钥，则**无需理会**这个提示：
![](https://res.cloudinary.com/sycamore/image/upload/v1704011070/Typera/2023/12/c978f6c017b98d82eef567df860c9033.png)
另附，本文镜像（**win7** 企业版)的产品密钥：`33PXH-7Y6KF-2VJC9-XBBR8-HVTHH`，
若激活失败，方法如下：
> 1.  以管理员身份启动cmd
> 2.  `slmgr /skms kms.03k.org`
> 3.  `slmgr /ipk 33PXH-7Y6KF-2VJC9-XBBR8-HVTHH`
> 4. `slmgr /ato`

5. 填写虚拟机 名称、安装目录：
![](https://res.cloudinary.com/sycamore/image/upload/v1704011074/Typera/2023/12/4bb7d478563dee6ac3eba031d54bcd80.png )
6. 填写磁盘容量：
![](https://res.cloudinary.com/sycamore/image/upload/v1704011077/Typera/2023/12/27e06d25f47f9fa092c86337b9ff76e7.png)
> 默认即可，**无需理会** 空间分配得 是否 **过大**，
> 毕竟虚拟机不可能一下子把这些空间全用上，反而后续再**扩容** 才是**麻烦事**

8. 一路默认，完成安装，等待即可：
![](https://res.cloudinary.com/sycamore/image/upload/v1704011080/Typera/2023/12/ba138c24863acc2f766c9dc2c97e4e7c.png)![](https://res.cloudinary.com/sycamore/image/upload/v1704011091/Typera/2023/12/c67cd9c3eca856dcf7b9afffe42ce04b.png)

进入 win7 桌面后，安装完成！
## 安装 VMware-Tools
这时候的虚拟机，是**没有安装 VMware-Tools** 的（Windows 的都得手动安装）

### 完全没有问题的 手动安装步骤
当然，完全**没有问题**的**手动安装**很简单，步骤如下：
1. 开启 **安装向导**
> `虚拟机 -> 安装 VMware-Tools`，耐心等待后，将**自动**开启安装，
> 若等待时间太长，按下图所示操作（只有点击`安装 VMware-Tools`选项后，才会挂载上**正确**的 D 盘）
> <img src="https://res.cloudinary.com/sycamore/image/upload/v1704011088/Typera/2023/12/9518839fc213f5938b8332abff0dc02b.png" style="zoom:50%;" />
2. 点击运行 **运行 setup64.exe** ，出现一路弹窗
<img src="https://res.cloudinary.com/sycamore/image/upload/v1704011124/Typera/2023/12/5db950f7def8f35c953c8b3c4a42d881.png" style="zoom: 33%;" /><img src="https://res.cloudinary.com/sycamore/image/upload/v1704011124/Typera/2023/12/5db950f7def8f35c953c8b3c4a42d881.png" style="zoom:33%;" /><img src="https://res.cloudinary.com/sycamore/image/upload/v1704011159/Typera/2023/12/797cdb56de4efbdd991810b2c51b8bc9.png" style="zoom:33%;" /><img src="https://res.cloudinary.com/sycamore/image/upload/v1704011139/Typera/2023/12/664d1586ebe92c056b2f6942ec1da5db.png" style="zoom:33%;" />
成功开启 **安装向导**~
<img src="https://res.cloudinary.com/sycamore/image/upload/v1704011193/Typera/2023/12/1c360a3a308086b1e217dc746532a859.png" style="zoom:33%;" />
3. 下一步 -> 选择**典型安装** -> 下一步 -> 安装 -> 安装成功！
<img src="https://res.cloudinary.com/sycamore/image/upload/v1704011314/Typera/2023/12/cfee97b9944dbec5002894eb353bc189.png" style="zoom:33%;" />
<img src="https://res.cloudinary.com/sycamore/image/upload/v1704011219/Typera/2023/12/fae7cf18234e155a74fa9d3acb0bcb1d.png" style="zoom:33%;" />
### 错误处理
但是，现实总是有 **各种意外**，总会有很多 **问题** 出现：
（每步都会有！）
#### 选项`安装 VMware-Tools` 为 灰色
如下图所示，这个安装选项是 **灰色** 的：
<img src="https://res.cloudinary.com/sycamore/image/upload/v1704011224/Typera/2023/12/c4f0dc2b49eaa529a837a52443102b74.png" style="zoom:33%;" />
**解决办法：**

1. 关闭虚拟机：
<img src="https://res.cloudinary.com/sycamore/image/upload/v1704011382/Typera/2023/12/409c36c79d3f79d5fc923038d1cae855.png" style="zoom: 50%;" />
2. 打开虚拟机设置 -> 选中软盘 -> 移除 -> 确定：
<img src="https://res.cloudinary.com/sycamore/image/upload/v1704011391/Typera/2023/12/97933ab1b93b6f58c9bf98de5a695e25.png" style="zoom: 25%;" />
3. 启动虚拟机

可以看到，现在可以点击 `安装 VMware-Tools` 选项了：
<img src="https://res.cloudinary.com/sycamore/image/upload/v1704011415/Typera/2023/12/27bb09d7fbc23a99fdad2bb17465de90.png" style="zoom:50%;" />

#### Windows 无法验证此驱动程序软件的发布者
按照正常步骤启动 **安装向导** 后，提示：**Windows 无法验证此驱动程序软件的发布者**：
<img src="https://res.cloudinary.com/sycamore/image/upload/v1704011423/Typera/2023/12/7344a093df7c3d0378f6ad0272d2da46.png" style="zoom:33%;" />

也不用做啥**无谓**的挣扎，这就是**报错**，可以直接退出了，后续报错如下：

<img src="https://res.cloudinary.com/sycamore/image/upload/v1704011428/Typera/2023/12/9fbc42a80baf094cf36a2a1ee0faa1a0.png" style="zoom:33%;" /><img src="https://res.cloudinary.com/sycamore/image/upload/v1704011441/Typera/2023/12/a8266fa96d0098dd1d0ebf67c259dbc3.png" style="zoom:25%;" />

**原因：**
活用搜索之后，我有了大致的了解：

> 大概是 **Win7** 用的**驱动程序签名算法**，只支持 **SHA1**，
然后我用的又是：最新的 **VMware Workstation Pro 16**，
大概 **Vmware-Tools** 用的是 **SHA2**，所以通不过验证

**解决方法：**
1. 下载安装 **补丁kb4474419** 来支持SHA2算法。
[下载地址](https://www.catalog.update.microsoft.com/Search.aspx?q=kb4474419)
选择**符合的版本**下载（本文用的是 企业版的 **x64** ，也不是啥 **服务器** 版本，直接下载最后的即可）：
<img src="https://res.cloudinary.com/sycamore/image/upload/v1704011462/Typera/2023/12/9d7cf0dc62e194752ce64acff268a0f4.png" style="zoom: 33%;" />
<br>
2. 利用 **FTP** 传入虚拟机
因为没有安装 **VMwarae-Tools**，所以虚拟机里 **没有网络连接**，也不能搞**共享文件夹**，只能使用 **FTP** 把补丁传进去。
推荐 **工具+文章**：[利用3CDaemon搭建FTP服务](https://blog.sycamore.top/2022/04/09/%E5%88%A9%E7%94%A83CDaemon%E6%90%AD%E5%BB%BAFTP%E6%9C%8D%E5%8A%A1/)（工具轻量便捷，当然你也可以自己搭 **FTP**）
<br>
3. 传入后，双击**运行** 补丁文件 即可（选择默认）：
<img src="https://res.cloudinary.com/sycamore/image/upload/v1704011466/Typera/2023/12/3b78e80e548be7f2ffd94ad11df0b24f.png" width=300 height=150 /><img src="https://res.cloudinary.com/sycamore/image/upload/v1704013543/Typera/2023/12/139f37b41fb83453846760f2e9d7f95f.png" width=300 /><img src="https://res.cloudinary.com/sycamore/image/upload/v1704013524/Typera/2023/12/0c6bb7564a7959d634afe58301666b43.png" width=300 height=200 /><img src="https://res.cloudinary.com/sycamore/image/upload/v1704011469/Typera/2023/12/0c8795cbb61aa3496c107f37ec56c38c.png" width=300 height=200 />
<br>
4. 重启后，可**正常**安装

## 创建 win7 共享文件夹
已经安装了 **VMware-Tools**，创建 **共享文件夹** 的动作就简单多了。
### VMware 虚拟机设置中添加
1. 打开虚拟机设置：
<img src="https://res.cloudinary.com/sycamore/image/upload/v1704011489/Typera/2023/12/4a53a9e9813aec7a05d218b75e3e8667.png" style="zoom:33%;" />
<br>
2. 按下图顺序操作，进入 **添加共享文件夹向导**：
<img src="https://res.cloudinary.com/sycamore/image/upload/v1704011494/Typera/2023/12/a8613435610b1698b6f64c749d906a24.png" style="zoom:33%;" />
<br>
3. 下一步 -> 填写 **主机路径** 和 虚拟机中显示的**名称** -> 完成！
<img src="https://res.cloudinary.com/sycamore/image/upload/v1704011496/Typera/2023/12/cf59190da10a0138614a134e7cfb9a25.png" alt="图 1" style="zoom:33%;" /><img src="https://res.cloudinary.com/sycamore/image/upload/v1704011499/Typera/2023/12/a051de4369b412a3cdfb32ef6896ab0a.png" alt="图 3" style="zoom:33%;" /><img src="https://res.cloudinary.com/sycamore/image/upload/v1704011509/Typera/2023/12/63ce694dc5f2b1428595f2fc187ad1b9.png" alt="图 2" style="zoom:33%;" />
### win7 虚拟机中 映射网络驱动器
1. 打开 **控制面板** -> **网络和 internet** -> **网络和共享中心**，更改网络为：家庭 / 工作<img src="https://res.cloudinary.com/sycamore/image/upload/v1704011504/Typera/2023/12/c4aed9b3c78629168582da06c5028d62.png" style="zoom:33%;" />
<br>
2. 选中 **计算机** -> 选择 **映射网络驱动器** -> **浏览**（等待搜索完毕） -> `vmware-host \ Shared Folders \ 共享文件夹名` -> 确定 -> 完成 ！
<img src="https://res.cloudinary.com/sycamore/image/upload/v1704011549/Typera/2023/12/7241038b0f9c1810e40eca0d9e61063f.png" style="zoom:33%;" />

可以看到，完成 **映射** 后，在驱动器(Z:)下，出现了之前**设置**里添加的 **共享文件夹**：
<img src="https://res.cloudinary.com/sycamore/image/upload/v1704011551/Typera/2023/12/849b4af650d6a33c3e897cf93adf25b6.png" style="zoom:33%;" />

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
![](https://res.cloudinary.com/sycamore/image/upload/v1704011578/Typera/2023/12/d71056d7226535c865c84cfb32993188.png)
下哪个都行，瞅准 64 / 32 位的版本问题就行。

#### 安装：
我下的 Zip 文件，由 **共享文件夹** 传入虚拟机，然后解压到 `C:\Program Files`目录：
<img src="https://res.cloudinary.com/sycamore/image/upload/v1704011584/Typera/2023/12/e103c81a48ea89479a4c58bdadff4e51.png" style="zoom:33%;" />
这样 SSH 就好了，后续**配置完成**就可以使用了

<br>

**安装 sshd 服务：**

以**管理员**身份运行 **cmd**，
**cd** 到安装目录，输入命令：`powershell.exe -ExecutionPolicy Bypass -File install-sshd.ps1`
<img src="https://res.cloudinary.com/sycamore/image/upload/v1704011586/Typera/2023/12/7f0e2aeede30e9e7bef278cd799999d6.png" style="zoom:33%;" />

#### 配置：
- **1. 添加到环境变量:**
计算机右键 -> 属性 -> 高级系统设置 -> 环境变量—系统变量—Path -> 双击编辑 **Path**，添加：`;C:\Program Files\OpenSSH-Win64`（即：`;安装目录`）
<img src="https://res.cloudinary.com/sycamore/image/upload/v1704011589/Typera/2023/12/96b3372363059f03c69026e1df16a6a4.png" style="zoom:33%;" /> <img src="https://res.cloudinary.com/sycamore/image/upload/v1704011592/Typera/2023/12/2498a6600d64e23cb30890f4774f5ed7.png" style="zoom:33%;" /><img src="https://res.cloudinary.com/sycamore/image/upload/v1704011595/Typera/2023/12/b42c72c3269992563814f5085e0d7c0c.png" style="zoom:33%;" />
**CMD** 输入：`ssh` 验证，成功添加！
<img src="https://res.cloudinary.com/sycamore/image/upload/v1704011637/Typera/2023/12/ad67bc3965d7e26632fc679eb4b830fd.png" style="zoom:33%;" />
成功安装！
<br>
- **2. 配置sshd服务:**<br>
**配置开机自启sshd服务：**
命令：`sc config sshd start= auto`
<img src="https://res.cloudinary.com/sycamore/image/upload/v1704011644/Typera/2023/12/a13290b8e8e00b19358fbf1a09101eb6.png" style="zoom:33%;" /><br>
**开启 sshd 服务：**
命令：`net start sshd`
<img src="https://res.cloudinary.com/sycamore/image/upload/v1704011647/Typera/2023/12/487dc56353077dac03f1a549065a0410.png" style="zoom:33%;" /><br>
**开启 22 端口**
（已关闭防火墙的不用执行）
命令：`netsh advfirewall firewall add rule name=sshd dir=in action=allow protocol=TCP localport=22`
<img src="https://res.cloudinary.com/sycamore/image/upload/v1704011650/Typera/2023/12/733b5d4ef353b9436e8e4fc75ccbb569.png" style="zoom:33%;" />
#### Xshell 连接试验
1. 命令：` ipconfig`，获取当前 Win7 虚拟机的 **IP 地址** ：192.168.158.135
<img src="https://res.cloudinary.com/sycamore/image/upload/v1704011652/Typera/2023/12/8ba32cc228e050ff54b5daa5b41e357a.png" style="zoom:33%;" />

2. **Xshell** 建立新会话：
<img src="https://res.cloudinary.com/sycamore/image/upload/v1704011656/Typera/2023/12/d86af85d7896e644d181c9f1373a6a16.png" style="zoom:33%;" />
3. 接收保存 Win7 虚拟机 SSH **密钥**：
<img src="https://res.cloudinary.com/sycamore/image/upload/v1704011689/Typera/2023/12/cf3013572443782af0cc280791d0a5f8.png" style="zoom:33%;" />
4. 输入正确的 **用户名**、**密码** 后，成功登录 Win7：
<img src="https://res.cloudinary.com/sycamore/image/upload/v1704011693/Typera/2023/12/73a799a15a695318a344898afe732f73.png" style="zoom: 50%;" />

