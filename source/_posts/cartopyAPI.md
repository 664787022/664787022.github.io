---
title: Cartopy 调用"天地图"底图
date: 2023-03-16 14:23:42
tags: Cartopy调用地图底图AIP
category: 编程
cover: /img/cover10.jpg
---

## 前言

科研绘图上地图底图一般是白色的，加上海岸线也就成底图。这种做法的好处是如果我们需要向底图上添加等值线、填色图等附有彩色信息的图案或线条，这种信息在白底下更突出。作为可以绘图，这种白底也最简单、严肃。

但是如果我们要画出某个台风的移动路径，偌大的白图上就横躺这几根线条略显单调。这时如果能丰富底图，整张图的效果会有很大提升。

使用这种底图需要调用其他网站的地图接口，让图像叠加在`Cartopy`的坐标轴内。

## Cartopy无网络底图

`Cartopy`内置了一种底图 `ax.stock_img()`，不需要利用网络接口。缺点就是分辨率很差。

```python
import matplotlib.pyplot as plt
import cartopy.crs as ccrs
from cartopy.mpl.gridliner import LONGITUDE_FORMATTER, LATITUDE_FORMATTER
import pandas as pd
import numpy as np

lon = np.array([126.4, 126.1, 125.9, 125.6, 125.2, 124.8, 124.5, 124.1, 123.7,
       123.4, 123.3, 123.5, 123.5, 123.5, 123.4, 123. , 122.6, 122.1,
       121.5, 121.2, 120.6, 119.8, 119.8, 120.1, 120.5, 120.8, 121.3,
       122.6, 123.7, 125.5, 126.3, 127.6, 130.1, 131.3, 132.3, 133.3,
       134.6, 136.2, 137.6, 139.4])

lat = np.array([20.1, 20.2, 20.1, 19.8, 19.3, 18.7, 18.5, 18.3, 18.1, 18. , 18.1,
       18.6, 19.3, 20.3, 21.2, 22.4, 23.2, 24.1, 24.7, 25.2, 26.1, 26.8,
       27.3, 28.1, 29.4, 31.4, 33. , 33.8, 35.2, 37.6, 38.4, 39.1, 40.1,
       41. , 42. , 42.7, 43.3, 44.1, 44.6, 45. ])


#%% 定义绘图函数
def getMap(proj=ccrs.PlateCarree(), extent=[100, 180, 0, 60]):
    fig = plt.figure(figsize=(12,12))
    proj = ccrs.PlateCarree()
    ax = fig.add_subplot(111, projection=proj)
    ax.set_extent(extent, crs=ccrs.PlateCarree())


    # 添加刻度
    lon_lat = ax.gridlines(draw_labels=True, linewidth=0, color='k', alpha=0.2, linestyle='--')
    lon_lat.xlabels_top = False
    lon_lat.ylabels_right = False 
    lon_lat.xformatter = LONGITUDE_FORMATTER 
    lon_lat.yformatter = LATITUDE_FORMATTER
    return fig, ax 


fig1, ax1 = getMap()

# 添加底图
ax1.stock_img()
ax1.plot(lon, lat, '.-r',transform=ccrs.PlateCarree())
```

<img src="https://img-blog.csdnimg.cn/e6295dcbfd4a46ceb204abe31d75f7de.png" title="" alt="" data-align="center">

## Cartopy 连接国外API

暂时连不上，以后再码

[Web services &#8212; cartopy 0.21.0 documentation](https://scitools.org.uk/cartopy/docs/latest/gallery/web_services/index.html)

## Cartopy 理解国内”天地图“网站API

### 第一步：修改Cartopy文件

安装好Cartopy后，修改以下文件

```
\Anaconda3\envs\你的虚拟环境名称\Lib\site-packages\cartopy\io\img_tiles.py
```

如果用的是base环境，路径如下

```
\Anaconda3\Lib\site-packages\cartopy\io\img_tiles.py
```

在`imh_tiles.py`文件末尾添加

```python
# 天地图矢量
class TDT_vec(GoogleWTS):
    def _image_url(self, tile):
        x, y, z = tile
        key = 'f51d7378813e172b83c8edc7ddedb1c9'
        url = 'http://t0.tianditu.gov.cn/DataServer?T=vec_w&x=%s&y=%s&l=%s&tk=%s' % (x, y, z, key)
        return url

# 天地图遥感
class TDT_img(GoogleWTS):
    def _image_url(self, tile):
        x, y, z = tile
        key = 'f51d7378813e172b83c8edc7ddedb1c9'
        url = 'http://t0.tianditu.gov.cn/DataServer?T=img_w&x=%s&y=%s&l=%s&tk=%s' % (x, y, z, key)
        return url

# 天地图地形
class TDT_ter(GoogleWTS):
    def _image_url(self, tile):
        x, y, z = tile
        key = 'f51d7378813e172b83c8edc7ddedb1c9'
        url = 'http://t0.tianditu.gov.cn/DataServer?T=ter_w&x=%s&y=%s&l=%s&tk=%s' % (x, y, z, key)
        return url
```

### 第二部：申请“天地图”密钥

在网站 [天地图API](http://lbs.tianditu.gov.cn/server/MapService.html) 注册登陆账号。申请密钥：

<img title="" src="https://img-blog.csdnimg.cn/65c411c7d08b45b18ba52e837a8563a3.png" alt="" data-align="center" width="358">

点击“创建新应用”，内容随便填写

<img title="" src="https://img-blog.csdnimg.cn/ef39262500cd4f10a8823c9318a18109.png" alt="" data-align="center" width="440">

<img title="" src="https://img-blog.csdnimg.cn/968cd3f229054f5b8a7e0b193e255ab5.png" alt="" data-align="center" width="337">

然后就得到密钥了：

<img title="" src="https://img-blog.csdnimg.cn/0d9c7a0cdea6409fad21fd256af03e44.png" alt="" data-align="center" width="477">

如果不想申请密钥，可以用我以前的密钥，就是`imh_tiles.py`中已经填好的，key = 'f51d7378813e172b83c8edc7ddedb1c9'。但是这个申请的不知道什么时候可能会失效。

> 个人申请的密钥一天调用上限是1万次。如果程序运行遇到网络问题、被禁止访问时，程序会不停地调用这个接口，很容易超过1万次。所以遇到报错要及时手动停止程序。

### 第三步：程序使用，绘图程序

```python
import cartopy.io.img_tiles as cimgt

def getMap(nrows=1, ncols=1, proj=ccrs.PlateCarree(), extent=[100, 180, 0, 60]):

    fig, ax = plt.subplots(nrows, ncols, subplot_kw=dict(projection=proj),figsize=(36,12))
    for axx in ax:
        axx.set_extent(extent, crs=ccrs.PlateCarree())


        # 添加刻度
        lon_lat = axx.gridlines(draw_labels=True, linewidth=0, color='k', alpha=0.2, linestyle='--')
        lon_lat.xlabels_top = False
        lon_lat.ylabels_right = False 
        lon_lat.xformatter = LONGITUDE_FORMATTER 
        lon_lat.yformatter = LATITUDE_FORMATTER
    return fig, ax 


fig3, ax3 = getMap(nrows=3)

# 调用天地图
a = cimgt.TDT_vec() # 矢量图
b = cimgt.TDT_img() # 影像图
c = cimgt.TDT_ter() # 地形图

ax3[0].add_image(a, 4) # 数字4表示第四图层。1-9数字越高清晰度越好，但程序花费时间越多
ax3[1].add_image(b, 4)
ax3[2].add_image(c, 4)

for i in range(3):
    ax3[i].plot(lon, lat, '.-r',transform=ccrs.PlateCarree())
```

<img src="https://img-blog.csdnimg.cn/91152be5da344cb0a00ac5d601f7f569.png" title="" alt="" data-align="center">
