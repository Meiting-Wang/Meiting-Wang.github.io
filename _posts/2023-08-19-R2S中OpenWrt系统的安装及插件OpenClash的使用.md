---
title: R2S 中 OpenWrt 系统的安装、更新、设置及插件 OpenClash 的使用
permalink: /aa9040d613e8b8913594af76f858dfd1
tags: fq
---

这篇文章将介绍 R2S 中 OpenWrt 系统的安装、更新、设置及插件 OpenClash 的使用（以旁路由的视角）。我之所以采用旁路由的方式，是因为如果哪一天软路由挂了，我们的核心网络不会受到影响。

<!--more-->

## 主路由的设置

我的主路由是**小米 Redmi 路由器 AC2100**。一般而言这部分的设置应该是你之前就已经完成了。现假设你还没有完成，这里分两个方面进行讲解。

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

  ![](https://cdn.staticaly.com/gh/Meiting-Wang/pictures@main/picgo/202308202323848.png){:.shadow}

  ![](https://cdn.staticaly.com/gh/Meiting-Wang/pictures@main/picgo/202308201652837.png){:.shadow}

- 进入**网络**>**接口**>**LAN口**>**编辑**，进行如下设置：

  ![](https://cdn.staticaly.com/gh/Meiting-Wang/pictures@main/picgo/202308201617373.png){:.shadow}

  ![](https://cdn.staticaly.com/gh/Meiting-Wang/pictures@main/picgo/202308202325914.png){:.shadow}

  ![](https://cdn.staticaly.com/gh/Meiting-Wang/pictures@main/picgo/202308201625670.png){:.shadow}

- 进入**网络**>**防火墙**，进行如下设置：

  ![](https://cdn.staticaly.com/gh/Meiting-Wang/pictures@main/picgo/202308201645101.png){:.shadow}

- 至此，非入侵模式设置完毕。

## 入侵模式设置

对于**非入侵模式**，它也有缺点，就是每个连接到该局域网的终端，都需要手动设置ip地址，才能实现科学上网。那么有没有一种方式使得连接上该局域网的终端都自动实现科学上网？答案是有的。那这个就被称为是入侵模式了，即会对家庭核心网络（运营商-光猫-主路由）造成影响。换个说法，如果哪天软路由挂了，则整个局域网都瘫痪了。**在前面非入侵模式设置的基础上**，这里说一下需要更改的设置：

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

## PassWall 设置与 OpenClash 内核的安装和更新

前面旁路由已经搭建完毕，如果要实现魔法上网，对应插件的运行肯定是少不了的。然而，明明我们使用的 OpenClash，为何还需设置 PssWall。原因在于，初始版本的 OpenClash 是没有内核的，

![](https://cdn.staticaly.com/gh/Meiting-Wang/pictures@main/picgo/202308201900085.png){:.shadow}

这样将导致 OpenClash 无法启动。然而，要顺利安装内核大抵也需要魔法上网，所以我们可以先通过 PassWall 构建魔法上网环境，其次再为 OpenClash 安装内核和更新。下面为使用 PassWall 构建魔法上网环境的流程：

- 如果有单纯的节点链接，可以进入**节点列表**>**通过链接添加节点**进行添加节点。
- 如果有机场的订阅链接，可以进入**节点订阅**>**添加**，添加完毕后点击**保存并应用**。回到**节点订阅**界面，在刚刚添加的订阅一栏中，点击**手动订阅**，并等待运行完成。此时订阅链接包含的节点被解析完毕。
- 进入**节点列表**，点击使用一个较为合适的节点。
- 进入**基本设置**>**模式**，设置好代理模式（TCP与UDP默认代理模式设置为“中国列表以外”或“全局代理”）
- 进入**基本设置**>**主要**，打开**主开关**，UDP 节点设置为与 TCP 节点相同，点击**保存并应用**。
- 此时 PassWall 的魔法上网环境已经搭建完成。

> 这里要注意的是，如果你采用的是非入侵模式，此时你会发现一个奇怪的现象，在 PasWall 主界面，在测试谷歌连接时发现没有问题，但连接主路由下面的设备（如有线的台式电脑、连接 Wifi 的手机）还是无法魔法上网。这正是非入侵模式的特色，要实现局域网下的连接设备的魔法上网，还需要对每台设备进行设置，这个后面会讲到。然而，无论怎么样，软路由本身已经可以魔法上网了，也就是说，它自己本身可以去访问外网安装和更新 OpenClash 内核了。

至此，OpenClash 已经有了安装和更新内核的网络基础。这时，我们**进入服务**>**OpenClash**>**插件设置**>**版本更新**，点击**一键检查更新**，并等候插件安装更新完毕（可刷新本页面或进入**服务**>**OpenClash**>**运行日志**查看结果）

## OpenClash 的部署

关闭 PassWall 插件的运行，开始着手 OpenClash 插件的部署：

- 进入**插件设置**>**模式设置**
  - 将运行模式改为 **Fake-IP (增强) 模式**
  - 打开 **UDP 流量转发**，如果你的节点又这个功能的话
  - 代理模式选择 **Rule【策略代理】**
  - 点击**保存配置**
- 进入**插件设置**>**流量控制**
  - 启用**路由本机代理**
  - 启用**禁用QUIC**
  - 启用**实验性：绕过中国大陆IP**
  - 启用**仅允许内网**
  - 点击**保存配置**
- 进入**插件设置**>**DNS设置**
  - 本地DNS劫持选择**使用 Dnsmasq 转发**
  - 启用**禁止 Dnsmasq 缓存 DNS**
  - 点击**保存配置**
- 进入**覆写设置**>**常规设置**
  - **URL-Test 策略组切换灵敏度(ms)** 设置为 25（可自定义设置）
  - 点击**保存配置**
- 进入**覆写设置**>**DNS设置**
  - 启用**自定义上游 DNS 服务器**
  - 禁用**追加上游 DNS**（不然不知道给你追加了什么垃圾dns服务器）
  - 启用**追加默认 DNS**
  - 启用 **Fake-IP 持久化**
  - 点击**保存配置**
- 进入**配置订阅**（如果你有 Clash 订阅链接的话）
  - 为订阅设置好自动更新策略
  - 点击**添加**，之后将自己的订阅链接部署进去
  - 点击**保存配置**
- 进入**配置管理**（如果你有 Clash 配置文件的话）
  - 通过**选择文件**添加自己的配置文件，并上传
  - 为上传好的配置文件重命名
- 完成上述配置后，回到主界面，点击**启动 OpenClash**，完毕后即可实现软路由的魔法上网。

## 非入侵模式下的终端设置

**在入侵模式下，你的所有终端已全部实现魔法上网。无需再进行本部分设置**。在非入侵模式下，尽管软路由可以魔法上网，但连接在主路由下的终端还无法实现魔法上网。基于非入侵式旁路由的特点，我们还需要对每个终端进行额外设置。

- 如果你的是 Windows 10，进入设置>网络和Internet>状态>属性>IP设置>编辑>选择手动>打开ipv4，进行如下设置：

  ![](https://cdn.jsdelivr.net/gh/Meiting-Wang/pictures/picgo/picgo-202206280136359.png){:.shadow}

  > 这里的网关指向了旁路由。我们知道旁路由的网关指向了主路由，于是之后上网的数据路径为 windows>旁路由>主路由>运营商。

- 如果你的是 Android，在对应 Wifi 界面进行如下设置：

  ![](https://cdn.jsdelivr.net/gh/Meiting-Wang/pictures/picgo/picgo-202206280140302.png){:.shadow}

其他设备的配置与上面的类似。

## 结语

一切都设置完毕后，查看效果。如果还是有些问题，则将所有设备重启（包括电脑、光猫、硬由器、软路由）。稳定之后，如果还是有问题，就需要一一排查问题所在了（检查是否严格按照文章的步骤进行设置；对应特定的报错，搜索引擎查找资料等）

## 参考资料

- [Blog: Openwrt 作为旁路网关（不是旁路由！！）正确配置方法，性能测试 —— 破解迷思](https://www.right.com.cn/forum/thread-5512947-1-1.html)
- [Blog: OpenWrt旁路由设置教程—小白也能看懂的超详细教程](https://www.kancloud.cn/lincong/lcjc/2791977)
- [Blog: 软路由科学上网,openclash,openwrt IPv6配置](https://www.hughh.top/posts/soft-routing-guide-3/)
- [youtube: OpenClash使用教程，添加节点|过滤广告|dns防劫持|秒解析| 添加订阅|流量分流|策略组讲解，OpenWrt软路由翻墙，AdGuardHome+openclash详细配置教程，解决DNS污染](https://www.youtube.com/watch?v=2YYa-IM1H8E&list=PLgaEKKVPYE0ROrTD6k1QscgXasA71GheX)
- [youtube: 软路由做旁路由三步搞定！openwrt软路由 R2S R4S openwrt软路由上网设置](https://www.youtube.com/watch?v=w7rwNF2Q3lM)
- [youtube: R2S软路由销量之王！R2S安装openwrt攻略 openwrt软路由设置](https://www.youtube.com/watch?v=ZCmbbnIBD78)





















