---
title: "Hugo入门及部署"
date: 2023-01-11 00:00:00
draft: false
author: ["oeong"]
categories: 
- 
tags: 
- tech
- hugo
description: ""
showToc: true # 显示目录
TocOpen: true # 自动展开目录
---

## Hugo是什么？

https://gohugo.io/

> The world’s fastest framework for building websites.

Hugo是一个用Go编写的静态HTML和CSS网站生成器。它针对速度、易用性和可配置性进行了优化。Hugo将一个带有内容和模板的目录，渲染成一个完整的HTML网站。

Hugo可以在几秒内渲染出一个中等规模的网站，其中每个页面内容的渲染时间约为1毫秒。

Hugo依靠带有Front Matter元数据的Markdown文件，而且可以在任何目录中运行Hugo。Front matter定义着每篇文章的属性，比如标题、分类等。

## 怎么使用Hugo？

### 前置准备

安装Git

安装Hugo

```shell
# macOS
brew install hugo

# Windows
choco install hugo -confirm

# Linux
snap install hugo
```

```
hugo version
hugo help
```

### 创建站点

用hugo生成目录名为quickstart的网站

```
hugo new site quickstart
```

进入quickstart文件夹，初始化Git仓库

```
cd quickstart
git init
```

```
$ tree
.
├── archetypes				文章模板
│   └── default.md
├── config.toml				配置文件
├── content						文章目录
├── data							数据文件
├── layouts						布局模板
├── public						构建网站生成的静态文件
├── static						静态资源
└── themes						主题目录
```

选择[主题](https://themes.gohugo.io/)。克隆[PaperMod](https://themes.gohugo.io/themes/hugo-papermod/)主题到themes目录，将其作为Git子模块添加到项目中。在网站配置文件中添加一行，表示当前的主题。

```
git submodule add https://github.com/adityatelange/hugo-PaperMod themes/PaperMod
echo "theme = 'PaperMod'" >> config.toml
```

启动Hugo开发服务器

```
hugo server
```

### 添加内容

添加一个新页面，默认根据archetypes/default.md生成带有元数据的markdown文件。

```
hugo new posts/my-first-post.md
```

```
---
title: "My First Post"
date: 2023-01-01T09:03:20-08:00
draft: true
---
```

```
## Introduction

This is **bold** text, and this is *emphasized* text.

Visit the [Hugo](https://gohugo.io) website!
```

启动Hugo开发服务器，预览网站，--buildDrafts或-D表示会显示草稿内容（draft: true）

```
hugo server --buildDrafts
hugo server -D
```

在终端显示的URL上查看网站。当继续添加和改变内容时，保持开发服务器的运行。在源文件处修改的内容可以实时地显示在网页上，而不用再次敲代码生成再预览。

### 配置站点

Hugo配置文件config放置在根目录下，并且支持三种格式：toml，yaml，yml，默认为toml格式。

```
baseURL = 'http://example.org/'
languageCode = 'en-us'
title = 'My New Hugo Site'
theme = 'PaperMod'
```

### 发布站点

构建网站，并生成public文件夹，可以将public部署到云服务器或者托管到github上。

```
hugo
```
发布站点时，不会显示草稿，过期及未来的内容。

- draft为true
- expiryDate在过去

- date、publishDate在未来

## 个性化配置

###  修改模板

修改Front Matter模板 archetypes/default.md，生成的文章默认采用此模板。

```
vim archetypes/default.md
```

```
---
title: "{{ replace .Name "-" " " | title }}"
date: {{ .Date }}
draft: true
author: ["xxx"]
tags: 
-
description: ""
---
```

### 配置文件

站点配置文件config改成.yaml后缀的写法，因为yaml格式更适合阅读，配置详见[Configure Hugo](https://gohugo.io/getting-started/configuration/)。

```
mv config.toml config.yaml
vim config.yaml
```

```
baseURL: "http://example.org/"
languageCode: en-us
title: Hugo
theme: PaperMod

languages:
    en:
        languageName: "English"
        weight: 1
        taxonomies:
            category: categories
            tag: tags
            series: series
        profileMode:
            enabled: true
            buttons:
                - name: 👨🏻‍💻 技术
                  url: posts/tech
                - name: 📕 阅读
                  url: posts/read
                - name: 🏖 生活
                  url: posts/life
        menu:
            main:
                - name: search
                  url: search
                  weight: 1
                - name: posts
                  url: posts
                  weight: 5
                - name: archives
                  url: archives
                  weight: 10                
                - name: tags
                  url: tags
                  weight: 15

params:
    label:
        text: "Hugo"
        icon: "<link / abs url>" # 位于static下
        iconHeight: 35
    env: production # to enable google analytics, opengraph, twitter-cards and schema.
    # description: "..."
    author: Hugo
    defaultTheme: auto  # defaultTheme: light or  dark 
    disableThemeToggle: false
    DateFormat: "2006-01-02"
    ShowShareButtons: true
    ShowReadingTime: true
    displayFullLangName: true
    ShowPostNavLinks: true
    ShowBreadCrumbs: true
    ShowCodeCopyButtons: true
    hideFooter: false # 隐藏页脚
    ShowWordCounts: true
    VisitCount: true
    Reward: true # 打赏
    ShowLastMod: true #显示文章更新时间
    ShowToc: true # 显示目录
    TocOpen: true # 自动展开目录
    comments: true

    homeInfoParams:
        Title: "Hi there."
        Content: >
            Welcome to my blog.

    socialIcons:
        - name: twitter
          url: "https://twitter.com"
        - name: github
          url: "https://github.com"
        - name: Rss
          url: "index.xml"

    editPost:
        URL: "https://github.com/xxx/xxx/tree/main/content"
        Text: "Suggest Changes" # edit text
        appendFilePath: true # to append file path to Edit link

    assets:
        disableHLJS: true
        favicon: "<link / abs url>"
        favicon16x16: "<link / abs url>"
        favicon32x32: "<link / abs url>"
        apple_touch_icon: "<link / abs url>"
        safari_pinned_tab: "<link / abs url>"

    cover:
        hidden: false # hide everywhere but not in structured data
        hiddenInList: false # hide on list pages and home
        hiddenInSingle: false # hide on single page

    fuseOpts:
        isCaseSensitive: false
        shouldSort: true
        location: 0
        distance: 1000
        threshold: 0.4
        minMatchCharLength: 0
        keys: ["title", "permalink", "summary"]

minify:
    disableXML: true

outputs:
    home:
        - HTML
        - RSS
        - JSON

paginate: 5 # 首页每页显示的文章数
enableInlineShortcodes: true
enableEmoji: true # 允许使用 Emoji 表情，建议 true
enableRobotsTXT: true # 允许爬虫抓取到搜索引擎，建议 true
hasCJKLanguage: true # 自动检测是否包含 中文日文韩文 如果文章中使用了很多中文引号的话可以开启
buildDrafts: false
buildFuture: false
buildExpired: false
googleAnalytics:  # 谷歌统计
```

### 目录设置

content/posts 新建文件夹 tech、read、life

content里每个文件夹内都要添加一个_index.md文件，该文件里面可以加Front Matter用来控制标题或其它的展示

```
mkdir content/posts/tech
vim content/posts/tech/_index.md

---
title: "👨🏻‍💻 技术"
description: "不积跬步，无以至千里；不积小流，无以成江海"
hidemeta: true # 是否隐藏文章的元信息，如发布日期、作者等
---
```



```
mkdir content/posts/read
vim content/posts/read/_index.md

---
title: "📕 阅读"
description: "读书如不及时做笔记，犹如雨落大海没有踪迹"
hidemeta: true # 是否隐藏文章的元信息，如发布日期、作者等
---
```



```
mkdir content/posts/life
vim content/posts/life/_index.md

---
title: "🏖 生活"
description: "记录生活、热爱生活、感受生活"
hidemeta: true # 是否隐藏文章的元信息，如发布日期、作者等
---
```

### 菜单配置

content 新建文件 search.md、archives.md

search页面可以搜索文章内容

```
vim content/search.md

---
title: "search"
layout: "search"
---
```

archives页面将文章按时间归档

```
vim content/archives.md

---
title: "archives"
layout: "archives"
---
```

### 添加内容

在content目录的posts目录下自定义分类tech、read、life后，可以指定目录生成文章。

```
hugo new posts/tech/tech-post.md
```

### 模板推荐

[PaperMod 模板样例](https://github.com/adityatelange/hugo-PaperMod/tree/exampleSite)

[sulv-hugo-papermod](https://github.com/xyming108/sulv-hugo-papermod) 是一个根据PaperMod所修改的主题，使用它的模板，只需修改个人信息。

## 部署博客

将Hugo博客部署到公网，使得别人可以访问：

1. 域名和服务器
2. 托管到Github

以`<username>.github.io`形式命名的仓库，上传`hugo`生成的`public`文件，使用 GitHub Pages 实现网站部署，可以通过域名 CNAME 解析使用自定义域名。

### 上传public

进入到public目录，将public的内容推送到GitHub

```
 # 进入到public目录
 cd public
 
 # 初始化git仓库
 git init
 
 # 将所有内容添加到git
 git add .
 
 # 提交到git本地
 git commit -m "message"
 
 # 关联到远程git仓库
 git remote add origin https://github.com/<username>/<username>.github.io.git
 
 # 推送到远程git仓库
 git push origin master
```

### 访问公网地址

访问`https://<username>.github.io`，成功部署到GitHub Pages，可以通过域名 CNAME 解析使用自定义域名。
