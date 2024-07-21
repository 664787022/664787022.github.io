---
title: LBM 安装-运行-修改-debug
date: 2023-12-29 09:42:13
tags: 
    - Linux
    - 软件
category: 经验总结
cover: /img/cover18.png
---

[TOC]





## 前言

LBM（linear baroclinic model）[LBM main (u-tokyo.ac.jp)](https://ccsr.aori.u-tokyo.ac.jp/~lbm/sub/lbm.html)是日本人开发的线性斜压模式。它运行快，资源占用少，易上手。给定背景场和强迫场，可以得到大气的定常响应。利用LBM可以快速验证自己的猜测和结论。

这几天安装、运行、调试了LBM，大致摸清了整个流程。其中有许多坑点，但都被解决了，下文将记录安装运行流程和坑点。

## 安装

首先需要向LBM的管理人员索要账号和密码以下载LBM，他的邮箱是 hayashi.michiya@nies.go.jp

我的账号密码记录在所邮箱中。

接着安装LBM的流程基本是跟着洪海旭师兄在CDSN上的博文来的[LBM模式学习·保姆级安装及初步使用教程_lbm保姆-CSDN博客](https://blog.csdn.net/weixin_42762673/article/details/124043455) 以及 [线性斜压模式LBM学习&安装实录 - chinagod - 博客园 (cnblogs.com)](https://www.cnblogs.com/jiangleads/p/11893290.html) 

两篇博文分别使用的是ICC和GCC编译模式，我只使用了GCC。第一篇博文提到`sysdep_linux20201125.tar.gz` 文件，也是从LBM官网上下载。

以下是文件结构

[![piLQsOK.md.jpg](https://s11.ax1x.com/2023/12/29/piLQsOK.md.jpg)](https://imgse.com/i/piLQsOK)

## 运行

### 1. 分辨率设置

位置：$LNHOME/Lmake.inc

参见洪海旭博文

### 2. 生成可执行文件

位置: $LNHOME/model/src
``` linux
make clean
make lib lbm
```

结果应在 $LNHOME/model/bin/linux 下生成一个 lbm2.t21ml20ctintgr (数字表示分辨率，随分辨率选择而改变)

### 3. 编译大气基本态

位置: $LNHOME/solver/util
``` linux
$ make bs
```

位置: $LNHOME/solver/util/SETPAR
``` bash
&nmcp cncep='大气基本态.t21.grd',
	  cncep2='大气基本态.ps.t21.grd', # 地面气压
	  calt= 'disk1/xhw/LBM/ln_solver/bs/gt3/grz/t21',
	  kmo=起始月份, navg=3三月平均, ozm=f是否纬向平均, osw=f是否纬向对称, ousez=t是否转化为sigma坐标系
```

如果用EC模块，则改
``` bash
&nmecm cecm='大气基本态.t21.grd',
	  calt= 'disk1/xhw/LBM/ln_solver/bs/gt3/grz/t21',
	  kmo=起始月份, navg=3三月平均, ozm=f是否纬向平均, osw=f是否纬向对称, ousez=t是否转化为sigma坐标系
```

修改基本态文件输出位置
``` bash
 &nmbs  cbs0='/disk1/xhw/LBM/ln_solver/bs/gt3/ncepsum.t21l20',

        cbs='/disk1/xhw/LBM/ln_solver/bs/grads/ncepsum.t21l20.grd'
```

生成大气基本态
``` linux
$ ./ncepsbs  # 调用NCEP模块

# 或者

$ ./ecmsbs  # 调用EC模块
```

### 4. 编译大气强迫场

位置: $LNHOME/solver/util/SETPAR

预先在 $LNHOME/data/ 下创建好 `frc` 文件夹和 `out` 文件夹用来存放强迫场和输出文件，文件夹名称可以根据case的内容自定义

修改强迫场输出位置
``` bash
 &nmfin cfm='/disk1/xhw/LBM/ln_solver/data/frc/frc.t21l20.classic.mat', # 用不到可以不改

        cfg='/disk1/xhw/LBM/ln_solver/data/frc/frc.t21l20.classic.grd' # 强迫文件的输出位置，如果自己建立强迫场，不要把自建强迫场放在这

        fact=1.0,1.0,1.0,1.0,1.0
```

修改强迫方式
``` bash
&nmvar ovor=f, odiv=f, otmp=t, ops=f, osph=f
 
# 涡度强迫关闭，散度强迫关闭，温度强迫打开，地表气压强迫关闭，湿度强迫关闭
```

强迫位置、形状

``` bash
 &nmhpr khpr=1,  # khpr=1/2代表椭圆/水平均匀的强迫

        hamp=1.,  # 振幅(单位是1/day)

        xdil=40.,  # xdil是纬向范围(就是多少个格点衰减到0)

        ydil=12., # ydil是经向范围

        xcnt=210., # xcnt是强迫的中心经度
 
        ycnt=0.  # ycnt是强迫的中心纬度

 &end
```

强迫廓线
``` bash
 &nmvpr kvpr=2, # kvpr是垂直廓线的函数(1.是正弦函数，2是gamma函数，3是上下均匀的)

        vamp=8, # 垂直廓线的振幅

        vdil=20., # 膨胀系数(仅在垂直廓线函数设置为gamma函数的时候才生效

        vcnt=0.45 # vcnt是垂直方向上强迫最大值所在的层次

 &end
```

所有参数的意思都可以查阅：$LNHOME/solver/util/param_list

编译并输出强迫场
位置: $LNHOME/solver/util
``` linux
$ make clean
$ make
$ ./mkfrcng
```

### 5. 结合强迫场和基本态并运行模式

位置: $LNHOME/model/sh/tintgr
找一个 `.csh` 文件作为修改模板，可以选择 `linear-run.classic.copy.csh` ，修改以下内容
``` bash
setenv FDIR     $LNHOME/data/frc                 # 强迫场所在位置
setenv DIR      $LNHOME/data/out                 # 模式输出位置

setenv BSFILE   $LNHOME/bs/gt3/ncepsum.t21l20    # 基本态位置


setenv FRC      $FDIR/frc.t21l20.classic.grd      # 用于强迫场随时间改变的情况，如果设置了SFRC
												  # 这一项不生效
setenv SFRC     $FDIR/frc.t21l20.classic.grd      # 稳定强迫场的文件名，
												  # 是之前我们./mkfrcng生成的强迫场。 如果自建强迫场，把自建强迫场路径放在这

setenv TEND     59 # 模式积分的时长，根据摸鱼咯的博客的说明可知，tend=51天的时候，模式运行20天，tend=59的时候模式运行27天，这里设置了tend=59，使其运行27天。


&nmtime start=0,1,1,0,0,0, end=0,1,$TEND,0,0,0             &end # 这一项作用未知，注意0,1

```

运行模式
``` linux
csh linear-run.classic.copy.csh
```

### 6. 简短运行流程

```bash
# 1. 编译模式
cd $LNHOME/model/src
make clean
make lib

# 2. 准备背景场（如果改背景场了，就必须从这步开始）
# 编辑SETPAR
cd $LNHOME/solver/util
make clean
make bs
./ncepsbs

# 3. 编译模式
cd $LNHOME/model/src
make clean.special
make lbm

# 4. 准备强迫场 (如果不改背景场，只做4和5就行)
# 编辑SETPAR
cd $LNHOME/solver/util
make clean
make
./mkfrcng

# 5. 运行模式
cd $LNHOME/model/sh/tintgr
csh linear-run.classic.copy3.csh


# 6. 用 gt2gr 输出合并的grd
cd $LNHOME/solver/util
./gt2gr
cd $LNHOME/data/out_indianOcean
cdo -f nc import_binary combinedt42.ctl combined.nc


# 7 强迫场转nc
cd $LNHOME/data/frc_indianOcean
cdo -f nc import_binary frc.t42l20.classic.ctl frc.t42l20.classic.nc

```

## 运行Debug

如果出现如下错误,  是 `/disk1/xhw/LBM/ln_solver/model/src/sysdep/Makedef.linux` 和 `/disk1/xhw/LBM/ln_solver/model/src/sysdep/Makedef.linux`没有设置好。

```
# 不应该是 -convert big_endian , 这种写法是icc的写法。我用的是gcc，应该在Makedef.linux 中改成 -fconvert=bing-endian

gfortran -O2 -u -mcmodel=medium -shared-intel -convert big_endian -no-vec    -I/disk1/xhw/LBM/ln_solver/model/src/include  -DSYS_AVATAR -DSYS_UNIX -DCODE_ASCII -DCODE_IEEE -DOPT_NOPHYSICS -DOPT_NOUSER -DOPT_CLASSIC -I/disk1/xhw/LBM/ln_solver/model/src/include   -c -o pmisc.o pmisc.F
gfortran: error: big_endian: No such file or directory
gfortran: error: unrecognized command line option ‘-shared-intel’
gfortran: error: unrecognized command line option ‘-convert’
gfortran: error: unrecognized command line option ‘-no-vec’
```

或

```
# 这个错误是啥原因忘记了
gfortran -O2 -u -mcmodel=medium -fconvert=big-endian    -I/disk1/xhw/LBM/ln_solver/model/src/include  -DSYS_AVATAR -DSYS_UNIX -DCODE_ASCII -DCODE_IEEE -DOPT_NOPHYSICS -DOPT_NOUSER -DOPT_CLASSIC -I/disk1/xhw/LBM/ln_solver/model/src/include   -c -o atmmain.o atmmain.F
gfortran -O2 -u  atmmain.o		 astrt-2.o aadmn-2.o dadmn-2.o dterm-2.o dgdyn-2.o dstep-2.o dintg-2.o dsetd-2.o dbulk.o          /disk1/xhw/LBM/ln_solver/model/lib/linux/liblbm2t21ml20c.a   -o /disk1/xhw/LBM/ln_solver/model/bin/linux/lbm2.t21ml20ctintgr
/usr/lib/gcc/x86_64-redhat-linux/4.8.5/../../../../lib64/crt1.o: In function `_start':
(.text+0x20): undefined reference to `main'
collect2: error: ld returned 1 exit status

```

这里再贴一下 `/disk1/xhw/LBM/ln_solver/model/src/sysdep/Makedef.linux` 和 `/disk1/xhw/LBM/ln_solver/solver/include/make.inc.linux`

```bash
# /disk1/xhw/LBM/ln_solver/model/src/sysdep/Makedef.linux
#
#   Linux system dependent include for Makefile
# 

#SYSFFLAGS	= -O -u
#SYSFFLAGS       = -O2 -u -mcmodel=medium -shared-intel -convert big_endian -no-vec
SYSFFLAGS	= -O2 -u -mcmodel=medium -fconvert=big-endian
#SYSCFLAGS	= 
#SYSCFLAGS       = -DX_WCHAR -shared -mcmodel=medium
SYSCFLAGS	= -DX_WCHAR
#SYSLDFLAGS      = -O2 -u
SYSLDFLAGS	= 
#SYSCPPFLAGS     = -DSYS_AVATAR -DSYS_UNIX -DCODE_ASCII -DCODE_IEEE
SYSCPPFLAGS 	= -DSYS_Linux -DSYS_UNIX -DCODE_ASCII -DCODE_IEEE #-DCODE_ENDIAN
SYSAUTODBL	= -r8
SYSDEBUG	= -g
SYSCHECK	= -C
LINKOPT		=
SYSLIBINC       = yy$(SYSTEM).o
#SYSLIB          = -lc

# MAKE		= make
CC		= gcc
#FC		= g77
#LD		= g77
#FC		= f77
#LD		= f77
FC		= gfortran
LD		= gfortran
#FC		= gfortran
#LD		= gfortran
AR		= ar vru
RM		= rm -f
CP		= cp
MV		= mv -f
LN		= ln -s
RANLIB		= ranlib
CAT		= cat
INSTALL		= cp
MD		= mkdirhier
JLATEX		= bigjlatex
DVI2JPS		= dvi2ps
PRINT		= ltype
PRINTSTAMP	= .print
INDEX		= etags -wx
TAGS		= etags
TOUCH		= touch
ECHO		= echo
CPP		= cpp
FPP     	= 

SYSXLIBDIR	= /usr/X11R6/lib
SYSXLIBNAME	= X11
SYSXLIBS	= -L$(SYSXLIBDIR) -l$(SYSXLIBNAME)
###SYSXLIBS	= -l$(SYSXLIBNAME)

PACKFILE        = Linux.ftr
PACKDIR		= $(SRCDIR)/Linux

world:	all

.SUFFIXES : .pac .F

$(PACKFILE):

.F.pac:
	echo "*/ADD NAME="$*.F >> $(PACKFILE)
	cat $< >> $(PACKFILE)


```

```
# /disk1/xhw/LBM/ln_solver/solver/include/make.inc.linux

####################################################################
#  LAPACK make include file.                                       #
#  LAPACK, Version 2.0                                             #
#  September 30, 1994                                                 #
####################################################################
#
#  The machine (platform) identifier to append to the library names
#
PLAT = LINUX
#  
#  Modify the FORTRAN and OPTS definitions to refer to the
#  compiler and desired compiler options for your machine.  NOOPT
#  refers to the compiler options desired when NO OPTIMIZATION is
#  selected.  Define LOADER and LOADOPTS to refer to the loader and 
#  desired load options for your machine.
#
FORTRAN  = gfortran
OPTS     = -O2 -fconvert=big-endian -mcmodel=medium 
#-fallow-argument-mismatch
NOOPT    = -O0 -fconvert=big-endian -mcmodel=medium
LOADER   = gfortran
LOADOPTS = -fconvert=big-endian 
#-fallow-argument-mismatch
#FORTRAN  = ifort -lgfortran
#OPTS     = -O -u -convert big_endian -mcmodel=medium -fpe0 -traceback -g -check all
#NOOPT    = -u -convert big_endian  -mcmodel=medium -fpe3 -traceback -g -check all
#LOADER   = ifort -lgfortran
#LOADOPTS = -convert big_endian -mcmodel=medium -fpe3 -traceback -g -check all
#
#  The archiver and the flag(s) to use when building archive (library)
#  If you system has no ranlib, set RANLIB = echo.
#
ARCH     = ar
ARCHFLAGS= cr
RANLIB   = ranlib
#
RM       = rm -f
CP	 = cp -f
MV	 = mv -f
#
#  The location of the libraries to which you will link.  (The 
#  machine-specific, optimized BLAS library should be used whenever
#  possible.)
#
BLASLIB      = /disk1/xhw/LBM/lapack-3.9.0/librefblas.a
LAPACKLIB    = /disk1/xhw/LBM/lapack-3.9.0/liblapack.a
TMGLIB       = /disk1/xhw/LBM/lapack-3.9.0/libtmglib.a
EIGSRCLIB    = 
#
#  LBM library
#
LDLIBS       = $(LNHOME)/model/lib/$(ARC)/liblbm2$(HRES)m$(VRES)c.a
#
# byte unit
#
MBYT	= 1
#MBYT	= 4
```

## 自制强迫场

LBM支持自动生成椭圆等形状的强迫场，包括温度、涡度、散度、气压强迫。然而当我们想要加多个强迫场，比如一个热源，一个冷源就比较麻烦了。但是我们可以自己根据LBM强迫场的格式，生成对应的文件，替换掉LBM自建的强迫场文件。这样可以随心所欲地加入强迫场的强度、形状，而且更贴近观测。

LBM强迫场是由 `.grd` 和 `.ctl` 给出的。我们需要做的是，读出 `.grd` ，查看内部变量内容，分辨率等要素。然后做出自己期望的强迫场，替换掉`.grd`。具体步骤如下

1. 用 `cdo` 将LBM自建强迫场转为 nc 文件方便读取查看。`cdo -f nc import_binary frc.t42l20.classic.ctl frc.t42l20.classic.nc` 

2. python 读取 `frc.t42l20.classic.nc` 查看其内容。以设定温度强迫为例。改变nc文件中的 `t` 变量。

3. 将新的强迫场输出为新的 nc 文件`newFrc.nc` 。变量t, d ,v 都是多高度层的，而变量p是地面气压是单高度层的，由于后续需要用 `Grads` 读取，而 `Grads` 无法直接用 `sdfopen` 同时读取多个高度维数据集，需要分两个文件读取。所以需要先输出一个 `newFrc.nc` 变量包括t,d,v。再另输出一个 `newFrc_p.nc` 变量包括p。如果使用 `xarray.Dataset.to_netcdf()` 输出nc文件。需添加 `format='NETCDF3_CLASSIC'`

   `forcing['p'].to_netcdf('/disk1/xhw/LBM/ln_solver/data/frc_indianOcean/newFrc_p.nc',format='NETCDF3_CLASSIC')`

​		原因在于如果直接 `to_netcdf` 输出的是netcdf4，是 `little_endian` 小字节序的。而LBM全程使用的是 `big_endian` 大字节序的，会造成不匹配。添加 `format='NETCDF3_CLASSIC'` 后，python会以netcdf3输出nc文件，这个格式是 `little_endian` 的。



> *注意：LBM 自带的`.ctl` 的时间填的是 `TDEF 1 LINEAR 15jan0000 1mo` 这在转为nc文件并读取后时间会显示为
>
> `array([cftime.DatetimeGregorian(-1, 1, 15, 0, 0, 0, 0, has_year_zero=False)],dtype=object)`
>
> 这在后续的处理中可能引起不便，因此可以将 强迫场`.ctl` 中的时间改为 `TDEF 1 LINEAR 15jan2000 1mo` 或在python输出nc文件之前将时间替换`forcing['time'] = np.array([np.datetime64('2000-01-15')])` 



4. 得到 `newFrc.nc` 和 `newFrc_p.nc` 后，使用 `Grads` 读取, 我用的是opengrads气象家园整合版。（由于ip原因，我在服务器上没有用grads，文件是传到本地用grads处理的，原因见[ncview安装和踩坑 | XHW's Blog (664787022.github.io)](https://664787022.github.io/2023/11/19/ncview/)）

   ```gs
   'reinit'
   'sdfopen d:/user/pycode/LBM/makeFrc/newFrc.nc'
   'sdfopen d:/user/pycode/LBM/makeFrc/newFrc_p.nc'
   
   
   'set gxout fwrite'
   * 输出参数sq顺序输出，cl覆写，be大字节序输出，可在谷歌查到
   'set fwrite -sq -cl -be d:/user/pycode/LBM/makeFrc/newFrc.grd' 
   'set lon 0 357.1875'
   'set lat -87.864 87.864'
   
   * 循环写入顺序： 高度->变量->时间
   i=1
   while(i<=1)
       'set t 'i''
       
       'set dfile 1'
       j=1
       while(j<=20)
           'set z 'j''
           'd v'
           j=j+1
       endwhile
       
       j=1
       while(j<=20)
           'set z 'j''
           'd d'
           j=j+1
       endwhile
       
       j=1
       while(j<=20)
           'set z 'j''
           'd t'
           j=j+1
       endwhile
       
       'set dfile 2'
       j=1
       while(j<=1)
           'set z 'j''
           'd p'
           j=j+1
       endwhile  
     
       
       i=i+1
   endwhile
   
   'disable fwrite'
   ```

   > *注意：在写入之前应该先使用 `q ctlinfo` 看出 `Grads` 读取后数据的排列顺序（例如纬度是由北到南还是由南到北，高度是由小到大还是有大到小）。一般来说，不过当时python 输出的顺序是怎样的，`Grads` 读取后纬度是-90~90，高度是0~1（sigma坐标系）。这时写入 `newFrc.grd` 后顺序也是这样的。但是LBM给的 强迫场 `.ctl`示例文件是的纬度是-90~90，高度是1~0，且设置了`OPTIONS SEQUENTIAL YREV` 。 本来`.ctl` 与 grads输出的`.grd` 的纬度都是-90~90，是相匹配的。但是设置 `YREV`  （y轴reverse）意味着LBM读取 grads输出的 `.grd` 会以 90~-90的方式读入，这就反了。而真正需要 `reverse` 的是z轴。 所以需要更改 `.ctl` 里的option为 `OPTIONS SEQUENTIAL ZREV`。 当然直接更改XDEF、YDEF、ZDEF以匹配输出的 `.grd` 也可以。下面给出一个示例 `.ctl`

   ```gs
   * sample forcing pattern
   DSET ^newFrc.grd
   * BYTESWAPPED
   OPTIONS SEQUENTIAL ZREV
   TITLE dumy
   UNDEF -999.
   OPTIONS big_endian
   XDEF 128 LINEAR 0. 2.81250
   YDEF 64  LEVELS 
   -87.864 -85.097 -82.313 -79.526 -76.737 -73.948 -71.158 -68.368 -65.578 
   -62.787 -59.997 -57.207 -54.416 -51.626 -48.835 -46.045 -43.254 -40.464 
   -37.673 -34.883 -32.092 -29.301 -26.511 -23.720 -20.930 -18.139 -15.348 
   -12.558  -9.767  -6.976  -4.186  -1.395   1.395   4.186  6.976   9.767  
   12.558  15.348  18.139  20.930  23.720  26.511  29.301 32.092  34.883  
   37.673  40.464  43.254  46.045  48.835  51.626  54.416  57.207  59.997  
   62.787  65.578  68.368  71.158  73.948  76.737  79.526  82.313  85.097  
   87.864 
   ZDEF 20 LEVELS 0.99500 0.97999 0.94995 0.89988 0.82977 0.74468 
   0.64954 0.54946 0.45447 0.36948 0.29450 0.22953 0.17457 0.12440 
   0.0846830 0.0598005 0.0449337 0.0349146 0.0248800 0.00829901
   TDEF 1 LINEAR 15jan2000 1mo
   VARS 4
   v      20 99 vor.   forcing [s**-2]
   d      20 99 div.   forcing [s**-2]
   t      20 99 temp.  forcing [K s**-1]
   p      1  99 sfc.Ln(Ps) forcing
   ENDVARS
   ```

   5. 将生成了 `newFrc.grd` 和对应 `newFrc.ctl` （需同名）放入 `/disk1/xhw/LBM/ln_solver/data/frc_indianOcean` (自建)。修改 `/disk1/xhw/LBM/ln_solver/model/sh/tintgr` 里的 `linear-run.classic.copy3.csh` （根据需要调整）。将 FRC 和 SFRC改为自建强迫场路径

      ```
      setenv FRC      $FDIR/newFrc.grd               # initial perturbation
      setenv SFRC     $FDIR/newFrc.grd               # steady forcing
      ```

      完整文件如下

      ```bash
      ###
       # @Author: xhw
       # @Date: 2023-12-10 22:32:50
       # @LastEditTime: 2023-12-11 16:18:39
       # @FilePath: /xhw/LBM/ln_solver/model/sh/tintgr/linear-run.classic.copy3.csh
       # @Description: 
      ### 
      #!/bin/csh -f
      #
      #      sample script for linear model run (dry model)
      #
      # NQS command for mail
      #@$-q   b
      #@$-N   1
      #@$-me
      #
      setenv LNHOME   /disk1/xhw/LBM/ln_solver                 # ROOT of model
      setenv LBMDIR   $LNHOME/model                          # ROOT of LBM 
      setenv SYSTEM   linux                                 # execute system
      setenv RUN      $LBMDIR/bin/$SYSTEM/lbm2.t42ml20ctintgr # Excutable file
      setenv TDIR     $LNHOME/solver/util
      #setenv FDIR     $LNHOME/data                           # Directory for Output
      setenv FDIR     $LNHOME/data/frc_indianOcean                 # Directory for Output
      setenv DIR      $LNHOME/data/out_indianOcean                       # Directory for Output
      #setenv BSFILE   $LNHOME/bs/gt3/ncepwin.t21l20          # Atm. BS File
      setenv BSFILE   $LNHOME/bs/gt3/ncepwin.t42l20          # Atm. BS File
      setenv RSTFILE  $DIR/Restart.amat                      # Restart-Data File
      #setenv FRC      $FDIR/frc.t21l20.classic.grd           # initial perturbation
      #setenv SFRC     $FDIR/frc.t21l20.classic.grd           # steady forcing
      # setenv FRC      $FDIR/frc.t42l20.classic.grd               # initial perturbation
      # setenv SFRC     $FDIR/frc.t42l20.classic.grd               # steady forcing
      setenv FRC      $FDIR/newFrc.grd               # initial perturbation
      setenv SFRC     $FDIR/newFrc.grd               # steady forcing
      
      
      setenv TRANS    gt2gr
      setenv TEND     59
      #
      #
      if (! -e $DIR) mkdir -p $DIR
      cd $DIR
      \rm SYSOUT
      echo job started at `date` > $DIR/SYSOUT
      /bin/rm -f $DIR/SYSIN
      #
      #      parameters
      #
      cat << END_OF_DATA >>! $DIR/SYSIN
       &nmrun  run='linear model'                                 &end
       &nmtime start=0,1,1,0,0,0, end=0,1,$TEND,0,0,0             &end
       &nmhdif order=4, tefold=0.5, tunit='DAY'                   &end
       &nmdelt delt=40, tunit='MIN', inistp=2                     &end
       &nmdamp ddragv=0.5,0.5,0.5,20.,20.,20.,20.,20.,20.,20.,20.,20.,20.,20.,20.,20.,20.,20.,1.,1.,
               ddragd=0.5,0.5,0.5,20.,20.,20.,20.,20.,20.,20.,20.,20.,20.,20.,20.,20.,20.,20.,1.,1.,
               ddragt=0.5,0.5,0.5,20.,20.,20.,20.,20.,20.,20.,20.,20.,20.,20.,20.,20.,20.,20.,1.,1.,
               tunit='DAY'                                           &end
       &nminit file='$BSFILE' , DTBFR=0., DTAFTR=0., TUNIT='DAY'   &end
       &nmrstr file='$RSTFILE', tintv=1, tunit='MON',  overwt=t    &end
      
       &nmvdif vdifv=1.d3,1.d3,1.d3,1.d3,1.d3,1.d3,1.d3,1.d3,1.d3,1.d3,1.d3,1.d3,1.d3,1.d3,1.d3,1.d3,1.d3,1.d3,1.d3,1.d3,
               vdifd=1.d3,1.d3,1.d3,1.d3,1.d3,1.d3,1.d3,1.d3,1.d3,1.d3,1.d3,1.d3,1.d3,1.d3,1.d3,1.d3,1.d3,1.d3,1.d3,1.d3,
               vdift=1.d3,1.d3,1.d3,1.d3,1.d3,1.d3,1.d3,1.d3,1.d3,1.d3,1.d3,1.d3,1.d3,1.d3,1.d3,1.d3,1.d3,1.d3,1.d3,1.d3,                         &end
       &nmbtdif tdmpc=0.                                           &end
       &nmfrc  ffrc='$FRC',   oper=f, nfcs=1                       &end
       &nmsfrc fsfrc='$SFRC', ofrc=t, nsfcs=1, fsend=-1,1,30,0,0,0 &end
      
       &nmchck ocheck=f, ockall=f                                  &end
       &nmdata item='GRZ',    file=''                              &end
      
       &nmhisd tintv=1, tavrg=1, tunit='DAY'                       &end
       &nmhist item='PSI',  file='psi', tintv=1, tavrg=1, tunit='DAY' &end
       &nmhist item='CHI',  file='chi', tintv=1, tavrg=1, tunit='DAY' &end
       &nmhist item='U',    file='u',   tintv=1, tavrg=1, tunit='DAY' &end
       &nmhist item='V',    file='v',   tintv=1, tavrg=1, tunit='DAY' &end
       &nmhist item='OMGF', file='w',   tintv=1, tavrg=1, tunit='DAY' &end
       &nmhist item='T',    file='t',   tintv=1, tavrg=1, tunit='DAY' &end
       &nmhist item='Z',    file='z',   tintv=1, tavrg=1, tunit='DAY' &end
       &nmhist item='PS',   file='p',   tintv=1, tavrg=1, tunit='DAY' &end
      END_OF_DATA
      #
      #  run
      #
      $RUN < $DIR/SYSIN >> $DIR/SYSOUT
      #
      cd $TDIR
      $TRANS
      echo job end at `date` >> $DIR/SYSOUT
      ```

      

      ## 关于Grads

      对于使用opengrads气象家园整合版，需要设置一些环境变量。以管理员模式运行编辑器。参考[解决opengrads打开NC格式文件显示ununits.dat error的方法-编程作图-气象家园_气象人自己的家园 (06climate.com)](http://bbs.06climate.com/forum.php?mod=viewthread&tid=37910&fromuid=103735)

      ```
      上面系统变量值根据安装版本不同有所修改，用EXE安装的opengrads2.0设置如下：
      在“系统变量”中选“Path"----点“编辑”----加入“C:\OpenGrADS\Contents\Cygwin\Versions\2.0.2.oga.2\i686;”
                    在“系统变量”中点“新建”----设置变量名“GADDIR”----变量值“C:\OpenGrADS\Contents\Resources\SupportData”
                    在“系统变量”中点“新建”----设置变量名“GASCRP”----变量值“C:\OpenGrADS\Contents\Resources\Scripts"
      ```

      

      
