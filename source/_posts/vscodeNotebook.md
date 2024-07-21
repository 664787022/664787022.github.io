---
title: VsCode使用jupyter时附加交互窗口
date: 2024-04-30 18:26:48
tags: 经验总结
cover: /img/cover21.png
---

## 前言

Vscode里使用jupyter notebook是很方便的事情，但我习惯使用F9逐行运行。这样方便调试和查看变量。但是在notebook中使用F9跳出的交互窗口与notebook本身并不共享内存，也就是在交互窗口与notebook之间数据不互通。Github上也有不少帖子在呼吁这一功能的增加，例如[Support a notebook "scratch pad" and/or integrate interactive window experience for notebooks · Issue #4573 · microsoft/vscode-jupyter (github.com)](https://github.com/microsoft/vscode-jupyter/issues/4573) 和 [Support a scratchpad for a jupyter notebook · Issue #6484 · microsoft/vscode-jupyter (github.com)](https://github.com/microsoft/vscode-jupyter/issues/6484)。 目前有一个可行的解决方案来自第二个链接。

## jupyter 添加conda环境

jupyter使用的比较少，我才发现在使用之前需要先做一些操作才能找到conda环境

如果jupyter显示内核不可用

```bash
python -m ipykernel install --user
```



如果找不到自己的conda环境

```bash
python -m ipykernel install --user --name 环境名
```



## 从终端启动notebook

这个可行方案需要将notebook和交互窗口链接到同一个内核上。在终端命令行输入

```bash
jupyter notebook
```

会输出一个URL链接，形如 `http://localhost:8889/?token=a8dfgfdgfd757fdfsggsgb3687e8967fbdfhfdhgdgdfgcff` 。

点击Vscode notebook的选择内核--->选择其他内核--->现有jupyter服务器。 输入以上URL，取一个名字例如test1。选择自己的conda环境。

这样notebook就配置好了。在使用F9后会出现交互窗口，交互窗口需要选择内核--->选择其他内核--->现有jupyter服务器。 选择test1，选择和notebook同样的环境(会出现`1连接` 的字样，就选择这一个，因为这正是notebook所正在连接的)。 然后就配置完成啦！



