---
title: "Hugo部署记录"
date: 2022-08-04T20:51:12+08:00
author: "oeong"
categories: 
- 
tags: 
- tech
- hugo
- linux
draft: false
description: "Hugo is the world’s fastest framework for building websites."
---

[Hugo](https://github.com/gohugoio/hugo) is the world’s fastest framework for building websites.

<!--more-->

最近从hexo换到hugo框架，hugo是一个用go语言编写的静态网站生成器，号称世界上最快的构建网站工具。在此，简单记录本地搭建hugo，部署到服务器的过程。

## 本地


配置config.yml

```yml
baseURL: "https://oeong.com/"

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
git remote add gitee https://gitee.com/oeong/hugo-of-oeong.git
```

写运行脚本`vim run.sh`

```sh
hugo=/www/wwwroot/hugo
cd ${hugo}/hugo-of-oeong
# 拉取远程仓库的代码
git pull gitee main
# 构建项目，生成public，外面的文件会默认替换主题的文件
hugo
```

如果是从其他地方copy过来的站点，有可能遇到下面的问题，这个时候需要重新git clone一下主题

```sh
WARN 2021/02/03 10:56:17 found no layout file for "HTML" for kind "home": You should create a template file which matches Hugo Layouts Lookup Rules for this combination.
```

配置`nginx.conf`

```conf
server
{
    listen 80;
    server_name oeong.com;
    index index.php index.html index.htm default.php default.htm default.html;
    # 网站根路径是打包后的public
    root /www/wwwroot/hugo/hugo-of-oeong/public;
}
```

定时任务执行`run.sh` ，自动拉取新代码，构建项目

```sh
crontab -e
# 设置定时任务，每小时执行一次
0 */1 * * * /bin/bash /www/wwwroot/hugo/run.sh
```

## 参考

- [hugo-PaperMod](https://github.com/adityatelange/hugo-PaperMod) 
- [sulv-hugo-papermod](https://github.com/xyming108/sulv-hugo-papermod)
- [Hugo 部署到自己服务器](https://www.jianshu.com/p/62e51e8d2d84)
- [浅谈我为什么从 HEXO 迁移到 HUGO](https://sspai.com/post/59904)
