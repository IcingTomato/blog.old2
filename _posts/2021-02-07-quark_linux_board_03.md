---
layout: post
title: "Let's Play Quark Linux Board - Episode 3: How to make Kernel?"
description: "Quark Linux Board Kernel Tutorial"
comments: false
keywords: "Quark, Linux"
---

# 1 Linux Mainline简介

Mainline即主线的意思，Linux内核的开发分为Linus维护的主线、其他开发分支以及各种稳定版本。开发分支最终都会统一提交到Linus维护的主线中。 最新版本的U-boot和主线Linux内核已经支持了全志的H3/H5 CPU，我们在最新版本的的U-boot和主线Linux内核的基础上进行了定制开发，使其能支持上NanoPi H5/H3/H2+系列的开发板。

注意: 本维基的内容仅适用于基于Linux-4.14内核的系统固件，请不要在基于全志原厂H5-Linux-3.10/H3-Linux-3.4内核的系统固件上执行本维基里描述的操作。

# 2 特性

[Sunxi-mainline-kernel-4.14-features.xlsx](https://wiki.friendlyarm.com/wiki/index.php/File:Sunxi-mainline-kernel-4.14-features.xlsx)

# 3 为H3/H2+编译Linux-4.14 BSP

## 3.1 安装交叉编译器

访问[此处下载地址](https://download.friendlyarm.com/nanopineo)的toolchain目录，下载交叉编译器arm-cortexa9-linux-gnueabihf-4.9.3.tar.xz，然后解压编译器:

```shell
$ mkdir -p /opt/FriendlyARM/toolchain
$ tar xf arm-cortexa9-linux-gnueabihf-4.9.3.tar.xz -C /opt/FriendlyARM/toolchain/
```

然后将编译器的路径加入到PATH中，用vi编辑vi ~/.bashrc，在末尾加入以下内容：

```shell
$ export PATH=/opt/FriendlyARM/toolchain/4.9.3/bin:$PATH
$ export GCC_COLORS=auto
```

执行一下~/.bashrc脚本让设置立即在当前shell窗口中生效，注意"."后面有个空格：

```shell
$ . ~/.bashrc
```

这个编译器是64位的，不能在32位的Linux系统上运行，安装完成后，你可以快速的验证是否安装成功：

```shell
$ arm-linux-gcc -v
gcc version 4.9.3 (ctng-1.21.0-229g-FA)
```

## 3.2 编译U-boot

下载U-boot源码，并切换分支:

```shell
$ git clone https://github.com/friendlyarm/u-boot.git -b sunxi-v2017.x --depth 1
```

编译U-boot:

```shell
$ apt-get install swig python-dev python3-dev
$ cd u-boot
$ make nanopi_h3_defconfig ARCH=arm CROSS_COMPILE=arm-linux-
$ make ARCH=arm CROSS_COMPILE=arm-linux-
```

这里使用的配置文件nanopi_h3_defconfig可以支持友善电子所有的H3/H2+的开发板。
编译成功后会生成文件u-boot-sunxi-with-spl.bin。

更新SD上的U-boot:
将SD卡插入PC中，然后执行如下命令:

```shell
$ cd u-boot
$ dd if=u-boot-sunxi-with-spl.bin of=/dev/sdX bs=1024 seek=8
$ sync && eject /dev/sdX
```

/dev/sdx请替换为实际的TF卡设备文件名。
sync命令可以确保数据成功写到TF卡中，eject命令用于弹出TF卡。

当正在使用SD卡运行系统时，也可以先用scp命令拷贝u-boot-sunxi-with-spl.bin到开发板上，然后用dd命令更新SD卡上的U-boot:

```shell
$ scp u-boot-sunxi-with-spl.bin root@192.168.1.230:/root/
$ dd if=/root/u-boot-sunxi-with-spl.bin of=/dev/mmcblk0 bs=1024 seek=8
```

如果是带有eMMC的开发板，当正在使用eMMC运行系统时，也可以先用scp命令拷贝u-boot-sunxi-with-spl.bin到开发板上，然后用dd命令更新eMMC上的U-boot:

```shell
$ scp u-boot-sunxi-with-spl.bin root@192.168.1.230:/root/
$ dd if=/root/u-boot-sunxi-with-spl.bin of=/dev/mmcblk0 bs=1024 seek=8
```

NanoPi H3/H2+开发板的启动设备的设备节点总是/dev/mmcblk0。

## 3.3 编译Linux内核

下载Linux内核源码，并切换分支:

```shell
$ git clone https://github.com/friendlyarm/linux.git -b sunxi-4.14.y --depth 1
```

编译和更新Linux内核:

```shell
$ apt-get install u-boot-tools
$ cd linux
$ touch .scmversion
$ make sunxi_defconfig ARCH=arm CROSS_COMPILE=arm-linux-
$ make zImage dtbs ARCH=arm CROSS_COMPILE=arm-linux-
```

编译完成后会在arch/arm/boot/目录下生成zImage，并且在arch/arm/boot/dts/目录下生成dtb文件。

假设SD卡的boot分区挂载在/media/SD/boot/，更新SD卡上的zImage和dtb文件:

```shell
$ cp arch/arm/boot/zImage /media/SD/boot/
$ cp arch/arm/boot/dts/sun8i-*-nanopi-*.dtb /media/SD/boot/
```

也可以用scp命令通过网络更新:

```shell
$ scp arch/arm/boot/zImage root@192.168.1.230:/boot
$ scp arch/arm/boot/dts/sun8i-*-nanopi-*.dtb root@192.168.1.230:/boot
```

编译和更新驱动模块:

```shell
$ cd linux
$ make modules ARCH=arm CROSS_COMPILE=arm-linux-
```

假设SD卡的rootfs分区挂载在/media/SD/rootfs/，更新SD卡上rootfs的驱动模块:

```shell
$ cd linux
$ make modules_install INSTALL_MOD_PATH=/media/SD/rootfs/ ARCH=arm CROSS_COMPILE=arm-linux-
```

# 4 为H5编译Linux-4.14 BSP

## 4.1 安装交叉编译器

访问[此处下载地址](http://download.friendlyarm.com/nanopineo2)的toolchain目录，下载交叉编译器gcc-linaro-6.3.1-2017.02-x86_64_aarch64-linux-gnu.tar.xz，然后解压编译器:

```shell
$ mkdir -p /opt/FriendlyARM/toolchain
$ tar xf gcc-linaro-6.3.1-2017.02-x86_64_aarch64-linux-gnu.tar.xz -C /opt/FriendlyARM/toolchain/
```

然后将编译器的路径加入到PATH中，用vi编辑vi ~/.bashrc，在末尾加入以下内容：

```shell
$ export PATH=/opt/FriendlyARM/toolchain/gcc-linaro-6.3.1-2017.02-x86_64_aarch64-linux-gnu/bin:$PATH
$ export GCC_COLORS=auto
```

执行一下~/.bashrc脚本让设置立即在当前shell窗口中生效，注意"."后面有个空格：

```shell
$ . ~/.bashrc
```

安装完成后，你可以快速的验证是否安装成功：

```shell
$ aarch64-linux-gnu-gcc -v
gcc version 6.3.1 20170109 (Linaro GCC 6.3-2017.02)
```

## 4.2 编译U-boot

下载U-boot源码，并切换分支:

```shell
$ git clone https://github.com/friendlyarm/u-boot.git -b sunxi-v2017.x --depth 1
```

编译U-boot:

```shell
$ apt-get install swig python-dev python3-dev
$ cd u-boot
$ make nanopi_h5_defconfig CROSS_COMPILE=aarch64-linux-gnu-
$ make CROSS_COMPILE=aarch64-linux-gnu-
```

这里使用的配置文件nanopi_h5_defconfig可以支持友善电子所有的H5的开发板。
更新SD上的U-boot:

将SD卡插入PC中，然后执行如下命令:

```shell
$ cd u-boot
$ dd if=spl/sunxi-spl.bin of=/dev/sdX bs=1024 seek=8
$ dd if=u-boot.itb of=/dev/sdX bs=1024 seek=40
```

/dev/sdx请替换为实际的TF卡设备文件名。

当正在使用SD卡运行系统时，也可以先用scp命令拷贝sunxi-spl.bin和u-boot.itb到开发板上，然后用dd命令更新SD卡上的U-boot:

```shell
$ scp spl/sunxi-spl.bin root@192.168.1.230:/root/
$ scp u-boot.itb root@192.168.1.230:/root/
$ dd if=/root/sunxi-spl.bin of=/dev/mmcblk0 bs=1024 seek=8
$ dd if=/root/u-boot.itb of=/dev/mmcblk0 bs=1024 seek=8
```

如果是带有eMMC的开发板，当正在使用eMMC运行系统时，也可以先用scp命令拷贝sunxi-spl.bin和u-boot.itb到开发板上，然后用dd命令更新eMMC上的U-boot:

```shell
$ scp spl/sunxi-spl.bin root@192.168.1.230:/root/
$ scp u-boot.itb root@192.168.1.230:/root/
$ dd if=/root/u-boot-sunxi-with-spl.bin of=/dev/mmcblk0 bs=1024 seek=8
```

NanoPi H5开发板的启动设备的设备节点总是/dev/mmcblk0。

## 4.3 编译Linux内核

下载Linux内核源码，并切换分支:

```shell
$ git clone https://github.com/friendlyarm/linux.git -b sunxi-4.14.y --depth 1
```

编译和更新Linux内核:

```shell
$ cd linux
$ touch .scmversion
$ make sunxi_arm64_defconfig ARCH=arm64 CROSS_COMPILE=aarch64-linux-gnu-
$ make Image dtbs ARCH=arm64 CROSS_COMPILE=aarch64-linux-gnu-
```

编译完成后会在arch/arm64/boot/目录下生成Image，并且在arch/arm64/boot/dts/allwinner/目录下生成dtb文件。

假设SD卡的boot分区挂载在/media/SD/boot/，更新SD卡上的Image和dtb文件:

```shell
$ cp arch/arm64/boot/Image /media/SD/boot/
$ cp arch/arm64/boot/dts/allwinner/sun50i-h5-nanopi*.dtb /media/SD/boot/
```

也可以用scp命令通过网络更新:

```shell
$ scp arch/arm64/boot/Image root@192.168.1.230:/boot
$ scp arch/arm64/boot/dts/allwinner/sun50i-h5-nanopi*.dtb root@192.168.1.230:/boot
```

编译和更新驱动模块:

```shell
$ cd linux
$ make modules ARCH=arm64 CROSS_COMPILE=aarch64-linux-gnu-
```

假设SD卡的rootfs分区挂载在/media/SD/rootfs/，更新SD卡上rootfs的驱动模块:

```shell
$ cd linux
$ make modules_install INSTALL_MOD_PATH=/media/SD/rootfs/ ARCH=arm64 CROSS_COMPILE=aarch64-linux-gnu-
```
