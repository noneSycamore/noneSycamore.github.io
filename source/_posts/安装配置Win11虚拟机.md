---
title: 安装配置 Win11 虚拟机
date: 2022-04-10 18:35:51
tags: [Windows,虚拟机]
categories: 
 - 虚拟机
 - Windows
index_img: https://cdn.jsdelivr.net/gh/noneSycamore/noneSycamore.github.io/2022/04/10/%E5%AE%89%E8%A3%85%E9%85%8D%E7%BD%AEWin11%E8%99%9A%E6%8B%9F%E6%9C%BA/11.jpg
banner_img: https://cdn.jsdelivr.net/gh/noneSycamore/noneSycamore.github.io/2022/04/10/%E5%AE%89%E8%A3%85%E9%85%8D%E7%BD%AEWin11%E8%99%9A%E6%8B%9F%E6%9C%BA/11.jpg
---
手贱...删了电脑里所有的虚拟机，还没有备份...这是重新安装 Win11 的记录
<!-- more -->
## Win11 镜像下载
还是 **MSDN** 香啊！
同域名下的另一个网站（试运行）：[NEXT, ITELLYOU](https://next.itellyou.cn/)
点击 顶部导航栏 的 **原版网站**：
![](https://cdn.jsdelivr.net/gh/noneSycamore/blog_pic_url/win11vm2.png)

选择 **Windows 11** ：
![](https://cdn.jsdelivr.net/gh/noneSycamore/blog_pic_url/win11vm1.png)
本文镜像为 **Win11 专业版**：
![](https://cdn.jsdelivr.net/gh/noneSycamore/blog_pic_url/win11vm3.png)
图中两版本的**区别**：
> business editions版本包含：Education(教育版)、Enterprise (企业版)、Professional(专业版)

> consumer editions版本包含：Home(家庭版)、Education(教育版)、Professional(专业版)

**另附**：本文镜像的 **磁力链接**：
> ```
> ed2k://|file|zh-cn_windows_11_business_editions_updated_march_2022_x64_dvd_7df6eae1.iso|5582235648|B7C9D076AE16A10C9D2610207577F28D|/
> ```

## 安装 Win11 虚拟机
### 新建虚拟机向导
1. 文件 -> 新建虚拟机，进入 **新建虚拟机向导**，
点击下一步，进入下图画面，选择 安装来源：
![](https://cdn.jsdelivr.net/gh/noneSycamore/blog_pic_url/win11vm4.png)

2. 下一步，选择虚拟机的 **操作系统**。
（因为 **VMware** 还没添加 **Win11** 的版本，所以选择 **Windows 10 x64**：
![](https://cdn.jsdelivr.net/gh/noneSycamore/blog_pic_url/win11vm5.png)

3. 下一步，选择磁盘容量（最好大于 **60** GB）
![](https://cdn.jsdelivr.net/gh/noneSycamore/blog_pic_url/win11vm6.png)

4. 更改安装的 **硬件**：
因为从 Win10 升级到 Win11 有 **最低硬件要求**，即：

	-   **处理器**：1 GHz 或更快，在兼容的 64 位处理器或片上系统 (SoC) 上具有两个或更多内核。
	-   **RAM**：4 GB 或更大。
	-   **存储空间**：安装 Windows 11 需要 64 GB 或更大的可用存储空间。

	![](https://cdn.jsdelivr.net/gh/noneSycamore/blog_pic_url/win11vm7.png)

点击 **完成** 后，退出 向导

### 更改虚拟机设置
从 **新建虚拟机向导** 退出后，先 **不要** 启动虚拟机，
因为这时候启动**安装**，还是会 在安装过程中 提醒：
![](https://cdn.jsdelivr.net/gh/noneSycamore/blog_pic_url/win11vm12.png)

我们还需要 更改几项虚拟机**设置**：
打开 虚拟机设置，
1. `选项 -> 访问控制 -> 加密 -> 输入密码`
![](https://cdn.jsdelivr.net/gh/noneSycamore/blog_pic_url/win11vm13.png)

2. `硬件 -> 添加 -> 可信平台模块 -> 完成`
（此后每次点开这个虚拟机，都要输 **密码** 了）
![](https://cdn.jsdelivr.net/gh/noneSycamore/blog_pic_url/win11vm14.png)

现在再启动虚拟机，安装就不会提示：**无法运行 Win11** 了.

### 启动虚拟机，开始安装
1. 打开后会遇到下图所示的画面，
![](https://cdn.jsdelivr.net/gh/noneSycamore/blog_pic_url/win11vm8.png)
不要等太久再 “按任意键”，
因为如果时间过了，会提示 `Time out`，然后就 **卡** 在下图所示的画面了：
![](https://cdn.jsdelivr.net/gh/noneSycamore/blog_pic_url/win11vm9.png)

2. 一波 `Next` 过后，我们选择安装的 **操作系统版本**（我选的专业版）：
![](https://cdn.jsdelivr.net/gh/noneSycamore/blog_pic_url/win11vm10.png)

3. 遇到这一步时，选择自定义：仅安装 Windows （高级），
因为我们是要 **完整地**安装，而非更新。
![](https://cdn.jsdelivr.net/gh/noneSycamore/blog_pic_url/win11vm15.png)

4. 这一步，选择 “新建”，就是要**分配** **C盘**、**D盘**，把 Windows 安装在分配的磁盘里。
![](https://cdn.jsdelivr.net/gh/noneSycamore/blog_pic_url/win11vm16.png)

5. 到这里，大致要 **注意** 的安装步骤就没了，开始等待：
![](https://cdn.jsdelivr.net/gh/noneSycamore/blog_pic_url/win11vm17.png)
从这里开始，就是通常的 Windows 启动步骤了：
（没人不会吧，放张图，就不说了）
![](https://cdn.jsdelivr.net/gh/noneSycamore/blog_pic_url/win11vm18.png)

5. 完成！等待即可 ~
![](https://cdn.jsdelivr.net/gh/noneSycamore/blog_pic_url/win11vm19.png)

## 安装 VMware-Tools
因为 后面要 **激活** Win11，几个命令很长（没装就不能 **复制**），

而且后续使用，肯定是有 **VMware-Tools** 更方便，

所以我们在激活之前，先装一下 **VMware-Tools**


1. `虚拟机 -> 安装 VMware-Tools`

<img src="https://cdn.jsdelivr.net/gh/noneSycamore/blog_pic_url/win11vm22.png " width=300 />
2. 耐心等待运行 **安装向导**，
如果实在是太慢了，等不及了，就进入 **文件资源管理器**，找到 D 盘，双击运行 `setup64` 程序：
（这个 **DVD 驱动器(D:)** ，只有 第一步点了 `安装 VMware-Tools` 按钮之后才有）
![](https://cdn.jsdelivr.net/gh/noneSycamore/blog_pic_url/win11vm23.png)
3. 两个加载的 弹窗 之后，成功打开 **安装向导**：
（只需要注意选择 **典型安装** ，**Win11** 的 **VMware-Tools** 大概率不会报错）
安装完成后，**重新启动** 虚拟机
<img src="https://cdn.jsdelivr.net/gh/noneSycamore/blog_pic_url/win11vm24.png " width=300 height=250 /><img src="https://cdn.jsdelivr.net/gh/noneSycamore/blog_pic_url/win11vm25.png " width=300 height=250 />

## 激活 Win11 专业版
现在安装好的 Win11 是没有激活的，不能长时间使用：
![](https://cdn.jsdelivr.net/gh/noneSycamore/blog_pic_url/win11vm20.png )
**激活步骤：**
1. 以管理员身份打开 **CMD**：
<img src="https://cdn.jsdelivr.net/gh/noneSycamore/blog_pic_url/win11vm21.png" width=600 height=300 />
2. **安装 KMS 客户端密钥**，
命令：`slmgr /ipk W269N-WFGWX-YVC9B-4J6C9-T83GX`
<img src="https://cdn.jsdelivr.net/gh/noneSycamore/blog_pic_url/win11vm26.png " width=600 height=300 />
3. **设置 KMS 服务器**，
命令：`slmgr /skms s8.uk.to`
如果执行失败，说明该 KMS 服务器 可能已失效。
尝试**更换** 该命令后半部分的 **KMS 服务器名**，[查询地址传送门](https://kms.msguides.com/)
![](https://cdn.jsdelivr.net/gh/noneSycamore/blog_pic_url/win11vm27.png)
4. **激活 Windows**
命令：`slmgr /ato`
![](https://cdn.jsdelivr.net/gh/noneSycamore/blog_pic_url/win11vm29.png)

成功**激活** ！
![](https://cdn.jsdelivr.net/gh/noneSycamore/blog_pic_url/win11vm28.png)
## 添加共享文件夹
步骤和 **Win7** 类似，
1. 虚拟机设置中添加 **共享文件夹**

2. `控制面板 -> 网络和 Internet -> 网络和共享中心 -> 高级共享设置`，
启动当前网络类型（专用/公用）的 **网络发现**
![](https://cdn.jsdelivr.net/gh/noneSycamore/blog_pic_url/win11vm30.png)
3. `此电脑 -> 映射网络驱动器`：
![](https://cdn.jsdelivr.net/gh/noneSycamore/blog_pic_url/win11vm31.png)
4. 浏览，选择 **映射的目录**，确定即可：
![](https://cdn.jsdelivr.net/gh/noneSycamore/blog_pic_url/win11vm33.png)
![](https://cdn.jsdelivr.net/gh/noneSycamore/blog_pic_url/win11vm32.png)

完成 **共享文件夹** 的添加！
![](https://cdn.jsdelivr.net/gh/noneSycamore/blog_pic_url/win11vm34.png)
