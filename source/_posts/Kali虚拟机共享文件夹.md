---
title: Kali虚拟机共享文件夹
date: 2022-04-09 15:53:08
tags: [Kali,虚拟机]
categories: 
 - 虚拟机
 - Kali-Linux
index_img: https://res.cloudinary.com/sycamore/image/upload/v1704033464/Typera/2023/12/d264247e34cfddb13d09c3a03d792b0e.png
banner_img: https://res.cloudinary.com/sycamore/image/upload/v1704033464/Typera/2023/12/d264247e34cfddb13d09c3a03d792b0e.png
---
KALI 虚拟机创建 共享文件夹，方便主机和虚拟机之间的 文件传输。
<!-- more -->

> 最近总是要**反复**地**建虚拟机**，**共享文件夹**又极大地方便了，主机和虚拟机之间的**文件传输**。
> 所以就写了这篇文章，**记录**一下创建共享文件夹的过程。

## 步骤
### ①VMware 添加共享目录
选中**要设置的**虚拟机 -> 右键设置，打开如下界面，按图示步骤完成添加：



![](https://res.cloudinary.com/sycamore/image/upload/v1704010546/Typera/2023/12/d6ab80b4096b31d9e8277a1d2d17e15d.png)



**主机路径**为主机上**共享文件夹目录**的位置；
**名称**会默认填写为**主机路径**的文件夹名称：
![](https://res.cloudinary.com/sycamore/image/upload/v1704010548/Typera/2023/12/c59203c3a6958a3352bb21e94c16cb71.png)



### ②安装 Vmware-Tools
> 命令：`apt-get install open-vm-tools-desktop fuse`

**[注意]：**命令有**多种可能**报错，包括但不限于：
- 非 **Debian** 系列 **Linux** 主机**。（Windows** 命令不同，**安卓**还需自行下载**）**
<br>
- 已安装 **Vmware-Tools** 。（若后续操作**无误**，则跳过此步；若后续操作**报错**，则返回，手动重新安装 **Vmware-Tools**）
<br>
- **apt-get** 找不到 **VMTools** 的安装包。
更新 **apt-get** ：`apt-get update` ，
还不行则尝试安装 **open-vm-tools** （命令里删去 -desktop ），
若还不行，活用搜索


### ③命令行查看共享目录（检查）
> 命令：`vmware-hgfsclient`

反馈如下：
![](https://res.cloudinary.com/sycamore/image/upload/v1704010551/Typera/2023/12/fd165b4e941f29eb2b73528b4c890149.png)

### ④新建文件夹
> 命令：`mkdir -p /mnt/hgfs/共享文件夹名`
![](https://res.cloudinary.com/sycamore/image/upload/v1704010553/Typera/2023/12/fde917c65af6fc2e96f68686e71cfeb5.png)
### ⑤创建共享文件夹
> 命令： `/usr/bin/vmhgfs-fuse .host:/ /mnt/hgfs/ -o subtype=vmhgfs-fuse,allow_other`
![](https://res.cloudinary.com/sycamore/image/upload/v1704010556/Typera/2023/12/a6c609c7898331e555c1e1a2e217fd26.png)
### ⑥开机自动挂载共享文件夹
> 命令：`vim /etc/fstab` ，更改文件 `/etc/fstab`
> 文末添加：`.host:/  /mnt/hgfs/  fuse.vmhgfs-fuse   allow_other   0       0`
> ![](https://res.cloudinary.com/sycamore/image/upload/v1704010561/Typera/2023/12/4bc901d11c40cdadad0e5a26b4113a8f.png)
## 总结：

1. **VMware 设置** 添加共享目录
<br>
2. 安装 **Vmware-Tools** （已安装则**可省略**）
<br>
3. 命令行**查看**共享目录（检查 **VMware 设置**里是否创建成功）
<br>
4. 新建文件夹（目录固定，名字与 **1** 中相同）
<br>
5. **创建**共享文件夹
<br>
6. 开机**自动挂载**共享文件夹
