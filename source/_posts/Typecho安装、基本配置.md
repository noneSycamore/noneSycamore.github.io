---
title: Typecho安装、基本配置
date: 2022-03-14 22:38:44
tags: [云服务器,Typecho]
categories:
 - 云服务器 
 - Typecho
index_img: https://res.cloudinary.com/sycamore/image/upload/v1704033556/Typera/2023/12/9130289fab8c8fd13edb68a0aee26b93.png
banner_img: https://res.cloudinary.com/sycamore/image/upload/v1704033556/Typera/2023/12/9130289fab8c8fd13edb68a0aee26b93.png
---
记录安装Typecho的方法，以及主题、插件的安装方式。
<!-- more -->
Typecho是一个体量和Wordpress相当的博客程序，各类主题、插件xit比较多，大多也较为完善，所以闲暇之余我就在某个子域名下安装了Typecho，

这篇文章就是记录安装Typecho的方法，基本设置的位置，以及主题、插件的安装方式。

这篇文章的篇幅不会太长，因为这...实在是太简单了！
## Typecho安装
### 准备
1. 一个能与服务器进行文件传输的方式，
2. 提前建好**网站根目录**（比如/www/wwwroot/你的域名），
3. 提前建好一个**数据库**

当然以上都可以用宝塔面板来搞，**添加站点**即可，详见：[宝塔添加站点+一键部署WordPress系统](https://blog.sycamore.top/2022/03/14/%E5%AE%9D%E5%A1%94%E6%B7%BB%E5%8A%A0%E7%AB%99%E7%82%B9-%E4%B8%80%E9%94%AE%E9%83%A8%E7%BD%B2wordpress%E7%B3%BB%E7%BB%9F/)
### 下载安装包
去官网：[链接](http://typecho.org/)，
点击立即下载，然后点击下载正式版：
贴个 [链接](http://typecho.org/downloads/1.1-17.10.30-release.tar.gz) ，<- 这是我正在撰写博客的时候的链接（2022/03/14）

### 上传、解压
用你的方式，上传压缩包到**网站根目录**
以宝塔为例：
![](https://res.cloudinary.com/sycamore/image/upload/v1704010833/Typera/2023/12/b9b89bd1217d73b778ed9998579495a1.png)
上传完毕之后，直接解压，然后你会获得一个build文件夹
![](https://res.cloudinary.com/sycamore/image/upload/v1704010844/Typera/2023/12/4df9b42ebee9eaabbcb36648bf74c92f.png)
进入build文件夹 -> 全选 -> 剪贴 -> 退出build文件夹，在根目录粘贴
![](https://res.cloudinary.com/sycamore/image/upload/v1704010853/Typera/2023/12/85e02df271638fd1989e8a7752781b12.png)

### 信息填写
进入你的域名，无误的话，你会看到这个：
![](https://res.cloudinary.com/sycamore/image/upload/v1704010863/Typera/2023/12/ffc77fe74d47807af977dda33fb112cc.png)

点击 “我准备好了，开始下一步”

![](https://res.cloudinary.com/sycamore/image/upload/v1704010867/Typera/2023/12/a7b3b4540b951dd6e24aa42d637bcb38.jpg)
这里的内容，详细请看：[宝塔添加站点+一键部署WordPress系统](https://blog.sycamore.top/2022/03/14/%E5%AE%9D%E5%A1%94%E6%B7%BB%E5%8A%A0%E7%AB%99%E7%82%B9-%E4%B8%80%E9%94%AE%E9%83%A8%E7%BD%B2wordpress%E7%B3%BB%E7%BB%9F/) ，与WordPress极为相似，故不再赘述。
其中，如下几项是**必须修改**的：

- 数据库用户名
- 数据库密码
- 数据库名
- 邮件地址（得改）

如下几项是**可以按个人喜好填写**的（但必须要写，**不能空着**）：
- 数据库前缀（建议保留，没啥必要改，除非你一个数据库连两个网站，那就必须得改不一样的）
- 用户名
- 登陆密码

不要更改网站地址...
所有信息填写完毕之后，点击 “确认，开始安装”即可

如果你看到这个画面，就说明你安装成功了
![](https://res.cloudinary.com/sycamore/image/upload/v1704010872/Typera/2023/12/fdb159438670ee67f8f60c7986e260c9.png)
## Typecho基本配置
因为要讲配置，这里就直接从上图的第一个链接进入**控制面板**了。
个人设置什么的就不提了，
撰写，可以写**文章**和**页面**，都是用Markdown进行编辑的。
管理，则是管理文章、页面、评论、分类各种东西，
总体上来说简单易懂，和Wordpress差别不大，区别**仅在于各个功能位置的不同**，

这里主要还是讲一下**插件**和**主题**的安装：
> 其实也简单，把你获得的压缩包上传到对应文件夹下，然后解压缩就行了，

> 插件对应 /usr/plugins
> 主题对应 /usr/themes

当你解压缩操作完成之后，就会分别出现在控制面板的:
> 控制台 -> 插件
> 控制台 -> 外观

再之后的事情，就因插件、主题而异了