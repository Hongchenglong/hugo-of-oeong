---
title: "commit message格式"
date: 2022-08-04T14:20:42+08:00
author: "oeong"
categories: 
- 
tags: 
- tech
- git
draft: false
description: "<type>(<scope>): <subject>"
---

`git commit -m "<message>"`是git提交代码的命令，commit message应该清晰明了，说明本次提交的目的，具体做了什么操作，方便之后定位先前版本的代码。

<!--more-->

但是日常工作中，开发人员往往比较随意，commit message没有规范，日后维护比较困难。所以在今后的工作中，我们可以参考[Git Commit Template](https://plugins.jetbrains.com/plugin/9861-git-commit-template)的commit message格式：
`<type>(<scope>): <subject>`

## type（必须）
用于说明git commit的类别，只允许使用下面的标识。

- feat：新功能（feature）
- fix：修复bug
- docs：文档（documentation）
- style：格式，不影响代码运行的变动，空格、注释
- refactor：重构，即不是新增功能，也不是修改bug的代码变动
- perf：优化相关，比如提升性能、体验
- test：增加测试
- chore：构建过程或辅助工具的变动
- revert：回滚到之前的版本

## scope（可选）

scope用于说明 commit 影响的范围，比如数据层、控制层、视图层等等。

## subject（必须）

subject是commit目的的简短描述，不超过50个字符。结尾不加句号或其他标点符号。

最后，根据以上规范，commit message将是如下的格式：
```
feat(Controller): 用户查询接口开发
```

## 参考

- IDEA插件：[Git Commit Template](https://plugins.jetbrains.com/plugin/9861-git-commit-template)