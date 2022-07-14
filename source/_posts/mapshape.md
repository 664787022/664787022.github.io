---
title: 地图文件使用技巧
date: 2022-07-08 22:14:11
tags: geopandas
category: 编程 tips
cover: /img/cover6.jpg
---

## 前言

记录一下使用地图文件的小技巧吧



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
