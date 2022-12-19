---
title: 地图及地图文件使用技巧
date: 2022-07-08 22:14:11
tags: geopandas
category: 编程 tips
cover: /img/cover6.jpg
---

## 前言

记录一下使用地图及地图文件的小技巧吧

---

## 地图的合并

bou2_4p.shp 由各个省份的polygon组成。 如何将江苏省和山东省的polygon合并组成一个polygon呢？

```python
import geopandas as gpd
import shapely

# 读取数据
china = gpd.read_file('bou2_4p.shp', encoding='gbk')

# 提取江苏和山东的 polygon
province = china.loc[china.NAME.isin(['江苏省','山东省']), 'geometry']

# 合并polygon
polygon_combine = shapely.ops.unary_union(province)
```

---

&nbsp;

## Proplot极地投影画出直线段

今天作图的时候想在地图上取一个剖面，于是想现在图上画出剖面线段。这件事本来在等经纬度投影下是一件很容易的事情，然而我的地图是北极投影，做出来的效果并不是想象中的样子。

```python
import proplot as pplt
fig, ax = pplt.subplots(proj='npaeqd', proj_kw={'lon_0':160})
ax.stock_img()
ax.plot([90,210],[80,30], marker='o', transform='npaeqd')
ax.format(labels=True, coast=True)
```

<img title="" src="https://img-blog.csdnimg.cn/a71659de2e6b4d98a61b8f2c5b0f43fd.png" alt="请添加图片描述" data-align="center">

如上所示，我想在`(90E,80N)`和`(210E, 30N)`之间画一个线段，然而并不能实现。这并不是 `Proplot`的问题，问题在于极地投影下经纬度并不 `（-180~180，-90-90）` 的范围。我们需要将等经纬度投影下的`(90E,80N)`和`(210E, 30N)` 转换到极地投影下的经纬度坐标。如何实现呢？ 其实在 [<font color=CornflowerBlue>利用 geopandas 地图白化 | XHW's Blog (664787022.github.io) </font>](https://664787022.github.io/2022/06/22/geomask/) 这篇博文里讲了类似的方法。

```python
import proplot as pplt
import cartopy.crs as ccrs
from matplotlib.path import Path  

# 将等经纬度投影的经纬度转为极地投影下的坐标
pp = ccrs.NorthPolarStereo()
path_clip = Path(pp.transform_points(ccrs.PlateCarree(),
                 np.array([90,210]), np.array([80,30]))[:,0:2])

fig, ax = pplt.subplots(proj='npaeqd', proj_kw={'lon_0':160})
ax.stock_img()
ax.plot(path_clip.vertices[:,0],path_clip.vertices[:,1], marker='o',
        transform='npaeqd')
ax.format(labels=True, coast=True)
```

<img src="https://img-blog.csdnimg.cn/681da9e3b5444bce93a3c583445e81b5.png" title="" alt="在这里插入图片描述" data-align="center">

如果不使用` Proplot` 而直接用 `Cartopy` ，情况会更简单一点。因为在 `Cartopy下` 可以使用 `ccrs.Geodetic()`  而 `Proplot` 似乎没有把 `ccrs.Geodetic()` 加入进自己的代码。

```python
import matplotlib.pyplot as plt
import cartopy.crs as ccrs

fig = plt.figure()
ax = fig.add_subplot(1, 1, 1, projection=ccrs.NorthPolarStereo(central_longitude=160))

ax.stock_img()
ax.coastlines() 
# 注意这里使用的是ccrs.Geodetic()，使用ccrs.NorthPolarStereo是没用的
ax.plot([90,210],[80,30], marker='o', transform=ccrs.Geodetic())
```

<img src="https://img-blog.csdnimg.cn/9ce0b9e361084cc091894ec2a84453c0.png" title="" alt="在这里插入图片描述" data-align="center">

---
