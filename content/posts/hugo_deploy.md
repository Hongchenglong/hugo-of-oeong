---
title: "Hugo_depoly"
date: 2022-08-04T20:51:12+08:00
# weight: 1
# aliases: ["/first"]
tags: ["linux", "hugo"]
author: "oeong"
# author: ["Me", "You"] # multiple authors
draft: true
hidden: true
description: "Hugo - The world’s fastest framework for building websites"
showToc: true
TocOpen: false
hidemeta: false
comments: false
UseHugoToc: true
canonicalURL: "https://canonical.url/to/page"
disableHLJS: true # to disable highlightjs
disableShare: false
disableHLJS: false
hideSummary: false
searchHidden: false
ShowReadingTime: true
ShowBreadCrumbs: true
ShowPostNavLinks: true
ShowWordCount: true
ShowRssButtonInSectionTermList: true
cover:
    image: "<image path/url>" # image path/url
    alt: "<alt text>" # alt text
    caption: "<text>" # display caption under cover
    relative: false # when using page bundles set this to true
    hidden: true # only hide on current single page
editPost:
    URL: "https://github.com/Hongchenglong/hugo-of-oeong/blob/main/content"
    Text: "Suggest Changes" # edit text
    appendFilePath: true # to append file path to Edit link
---

The world’s fastest framework for building websites

<!--more-->

hugo: https://github.com/gohugoio/hugo

hugo模板：https://github.com/adityatelange/hugo-PaperMod

## 本地


配置config.yml

```
params:
  label:
    text: "Home"
    icon: /assets/img/Neutral_Face_Emoji_grande.png
    iconHeight: 35
```

## 服务器

写运行脚本
```bash
vim run.sh
```

```sh
hugo=/www/wwwroot/hugo
cd ${hugo}/hugo-of-oeong
git pull
# 构建项目，生成public
hugo --theme=PaperMod --baseUrl="" --buildDrafts
```

部署在Nginx上，将img复制到public/assets/ 
```bash
cp -r ${hugo}/hugo-of-oeong/assets/img/ ${hugo}/hugo-of-oeong/public/assets/ 
```

定时任务

```sh
crontab -e
# 写入定时任务，每小时执行一次
0 */1 * * * /bin/bash /www/wwwroot/hugo/run.sh
```

