---
title: 我的第一篇文章！！！O(∩_∩)O哈哈~
categories: 碎碎念
tags: 测试
cover: /img/cover2.png
date: 2022-05-19
updated: 2022-05-22 

---

# 第一篇文章！！！

这是第一篇文章，测试一下效果

本博客计划写一些<font color=blue>**气象**</font>方面的学习经验。如<font color=blue>***气象编程、学习笔记、文献回顾总结***</font>。

另外还有<font color=green>**英语学习**。*如口语句式、学术论文写作笔记*</font>。

最后可能有一些<font color=red>**日记性质的文章**</font>，记录自己五年读博生涯。

下面测试一下<mark style="background-color：yellow">markdown</mark>

### 1. 首先是代码块

```python
#%% 去趋势1979-2020,春、秋季位势高度
temp = data2.sel(time=slice('1979','2020'))
hgt500Spring1979_2020Detrend = temp.sel(time=temp['time.season']=='MAM').mean('time')
hgt500Autumn1979_2020Detrend = temp.sel(time=temp['time.season']=='SON').mean('time')
```

### 2. 然后是图片

 ![惠](https://s1.ax1x.com/2023/03/30/pp2EaFA.jpg#pic_center)

### 3. 试一下公式

$y={x^2}$
$y = {x^2} + 2x - { {\rm{T} }_0} + {\mu ^4}\sqrt { { {\rm{v} }^2} + {b^2} }$

update test哈哈