# CloudFlare Workers可以搭建博客了

![INIT](https://s3.ax1x.com/2020/12/22/rrP81S.png)

## 言前

我一开始搭建博客是使用Google Blogger发布博客，但后来尝试使用其他网站来搭建。但限制太多😭😭😭。

后面我尝试使用免费服务器+Wordpress来搭建博客，但操作太难了。

直接从Wordpress出现很多不能自定义的情况了。

那个Google Blogger我一直都没有更新。

在最后面我发现到了这款软件，也就是这个博客。把我启动了新的希望。

> 我默认使用的主题是Default2.0（2.0是必须的），我不需要这么那个。

首帖子将帮你如何搭建此博客。

> 注意：此博客软件已从2020-01-06停止更新，任何问题将不会得到解决。
在2025-6-9提交了最后一个更新。

## 功能

### 主要特点


- 使用 workers 提供的 KV 作为数据库
- 使用 cloudflare 缓存 html 来降低KV的读写
- 所有 html 页面均为缓存,可达到静态博客的速度
- 使用 KV 作为数据库,可达到 wordpress 的灵活性
- 后台使用 markdown 语法,方便快捷
- 一键发布(页面重构+缓存清理)

### 承载能力

- KV 基本不存在瓶颈,因为使用了缓存,读写很少
- 唯一瓶颈是 workers 的日访问量 10w,大约能承受2万 IP /日
- 文章数: 1G 存储空间,几万篇问题不大

更多功能在与更新在[更新内容](https://blog.gezhong.vip/article/009000/update-log.html)里查看。

## 如何部署

部署方式可以从[官方](https://blog.gezhong.vip/article/000016/cloudflare-workers-blog.html)查看。

1. 首先复制[index.js](https://github.com/gdtool/cloudflare-workers-blog/blob/master/index.js)里面所有内容。
2. 去往**CloudFlare Workers**，创建一个Workers。名字随便。
3. 在所需要设置写入：
```
"codeBeforHead":`<script src='//unpkg.com/valine/dist/Valine.min.js'></script＞`,//其他代码,显示在</head>前
"commentCode":`<div id="vcomments"></div>
    <script＞
        new Valine({
            el: '#vcomments',
            appId: '你的AppID',
            appKey: '你的AppKey'
        })
    </script＞`,//评论区代码
```
	注意：若是国际版请在`new Valine({`里面添加`serverURLs`（值在设置 - 应用凭证 - REST API 服务器地址里的URL）否则会报错。

	你可以自定义输入框占位提示符，在`new Valine({`里面添加`placeholder`，值为你想要的提示符。

	在`new Valine({`里面添加`visitor: 'true'`并在`"otherCodeA"`里面写入`阅读次数:`可以显示阅读次数。


	![Visitors](https://s3.ax1x.com/2020/12/24/rcbS6s.png)

4. 保存并部署，在管理面板里 -> 发布页面点击**发布**按钮即可生效。

## 首次使用

1. 需要在管理面板 -> 设置 -> 分类输入一些分类内容，例:`["类别A","类别B","类别C","类别D"]`

2. 设置菜单，例:`[{"title":"技术文章","url":"/category/技术文章"},{"title":"管理","url":"/admin"}]`

## 发布帖子

![上面内容](https://cp.qtdt.qzz.io/api/p/files/photo/blog-add-new.png?download=false&sign=I9KANpVFloituWtoEzUpLGUlkqNp9R%2Bt7JjolA%2BERFs%3D%3A0)

- 最上面一行是标题
- 特色图片指的是此博客封面
- 永久链接指的是博客链接
- 创建日期必须是当天创建的帖子
- 分类，必选
- 标签，没必要，用逗号分开。
- 权重，不知道
- 更新平率，保存缓存的时长
- 下面的就是内容，使用的是Markdown格式

要发布此贴纸需要点击上面的**保存**才能发布。

需要在管理面板里 -> 发布页面点击**发布**才能生效。

## 更多主题

你可以在[其他主题](https://blog.gezhong.vip/article/000022/theme2.html)找到你想要的主题，默认为Default2.0。

设置主题需要修改信息里的`"themeURL"`并发布才能生效。例如：
```
"themeURL" : "https://raw.githubusercontent.com/gdtool/cloudflare-workers-blog/master/themes/default2.0/", // 模板地址,以 "/"" 结尾
```

开发主题可以参考此[文章](https://blog.gezhong.vip/article/000021/themeHelp.html)。

## 开发

> 开发博客与评论文档没人写，所以你自己看着办吧。

开发博客软件可以下载[不小心找到源码了](https://github.com/gdtool/cloudflare-workers-blog/raw/refs/heads/master/cfblog-source.zip)。

开发评论软件可以下载[又不小心搜到源码了](https://github.com/xCss/Valine/archive/refs/heads/master.zip)。

## 其他功能

这下面就是此博客可用功能

- [自建不蒜子](https://busuanzi.9420.ltd/): 简单、轻量的网页计数器。
- [一言开发者中心](https://developer.hitokoto.cn/): 用代码表达言语的魅力，用代码书写山河的壮丽。