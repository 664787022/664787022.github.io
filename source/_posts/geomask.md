---
title: 利用geopandas地图白化
date: 2022-06-22 09:14:14
tags:     
    - 白化
    - proplot
category: 编程
cover: /img/cover6.png
---

## 前言

偶然间看到摸鱼咯大佬在和鲸社区发的帖子 [<font color=CornflowerBlue>geopandas白化</font>](https://www.heywhale.com/mw/project/621450308da0860017bdfb1a)，利用了`geopandas`对等值线进行白化。以往我是用气象家园中的maskout.py函数进行白化的。但使用maskout.py需要结合meteoinfo对地图文件进行查看，相对来说还是比较麻烦的。在这里就记录一下使用geopandas的方法。

以下用的数据存放在网盘中

[<font color=CornflowerBlue>百度网盘：j4d3</font>](https://pan.baidu.com/s/1ExMNF1-yv0OsVg8CH4fbxA)

---

## 代码示例

```python
import proplot as pplt
import xarray as xr
import pandas as pd
import numpy as np
data = xr.open_dataset('D:/data_english/era5/slp.sst.pre.1979-2020mon.global.nc')

# 海平面气压距平
slp = data['msl'][:,0,...].sel(latitude=slice(None,None,4), longitude=slice(None,None,4))
lon, lat = np.meshgrid(slp.longitude, slp.latitude)

gb = slp.groupby('time.month')
clim = gb.mean(dim="time")
slpa = gb - clim

# 随便取一年
slpa = slpa[0,...]
```

### 未白化的状况

只看中国周围吧

```python
fig, ax = pplt.subplots(proj='cyl',                        # 等经纬度投影
                        lonlim=(70, 140), latlim=(10, 60)) # 设置extent

kw = {'cmap':'RdBu',        # 设置cmap
      'extend':'both',      # 设置extend
      'symmetric':True}     # 保证 0 在 colorbar中间

fill = ax[0].contourf(lon, lat, slpa, **kw, vmin=-900) # 等值线填色

ax.format(labels=True,                 # 经纬度标签
          coast=True,                  # 海岸线
          gridlabelsize='xx-small')    # 经纬度标签字体大小

fig.colorbar(fill, label='',                 # 取掉colorbar的label
                   ticklabelsize='xx-small', # colorbar tick字体大小
                   width=0.1)                # colorbar宽度
```

<img title="" src="https://s1.ax1x.com/2023/03/30/pp2E7mF.png" alt="" data-align="center" width="473">

---

### geopandas 读取 shp

`下面利用bou2_4p.shp对中国区域进行白化。先看一下geopandas读取shp文件的结果。`

```python
import geopandas as gpd
from shapely.geometry import Point
from matplotlib.path import Path
from cartopy.mpl.patch import geos_to_path
import cartopy.crs as ccrs

shp = gpd.read_file('bou2_4p.shp',encoding='gbk')

shp
```

```
    AREA    PERIMETER    BOU2_4M_    BOU2_4M_ID    ADCODE93    ADCODE99    NAME    geometry
0    54.447    68.489    2    23    230000    230000    黑龙江省    POLYGON ((121.48844 53.33265, 121.49954 53.336...
1    129.113    129.933    3    15    150000    150000    内蒙古自治区    POLYGON ((121.48844 53.33265, 121.49738 53.321...
2    175.591    84.905    4    65    650000    650000    新疆维吾尔自治区    POLYGON ((96.38329 42.72696, 96.35991 42.70969...
3    21.315    41.186    5    22    220000    220000    吉林省    POLYGON ((123.17104 46.24668, 123.21857 46.269...
4    15.603    38.379    6    21    210000    210000    辽宁省    POLYGON ((123.69019 43.37677, 123.70496 43.381...
...    ...    ...    ...    ...    ...    ...    ...    ...
920    0.000    0.037    922    3110    810000    810000    香港特别行政区    POLYGON ((114.24527 22.18337, 114.24348 22.184...
921    0.000    0.018    923    3109    810000    810000    香港特别行政区    POLYGON ((114.28620 22.18478, 114.28435 22.185...
922    0.000    0.014    924    3112    810000    810000    香港特别行政区    POLYGON ((114.30350 22.18492, 114.30413 22.186...
923    0.000    0.079    925    3114    810000    810000    香港特别行政区    POLYGON ((114.25628 22.16027, 114.25436 22.163...
924    0.000    0.011    926    3115    810000    810000    香港特别行政区    POLYGON ((114.29893 22.17812, 114.30064 22.178...
```

---

### 关键白化操作

```python
china = shp['geometry'].tolist()

# 生成裁剪路径 – 关键操作1
path_clip = Path.make_compound_path(*geos_to_path(china))
# 将裁剪路径应用到图层 – 关键操作2
[collection.set_clip_path(path_clip, transform=ax.transData) for collection in fill.collections]
```

<img title="" src="https://s1.ax1x.com/2023/03/30/pp2ERFs.png" alt="" data-align="center" width="458">

<font size=5 color="blue"> 可直接添加图窗画区域边缘 </font>

```python
# 绘制多边形边缘线
# bou1_4l包括国界线和南海九段线
shp2 = gpd.read_file('bou1_4l.shp',encoding='gbk') 
ax.add_geometries(shp2['geometry'].tolist(), crs=ccrs.PlateCarree(), facecolor='none', edgecolor='black')
fig
```

<img title="" src="https://s1.ax1x.com/2023/03/30/pp2EbTJ.png" alt="" data-align="center" width="436">

<font size=5 color="blue"> 合并添加多个shp </font>

```python
# 也可添加多个shp
# bou2_4p包括国界和省界
shp = gpd.read_file('bou2_4p.shp',encoding='gbk') 
shp2 = gpd.read_file('bou1_4l.shp',encoding='gbk') 

com = shp2['geometry'].append(shp['geometry']) # 合并两个shp
# 或者 com = shp2['geometry'].tolist() + shp['geometry'].tolist()

ax.add_geometries(com, crs=ccrs.PlateCarree(), facecolor='none', edgecolor='black')
fig
```

<img title="" src="https://s1.ax1x.com/2023/03/30/pp2EvSx.png" alt="" data-align="center" width="434">

---

### 风矢量的白化

quiver生成的对象与contourf生成的对象不同，`它不包含collection属性`。所以白化操作略有不同。

```python
# 读取资料
data2 = xr.open_dataset('GH.UV.500_850hPa.1979-2020.nc')
u = data2['u'][:,0,0,...].sel(latitude=slice(60,10,4), longitude=slice(70,140,4))
v = data2['v'][:,0,0,...].sel(latitude=slice(60,10,4), longitude=slice(70,140,4))

# 取距平
gb = u.groupby('time.month')
clim = gb.mean(dim="time")
ua = gb - clim
ua = ua[0,...]

gb = v.groupby('time.month')
clim = gb.mean(dim="time")
va = gb - clim
va = va[0,...]

lon2, lat2 = np.meshgrid(u.longitude,v.latitude)
```

```python
d=1
tt = ax.quiver(lon2[::d,::d],lat2[::d,::d],ua[::d,::d],va[::d,::d])

# 剪切白化
tt.set_clip_path(path_clip, transform=ax.transData)
```

<img title="" src="https://s1.ax1x.com/2023/03/30/pp2VSOO.png" alt="" data-align="center" width="476">

{%label 对于quiver，数据范围最好保证在extent范围内。如果使用-180~180的数据，而extent只设定在70-120，那么画出来的矢量箭头会非常小，需要手动调整scale。一般来说需要进一步调整降低箭头密集度，并调整scale red%}

---

### contour 和 clabel的白化

`contour的白化方法与contourf白化方法相同。contour生成对象后，提取collection循环切片即可。`

```python
# 读入数据
import proplot as pplt
import xarray as xr
import pandas as pd
import numpy as np
import geopandas as gpd
from matplotlib.path import Path
from cartopy.mpl.patch import geos_to_path
import cartopy.crs as ccrs
from shapely.geometry import Polygon as ShapelyPolygon
from shapely.geometry import Point as ShapelyPoint

data = xr.open_dataset('D:/data_english/era5/slp.sst.pre.1979-2020mon.global.nc')

#%% 

slp = data['msl'][:,0,...].sel(latitude=slice(None,None,4), longitude=slice(None,None,4))
lon, lat = np.meshgrid(slp.longitude, slp.latitude)

gb = slp.groupby('time.month')
clim = gb.mean(dim="time")
slpa = gb - clim
slpa = slpa[0,...]
```

```python
# 创建等值线和labels
fig, ax = pplt.subplots(proj='cyl',lonlim=(70, 140), latlim=(10, 60))

kw = { 'cmap':'RdBu_r','extend':'both', 'symmetric':True}

fill = ax[0].contourf(lon, lat, slpa, **kw, vmin=-900,values=20)
con = ax[0].contour(lon, lat, slpa, levels=fill.levels,
                    color='black',linewidth=0.2)

cb = ax[0].clabel(con,levels=fill.levels)
ax.format(labels=True, coast=True, gridlabelsize='xx-small')

fig.colorbar(fill, label='', ticklabelsize='xx-small', width=0.1)
```

<img title="" src="https://s1.ax1x.com/2023/03/30/pp2VktA.png" alt="" data-align="center" width="380">

下面对`等值线白化`

```python
shp = gpd.read_file('D:/anaconda_spyder_filesave/mission/mission9/0619/shpfile/bou2_4p.shp',encoding='gbk')
ee = shp['geometry'].tolist()


# 生成裁剪路径 – 关键操作1
path_clip = Path.make_compound_path(*geos_to_path(ee))

# 将裁剪路径应用到图层 – 关键操作2

# 对填色图白化
[collection.set_clip_path(path_clip, transform=ax.transData) for collection in fill.collections]

# 对等值线白化
[collection.set_clip_path(path_clip, transform=ax.transData) for collection in con.collections]

fig
```

<img title="" src="https://s1.ax1x.com/2023/03/30/pp2VGpq.png" alt="" data-align="center" width="352">

可以看到labels还是到处乱飞，下面需要对labels白化。然而labels对象是Text组成的列表，操作过程以上等值线白化又有不同。

```python
# clabel白化
# cb = ax[0].clabel(con,levels=fill.levels)

for text_object in cb:
    if not path_clip.contains_point(text_object.get_position()):
        text_object.set_visible(False)  
fig
```

<img title="" src="https://s1.ax1x.com/2023/03/30/pp2VYcV.png" alt="" data-align="center" width="397">

`path_clip.contains_point` 判断点是否在路径所包围的区域内

---

### 非等经纬度投影白化

`以上白化操作ax的投影皆为ccrs.PlateCarree()`, `数据投影也为ccrs.PlateCarree()`。因此无论是画图还是白化都不需要额外的操作来转化点的坐标。

需要注意的是，在创建ax时，`projection参数是对ax进行投影设置`。即若projection=ccrs.PlateCarree()，则我们最后看到的图就是等经纬度投影的图。若projection=ccrs.LambertConformal()，则我们最后看到的图就是兰伯特投影的样子。

然而`在contourf的transform和ax.set_extent()中设置的crs的意义不同，它们要求我们告诉程序，为什么所输入的数据是取自怎样的投影`。一般来说，我们的数据都是格点数据，lon:-180~180, lat:-90~90。即我们的数据一般是等经纬度的，`所以transform和crs都设置为ccrs.PlateCarree()就可以了(不随projection的变化而变化)`。

详情可以看这里  [<font color=CornflowerBlue>transform和projection的意义</font>](https://scitools.org.uk/cartopy/docs/latest/tutorials/understanding_transform.html?highlight=transform)

此外，通常我们的shp文件提取出的点也是等经纬度的lon:-180~180, lat:-90~90。`而当projection=ccrs.LambertConformal()时就无法直接用以上程序直接进行白化`，因为坐标不对应。这个时候`需要先将路径Path转化到相应的projection上`。

注意即使我们的projection使用的是ccrs.PlateCarree()，但设置了中心经度例如projection=ccrs.PlateCarree(central_longitude=120)。也需要对路径点进行坐标转化。`路径点坐标系必须与 projection 完全一致`

```python
# 非等经纬度投影白化
path_clip = Path.make_compound_path(*geos_to_path(ee))

# 后面的操作会丢失codes信息，需要提前保存副本
codes = path_clip.codes

# 假设在创建ax时设置了兰伯特投影和中心经度、中心纬度
# fig, ax = pplt.subplots(proj='lcc',lonlim=(70, 140), 
#                       latlim=(10, 60),proj_kw={'lon_0':100,'lat_0':30})

# 必须与projection一致
pp = ccrs.LambertConformal(central_longitude=100, central_latitude=30)

# 这一步将处于ccrs.PlateCarree()里的路径点转化到 pp 投影上
path_clip = Path(pp.transform_points(ccrs.PlateCarree(),path_clip.vertices[:,0], path_clip.vertices[:,1])[:,0:2],codes=codes)
```

{% note success simple %}

codes似乎标记了多边形个体，每个多边形用有一个数字存在codes中。如果不添加codes参数，例如大陆和海南岛之间会有路径穿过。

摸鱼咯大佬的帖子中使用的是ccrs.Geodetic()而不是ccrs.PlateCarree()来转化路径点，我不清楚有什么区别。我觉得ccrs.PlateCarree()更合理一些。
{% endnote %}

由此，我们得到了一个`新的path_clip`，后面的白化过程就与之前的内容完全一致了。如果我们不是用等经纬度投影创建坐标轴，就`需要将路径点的坐标转化到相应的projection上`。

---

### 南海小图

有时候在画中国地图时需要对地图右下角添加一个小图来显示南海地区。这个小图可以和主图完全相同，只需要调整`extent`即可。然而，在白化之后会出现如下图的情况。

<img src="https://s1.ax1x.com/2023/03/30/pp2VaBF.png" title="" alt="" data-align="center">

小图范围内虽然白化成功，但是小图之外的图像并没有去除掉。原因在于`ax.set_extent()`和`collection.set_clip()`这两个命令相互覆盖了。导致只有一个命令生效。解决的方法就是找到`extent`与`path_clip`的交集。思路来源于：[<font color=CornflowerBlue>链接</font>](https://mp.weixin.qq.com/s?__biz=Mzg4NzY4MzgxNw==&mid=2247488767&idx=1&sn=5df006905b3e16d7cc4a100988393b03&chksm=cf87fb79f8f0726f51ce8bb5c6bde9f8bcf5535bb4ca8db502083c0f9cee26c1a0e90d23bf90&mpshare=1&scene=23&srcid=06234bAPPyrWvy7gJ1FgEOLf&sharer_sharetime=1661769196302&sharer_shareid=327e1b5af213919a0371744eb74c4650#rd) 。我对其代码进行了精简。

```python
from shapely import geometry as geo
from cartopy.mpl.patch import geos_to_path,path_to_geos

# proplot添加内嵌坐标轴
iax = ax.inset([140-11*0.8,10,11*0.8,24*0.8],transform='data')

# 填色图
fill2 = iax.contourf(lon, lat, o3, extend='both', robust=True)
iax.add_geometries(shp['geometry'], crs=ccrs.PlateCarree(), facecolor='None', )
iax.add_geometries(shp2['geometry'], crs=ccrs.PlateCarree(), facecolor='None', )

iax.format(lonlim=(109,120), latlim=(0,24))

extent = [109,120,0,24]
extentPolygon = geo.Polygon([
    (extent[0], extent[2]),
    (extent[0], extent[3]),
    (extent[1], extent[3]),
    (extent[1], extent[2]),
    (extent[0], extent[2]),
])

# 关键步骤*************
polygon_clip = []
for p in path_to_geos(path_clip): # 将 path 转 polygon
    polygon_clip.append(extentPolygon.intersection(p)) # 将交集填入列表

# 重新将交集 polygon 转为 path
path_clip2 = Path.make_compound_path(*geos_to_path(polygon_clip))
[collection.set_clip_path(path_clip2, transform=iax.transData) for collection in fill2.collections]
```

<img src="https://s1.ax1x.com/2023/03/30/pp2Vd74.png" title="" alt="" data-align="center">

---

## 总结

写了这么多，再回去看看觉得好乱。那就简单做个总结吧。

`文件读取`

```python
import geopandas as gpd

shp = gpd.read_file('./shpfile/china.shp')
china = shp['geometry'].tolist()
```

`剪切路径`

```python
from matplotlib.path import Path
from cartopy.mpl.patch import geos_to_path
import cartopy.crs as ccrs

path_clip = Path.make_compound_path(*geos_to_path(china))


# 如果 ax 不是等经纬度投影需要加上以下代码，以兰伯特投影为例
codes = path_clip.codes
pp = ccrs.LambertConformal(central_longitude=100, central_latitude=30)
path_clip = Path(pp.transform_points(ccrs.PlateCarree(),path_clip.vertices[:,0], path_clip.vertices[:,1])[:,0:2],codes=codes)
```

`等值线和填色图白化`

```python
# fill：填色图对象
# con：等值线对象
[collection.set_clip_path(path_clip, transform=ax.transData) for collection in fill.collections]
[collection.set_clip_path(path_clip, transform=ax.transData) for collection in con.collections]
```

`风矢量白化`

```python
# tt：quiver对象
tt.set_clip_path(path_clip, transform=ax.transData)
```

`clabel 白化`

```python
# cb：clabel对象
for text_object in cb:
    if not path_clip.contains_point(text_object.get_position()):
        text_object.set_visible(False) 
```

`polygon取交集白化`

```python
# extentPolygon 与 path_clip 取交集
polygon_clip = []
for p in path_to_geos(path_clip): # 将 path 转 polygon
    polygon_clip.append(extentPolygon.intersection(p)) # 将交集填入列表

# 重新将交集 polygon 转为 path
path_clip2 = Path.make_compound_path(*geos_to_path(polygon_clip))
[collection.set_clip_path(path_clip2, transform=iax.transData) for collection in fill2.collections]
```
