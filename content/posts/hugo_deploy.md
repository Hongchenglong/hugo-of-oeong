---
title: "hugo部署记录"
date: 2022-08-04T20:51:12+08:00
tags: ["hugo", "linux"]
author: "oeong"
draft: false
description: "Hugo is the world’s fastest framework for building websites."
---

[Hugo](https://github.com/gohugoio/hugo) is the world’s fastest framework for building websites.

<!--more-->

简单记录部署hugo的过程

## 本地


配置config.yml

```
params:
  label:
    text: "Home"
    icon: /assets/img/Neutral_Face_Emoji_grande.png
    iconHeight: 35
```

常用命令

```bash
# 启动hugo
hugo server -D
# 以post模板生成文章
hugo new --kind post posts/hugo_depoly.md
```

## 服务器

克隆仓库

```
git clone https://github.com/Hongchenglong/hugo-of-oeong.git
```

写运行脚本
```bash
vim run.sh
```

```sh
hugo=/www/wwwroot/hugo
cd ${hugo}/hugo-of-oeong
# 拉取远程仓库的代码
git pull
# 构建项目，生成public
hugo --theme=PaperMod --baseUrl="" --buildDrafts
```

配置nginx.conf

```conf
server
{
    listen 80;
    server_name hugo.oeong.com;
    index index.php index.html index.htm default.php default.htm default.html;
    root /www/wwwroot/hugo/hugo-of-oeong/public;
    
    ...
}
```

将img复制到public/assets/ 

```bash
cp -r ${hugo}/hugo-of-oeong/assets/img/ ${hugo}/hugo-of-oeong/public/assets/ 
```

定时任务

```sh
crontab -e
# 设置定时任务，每小时执行一次
0 */1 * * * /bin/bash /www/wwwroot/hugo/run.sh
```

## 参考

- [hugo-PaperMod](https://github.com/adityatelange/hugo-PaperMod) 

