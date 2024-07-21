---
title: 各类网站数据下载
date: 2023-11-15 20:08:01
tags: 数据下载
category: 经验总结
cover: /img/cover16.png
---

## 前言

前段时间在各种网站上下载数据，发现不是所有数据都想ERA5，NCEP资料那样用鼠标点击就很容易获取。例如EASE积雪、JRA55，FNL数据等等。在数据下载这方面就费了很大功夫。有必要整理一下，各类网站资料下载的快捷方法，以免重复造轮子



## FNL

当初下载这个数据是为了用它启动WRF，参考的教程是 [NECP FNL数据批量下载 - 知乎 (zhihu.com)](https://zhuanlan.zhihu.com/p/368000766)

这个教程说得挺详细，我一遍就成功了。

[https://rda.ucar.edu/datasets/ds083.2/index.html#!access](https://link.zhihu.com/?target=https%3A//rda.ucar.edu/datasets/ds083.2/index.html%23%21access) 如下，点击Web File Listing

[![piY4asx.md.png](https://z1.ax1x.com/2023/11/15/piY4asx.md.png)](https://imgse.com/i/piY4asx)


然后：

[![piY40eK.md.png](https://z1.ax1x.com/2023/11/15/piY40eK.md.png)](https://imgse.com/i/piY40eK)

找到自己需要的年份，我这里需要2019年的数据
[![piY4oFg.md.png](https://z1.ax1x.com/2023/11/15/piY4oFg.md.png)](https://imgse.com/i/piY4oFg)


勾选需要的数据，然后选择下载方式，这里建议直接选择第一个，下载快还方便(✪ω✪)



[![piY4WOP.md.png](https://z1.ax1x.com/2023/11/15/piY4WOP.md.png)](https://imgse.com/i/piY4WOP)

最后，把下载到的download.csh文件放到你想要的存放数据的文件夹，打开终端输入指令（Linux系统下）

```text
./download.csh password（后面跟你的NECP账户密码：我的是A开头，特殊符号结尾的那个）
```

```text
如有权限问题（permission），则输入指令chmod 777 download.csh 如果文件中修改了密码，还是报错未设置密码，可以输入dos2unix download.csh指令
```



## EASE 积雪

官方网站 https://nsidc.org/data/nsidc-0046/versions/4，使用`wget`下载

```bash
$ wget --load-cookies ~/.urs_cookies --save-cookies ~/.urs_cookies --keep-session-cookies --no-check-certificate --auth-no-challenge=on -r --reject "index.html*" -np -nH -r -e robots=off https://daacdata.apps.nsidc.org/pub/DATASETS/nsidc0046_weekly_snow_seaice/data/
```

在下载之前需要在home下添加 `.netrc` 文件，并添加以下内容

```bash
machine urs.earthdata.nasa.gov login 用户名(xiaoh*****66**) password 密码(A66*****22a*h)
```

顺便贴一下处理程序

```python
# 坐标信息
coords = xr.open_dataset('/disk3/snow.nsidc0046_weekly_snow_seaice/EASE2_N25km.geolocation.v0.9.nc')
latitude = coords.latitude
longitude = coords.longitude

filelist = glob.glob('/disk1/xhw/code/Myresearch/SavedData/EASE/pub/DATASETS/nsidc0046_weekly_snow_seaice/data/EASE2_N25km.snowice.*.bin')
filelist.sort()
time = []


snow = np.zeros((len(filelist),720*720))
for j in range(len(filelist)):
    time.append(np.datetime64(pd.to_datetime(filelist[j][-25:-17])))
    f = open(filelist[j],"rb")
    data = f.read()
    f.close()

    for i in range(len(data)):
        snow[j,i] = data[i]

    print(j,'/',len(filelist))

snow = snow.reshape((len(filelist),720,720))
```





