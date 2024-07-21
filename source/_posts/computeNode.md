---
title: VsCode连接到集群的计算节点
date: 2024-04-24 21:50:17
tags: Linux
category: Linux
cover: /img/cover01.jpeg
---

## 前言

最近拿到了大装置的账号，在大装置中用户在登陆节点登陆，在网络节点下载，在计算节点计算。VsCode可以正常连接到登陆节点，但在登陆节点运行程序、处理数据会引起节点拥堵。应当进一步连到计算节点上进行处理数据。



## 申请计算节点

大装置上的调度系统是slurm，可使用 `salloc` 申请计算节点

```bash
salloc -n 1 -c 1 -p cpu_single --mem=50G
```

在debug分区，申请ntask=1, cpu=1的节点资源, 申请50G内存，内存太小读取数据会导致崩溃

使用 `squeue` 查询申请到的节点名，假如是 `a3105n01`



## 跳板机

查询网络教程，我发现大神们是通过本地计算机作为”跳板“连接到计算节点的。首先应当在本地cmd中输入

```bash
ssh-keygen -t rsa
```

一路回车，将在`C:/User/用户名/.ssh/`下生成 `id_rsa.pub`



## 添加密钥

假设我们已经在登陆节点login02上使用xshell登陆。将 `id_rsa.pub`改名`myDesktop_id_rsa.pub`上传到 `~/.ssh/`。然后将密钥添加

```bash
cat myDesktop_id_rsa.pub >> ./authorized_keys
```



## 更改VsCode config

打开VsCode的SSH配置文件，添加

```bash
# 以下是连接登陆节点的配置
Host earthlab_vscode # 名字随便
    HostName login.earthlab.iap.ac.cn
    User elzd_2024_000125
    IdentityFile "c:\Users\dzz\Desktop\login.earthlab.iap.ac.cn_0419125906_rsa.txt"

# 以下是连接计算节点的配置
Host earthlab_Py_debug  # 名字随便
    HostName a3105n01
    User elzd_2024_000125
    ProxyCommand ssh.exe -W %h:%p earthlab_vscode # 注意是ssh.exe,不是ssh
```

