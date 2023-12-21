---
title: EasyBe主题设置+修改
date: 2022-03-15 00:08:40
tags: [云服务器,Typecho,主题]
categories:
 - 云服务器 
 - Typecho
index_img: https://cdn.jsdelivr.net/gh/noneSycamore/noneSycamore.github.io/2022/03/15/EasyBe%E4%B8%BB%E9%A2%98%E8%AE%BE%E7%BD%AE-%E4%BF%AE%E6%94%B9/1.png
banner_img: https://cdn.jsdelivr.net/gh/noneSycamore/noneSycamore.github.io/2022/03/15/EasyBe%E4%B8%BB%E9%A2%98%E8%AE%BE%E7%BD%AE-%E4%BF%AE%E6%94%B9/1.png
---
记录：我尝试搭建Typecho的博客——EasyBe，并粗略美化修改（挺精美的主题）
<!-- more -->
子域名下还可以搭网站，所以我就尝试搭了一下Typecho的博客，

## EasyBe主题安装
Typecho安装请看：

使用宝塔将EasyBe主题压缩包上传到usr/themes文件夹下，然后解压即可完成主题的初步安装
## EasyBe主题配置

### 吐点槽

这个主题大概是由于正在开发中的原因，我们直接启用主题后转到前端竟然是空白的，

由于是第一次接触Typecho，之前尝试安装的其他Typecho主题启用之后，起码都有一个基本的页面的，所以我直接懵逼了，后面想到大概是要在“设置外观”界面进行配置吧 (￣_￣|||)

虽然这一开始也很让人困惑，但是在参考了[开发者的GitHub](https://github.com/wangyang0210/EasyBe "开发者的GitHub")之后，还是完成了初步的配置，
总体来说，这个主题还是挺好看的
![如图是侧边栏展开的首页封面图](https://cdn.jsdelivr.net/gh/noneSycamore/blog_pic_url/eb1.jpg "如图是菜单栏展开的首页封面图")
![如图是页脚的画面，挺精美的](https://cdn.jsdelivr.net/gh/noneSycamore/blog_pic_url/eb2.jpg "如图是页脚的画面，挺精美的")
### 具体方法
#### **头像**。**昵称**、**职业**、**居住地**
这些就不说了，这些信息会出现在侧边栏顶部区域，
#### **CNZZ统计**
这个就是添加一个站点统计功能，可以不加，随个人喜好。该主题对样式进行了优化，首先要去 CNZZ（https://www.umeng.com/） 配置好统计的网站信息，然后把你的统计ID，填入下方代码对应的位置就可以了。
```html
 <span class="id_cnzz_stat_icon" id='cnzz_stat_icon_你的统计ID'></span>
 <script src='https://s19.cnzz.com/z_stat.php?id=你的统计ID&online=1&show=line' type='text/javascript'></script>
```
配置好之后会显示在页脚友情链接下方的位置
#### **备案信息**
这个就按照给的这个代码来就行了，你要做的只是去给你的域名备个案，然后更改一下代码中的汉字部分即可
```html
<div style="width:300px;margin:0 auto; padding:20px 0;">
    <a target="_blank" href="http://www.beian.gov.cn/portal/registerSystemInfo?recordcode=你的备案号" style="display:inline-block;text-decoration:none;height:20px;line-height:20px;">
        <img src="https://cdn.jsdelivr.net/gh/wangyang0210/pic//imgs/beian_icon.png" style="float:left;">
        <p style="float:left;height:20px;line-height:20px;margin: 0px 0px 0px 5px; color:#939393;">你的备案信息</p>
    </a>
</div>
```
#### **全局配置**
这里才是**重点**，要知道前面的内容配置好之后，大概率你的前端还是空白的，
因为正如其名，全局的配置基本都给放到这里来了，不过这样也挺好，因为这就意味着，我们可以更加自由地更改、设计博客的内容。这也是我特别喜欢这个主题的原因。
这里先放出一个GitHub上给出的原配置，可以直接复制看看效果(●'◡'●)
```html
<!-- global var -->
<script type="text/javascript">

    //博客全局配置
    window.cnblogsConfig = {

        // ---- GitHub文件源配置 ----
        GhUserName: 'wangyang0210', 
        GhRepositories: 'EasyBe', 
        GhVersions : '80e8d7f9b7acb7ab1318ac39cbfad7b0ed908edd', 

        // ---- 基础信息配置 ----custom
        blogUser      : "。思索",
        blogAvatar    : 
        "https://cdn.jsdelivr.net/gh/wangyang0210/Cnblogs-Theme@theme-simpleMemory/img/webp/nothome_top_bg.webp",
        blogStartDate : "2019-8-1", 
      
        // ---- 菜单配置 ----
        menuCustomList: { 
            
        },
        

       // ---- 网站配置 ----
        webpageTitleOnblur        : "(◍´꒳`◍) Hi, MyFriend", 
        webpageTitleOnblurTimeOut : 500, 
        webpageTitleFocus         : "(*´∇｀*) 欢迎回来！", 
        webpageTitleFocusTimeOut  : 1000, 
        webpageIcon : "https://files.cnblogs.com/files/wangyang0210/blog_logo.gif", 

        // ---- 进度条配置 ----
        progressBar: {
            id      : 'top-progress-bar',
            color   : '#77b6ff',
            height  : '2px',
            duration: 0.2
        },

        // ---- Loading配置 ----
        loading: {
            rebound: {
                tension: 16,
                friction: 5
            },
            spinner: {
                id: 'spinner',
                radius: 90,
                sides: 3,
                depth: 4,
                colors: {
                    background: '#f0f0f0',
                    stroke: '#272633',
                    base: null,
                    child: '#272633'
                },
                alwaysForward: true, // When false the spring will reverse normally.
                restAt: 0.5,         // A number from 0.1 to 0.9 || null for full rotation
                renderBase: false
            }
        },

        // ---- 页面动效配置 ----
        homeTopAnimationRendered: true, // true || false ,是否渲染主页头图动效
        homeTopAnimation: { // 主页头图动效设置
            radius: 15,
            density: 0.2,
            color: 'rgba(255,255,255, .2)', // 颜色设置，“random” 为随机颜色
            clearOffset: 0.3
        },

        essayTopAnimationRendered: true, // true || false ,是否渲染随笔页头图动效
        essayTopAnimation: { // 随笔页头图动效设置
            triW : 14,
            triH : 20,
            neighbours : ["side", "top", "bottom"],
            speedTrailAppear : .1,
            speedTrailDisappear : .1,
            speedTriOpen : 1,
            trailMaxLength : 30,
            trailIntervalCreation : 100,
            delayBeforeDisappear : 2,
            colors: [
                '#96EDA6', '#5BC6A9',
                '#38668C', '#374D84',
                '#BED5CB', '#62ADC6',
                '#8EE5DE', '#304E7B'
            ]
        },

        bgAnimationRendered: true, // true || false ,是否渲染背景动效
        backgroundAnimation : { // 背景动效设置
            colorSaturation: "60%",
            colorBrightness: "50%",
            colorAlpha: 0.5,
            colorCycleSpeed: 5,
            verticalPosition: "random",
            horizontalSpeed: 200,
            ribbonCount: 3,
            strokeSize: 0,
            parallaxAmount: -0.2,
            animateSections: true
        },

        // ---- 主页配置 ----
        homeTopImg    : [ 
             "https://cdn.jsdelivr.net/gh/wangyang0210/Cnblogs-Theme@theme-simpleMemory/img/webp/wallhaven-j55w9p_1920x1080.webp",
            "https://cdn.jsdelivr.net/gh/wangyang0210/Cnblogs-Theme@theme-simpleMemory/img/webp/wallhaven-dgzkw3_1920x1080.webp",
            "https://cdn.jsdelivr.net/gh/wangyang0210/Cnblogs-Theme@theme-simpleMemory/img/webp/home_top_bg.webp",
            "https://cdn.jsdelivr.net/gh/wangyang0210/Cnblogs-Theme@theme-simpleMemory/img/webp/wallhaven-x1wroo.webp",
            "https://cdn.jsdelivr.net/gh/wangyang0210/Cnblogs-Theme@theme-simpleMemory/img/webp/nothome_top_bg.webp",
            "https://cdn.jsdelivr.net/gh/wangyang0210/Cnblogs-Theme@theme-simpleMemory/img/webp/wallhaven-13gom9.webp",
            "https://cdn.jsdelivr.net/gh/wangyang0210/Cnblogs-Theme@theme-simpleMemory/img/webp/wallhaven-vg7lv3.webp",
            "https://cdn.jsdelivr.net/gh/wangyang0210/Cnblogs-Theme@theme-simpleMemory/img/webp/wallhaven-odej2m.webp",
            "https://cdn.jsdelivr.net/gh/wangyang0210/Cnblogs-Theme@theme-simpleMemory/img/webp/wallhaven-j5mz95.webp",
            "https://cdn.jsdelivr.net/gh/wangyang0210/Cnblogs-Theme@theme-simpleMemory/img/webp/19059-wallhaven-3911w9.webp",
            "https://cdn.jsdelivr.net/gh/wangyang0210/Cnblogs-Theme@theme-simpleMemory/img/webp/wallhaven-6k3oox.webp",
            "https://cdn.jsdelivr.net/gh/wangyang0210/Cnblogs-Theme@theme-simpleMemory/img/webp/for.webp",
            "https://cdn.jsdelivr.net/gh/wangyang0210/Cnblogs-Theme@theme-simpleMemory/img/webp/wallhaven-737jo3.webp",
            "https://cdn.jsdelivr.net/gh/wangyang0210/Cnblogs-Theme@theme-simpleMemory/img/webp/42476-wallhaven-oxzk8m.webp",
            "https://cdn.jsdelivr.net/gh/wangyang0210/Cnblogs-Theme@theme-simpleMemory/img/webp/wallhaven-oxdyvl.webp",
            "https://cdn.jsdelivr.net/gh/wangyang0210/Cnblogs-Theme@theme-simpleMemory/img/webp/44817-wallhaven-p8rdq9.webp"
        ],
        homeBannerText: "", 

        // ---- 随笔页配置 ----
        essayTopImg: [ 
               "https://cdn.jsdelivr.net/gh/wangyang0210/Cnblogs-Theme@theme-simpleMemory/img/webp/nothome_top_bg.webp",
            "https://cdn.jsdelivr.net/gh/wangyang0210/Cnblogs-Theme@theme-simpleMemory/img/webp/wallhaven-13gom9.webp"
        ],
        essayCodeHighlightingType: 'highlightjs', // 代码主题插件类型：cnblogs || highlightjs || prettify
        essayCodeHighlighting: 'monokai-sublime', // 代码高亮主题，具体主题参考文档
        essaySuffix:{ // 随笔后缀处配置
            aboutHtml    : '', // 关于博主，不配置使用默认
            copyrightHtml: '', // 版权声明，不配置使用默认
        },

        // ---- 页脚配置 ----
        bottomBlogroll: [ // 友情链接，[[链接名,链接]....]
            ["王洋", 'http://www.wangyangyang.vip'],
            ["申请坑位", 'https://msg.cnblogs.com/send/wangyang0210'],
            ["申请坑位", 'https://msg.cnblogs.com/send/wangyang0210'],
            ["申请坑位", 'https://msg.cnblogs.com/send/wangyang0210'],
            ["申请坑位", 'https://msg.cnblogs.com/send/wangyang0210'],
        ],
        bottomText: {  // 页脚标语
            icon: "❤️",
            left: "学无止境",
            right: "谦卑而行"
        },

        // ---- 控制台输出 ----
        consoleList: [
        ['wangyang0210 CNBlogs', 'https://www.cnblogs.com/wangyang0210'],
        ['wangyang0210 GitHub', 'https://github.com/wangyang0210'],
        ['wangyang0210 Email', '2752154874@qq.com']
        ],
    };

    // start cache
    $.ajaxSetup({cache: true});

    // load loadingJs
    $.getScript(getJsDelivrUrl('loading.js'), function () {

        // Loading start
        pageLoading.initRebound();
        pageLoading.initSpinner();
        pageLoading.spinner.init(pageLoading.spring, true);
        $.getScript(getJsDelivrUrl('jquery.mCustomScrollbar.min.js'), function () {
            $.getScript(getJsDelivrUrl('require.min.js'), function () {
                $.getScript(getJsDelivrUrl('config.js'), function () {
                    var staticResource = [
                        'optiscroll', 'ToProgress', 'rotate',
                        'snapSvg', 'classie', 'main4', 'tools'];
                    require(staticResource, function() {
                        require(['base'], function() {
                            (new Base).init();
                        });
                    });
                });
            });
        });
    });

    // get file url
    function getJsDelivrUrl(file, directory) {
        file = setFileNameMin(file, directory);
        return 'https://cdn.jsdelivr.net/gh/'+(window.cnblogsConfig.GhUserName)+'/'+(window.cnblogsConfig.GhRepositories)+'@'+(window.cnblogsConfig.GhVersions)+'/static/' + (file ? file : '');
    }

    // optimization file name
    function setFileNameMin(file, directory) {
        if (typeof file == 'undefined') return '';
        var suffix  = null,fileArr = file.split('.');
        if (fileArr.length > 0 && $.inArray(fileArr[(fileArr.length -1)], ['js', 'css']) != -1)
            {suffix    = fileArr.pop(); directory = suffix;}
        file.search('.min') == -1 && fileArr.push('min');
        suffix != null && fileArr.push(suffix);
        return (typeof directory !== 'undefined' ? (directory + '/' + fileArr.join('.')) : (fileArr.join('.')));
    }
</script>
```
## 如何简单地修改
这里将分块解释具体模块的含义，将从全局配置的代码和源文件两方面进行
### 全局配置部分
（此部分代码没有留全，仅展示说明用）
这里是github文件源配置，建议fork GitHub上面的原仓库，然后将这三个量修改成自己的信息，因为或许你以后要自己研究魔改，这样会方便很多。
#### GitHub文件源配置
**GhUserName**：GitHub用户名，
**GhRepositories**：你fork的仓库名，
**GhVersions**：你使用发布的版本号，可以和源文件一样用哈希，也可以使用‘v1.0.0’之类的。
```html
        // ---- GitHub文件源配置 ----
        GhUserName: 'wangyang0210', 
        GhRepositories: 'EasyBe', 
        GhVersions : '80e8d7f9b7acb7ab1318ac39cbfad7b0ed908edd', 
```
#### 基础信息配置
**blogUser**：用户名，将显示在首页大封面的正中央
**blogAvatar**：头像
**blogStartDate**：博客建立的时间，将影响页脚处博客运行时间的显示
```html
        // ---- 基础信息配置 ----custom
        blogUser      : "。思索",
        blogAvatar    : 
        "https://cdn.jsdelivr.net/gh/wangyang0210/Cnblogs-Theme@theme-simpleMemory/img/webp/nothome_top_bg.webp",
        blogStartDate : "2019-8-1", 
```
#### 网站标签栏配置
**webpageTitleOnblur**：你离开博客页面后显示在标签栏上的文字
**webpageTitleFocus**：你离开后回到博客页面显示的文字
**webpageTitleOnblurTimeOut**、**webpageTitleFocusTimeOut**不用修改，表示文字失效时间
**webpageIcon**：你的网站图标，就是显示在浏览器标签栏里的那个
![左侧的是网站图标](https://cdn.jsdelivr.net/gh/noneSycamore/blog_pic_url/eb4.jpg "左侧的是网站图标")
```html
       // ---- 网站配置 ----
        webpageTitleOnblur        : "(◍´꒳`◍) Hi, MyFriend", 
        webpageTitleOnblurTimeOut : 500, 
        webpageTitleFocus         : "(*´∇｀*) 欢迎回来！", 
        webpageTitleFocusTimeOut  : 1000, 
        webpageIcon : "https://files.cnblogs.com/files/wangyang0210/blog_logo.gif", 
```
#### 进度条（未做更改）
进度条无需变动，用原配置即可
其中**duration**的单位是s,是页面滑动后进度条移动到相应位置的时间,比如页面从0滑动到50%,进度条花0.2s从0到达50%
```html
        // ---- 进度条配置 ----
        progressBar: {
            id      : 'top-progress-bar',
            color   : '#77b6ff',
            height  : '2px',
            duration: 0.2
        },
```
#### Loading动画配置(✿◕‿◕✿)
这个超有意思的，
我们使用原配置打开博客，应该能看到经典的三层三角形旋转的加载动画，这里的配置可以自行修改这个loading动画~
**rebound**：这里修改的是旋转、回弹的速度
**radius**：这个是旋转的图案的大小
**sides**：这个是图案的边数，三角形就是3
**depth**：这个是图案的深度，简单来说就是内嵌几个多边形
**background**：整个大页面的背景颜色
**stroke**：旋转图案的边的颜色，就是轮廓线条的颜色
**base**：没出现旋转图案的时候的原位置的颜色，就是这个图案是在啥颜色上方旋转的
**child**：旋转图案内填充的颜色
**alwaysForward**：ture就是一直一个方向转，false的话会加一点回旋的效果，
**restAt**：旋转的程度，旋转的角度的量化，数值越小，转的角度越小
**renderBase**：如果设置了base的颜色，就把这个设为true即可
loading的**原配置**：
```html
        // ---- Loading配置 ----
        loading: {
            rebound: {
                tension: 16,
                friction: 5
            },
            spinner: {
                id: 'spinner',
                radius: 90,
                sides: 3,
                depth: 4,
                colors: {
                    background: '#f0f0f0',
                    stroke: '#272633',
                    base: null,
                    child: '#272633'
                },
                alwaysForward: true, // When false the spring will reverse normally.
                restAt: 0.5,         // A number from 0.1 to 0.9 || null for full rotation
                renderBase: false
            }
        },
```
再放一个**我配置的一个loading**，黑色背景，六边形仅边框：
```html
        loading: {
            rebound: {
                tension: 46,
                friction: 3
            },
            spinner: {
                id: 'spinner',
                radius: 120,
                sides: 6,
                depth: 6,
                colors: {
                    background: '#181818',
                    stroke: '#F4CA0C',
                    base: '#181818',
                    child: '#181818'
                },
                alwaysForward: false, // When false the spring will reverse normally.
                restAt: 0.2,         // A number from 0.1 to 0.9 || null for full rotation
                renderBase: true
            }
        },
```
#### 主页封图
页面动效配置我没有更改，因为原动效已经超级好看了

**homeTopImg**是主页封面大图的配置，里面填充自己想放的图片，会随机显示，
貌似**homeBannerTextType**能设置一言标语，尚未成功...
```html
        // ---- 主页配置 ----
        homeTopImg    : [ 
             "https://cdn.jsdelivr.net/gh/wangyang0210/Cnblogs-Theme@theme-simpleMemory/img/webp/wallhaven-j55w9p_1920x1080.webp",
            "https://cdn.jsdelivr.net/gh/wangyang0210/Cnblogs-Theme@theme-simpleMemory/img/webp/wallhaven-dgzkw3_1920x1080.webp",
            "https://cdn.jsdelivr.net/gh/wangyang0210/Cnblogs-Theme@theme-simpleMemory/img/webp/home_top_bg.webp",
            "https://cdn.jsdelivr.net/gh/wangyang0210/Cnblogs-Theme@theme-simpleMemory/img/webp/wallhaven-x1wroo.webp",
            "https://cdn.jsdelivr.net/gh/wangyang0210/Cnblogs-Theme@theme-simpleMemory/img/webp/nothome_top_bg.webp",
            "https://cdn.jsdelivr.net/gh/wangyang0210/Cnblogs-Theme@theme-simpleMemory/img/webp/wallhaven-13gom9.webp",
            "https://cdn.jsdelivr.net/gh/wangyang0210/Cnblogs-Theme@theme-simpleMemory/img/webp/wallhaven-vg7lv3.webp",
            "https://cdn.jsdelivr.net/gh/wangyang0210/Cnblogs-Theme@theme-simpleMemory/img/webp/wallhaven-odej2m.webp",
            "https://cdn.jsdelivr.net/gh/wangyang0210/Cnblogs-Theme@theme-simpleMemory/img/webp/wallhaven-j5mz95.webp",
            "https://cdn.jsdelivr.net/gh/wangyang0210/Cnblogs-Theme@theme-simpleMemory/img/webp/19059-wallhaven-3911w9.webp",
            "https://cdn.jsdelivr.net/gh/wangyang0210/Cnblogs-Theme@theme-simpleMemory/img/webp/wallhaven-6k3oox.webp",
            "https://cdn.jsdelivr.net/gh/wangyang0210/Cnblogs-Theme@theme-simpleMemory/img/webp/for.webp",
            "https://cdn.jsdelivr.net/gh/wangyang0210/Cnblogs-Theme@theme-simpleMemory/img/webp/wallhaven-737jo3.webp",
            "https://cdn.jsdelivr.net/gh/wangyang0210/Cnblogs-Theme@theme-simpleMemory/img/webp/42476-wallhaven-oxzk8m.webp",
            "https://cdn.jsdelivr.net/gh/wangyang0210/Cnblogs-Theme@theme-simpleMemory/img/webp/wallhaven-oxdyvl.webp",
            "https://cdn.jsdelivr.net/gh/wangyang0210/Cnblogs-Theme@theme-simpleMemory/img/webp/44817-wallhaven-p8rdq9.webp"
        ],
        homeBannerText: "", 
```
#### 随笔页&页脚
**essayTopImg**可以设置随笔页封图，填写多个会随机显示，
**essayCodeHighlightingType**、**essayCodeHighlighting**无需更改，原主题就很不错了，不过你也可以根据cnblog的进行修改
**aboutHtml**、**copyrightHtml**：出现文章末尾
![评论上方](https://cdn.jsdelivr.net/gh/noneSycamore/blog_pic_url/eb5.jpg "评论上方")
```html
        // ---- 随笔页配置 ----
        essayTopImg: [ 
               "https://cdn.jsdelivr.net/gh/wangyang0210/Cnblogs-Theme@theme-simpleMemory/img/webp/nothome_top_bg.webp",
            "https://cdn.jsdelivr.net/gh/wangyang0210/Cnblogs-Theme@theme-simpleMemory/img/webp/wallhaven-13gom9.webp"
        ],
        essayCodeHighlightingType: 'highlightjs', // 代码主题插件类型：cnblogs || highlightjs || prettify
        essayCodeHighlighting: 'monokai-sublime', // 代码高亮主题，具体主题参考文档
        essaySuffix:{ // 随笔后缀处配置
            aboutHtml    : '', // 关于博主，不配置使用默认
            copyrightHtml: '', // 版权声明，不配置使用默认
        },
```
这是页脚配置，看注释就显而易见了。
```html
        // ---- 页脚配置 ----
        bottomBlogroll: [ // 友情链接，[[链接名,链接]....]
            ["王洋", 'http://www.wangyangyang.vip'],
            ["申请坑位", 'https://msg.cnblogs.com/send/wangyang0210'],
            ["申请坑位", 'https://msg.cnblogs.com/send/wangyang0210'],
            ["申请坑位", 'https://msg.cnblogs.com/send/wangyang0210'],
            ["申请坑位", 'https://msg.cnblogs.com/send/wangyang0210'],
        ],
        bottomText: {  // 页脚标语
            icon: "❤️",
            left: "学无止境",
            right: "谦卑而行"
        },
```
全局配置部分此后内容属于控制台调用输出等配置，尽量不要去更动
### 源文件更改
这里做出的修改都在**外观->编辑当前外观**下进行~
#### 左下角歌单修改
试了一下，这个左下角的播放器内的歌单应该是网易云音乐的，
如果不满意那里设定的歌单的话，或者想要DIY整个自己的，可以去**footer.php**修改你中意的歌单id，如下图↓
![歌单id修改](https://cdn.jsdelivr.net/gh/noneSycamore/blog_pic_url/eb6.jpg "歌单id修改")
如果不知道歌单id在哪里的话，直接点开你要的歌单的**网页**，下图中画红线的部分就是你要找的歌单id.
![找歌单id](https://cdn.jsdelivr.net/gh/noneSycamore/blog_pic_url/eb7.jpg "找歌单id")
#### 脑壳疼
随笔页的最后都摆了3个“脑壳疼”的链接，如果你试着点击，就会发现实际上这里啥也没有(/▽＼)
如果你对这里想放啥，有了成熟的想法，你可以尝试去修改**post.php**文件，
![脑壳疼修改](https://cdn.jsdelivr.net/gh/noneSycamore/blog_pic_url/eb8.jpg "脑壳疼修改")
具体方法已给出（就是我也实在没啥好的想法，只是看了一下该怎么改，没有尝试，不保证此方法的正确性）(￣▽￣)"
####侧边栏链接修改
这个主题的侧边栏还是很好看的，就是如果我们想DIY这里（↓）的链接的话，还是得去主题文件里改
![侧边栏链接展示](https://cdn.jsdelivr.net/gh/noneSycamore/blog_pic_url/eb9.jpg "侧边栏链接展示")

主要的代码在**sidebar.php**文件里，
其中**首页**、**管理**、**添加随笔**这三个如果不了解尽量不用去动（也没必要）
**联系**的链接是用于拉起无需好友验证的*QQ会话*，如需修改，首先要将**“UIN=”**字符后面的QQ号改成自己的（如果你的QQ在线状态服务已开启，就不用后面的动作了），
![侧边栏链接修改位置](https://cdn.jsdelivr.net/gh/noneSycamore/blog_pic_url/eb10.jpg "侧边栏链接修改位置")

然后去这个官网链接（http://shang.qq.com/v3/index.html） ，点击最上方的推广工具，再点击左侧的设置.
![QQ会话服务开启](https://cdn.jsdelivr.net/gh/noneSycamore/blog_pic_url/eb11.jpg "QQ会话服务开启")

找到会话能力，单击保存即可.
![QQ会话服务开启](https://cdn.jsdelivr.net/gh/noneSycamore/blog_pic_url/eb12.jpg "QQ会话服务开启")

这样联系点开的就是和你的QQ会话了（注意必须是手机，其次如果你测试的时候，QQ登的是你的号，那是拉不出这个会话的）

余下的链接修改就简单了，前两张的图里，红色方框改的是显示的文字，蓝色框里改的是对应的链接
## 总结

以上就是EasyBe主题的配置修改的全部内容，当然这只是最粗浅的改动，我最满意的地方还是DIY的那个loading动画(oﾟvﾟ)ノ.
后续如有改进，我还会继续填充.
