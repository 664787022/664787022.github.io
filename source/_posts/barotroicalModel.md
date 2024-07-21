---
title: barotroicalModel
date: 2024-06-09 14:43:02
tags:
---

## 前言

最近想试着用Fortran写一个正压原始方程的预报程序。在这过程中会遇到很多问题，例如fortran编译，程序编写等。这个博文就用来做记录了。

## 随笔

- ifort和gfortran

在用gfortran编译时遇到一下问题：

f951: Fatal Error: Reading module ‘/public/home/elzd_2024_000125/libs/netcdf/intel/4.7.4/include/netcdf.mod’ at line 1 column 2: Unexpected EOF compilation terminated.

原因是我在程序里用了 `use netcdf` 而我使用的netcdf是ifort编译的，因此在编译fortran程序是也得用ifort



- 编译顺序
  
  不同例如在main.f90里 `use` 了 constant.f90在编译时不能写为 `ifort main.f90 constant.f90 -o main` 。因为应该把constant.f90写在main.f90之前。或者

```shell
ifort  -c main.f90
ifort  -c constant.f90
ifort  main.o constant.o -o main


```
