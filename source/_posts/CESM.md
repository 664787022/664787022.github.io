---
title: CESM的安装及运行
date: 2024-03-21 11:17:00
tags: 
    - Linux
    - 软件
category: 经验总结
cover: /img/cover20.png
sticky: 1
---

## 关于CESM的安装

- 总的过程下来，安装的问题基本出在 `config_machines.xml` 和 `config_compilers.xml` 上。 对于这两个文件一定要根据自己的机器情况进行设置。

- 除此之外，在安装过程中，库的依赖库需要统一。例如在编译 `esmf` 时使用的是 `mpich` , 而在配置CESM时，我设置的是 `openmpi`。 这就导致在 `./case.build` 中出现 `mct` 等报错问题，最后我删除了`esmf` 用`openmpi` 重新编译解决了问题。 应该把CESM所有的库，以及这些库的依赖库都统一起来 (类似的还有`pnetcdf` 也应该统一成用`openmpi` 编译)。

- 另一个问题是网络问题，不过是在`./manage_externals/checkout_externals` 还是 `./case.submit` 都需要从网络下载一些文件。然而网络被墙，这些步骤频繁失败。解决方案可以是在本地开启`Clash` 代理，然后在`linux` 中开启使用本地的代理，从而让`linux` 连上本地开启的VPN。

- 还有一个关于Lapack的问题。这个库的编译参照[linux关于blas、lapack的安装和使用 - 知乎 (zhihu.com)](https://zhuanlan.zhihu.com/p/520848641) 但安装好在./case.build会出现类似`glam_strs2.F90:(.text+0x888): undefined reference to dcopy_` 的报错。主要是因为在gcc编译中链接库的顺序问题。解决方案是在config_compilers.xml的`<SLIBS>`中添加 ` <append>-L/disk1/xhw/libs/lapack/lib -llapacke -llapack -lcblas -lrefblas -lm -lgfortran</append>`

- build时报错 `relocation truncated to fit r_x86_64_32s against .data'` 。由于编译内存不足需要增加内存，在 `config_compilers.xml` 的 `FFLAGS` 里添加 `-mcmodel=medium`。[GCC 编译错误 relocation truncated to fit: R_X86_64_32S against `.bss'_relocation truncated to fit 错误-CSDN博客](https://blog.csdn.net/ai297313/article/details/42711837)

- submit后运行中断并报错`prterun noticed that process rank 2 with PID 313682 on node charney exited on signal 11 (Segmentation fault)`.原因是编译参数限制了堆栈的大小，不利于并行计算。输入`ulimit -s unlimited` 解决。[并行计算错误提示 - 第一原理 - 小木虫 - 学术 科研 互动社区 (muchong.com)](https://muchong.com/html/201308/6230859.html)

- ./case.submit后 `ERROR: No result from jobs [('case.run', None), ('case.st_archive', 'case.run or case.test')]` 。一方面case默认跑5天，但以月平均输出。由于5天run不足以输出月平均，所以就`no result`。可以修改`./xmlchange STOP_N=1,STOP_OPTION=nmonths`。另一方面即使修改了运行时长，如果你的机器没有batch（任务调度系统），那么仍然会输出这个错误。但在`archive`里可以找到运行输出的历史文件，这样的情况下可以忽视这个报错。[[case.submit error\] ERROR: No result from jobs [('case.run', None), ('case.st_archive', 'case.run or case.test')] | DiscussCESM Forums (ucar.edu)](https://bb.cgd.ucar.edu/cesm/threads/case-submit-error-error-no-result-from-jobs-case-run-none-case-st_archive-case-run-or-case-test.5740/#post-38647)

- 一开始我使用的是系统自带的gcc，然后编译安装了一系列库。后来在编译运行CESM时，出现一些报错，发现可能是gcc版本太低导致的。于是我自己编译安装了高版本的gcc。这样的情况下，需要重新编译安装之前版本gcc编译的库，否则会出现类似`come from different version of gcc` 的错误。另外，自己编译安装gcc在某个文件夹下后，需要手动修改所有`gcc/lib64/*.la` 的`libdir='$gcc/lib64'`和`dependency_libs`

- FWHIST运行报错 ` pio_support::pio_die:: myrank=-1 : ERROR: ionf_mod.F90:235 : NetCDF: Attempt to use feature that was not turned on when netCDF was built.MPI_ABORT was invoked on rank 1 in communicator MPI_COMM_WORLD` 。经历了用 `nccopy -k nc6 file.nc newfile.nc` 修改格式无果。最后在 [Not a NetCDF error for ionf_mod.F90? | DiscussCESM Forums (ucar.edu)](https://bb.cgd.ucar.edu/cesm/threads/not-a-netcdf-error-for-ionf_mod-f90.3843/) 找到了答案。`./xmlchange PIO_TYPENAME='netcdf'`

- 在大装置上还遇到了类似这个报错“`H5Zbzip2.c:6:18: fatal error: hdf5.h: No such file or directory`"。在大装置上，库都是通过module load导入的。而大装置上的hdf5似乎在编译时没有开始并行功能，导致如上报错。 解决方案是我自己用intelmpi重新编译hdf5，./configure CC=mpiicc FC=mpiifort CXX=mpiicpc  --enable-parallel --enable-fortran --enable-shared --prefix=/home/ydn/opt/software/hdf5-1.10.6/build . 并导入该hdf5

  

## CESM 文件夹结构

[![pF2IJVU.md.jpg](https://s21.ax1x.com/2024/03/17/pF2IJVU.md.jpg)](https://imgse.com/i/pF2IJVU)

[![pF2I1K0.png](https://s21.ax1x.com/2024/03/17/pF2I1K0.png)](https://imgse.com/i/pF2I1K0)

## CASE的建立到提交

新建case

```bash
cd $HOME/CESM/cime/scripts/

./create_newcase --case $HOME/CESM/cases/CASE --res RES --compset COMPSET --Mach myMach
```

Setup：生成`case.run`; namelist`usr_nl_xxx`;  `CaseDocs`。 `pelayout` 被固定

```bash
./case.setup
```

build

```bash
./case.build
```

提交

```bash
./case.submit
```

关于case的运行过程被记录在 `CaseStatus` 文件中

```
cd $HOME/CESM/cime/scripts/casename/CaseStatus
```

## 修改、查询.xml

-p 可以**模糊查询**名为`JOB_WALLCLOCK_TIME` 的变量设置

```bash
./xmlquery -p WALLCLOCK
```

修改允许时长

```bash
./xmlchange STOP_N=1,STOP_OPTION=nmonths
```

修改pelayout

```
./xmlchange NTASKS=xxx,NTHRDS=xxx,ROOTPE=xxx
```

修改（在./case.setup之前）

```bash
./xmlchange CONTINUE_RUN=TRUE
```

或者直接修改 `env_run.xml`

## namelist

namelist文件在 `$CASEROOT` 里，CAM模块的namelist名为 `user_nl_cam`

主要用于设置输出哪些变量，每几小时一平均，每个文件塞几个时次的变量

- **`nhtfrq`**: 输出频率
- **`mfilt`**: 每个文件塞的时次数
- **`fincl`**: 额外增添一些变量

`nhtfrq`

`nhtfrq=0` 表示月平均输出，`nhtfrq>0`按时间步长输出，`nhtfrq<0`按小时输出

```fortran
nhtfrq = -24  ! 逐日(24小时)
nhtfrq = -3  ! 逐3小时输出
```

`mfilt`

```fortran
! 逐日输出，每个文件里有365个时次
nhtfrq = -24   
mfilt = 365
```

> Note: 对于逐月输出的情况，设置mfilt无效. For monthly frequency, we always have: `mfilt = 1`。 每个月作为一个文件是上限？不存在12个月为一个文件的情况？

`fincl`

输出的历史文件的文件名会带有**`h0`**, **`h1`**, …, **`h9`**字段，一共至多有十个。`h0` 是默认输出的，带有这个字段的文件会输出模式默认输出的变量。如果我想增加几个变量输出，我可以进行一些设置`fincl2='xxx'`，这些变量会出现在`h1`字段的文件中。`fincl3` 控制`h2` ......

```fortran
! 在h0中以月平均输出默认变量。在h1中以逐小时输出UVT三个变量，十个小时为一个文件。在h2中以逐24小时输出UVT，十个小时为一个文件
nhtfrq = 0, -1, -24 
mfilt = 1, 10, 10 
fincl2 = 'U', 'V', 'T' 
fincl3 = 'PRECT'
```

默认情况是做平均输出，例如逐小时平均，逐24小时平均。可以通过添加flags变逐小时输出瞬时量。

- **`A`** ==> Average
- **`B`** ==> GMT 00:00:00 average
- **`I`** ==> Instantaneous
- **`M`** ==> Minimum
- **`X`** ==> Maximum
- **`L`** ==> Local-time
- **`S`** ==> Standard deviation

```fortran
! 逐月平均输出默认变量。在h1中，每3小时输出TQUV的瞬时量
fincl2   = 'T:I','Q:I','U:I','V:I'
nhtfrq   = 0, -3 
mfilt   = 1, 8
```

以上是CAM模块里的设置方法，对于海洋、陆面等模块的设置方法略有不同，参见 [Customize CAM output — CESM Tutorial (ncar.github.io)](https://ncar.github.io/CESM-Tutorial/notebooks/namelist/output/output_cam.html)

### 如何关闭各分量的输出

[How to turn off CESM history output | DiscussCESM Forums (ucar.edu)](https://bb.cgd.ucar.edu/cesm/threads/how-to-turn-off-cesm-history-output.7894/#post-47372)

## 附录

### xml 和 namelist 汇总

[CESM1.2 Model Component Namelists (ucar.edu)](https://www2.cesm.ucar.edu/models/cesm1.2/cesm/doc/modelnl/)



### namelist 汇总

[namelist](https://docs.cesm.ucar.edu/models/cesm2/settings/current/index.html)

### compsets

[CESM2 Component Sets Definition (ucar.edu)](https://docs.cesm.ucar.edu/models/cesm2/config/2.1.3/compsets.html)

### variable fields 汇总

[CAM](https://ncar.github.io/CAM/doc/build/html/users_guide/model-output.html#example-default-history-fields-and-master-field-lists)

[POP](https://ncar.github.io/CAM/doc/build/html/users_guide/model-output.html#example-default-history-fields-and-master-field-lists)

[CLM](https://www2.cesm.ucar.edu/models/cesm1.2/clm/models/lnd/clm/doc/UsersGuide/history_fields_table_40.xhtml)

[CICE](https://ncar.github.io/CICE/users_guide/ice_history.html)

[CISM](https://escomp.github.io/cism-docs/cism-in-cesm/versions/release-cesm2.0/html/controlling-output.html)

### case 命名规则

[![pF2IORs.png](https://s21.ax1x.com/2024/03/17/pF2IORs.png)](https://imgse.com/i/pF2IORs)

[Naming Conventions | Community Earth System Model (ucar.edu)](https://www.cesm.ucar.edu/models/cesm2/naming-conventions)

### 集群、节点、核心、任务

集群：相当于一个机房，机房里有很多计算机。这些计算机的集合就是集群

节点：机房里的每个计算机相当于节点

核心：每个计算机的处理器核心

任务：例如跑一次CESM实验就是一次任务，这个任务可以拆分成若干小任务，每个小任务分配给核心。

### 关于NTASKS，PES，MPITASK

XML设置中有若干设置并行计算的变量。经过一番探索初步摸清了它们的意义

| 表头                    | 表头                                                                                                    |
|:--------------------- | ----------------------------------------------------------------------------------------------------- |
| MAX_MPITASKS_PER_NODE | 每个节点上`MPI task`**的最大数量**。也可以在`config_machines.xml`里设置。                                                |
| MAX_TASKS_PER_NODE    | 所有分量每个节点上`(MPI tasks) * (threads)` 的总和。必须大于等于 `MAX_MPITASKS_PER_NODE`。也可以在 `config_machines.xml` 里设置。 |
| NTASKS                | 每个分量的`MPI task`数                                                                                      |
| NTHRDS                | 每个分量每个任务的`threads`数。必须大于等于1。如果等于1，表示对应分量的并行关闭。                                                        |
| ROOTPE                | `MPI task` 任务编号。                                                                                      |

对于一个case，如果

```fortran
NTASKS_ATM = 16
NTHRDS_ATM = 4
ROOTPE_ATM = 0

NTASKS_OCN = 64
NTHRDS_OCN = 1
ROOTPE_OCN = 16
```

[![pFWvGCt.png](https://s21.ax1x.com/2024/03/20/pFWvGCt.png)](https://imgse.com/i/pFWvGCt)

从上图可以知道程序实际只用了80个tasks，那么程序会向服务器申请80个tasks和128个pes处理器。前16个task用于处理atm，每个task由4个pes负责计算。后64个tasks用于处理ocn，每个task由1个pes负责计算。

这80个tasks的是没有重叠的，atm和ocn同时计算。如果ROOTPE_OCN=0, 那么前16个task就是和atm重叠的，ocn的前16个task需要等atm计算完成才能开始计算。

如果这时候 `ROOTPE_OCN = 64`

[![pFWzGX8.png](https://s21.ax1x.com/2024/03/20/pFWzGX8.png)](https://imgse.com/i/pFWzGX8)

由于ocn的task编号从64开始，导致atm和ocn之间有48个task和pes不会被使用，但这些仍然由程序向服务器申请下来。

### Compset 字母意义

| Designation | Active Components      | Data Components | Notes                                                                        |
| ----------- | ---------------------- | --------------- | ---------------------------------------------------------------------------- |
| A           | –                      | various         | All data components; used for software testing                               |
| **B**       | **atm, lnd, ice, ocn** | **–**           | **Fully active components**                                                  |
| C           | ocn                    | atm, ice, rof   |                                                                              |
| D           | ice                    | atm, ocn, rof   | Slab ocean model (SOM)                                                       |
| E           | atm, lnd, ice          | ocn             | Slab ocean model (SOM)                                                       |
| **F**       | **atm, lnd**           | **ice, ocn**    | **Sea ice in prescribed mode; some F compsets use fewer surface components** |
| G           | ice, ocn               | atm, rof        |                                                                              |
| I           | lnd                    | atm             |                                                                              |
| J           | lnd, ice, ocn          | atm             | Can be used to spin up the surface components                                |
| **P**       | **atm**                | **–**           | **CAM PORT compsets**                                                        |
| **Q**       | **atm**                | **ocn**         | **Aquaplanet compsets**                                                      |
| S           | –                      | –               | No components present; used for software testing                             |
| T           | glc                    | lnd             |                                                                              |
| X           | –                      | –               | Coupler-test components; used for software testing                           |

### 关于BHIST和B1850

1850的强迫保持在工业化前水平，2000的强迫保持在near present day水平ya,hist的强迫则是随时间演化的，可以理解为近真实情景的强迫的时间演变。所以如果使用B1850,和BHIST使用相同的初始时间RUN_STARTDATE,两个case的演化也是非常不同的。

原文链接：https://blog.csdn.net/qq_27984679/article/details/134903532

### 装库的一些编译选项

ncview

```bash
./configure --prefix=/disk1/xhw/opt/ncview --with-nc-config=$libspath/netcdf/bin/nc-config --with-udunits2_incdir=$libspath/udunits/include/ --with-udunits2_libdir=$libspath/udunits/lib/ --with-png_incdir=$libspath/libpng/include/ --with-png_libdir=$libspath/libpng/lib/
```

```bash
# hdf5
./configure --prefix=/disk1/xhw/libs/hdf5 --with-zlib=/disk1/xhw/libs/zlib --enable-shared --enable-fortran --enable-parallel4 --enable-cxx


#netcdf-c
./configure --prefix=/disk1/xhw/libs/netcdf LDFLAGS="-L/disk1/xhw/libs/hdf5/lib -L/disk1/xhw/libs/zlib/lib" CPPFLAGS="-I/disk1/xhw/libs/hdf5/include -I/disk1/xhw/libs/zlib/include" --enable-largefile --enable-netcdf-4 --enable-parallel4 --enable-shared


#netcdf-fortran
./configure --prefix=/disk1/xhw/libs/netcdf CPPFLAGS=-I/disk1/xhw/libs/netcdf/include LDFLAGS=-L/disk1/xhw/libs/netcdf/lib --enable-netcdf-4 --enable-shared


#netcdf-cxx
./configure --prefix=/disk1/xhw/libs/netcdf CPPFLAGS=-I/disk1/xhw/libs/netcdf/include LDFLAGS=-L/disk1/xhw/libs/netcdf/lib --enable-shared


#opempi
./configure --prefix=/disk1/xhw/libs/openmpi


#pnetcdf
./configure --prefix=/disk1/xhw/libs/pnetcdf --with-mpi=/disk1/xhw/libs/openmpi --enable-subfiling --enable-shared --enable-large-file-test --enable-null-byte-header-padding --enable-burst-buffering --enable-profiling


#lapack
https://zhuanlan.zhihu.com/p/520848641
cp make.inc.example make.inc
make blaslib
make cblaslib
make lapacklib
make lapackelib
```

### 一些疑问

1. hybrid和branch区别，什么是hydrid，为什么新建case都是hydrid
2. pelayout到底改怎么规划
3. RUN_REFCASE和RUN_REFDATE是什么
4. BHIST和B1850的区别
5. 很多文件的日期是从0001年开始算的，什么意思

PIcontrol使用的是工业革命前的强迫，对1850年重复模拟500或者300年，模拟这么多年目的是为了使系统达到稳定。B1850则是在别人模拟好的PIcontrol实验的基础上，用他们得到的数据作为初始场（这也就是REFCASE的意义和REFDATE=0500或0300的原因）。而B1850其实也是PIcontrol, 从REFCESE读取初始场后B1850重复地对1850年进行模拟 ([Suggestions for modifying the start date (CESM2) ](https://bb.cgd.ucar.edu/cesm/threads/suggestions-for-modifying-the-start-date-cesm2.4921/#post-35387)， 所以B1850的STARTDATE是0001年这种形式，表示第一年、第二年......。如果随意改变B1850的REFDATE可能导致模式找不到初始场数据。如果改变STARTDATE，没有意义

BHIST是Historical run。使用的初始场来自于别人跑的Historical run。他的时间是推进的，例如第一年是1979，第二年就是1980...... 

以上说的基本都是hybrid，就运行的初始场是别人运行好的restart文件。通过咨询张贺老师了解到，CESM使用startup就相当于全部自己提供初始场，与WRF的运行方式相同了。如果只模拟几天则不需要spin up，如果运行超过一年则最好spin up.



- 关于PElayout:

以全部NTASK=4， NTHRDS=4,   ROOTPE=0，MAX_MPITASKS_PER_NODE=MAX_TASKS_PER_NODE=40 为例。这种情况下，每个分量占用4个并行任务，每个任务使用4个线程（4个核心）。由于ROOTPE相同，这些分量是按顺序依次运行的。

这个时候如果运行./preview_run将输出

```
  nodes: 1
  total tasks: 4
  tasks per node: 4
  thread count: 4
```

其中 `total task=4` 很好理解，因为所有NTAKS=4，ROOTPE=0即所有的分量在前四个TASK上运行。如果`ROOTPE_OCN=4`, 将有`total task=8` 。如果`ROOTPE_OCN=2`, 将有`total task=6` 。注意`total task`是**总任务数**， 这些个任务数会被分配到若干个`node`运行。是`node`数去适应`total taks`的变化。`total task`将只与我们对任务的排列分配(NTASK,ROOTPE)有关。

对于`tasks per node=4`，模式会优先将所有任务分配到一个`node`上。 因为我们设置了 `MAX_MPITASKS_PER_NODE=40`, 它是所有分量的`NTASKS`的最大值。  `MAX_MPITASKS_PER_NODE=40`远大于我们设置的`total tasks=4`, 所以这四个任务全部被放到了一个`node上`，所以`nodes=1， tasks per node=4`

如果改变`MAX_MPITASKS_PER_NODE=3`，这意味着每个`node`上最多只能有3个任务，而我们一共有`total tasks=4` 。所以需要两个`node`。这时`nodes=2,  tasks per node=3`。(如果`total tasks <= MAX_MPITASKS_PER_NODE`,  则 `tasks per node = MAX_MPITASKS_PER_NODE`。如果`total tasks > MAX_MPITASKS_PER_NODE`,  则 `tasks per node <= MAX_MPITASKS_PER_NODE`。)

由此我们知道`MAX_MPITASKS_PER_NODE`是限制每个`node`上的任务数用的。 相对的，`MAX_TASKS_PER_NODE`受限制每个`node`上 `NTASKS*NTHRDS`用的。例如现在`MAX_TASKS_PER_NODE=40`，而 `tasks per node * thread count=4*4=16` 那么这同样将使得`nodes=1`。如果改变`MAX_TASKS_PER_NODE=15`，那么`nodes`将增加为1，`tasks per node` 将减小到3以使得二者乘积小于15。这个过程中`total tasks`不变。



### 未来计划

1. 看看文献，有没有人做个WACCM替换再分析，试着复现，建立 **baseline**

2. 试着用2°分辨率
3. 试着预报爆发性增温
4. 化学成分给气候态
5. MERRA2
