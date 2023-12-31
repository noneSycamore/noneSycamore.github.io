---
title: 安装配置 Win11 虚拟机
date: 2022-04-10 18:35:51
tags: [Windows,虚拟机]
categories: 
 - 虚拟机
 - Windows
index_img: https://res.cloudinary.com/sycamore/image/upload/v1704033769/Typera/2023/12/25793f68127f486bbbaa7d5bb6499ce4.jpg
banner_img: https://res.cloudinary.com/sycamore/image/upload/v1704033769/Typera/2023/12/25793f68127f486bbbaa7d5bb6499ce4.jpg
---
手贱...删了电脑里所有的虚拟机，还没有备份...这是重新安装 Win11 的记录
<!-- more -->

## Win11 镜像下载
还是 **MSDN** 香啊！
同域名下的另一个网站（试运行）：[NEXT, ITELLYOU](https://next.itellyou.cn/)
点击 顶部导航栏 的 **原版网站**：
<img src="https://res.cloudinary.com/sycamore/image/upload/v1704012174/Typera/2023/12/791dff305a14ba82d730664438c3b2eb.png" style="zoom: 33%;" />

选择 **Windows 11** ：
<img src="https://res.cloudinary.com/sycamore/image/upload/v1704012183/Typera/2023/12/2d57c74687e7f7757dedc6cfedff53cc.png" style="zoom: 25%;" />
本文镜像为 **Win11 专业版**：
![](https://res.cloudinary.com/sycamore/image/upload/v1704012200/Typera/2023/12/ff2d6147b7583139faac82d6b193eeec.png)
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
<img src="https://res.cloudinary.com/sycamore/image/upload/v1704012209/Typera/2023/12/d3a8942d2ad0b317c0cc62648ee8bf92.png" style="zoom: 50%;" />

2. 下一步，选择虚拟机的 **操作系统**。
（因为 **VMware** 还没添加 **Win11** 的版本，所以选择 **Windows 10 x64**：
<img src="https://res.cloudinary.com/sycamore/image/upload/v1704012220/Typera/2023/12/338edd4301cc6cad326035c9a4221cc5.png" style="zoom:50%;" />

3. 下一步，选择磁盘容量（最好大于 **60** GB）
<img src="https://res.cloudinary.com/sycamore/image/upload/v1704012564/Typera/2023/12/2982c11f8bc33629ed97c7027051ecaa.png" style="zoom: 50%;" />

4. 更改安装的 **硬件**：
	因为从 Win10 升级到 Win11 有 **最低硬件要求**，即：

	-   **处理器**：1 GHz 或更快，在兼容的 64 位处理器或片上系统 (SoC) 上具有两个或更多内核。
	-   **RAM**：4 GB 或更大。
	-   **存储空间**：安装 Windows 11 需要 64 GB 或更大的可用存储空间。

	<img src="https://res.cloudinary.com/sycamore/image/upload/v1704012657/Typera/2023/12/f5cdc00ac398b079aef715e9cef1d33d.png" style="zoom: 50%;" />

点击 **完成** 后，退出 向导

### 更改虚拟机设置
从 **新建虚拟机向导** 退出后，先 **不要** 启动虚拟机，
因为这时候启动**安装**，还是会 在安装过程中 提醒：
<img src="https://res.cloudinary.com/sycamore/image/upload/v1704012674/Typera/2023/12/41f08312d8479a1167c27196098b1ca3.png" style="zoom: 33%;" />

我们还需要 更改几项虚拟机**设置**：
打开 虚拟机设置，
1. `选项 -> 访问控制 -> 加密 -> 输入密码`
<img src="https://res.cloudinary.com/sycamore/image/upload/v1704012702/Typera/2023/12/863b1258fb1e625aad5724a82baee5c5.png" style="zoom:33%;" />

2. `硬件 -> 添加 -> 可信平台模块 -> 完成`
（此后每次点开这个虚拟机，都要输 **密码** 了）
<img src="https://res.cloudinary.com/sycamore/image/upload/v1704012721/Typera/2023/12/896f6935d4351cef18cdd1d971bd7487.png" style="zoom:33%;" />

现在再启动虚拟机，安装就不会提示：**无法运行 Win11** 了.

### 启动虚拟机，开始安装
1. 打开后会遇到下图所示的画面，
<img src="https://res.cloudinary.com/sycamore/image/upload/v1704012727/Typera/2023/12/ffcf4d54df07765c493a15ef76f6b25b.png" style="zoom:33%;" />
不要等太久再 “按任意键”，
因为如果时间过了，会提示 `Time out`，然后就 **卡** 在下图所示的画面了：
<img src="https://res.cloudinary.com/sycamore/image/upload/v1704012731/Typera/2023/12/e0b203eb588dda997504fb10073d24db.png" style="zoom:33%;" />

2. 一波 `Next` 过后，我们选择安装的 **操作系统版本**（我选的专业版）：
<img src="https://res.cloudinary.com/sycamore/image/upload/v1704012734/Typera/2023/12/0e49cc6f9b7014e5ed99939012d6ccf9.png" style="zoom:33%;" />

3. 遇到这一步时，选择自定义：仅安装 Windows （高级），
因为我们是要 **完整地**安装，而非更新。
<img src="https://res.cloudinary.com/sycamore/image/upload/v1704012746/Typera/2023/12/c63c3401280590e3a29245e4d714e38a.png" style="zoom:33%;" />

4. 这一步，选择 “新建”，就是要**分配** **C盘**、**D盘**，把 Windows 安装在分配的磁盘里。
<img src="https://res.cloudinary.com/sycamore/image/upload/v1704012750/Typera/2023/12/b8e71588df1d8b52f1a3daf9d281e353.png" style="zoom:33%;" />

5. 到这里，大致要 **注意** 的安装步骤就没了，开始等待：
<img src="https://res.cloudinary.com/sycamore/image/upload/v1704012752/Typera/2023/12/7b98b25772ebdc03a9bedc22257cb105.png" style="zoom: 25%;" />
从这里开始，就是通常的 Windows 启动步骤了：
（没人不会吧，放张图，就不说了）
<img src="https://res.cloudinary.com/sycamore/image/upload/v1704012772/Typera/2023/12/3db95d71ff0acde6daa635e63380e18b.png" style="zoom: 25%;" />

5. 完成！等待即可 ~
<img src="https://res.cloudinary.com/sycamore/image/upload/v1704012776/Typera/2023/12/faa285dbc5a0c474b52248c6449a25e3.png" style="zoom:25%;" />

## 安装 VMware-Tools
因为 后面要 **激活** Win11，几个命令很长（没装就不能 **复制**），

而且后续使用，肯定是有 **VMware-Tools** 更方便，

所以我们在激活之前，先装一下 **VMware-Tools**


1. `虚拟机 -> 安装 VMware-Tools`

<img src="https://res.cloudinary.com/sycamore/image/upload/v1704012778/Typera/2023/12/f656802af2a999811f4fe02887b4a46d.png" width=300 />

2. 耐心等待运行 **安装向导**，
    如果实在是太慢了，等不及了，就进入 **文件资源管理器**，找到 D 盘，双击运行 `setup64` 程序：
    （这个 **DVD 驱动器(D:)** ，只有 第一步点了 `安装 VMware-Tools` 按钮之后才有）
    <img src="https://res.cloudinary.com/sycamore/image/upload/v1704012842/Typera/2023/12/b3954036aa9224ddccd91c871f7f8893.png" style="zoom: 33%;" />
3. 两个加载的 弹窗 之后，成功打开 **安装向导**：
    （只需要注意选择 **典型安装** ，**Win11** 的 **VMware-Tools** 大概率不会报错）
    安装完成后，**重新启动** 虚拟机
    <img src="https://res.cloudinary.com/sycamore/image/upload/v1704012962/Typera/2023/12/9ae5db46573b558302c65d16791c0254.png" style="zoom: 25%;" /><img src="https://res.cloudinary.com/sycamore/image/upload/v1704013014/Typera/2023/12/2d1c0f84cbcffce42beae398d2f623e9.png" style="zoom: 25%;" />

## 激活 Win11 专业版

现在安装好的 Win11 是没有激活的，不能长时间使用：
<img src="https://res.cloudinary.com/sycamore/image/upload/v1704013091/Typera/2023/12/b46ec91f451c4de9a831ed9b69d5cc9a.png" style="zoom:25%;" />
**激活步骤：**

1. 以管理员身份打开 **CMD**：

  <img src="https://res.cloudinary.com/sycamore/image/upload/v1704013135/Typera/2023/12/e3b151d1971b81e2e763891ea9ecefb4.png" style="zoom: 25%;" />

  **安装 KMS 客户端密钥**，
  命令：`slmgr /ipk W269N-WFGWX-YVC9B-4J6C9-T83GX`
  <img src="https://res.cloudinary.com/sycamore/image/upload/v1704013159/Typera/2023/12/ced00a4b004c06e9f2356edb2e01e04c.png" width=600 height=300 style="zoom: 67%;" />

2. **设置 KMS 服务器**，
    命令：`slmgr /skms s8.uk.to`
    如果执行失败，说明该 KMS 服务器 可能已失效。
    尝试**更换** 该命令后半部分的 **KMS 服务器名**，[查询地址传送门](https://kms.msguides.com/)
    <img src="https://res.cloudinary.com/sycamore/image/upload/v1704013199/Typera/2023/12/9358882fffe07ef3c3e3db876afad89e.png" style="zoom: 33%;" />

3. **激活 Windows**
    命令：`slmgr /ato`
    <img src="https://res.cloudinary.com/sycamore/image/upload/v1704013202/Typera/2023/12/36bc8abb1ec174ec21129bf9f854bd61.png" style="zoom:33%;" />

成功**激活** ！
<img src="https://res.cloudinary.com/sycamore/image/upload/v1704013205/Typera/2023/12/c27217ec83ab6a9f50cd4ca7f0d53139.png" style="zoom: 25%;" />

## 添加共享文件夹
步骤和 **Win7** 类似，
1. 虚拟机设置中添加 **共享文件夹**

2. `控制面板 -> 网络和 Internet -> 网络和共享中心 -> 高级共享设置`，
启动当前网络类型（专用/公用）的 **网络发现**
<img src="https://res.cloudinary.com/sycamore/image/upload/v1704013228/Typera/2023/12/a92c22729e15e0585a84fcc1e112af53.png" style="zoom:33%;" />
3. `此电脑 -> 映射网络驱动器`：
<img src="https://res.cloudinary.com/sycamore/image/upload/v1704013236/Typera/2023/12/e265ff58617284810bf17a32bce6bbd7.png" style="zoom:33%;" />
4. 浏览，选择 **映射的目录**，确定即可：
<img src="https://res.cloudinary.com/sycamore/image/upload/v1704013241/Typera/2023/12/49ad0d1c6d3225352afa5ffe27df5cb8.png" style="zoom:33%;" />
<img src="https://res.cloudinary.com/sycamore/image/upload/v1704013259/Typera/2023/12/79379495f2c29c73d95616821a42be72.png" style="zoom: 33%;" />

完成 **共享文件夹** 的添加！
<img src="https://res.cloudinary.com/sycamore/image/upload/v1704013261/Typera/2023/12/ef8ab28424e1d5ed8eeea5da6f67beb4.png" style="zoom: 33%;" />
