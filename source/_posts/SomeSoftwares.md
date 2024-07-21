---
title: 一些装机软件
date: 2023-09-04 15:13:33
tags: 软件
category: 碎碎念
cover: /img/cover15.jpg
---



## 前言

记录一下最近用的一些实用软件，因为这些软件需要配置一些插件才好使。插件多，配置过程繁琐，所以记录一下。



## Zotero

- [zotero-pdf-translate](https://github.com/windingwind/zotero-pdf-translate) ：文献翻译插件，几乎不用怎么额外设置，很实用。支持Zotero7 beta

- [zotero-tag](https://github.com/windingwind/zotero-tag) ：标签插件，能够以颜色和标志给文献添加标签。添加文献后能够自动添加 “未读” 标签，打开pdf后自动去除 “未读”。但是目前（2023.9.4）作者还没有支持Zotero7。
- [zotero-style](https://github.com/MuiseDestiny/zotero-style) ：能够为Zotero添加更多列，能够将文献标签直接展示在主页面并可以为标签创建分类。实现类似Endnote的 “未读” 粗体和文献评级。支持Zotero7 beta



## Obsibian

- [Obsidian-Typora-Vue-Theme](https://github.com/ZekunC/Obsidian-Typora-Vue-Theme) : Obsibian的一款外观主题，仿Typora。我觉得比较好看
- [obsidian-editing-toolbar](https://github.com/PKM-er/obsidian-editing-toolbar) ：Obsibian不能直接对文本进行高亮、字体颜色等更改。这个插件安装后会出现一个工具栏，能够实现对文本的富文本操作（高亮等）
- [tag-wrangler](https://github.com/pjeby/tag-wrangler) ：标签管理插件，与 `zotero-tag` 类似为能够为标签创建分类。在文本内加入 `#标签` 即可创建一个标签(井号后没有空格)。
- [obsidian-image-auto-upload-plugin](https://github.com/renmu123/obsidian-image-auto-upload-plugin) ：自动将图片上传图床插件。当我们从Zotero笔记中复制一个图过来或屏幕截屏直接粘贴进Obsidian中时，这个插件会将该图通过 `PicGo` 自动上传图床。图片位置也会自动添加 `![](url)` 方便存储笔记图片。使用该插件前需要先下载安装 `PicGo` 软件



## PicGo

[PicGo](https://github.com/Molunerfinn/PicGo) 这是一款将图片快速上传图床的软件。提供 Github、腾讯云、阿里云、七牛图床等接口。我一般使用 Github作为图床， 图片存在仓库664787022/imagSave 内，使用前需要对 PicGo 进行配置。配置方法见文档：[配置手册 | PicGo](https://picgo.github.io/PicGo-Doc/zh/guide/config.html#smms) 



## ClickRun

[ClickRun鼠标连点器](https://github.com/InJeCTrL/ClickRun) 一个简易鼠标连点器。`F1,2,3,4...` 等键启动暂停。可设置点击间隔。



## EV录屏

[EV录屏 - 免费高清无水印的屏幕录制软件](https://www.ieway.cn/evcapture.html)  免费无水印录屏软件，很好用



## VScode插件

- Bookmarks: 书签，可以跳转代码
- folder-alias：可以给文件或文件夹加上别名，等于是一个备注

- vscode-icons: 改变文件图标
