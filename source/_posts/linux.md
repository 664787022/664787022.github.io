---
title: Linux 操作
date: 2022-07-11 16:50:38
tags: Linux
category: Linux
cover: /img/cover7.png
---

## 前言

记录Linux相关操作命令和学习过程、心得。学习网站：蓝桥云课程

---

## 基本操作

```bash
# 创建一个名为 file 的文件，touch是一个命令
touch file

# 进入一个目录，cd是一个命令
cd /etc/

# 查看当前所在目录
pwd

# 显示当前目录下文件名
ls
ls -a # 显示隐藏文件
ls *.txt


# 查看命令帮助
man
man ls
```

## 用户及文件权限管理

```bash
# 创建新用户
sudo adduser xiao

# 切换用户
su xiao

# 退出当前用户
exit
```

```bash
# 查看用户所在组
groups xiao

# 把用户加入sudo中
sudo usermod -G sudo lilei


# 删除用户
sudo deluser lilei --remove-home
```

### 查看文件权限

```bash
# 使用较长格式列出文件
ls -l
```

<img src="https://img-blog.csdnimg.cn/71ff22ee34ef4cb4b37c37104145f512.png" title="" alt="" data-align="center">

<img src="https://img-blog.csdnimg.cn/img_convert/0a5b24109ff8375c343f00533b98b772.png" title="" alt="" data-align="center">

<img src="https://img-blog.csdnimg.cn/img_convert/121612b91ffa7c0577d78980249c9d80.png" title="" alt="" data-align="center">

读权限，表示你可以使用 `cat <file name>` 之类的命令来读取某个文件的内容；写权限，表示你可以编辑和修改某个文件的内容；

执行权限，通常指可以运行的二进制程序文件或者脚本文件，如同 Windows 上的 `exe` 后缀的文件，不过 Linux 上不是通过文件后缀名来区分文件的类型。你需要注意的一点是，**一个目录同时具有读权限和执行权限才可以打开并查看内部文件，而一个目录要有写权限才允许在其中创建其它文件**，这是因为目录文件实际保存着该目录里面的文件的列表等信息。

- 变更文件所有者

```bash
# 需要切换到 xiao 用户执行以下操作
sudo chown xiao(用户名) iphone11(文件名)
```

- 更改文件权限

每个文件有三组固定的权限，分别对应`拥有者，所属用户组，其他用户`，**记住这个顺序是固定的**。文件的读写执行对应字母 `rwx`，以二进制表示就是 `111`，用十进制表示就是 `7`，对进制转换不熟悉的同学可以看看 [进制转换](https://baike.baidu.com/item/%E8%BF%9B%E5%88%B6%E8%BD%AC%E6%8D%A2/3117222)。例如我们刚刚新建的文件 iphone11 的权限是 `rw-rw-rw-`，换成对应的十进制表示就是 666，这就表示这个文件的拥有者，所属用户组和其他用户具有读写权限，不具有执行权限。

如果我要将文件 iphone11 的权限改为只有我自己可以用那么就可以用这个方法更改它的权限

```bash
# 修改权限
chmod 600 iphone11
ls -alh iphone11
```

<img src="https://img-blog.csdnimg.cn/img_convert/7a6097ba186d6053f4705a01321d7bee.png" title="" alt="" data-align="center">

---

## Linux 目录结构及文件基本操作

### 文件目录

> FHS（英文：Filesystem Hierarchy Standard 中文：文件系统层次结构标准），多数 Linux 版本采用这种文件组织形式，FHS 定义了系统中每个区域的用途、所需要的最小构成的文件和目录同时还给出了例外处理与矛盾处理。

FHS 定义了两层规范，第一层是， `/` 下面的各个目录应该要放什么文件数据，例如 `/etc` 应该放置设置文件，`/bin` 与 `/sbin` 则应该放置可执行文件等等。

第二层则是针对 `/usr` 及 `/var` 这两个目录的子目录来定义。例如 `/var/log` 放置系统日志文件，`/usr/share` 放置共享数据等等。

<img src="https://img-blog.csdnimg.cn/img_convert/b88605383677285c7c0d0e76157ffd9f.png" title="" alt="" data-align="center">

> `~` 目录位于 `/` 目录之下。例如进入`/` 之后，再进入 `home` ，再进入用户，也就进入了 `~` 目录。
> 
> `/` 目录下除了存放 `home` 以外还存放了一些系统文件夹，例如 `etc`, `bin`, `lib` 等等。
> 
> `~` 目录下则存放了 `Desktop` , `~` 更像是我们熟悉的 Windows。
> 
> 在使用绝对路径时，路径的起点是 `/` 目录。例如使用绝对路径进入`~` 时：
> 
>                                                 cd /home/xiao
> 
> home 前要加 '/'

### 文件基本操作

- 创建空白文件
  
  ```bash
  touch test
  ```
  
  > 若当前目录存在一个 test 文件夹，则 touch 命令，则会更改该文件夹的时间戳而不是新建文件。

&nbsp;

- 创建目录
  
  ```bash
  mkdir mydir
  ```

- 同时创建父目录(多级目录)
  
  ```bash
  mkdir -p father/son/grandson
  ```

- 复制文件
  
  ```bash
  cp test father/son/grandson
  ```

> 要成功复制**目录**需要加上 `-r` 或者 `-R` 参数，表示递归复制，就是说有点“株连九族”的意思。

&nbsp;

- 复制整个文件夹和其内文件
  
  ```bash
  cp -r father family
  ```

> 若 `family` 文件夹不存在，则生成 `father` 副本，并重命名为 `family`。若`family`存在，则在`family`下得到 `father` 副本。

&nbsp;

- 删除文件
  
  ```bash
  rm test
  
  # 若文件为只读文件，-f 参数忽视只读权限之间删除
  rm -f test
  
  # 删除目录
  rm -r family
  rm -rf family
  ```

- 移动文件、重命名
  
  ```bash
  mv file1 dir1
  
  # mv 还有重命名的作用
  mv file1_oldname file1_newname
  ```

- 查看文件
  
  ```bash
  cat file1
  
  # 显示行号
  cat -n passwd
  
  # 更专业的行号打印
  nl -b a file1
  
  # 分页查看
  more file1
  less file1
  
  # 查看文件头几行或尾几行
  head -n 5 file1 # 头5行
  tail -n 5 file1 # 尾5行
  ```

- 查看文件类型
  
  ```bash
  file filename
  ```

### 查找文件

```bash
find /etc/(文件目录) -name file.sh(文件名，有后缀则加后缀)

# 查找当前文件夹下以.c 为后缀的文件
find . -name "*.c"
```

> 如开头加 sudo 表示使用管理员权限。可解决一些权限不足的问题。
> 
> `-name` 不能乱丢
> 
> 此外还有 `locate`, `which`, `whereis` 等查找命令，不细说了

---

## 文件压缩与解压

- zip 解压
  
  ```bash
  zip -r -q -o dir.zip(要生成的压缩文件命) /home/Desktop(要压缩的文件或文件夹)
  
  # 把多个文件压缩在一起
  zip dir.zip file1 file2 file3
  ```
  
  > `-r`表示递归打包子目录内容。不加`-r` 则无法把文件夹内其他东西压缩在一起
  > 
  > `-p` 表示安静模式，不向屏幕输出信息
  > 
  > `-o` 表示输出文件
  > 
  > `zip /dir1/dir2/name.zip file1`  用这种方式将文件压缩到指定文件夹

&nbsp;

- 查看文件大小
  
  ```bash
  du -h file1
  ```
  
  > `-h`表示人类可读的形式

&nbsp;

- zip 解压
  
  ```bash
  unzip dir.zip
  
  # 使用安静模式，将文件解压到指定目录
  unzip -q file1.zip -d dir_zip
  ```
  
  > 若上述指定目录 `dir_zip` 不存在，将会自动创建

&nbsp;

- 仅查看压缩包内容
  
  ```bash
  unzip -l file1.zip
  ```
  
  > **注意：** 使用 unzip 解压文件时我们同样应该注意兼容问题，不过这里我们关心的不再是上面的问题，而是中文编码的问题，通常 Windows 系统上面创建的压缩文件，如果有有包含中文的文档或以中文作为文件名的文件时默认会采用 GBK 或其它编码，而 Linux 上面默认使用的是 UTF-8 编码，如果不加任何处理，直接解压的话可能会出现中文乱码的问题（有时候它会自动帮你处理），为了解决这个问题，我们可以在解压时指定编码类型。
  > 
  > 使用 `-O`（英文字母，大写 o）参数指定编码类型：
  > 
  > `unzip -O GBK 中文压缩文件.zip`

&nbsp;

- tar 压缩
  
  ```bash
  tar -P -cd file1.tar /home/Desktop
  ```
  
  > `tar` 命令压缩可直接将整个文件夹内容压缩进去。不需要像 `zip` 命令那样添加 `-r` 进行递归
  > 
  > `-P` 保留绝对路径符
  > 
  > `-c` 表示创建一个 tar 包文件
  > 
  > `-f` 用于指定创建的文件名，**注意文件名必须紧跟在 `-f` 参数之后**，比如不能写成 `tar -fc shiyanlou.tar`，可以写成 `tar -f shiyanlou.tar -c ~`。你还可以加上 `-v` 参数以可视的的方式输出打包的文件。

&nbsp;

- tar 解压
  
  ```bash
  tar -xf fil1.tar -C tardir
  ```
  
  > 解压目录 `tardir` 必须存在。目前还没找到解压到不存在的目录的方法。

&nbsp;

- 仅查看压缩包内容
  
  ```bash
  tar -tf file1.tar
  ```

- 总结 
  
  ```bash
  # zip：
  zip something.zip something # 打包
  unzip something.zip # 解包
  # 指定路径：-d 参数
  
  # tar：
  tar -cf something.tar something # 打包
  tar -xf something.tar # 解包
  # 指定路径：-C 参数
  ```
