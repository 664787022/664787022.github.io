---
title: 自定义Python函数
date: 2023-07-22 10:50:43
tags: 编程
category: 编程
cover: /img/cover14.jpg
---

[TOC]

## 前言

存储一下自己定义的常用函数。



## 标准化

```python
def getnorm(array):
    array = (array - array.mean())/array.std()
    return array
```



## 提取冬季

```python
def getDJF(DataArray):
  mat_w = DataArray.resample(time='QS-DEC').mean()
  mat_w = mat_w.sel(time=mat_w['time.month'] == 12)
  return mat_w
```



## 线性回归

```python
from sklearn.feature_selection import f_regression
def getReg(mat, sequence):
    A = np.vstack((sequence, np.ones((1, sequence.shape[0])))).T
    (a, b, c) = mat.shape
    mat_rshp = mat.copy().values.reshape((a, b*c))
    index = np.isnan(mat_rshp).any(axis=0)
    mat_rshp[:, index] = -999
    mat_rshp_reg = np.linalg.lstsq(A, mat_rshp)[0][0]
    mat_rshp_reg[index] = np.nan
    mat_reg = mat_rshp_reg.reshape((b, c))
    pvalue = f_regression(mat_rshp, sequence)[1].reshape(b, c)
    return mat_reg, pvalue
```



## 去趋势

```python
from scipy.signal import detrend
def getDetrend(array):
    index = np.isnan(array.values).any(axis=0)
    array.values[:, index] = -999
    array_detrend = detrend(array.values, axis=0)
    array_detrend[:, index] = np.nan
    return array.copy(data=array_detrend)

```



##  滑动平均

```python
def PointSmo(array, num=9, add=False):
    start = int((num-1)/2)
    end = array.shape[0] - int((num-1)/2)
    result = np.zeros_like(array) * np.nan
    for i in range(start, end):
        result[i] = array[i-int((num-1)/2):i+int((num-1)/2)+1].mean()
    if add:
        result = np.where(np.isnan(result), sequence, result)
    return result
```



## 计算相关

```python
from scipy.stats import pearsonr, linregress
def getCor(mat, sequence):
    cor = np.zeros(mat.shape[1:])
    pvalue = np.zeros(mat.shape[1:])
    for i in range(mat.shape[1]):
        for j in range(mat.shape[2]):
            cor[i,j], pvalue[i,j] = pearsonr(mat[:,i,j].values, sequence.values)
    return cor, pvalue
```



## Bootstrap合成检验

```python
def getBootstrap(mat1, mat2, comValue):
    comSize1 = mat1.shape[0]
    comSize2 = mat2.shape[0]
    N = 1000
    Mean1 = np.zeros((N, mat1.shape[1], mat1.shape[2]))
    Mean2 = np.zeros((N, mat2.shape[1], mat2.shape[2]))
    p = np.ones(mat1.shape[1:])

    for k in range(N):
        seed = np.random.randint(0, mat1.shape[0] , size=mat1.shape[0])
        sample = np.random.choice(seed, size=comSize1, replace=True)
        Mean1[k,...] = mat1[sample,...].mean(axis=0)
    for k in range(N):
        seed = np.random.randint(0, mat2.shape[0] , size=mat2.shape[0])
        sample = np.random.choice(seed, size=comSize2, replace=True)
        Mean2[k,...] = mat2[sample,...].mean(axis=0)
    Mean = Mean2 - Mean1
    p[np.where((comValue<np.percentile(Mean,2.5,axis=0)) | (comValue>np.percentile(Mean,97.5,axis=0)))] = 0.01
        
    return p
```



## 计算科氏参数

```python
from metpy.constants import earth_avg_angular_vel
def getCorio(latmat):
    _f = 2 * earth_avg_angular_vel.magnitude * np.sin(np.deg2rad(latmat))
    return _f
```



## Proplot投影

```python
import proplot as pplt
fig, ax = pplt.subplots(proj='cyl') # npaeqd 北极投影
ax.contourf(lon, lat, mat, colorbar=True)
ax.format(coast=True, labels=True)
```



## 画矩形

```python
from matplotlib.patches import PathPatch
from matplotlib.path import Path

def getRect(points, color='blue',lw=1, flag=True, path=False):
    # [75,90,50,60] # 经度，纬度
    if flag:
        rec = np.array([[points[0], points[3]], [points[0], points[2]], 
                        [points[1], points[2]], [points[1], points[3]], [points[0], points[3]]])
    else:
        rec = points
    pa = Path(rec)
    pathcopy = pa.copy()
    pa = pa.interpolated(100)
    patch = PathPatch(pa, facecolor='None', edgecolor=color,
            transform=ccrs.PlateCarree(), lw=lw)
    if path:
        return pathcopy
    else:
        return patch
    
ax[i].add_patch(getRect([-180,-120,5,25])) # 矩形
ax[i].add_patch(getRect(np.array([[150,0],[210,0],[240,10],[240,40],[150,0]]), flag=False)) # 非矩形用，如平行四边形
```



## 特定年份范围数据路径

```python
# 函数保留1979-2022年数据
import glob
def getDataPath(_path):
    pathFilter = glob.glob(_path)
    index = ((pd.Series(pathFilter).str[-7:-3].astype(int)>=1979)&(pd.Series(pathFilter).str[-7:-3].astype(int)<=2022)).to_list()
    pathFilter = np.array(pathFilter)[index].tolist()
    return pathFilter
```

