---
title: 宝塔添加站点+一键部署WordPress系统
date: 2022-03-14 19:51:27
tags: [云服务器,WordPress]
categories:
 - 云服务器 
 - WordPress
index_img: https://res.cloudinary.com/sycamore/image/upload/v1704033810/Typera/2023/12/6c1cf55e7f50b9ff2de9651151f5fef1.jpg
banner_img: https://res.cloudinary.com/sycamore/image/upload/v1704033810/Typera/2023/12/6c1cf55e7f50b9ff2de9651151f5fef1.jpg
---
这篇文章，前后两部分要分开看，
宝塔添加站点（自由安装博客系统）+一键部署WordPress
（依旧是小白向)
<!-- more -->

## 哔哔~
宝塔面板真的非常方便啊 d(*￣▽￣)==b

功能也很全面，安了宝塔都不用安其他的东西了，像Xshell之类的功能宝塔上面都有，我都直接一个宝塔解决了

还有图片啥的，都尽量配全了o_o ....
## 准备工作
一台安装好了宝塔面板的服务器，一个正确解析的域名

还有就是，**这篇文章要分两部分来看（之前的小失误）**，
1. 如果你想直接看如何**一键部署wordpress**的话，直接去第二部分吧，因为一键部署wordpress会**顺带帮你添加站点**。
2. 如果你想知道如何**添加站点**，然后后续装啥系统**再说**，就看看第一部分（当然你也可以装wordpress)

## 添加站点

按照下面的步骤来就可以：

1.左侧栏点击网站 -> 添加站点

2.填写网站信息

配置基本可以按照这个来，不过**FTP**创建不创建都无所谓，看个人需求，
当然**数据库**一定是要有的！
输入域名后，下面自动生成备注和目录名，无需修改

密码的话，使用自动生成的或者是自己的都无所谓，宝塔面板里可以**随时查看、修改**(只要你之前保存了宝塔的后台信息就可以)


> 再之后的要做的，就是手动装博客系统了，无论是选择**Wordpress**还是**Typecho**，或者**Emlog**（这个真没装过）？
基本的都是：下载安装包 -> 解压 -> 访问域名填写信息

贴一个安装Typecho的链接：[Typecho安装、基本配置](https://blog.sycamore.top/2022/03/14/Typecho安装、基本配置/)
> 剩下的基本靠你了，下面说的是，抛开前面内容不提的，一键部署**Wordpress**

## 一键部署wordpress
### 安装Wordpress包和数据库
我们要做的事情很简单：
1.左侧栏软件商店 -> 一键部署 -> 找到**Wordpress** -> 点击右面的一键部署
<img src="https://res.cloudinary.com/sycamore/image/upload/v1704013357/Typera/2023/12/36ce50208b3996f9bd5bfd12b269f631.png" style="zoom: 25%;" />

2.然后，会出现如下方所示的一张表：

<img src="https://res.cloudinary.com/sycamore/image/upload/v1704013352/Typera/2023/12/b0b344d889e9ed50d264020b11e91652.png" style="zoom: 33%;" />
填写准备好的域名的时候，下方的备注、根目录、数据库会自动填充。
点击提交

>如果你当真是跟着**从第一步过来**的话（也就是说你提前添加了，你准备的域名的网站），这里会报告如下错误：
<img src="https://res.cloudinary.com/sycamore/image/upload/v1704013354/Typera/2023/12/5c4d2bf7216b5cd6b0facab1e8b32042.png" style="zoom:50%;" />
然后你得返回刚刚的地方，把添加好的**网站、数据库、FTP**删除
ㄟ( ▔, ▔ )ㄏ

如果你成功了，你就会看到这个：
<img src="https://res.cloudinary.com/sycamore/image/upload/v1704013395/Typera/2023/12/ebe9183361ebaa64b1883c682fcceb0a.png" style="zoom:33%;" />
这些信息需要你记录一下，后续有用

### 访问站点
方便点，你可以直接点击上图所示的，下方那个绿色的链接访问，
如果你不小心手贱关掉了，直接访问你的**域名**就行了，不要慌。

有的时候，会比较慢，要等很久（但一般不是出错），这跟服务器啥的都有关系，然后不出意外的话，你会看到这个：
<img src="https://res.cloudinary.com/sycamore/image/upload/v1704013415/Typera/2023/12/93fa30be4fd2c90586fd8398de98f860.png" style="zoom:33%;" />
选择语言（友情提示：中文在最下面）
继续，然后，现在就开始！（这张图就不贴了吧，实在没啥可说的)

再就是填写数据库信息，还记得前面成功部署的那张图吗？
**数据库名、用户、密码**，前三项一一对应填入，后两项，emm...也无需更改
<img src="https://res.cloudinary.com/sycamore/image/upload/v1704013426/Typera/2023/12/8d800153bd7c05d5b2e4de02c56a62b3.png" style="zoom: 25%;" />
当然，若是你手贱没记住直接关上了前面那张图，这些信息在宝塔里面也能查到，
操作如下：
<img src="https://res.cloudinary.com/sycamore/image/upload/v1704013438/Typera/2023/12/16521e8e61d7c81778006964901e788e.png" style="zoom: 50%;" />

好了，填写好了之后，点击提交，再点击现在安装
<img src="https://res.cloudinary.com/sycamore/image/upload/v1704013445/Typera/2023/12/b0dfd354358bcc12ad69813bef2d5a6a.png" style="zoom: 33%;" />
现在，你就到了最后一步了，如下图：
<img src="https://res.cloudinary.com/sycamore/image/upload/v1704013445/Typera/2023/12/b0dfd354358bcc12ad69813bef2d5a6a.png" style="zoom: 33%;" />
**注意**：
> 这里填写的**用户名、密码以及邮箱**，是你今后登录网站后台的信息，
除了**站点标题**一栏你可以先随便填一个，其余的内容还是要**想好再写**，因为后续更改比较困难，也比较**麻烦**，不想麻烦的，还是好好填吧

至于，对搜索引擎的可见性，看个人吧，
这里wordpress**大概**是出于安全性考虑？ 才建议不勾，不过后面你在后台也能改

最后，点击安装wordpress，等待一会就行啦，
之后你想进后台还是查看网站，都随意了，
剩下的就是**自行探索**wordpress系统了，安装一个**好看的主题**吧