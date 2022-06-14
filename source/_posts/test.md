---
title: hexo相关命令以及本地文件备份
date: 2022-05-22 19:57:12
tags: 测试
cover: /img/cover4.jpg
category: 博客配置
---
今天为了整博客的图库差点把博客源文件整没了。恢复以后，尝试了很久在github上备份本地博客文件。参考了以下文章：
[博客备份与换设备](https://blog.csdn.net/weixin_44861399/article/details/104936907)

在这里顺便写点hexo相关命令，防止以后忘记了。

##### 清除和再生成 (大概是这个意思吧)
```bash
hexo clean && hexo g
```
##### 部署至github
```bash
hexo d
```
##### 生成静态地址(本地)
```bash
hexo s
```
##### 新建文章
```bash
hexo new post test
```
##### 将静态文件推送到master分支
```bash
hexo clean 
hexo d -g
```
##### 将相关更改推送到hexo分支
```bash
git add .
git commit -m "发表文章test"
git push origin hexo
```
