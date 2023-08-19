---
title: R2S 中 OpenWrt 系统的安装、更新、设置及插件 OpenClash 的使用
permalink: /aa9040d613e8b8913594af76f858dfd1
tags: fq 旁路由
---

这篇文章将介绍 R2S 中 OpenWrt 系统的安装、更新、设置及插件 OpenClash 的使用（以旁路由的视角）。

<!--more-->

## R2S 的购买

友善 R 系列产品（均为 ARM 架构）已经有很多种，一般而言，自己建议，如果家里宽带少于 500M，则入门级软路由 R2S 足以（目前某宝全套装在 300 元左右）；如果家里宽带为 500M~1000M，则 R4S 足以（目前某宝全套装在 600 元左右）。我自己的宽带低于 500M，于是采用了 R2S，目前已经稳定运行了 2 年多。这里说的是都是带外壳的产品，总之你不可能买个主板回来吧。对于 R2S 和 R4S，全套餐一般指的是：单机器+TF卡+电源+读卡器，而对于 USB 风扇问题，前者工作温度在 50℃ 上下，后者在 45 ℃上下，所以两者一般都无需再配 USB 风扇。R2S 的全套餐如下：

![](https://cdn.staticaly.com/gh/Meiting-Wang/pictures@main/picgo/202308200344643.png){:.shadow}

## 刷入 OpenWrt 系统

### 下载一个合适的 OpenWrt 系统

首先，我们要准备一个适合 R2S 的 OpenWrt 系统。这里推荐几个适用于 R2S 且 Star 较多的 GitHub 项目：

- [kiddin9 / OpenWrt_x86-r2s-r4s-r5s-N1](https://github.com/kiddin9/OpenWrt_x86-r2s-r4s-r5s-N1)
- [stupidloud / nanopi-openwrt](https://github.com/stupidloud/nanopi-openwrt)
- [DHDAXCW / NanoPi-R2S-rk3328](https://github.com/DHDAXCW/NanoPi-R2S-rk3328)

各位可以在里面下载自己喜欢的版本。这里尤其要说一下的就是，也是自己构建 OpenWrt 系统的方式，为上面推荐的第一个项目，其可以通过网站 [https://supes.top/](https://supes.top/) 在线定制自己的 OpenWrt 系统。这是非常好的，因为我们可能会有各种各样的需要，如不需要 SSR+ 插件、需要 OpenClash 和 PassWall 等等。 下面为我的构建过程：

![](https://cdn.staticaly.com/gh/Meiting-Wang/pictures@main/picgo/202308200409733.png){:.shadow}

然后点击“构建新固件”，等候 1~3 分钟，固件构建完成，然后在下载镜像中选择第一个文件进行下载。下载的文件名称大致为：`xx.xx-定制版-FRIENDLYARM_NANOPI-R2S-SQUASHFSSYSUPGRADE.IMG.GZ`

### 使用 balenaEtcher 刷入系统







进入 balenaEtcher

















