---
title: "Hugo_depoly"
date: 2022-08-04T20:51:12+08:00
# weight: 1
# aliases: ["/first"]
tags: ["default"]
author: "oeong"
# author: ["Me", "You"] # multiple authors
draft: true
description: "Desc Text."
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



run.sh

```sh
cd hugo-of-oeong
git pull
hugo --theme=PaperMod --baseUrl="" --buildDrafts
```

定时任务

```sh
crontab -e
# 写入任务，每小时执行一次
0 */1 * * * /bin/bash /www/wwwroot/hugo/run.sh
```

