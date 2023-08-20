---
title: R2S 中 OpenWrt 系统的安装、更新、设置及插件 OpenClash 的使用
permalink: /aa9040d613e8b8913594af76f858dfd1
tags: fq
---

这篇文章将介绍 R2S 中 OpenWrt 系统的安装、更新、设置及插件 OpenClash 的使用（以旁路由的视角）。我之所以采用旁路由的方式，是因为如果哪一天软路由挂了，我们的核心网络不会受到影响。

<!--more-->

## 主路由的设置

我的主路由是小米 Redmi 路由器 AC2100。一般而言这部分的设置应该是你之前就已经完成了。现假设你还没有完成，这里分两个方面进行讲解。

### 需要拨号上网

1. 用网线连接光猫的千兆网口与小米路由器的 WAN 口
2. 启动小米路由器，并用手机或电脑通过有线或无线连接到路由器
3. 通过 192.168.31.1 或 miwifi.com 进入小米路由器后端
4. 进入**常用设置**>**安全中心**，设置管理员密码
5. 进入**常用设置**>**局域网设置**，开启"DHCP服务“
6. 进入**常用设置**>**上网设置**>**上网设置**，上网方式选择 **PPPoE**，输入宽带的账户与密码后点击应用（宽带拨号上网）
7. 进入**常用设置**>**Wi-Fi设置**，设置2.4G wifi 与 5G wifi 的名称、密码与隐藏与否，并启用**MU-MIMO/Beamforming**
8. 进入**高级设置**>**QoS智能限速**，关闭**QoS智能分配**
9. 此时，小米路由器有线和 wifi 就都能上网了

### 无需拨号上网

如果光猫已经拨号了，那么此时主路由就无需再拨号了。其他的步骤与前面的都一样，不同的地方在于前面第 6 步：上网方式选择 **DHCP**（指的是由路由器控制一段IP地址范围，客户机登录接入路由器时就可以自动获得路由器分配的 IP 地址和子网掩码）。

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

然后点击“构建新固件”，等候 1~3 分钟，固件构建完成，然后在下载镜像中选择第一个文件进行下载。选择下载的文件名称大致为：`xx.xx-定制版-FRIENDLYARM_NANOPI-R2S-SQUASHFSSYSUPGRADE.IMG.GZ`

### 使用 balenaEtcher 刷入系统

进入 [balena](https://etcher.balena.io/) 下载 balenaEtcher，便携版或安装版均可。需要强调的是，该文件（以 .img.gz 结尾的文件名）通过 balenaEtcher 刷入 TF 卡，无需解压。在后续通过后台升级，该文件也无需解压，直接可用。我操作环境为 windows 系统。用管理员身份打开 balenaEtcher，之后

![](https://cdn.staticaly.com/gh/Meiting-Wang/pictures@main/picgo/202308200523603.png){:.shadow}

## R2S 与主路由的接线

由于我的 R2S 是作为旁路由而存在，所以其接线是很简单的，只需要将其当做普通的有线上网设备，方式为将主路由的 LAN 口连接上 R2S 的 LAN 口。

## 将 R2S 与主路由置于同一网段

在前面的定制化 OpenWrt 系统中，我所设置的后台地址与主路由在同一网段，所以这个问题自然而然就解决了（可直接略过这一步）。然而，对应那些非定制化的 OpenWrt 系统中，其后台地址有可能不会与主路由处于同一网段下，这个时候就无法在浏览器中通过其后台 IP 地址进入其后台。解决这个问题的流程如下（假设主路由的 IP 地址为 192.168.31.1，R2S 的 IP 地址为 192.168.2.1）：

- 修改本地网络的 IP，使之与 R2S 的 IP 地址处于同一网段（这时将无法上网）：

  ![](https://cdn.jsdelivr.net/gh/Meiting-Wang/pictures/picgo/picgo-202206270145931.png){:.shadow}

- 进入R2S后台（192.168.2.1）

- 进入**网络**>**接口**>**LAN口**>**编辑**>**基本设置**，找到ipv4地址一栏，并将其改为与小米路由器在同一网段的地址（如 192.168.31.2）。此时我们将无法再访问R2S后台。

- 回到前面的网络设置中，将 ip 设置再由手动设置改为自动（DHCP）。此时，由于 R2S 与小米路由器在同一个网段，则我们既可以访问R2S新设置的后台（192.168.31.2），也可以上网了。 

## OpenWrt 系统的更新与软件的安装

- 后期系统如果有更新，则不需要像上面一样重新刷入系统，而是可以通过进入**系统**>**备份与升级**>**刷写新的固件**，将最新的固件刷入 R2S
- 如果后期想安装其他的软件包，你可以进入**系统**>**软件包**中，更新列表后在线安装软件或上传本地软件包后进行安装。

## 非入侵模式设置

- 进入**系统**>**管理权**，重置主机密码

- 进入**系统**>**定时重启**，设置定时重启时间

- 进入**系统**>**设置向导**，进行如下设置：

  ![](https://cdn.staticaly.com/gh/Meiting-Wang/pictures@main/picgo/202308201652633.png){:.shadow}

  ![](https://cdn.staticaly.com/gh/Meiting-Wang/pictures@main/picgo/202308201652837.png){:.shadow}

- 进入**网络**>**接口**>**LAN口**>**编辑**，进行如下设置：

  ![](https://cdn.staticaly.com/gh/Meiting-Wang/pictures@main/picgo/202308201617373.png){:.shadow}

  ![](https://cdn.staticaly.com/gh/Meiting-Wang/pictures@main/picgo/202308201620343.png){:.shadow}

  ![](https://cdn.staticaly.com/gh/Meiting-Wang/pictures@main/picgo/202308201625670.png){:.shadow}

- 进入**网络**>**防火墙**，进行如下设置：

  ![](https://cdn.staticaly.com/gh/Meiting-Wang/pictures@main/picgo/202308201645101.png){:.shadow}

## 入侵模式设置

对于**非入侵模式**，它也有缺点，就是每个连接到该局域网的终端，都需要手动设置ip地址，才能实现科学上网。那么有没有一种方式使得连接上该局域网的终端都自动实现科学上网？答案是有的。那这个就被称为是入侵模式了，即会对家庭核心网络（运营商-光猫-主路由）造成影响。换个说法，如果哪天软路由挂了，则整个局域网都瘫痪了。在前面非入侵模式设置的基础上，这里说一下需要更改的设置：

- 进入**网络**>**接口**>**LAN口**>**编辑**>**DHCP服务器**，进行如下设置：

  ![](https://cdn.staticaly.com/gh/Meiting-Wang/pictures@main/picgo/202308201629168.png){:.shadow}

- 进入主路由（小米路由器）的后台（192.168.31.1），进入**常用设置**>**局域网设置**，关闭“DHCP服务”：

  ![](https://cdn.jsdelivr.net/gh/Meiting-Wang/pictures/picgo/picgo-202206280233893.png){:.shadow}

经过以上设置，我们就可以把整个网络系统的 DHCP 服务交由软路由控制。这时对于后来接上该网络的设置，无需任何其他的额外设置，即可实现魔法上网。

## 旁路由设置的总体思想

在前面阐释的非入侵模式和入侵模式的设置中，都需要遵从以下基本思想：

- 旁路由必须和主路由在同一网段
- 旁路由的网关必须指向主路由
- 防火墙开启IP动态伪装































