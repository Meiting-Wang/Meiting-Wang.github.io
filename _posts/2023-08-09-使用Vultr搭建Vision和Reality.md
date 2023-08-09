---
title: 使用 Vultr 搭建 Vision 和 Reality
tags: fq Vultr
---

依据以下资料：

- mack-a的博客文章：[2023-03-29：搭建最新的Vision和Reality防止VPS端口封禁](https://www.v2ray-agent.com/archives/1680104902581)
- 奶油之家的博客文章：[2023-07-23：一键搭建Xray新协议Reality VPS](https://naiyous.com/732.html)
- 一瓶奶油的视频教程：[2023-07-23：轻松一键搭建xray新协议reality vps实现科学上网](https://www.youtube.com/watch?v=sVupcPFLvxs&t=256s)

本人于2023年8月9日使用 Vultr 亲自搭建 Vision 和 Reality 魔法上网节点。

## Vultr 简介

Vultr 是一家来自美国的 VPS 商家，在全球各地都有对应的机房。它有如下特点：

- 一个服务器一个月在线时间小于28天，则流量按小时计费；若超过28天，则按月计费。
- 带宽使用量用出站流量测度，入站流量不计入带宽使用量

相关网站如下：

- [vultr 官网](https://www.vultr.com/)
- [vultr 中文网](https://www.vultrcn.com/)

## 筛选机房

Vultr 有全球各地的机房，那么哪个机房对于我们是更合适的？在实际情况中，并不是距离最近的机房就一定更合适，而需要检测当前网络下各个机房的 ping 值以及下载速度来决定。

- 进入[这里](https://www.vultrcn.com/9.html)下载一键测试脚本，解压后运行脚本，从中可得到延迟最低的机房
- 进入[这里](https://www.vultrcn.com/2.html)可测试各个机房的下载速度（各个机房都有 100M 和 1GB 的文件供用户测试） 

经过测试，在我本人的网络下，表现较好的机房如下：

- 日本-东京-Tokyo-62ms-15MB/s
- 印度-班加罗尔-Bangalore-87ms-10.5MB/s
- 印度-孟买-Mumbai-95ms-3.3MB/s
- 印度-德里NCR-Delhi NCR-116ms-6MB/s

依据以上数据，这里将使用 Tokyo 的机房进行搭建。

## 筛选 Cloud Compute

文章 [Vultr Cloud Compute四种方案VPS性能对比](https://www.vpscue.com/142.html)和[Vultr Cloud Compute VPS云服务器4种方案该怎么选 性能对比评测](https://hostcsr.com/526.html)都对 Vultr Cloud Compute 四种方案的 VPS 进行了测评，发现 AMD High Performance 的综合性能最高，并且价格方面也相对而言比价友好，所以这里将使用 Cloud Compute 的 AMD High Performance 进行搭建。

## 购买 VPS

- 进入 [vultr](https://www.vultr.com/)，注册并登入账户

- 点击 **Products**>**Instances**>**+**>**Deploy New Server**，做出以下选择，然后点击 **Deploy Now**

  |           项目           |                             选择                             |
  | :----------------------: | :----------------------------------------------------------: |
  |      Choose Server       |                        Cloud Compute                         |
  | CPU & Storage Technology |                     AMD High Performance                     |
  |     Server Location      |                         Tokyo-Japan                          |
  |       Server Image       |                        Debian 12 x64                         |
  |       Server Size        | ＄6/mouth,  ＄0.009/hour, 25GB NVMe, 1 vCPU, 1 GB Memory, 2 TB Bandwidth |
  |     Add Auto Backups     |                             OFF                              |
  |   Additional Features    |                         Enable IPv6                          |
  |         SSH Keys         |                           保持默认                           |
  | Server Hostname & Label  |                           自行定义                           |

- 部署完毕后，**Products** 界面的对应 VPS 上，会有 IP 生成。此时在自己电脑上，打开 cmd，输入 `ping <your ip>`，检测其 ping 值是否合理；进入[站长工具 ping 值检测网页](https://ping.chinaz.com/)，输入 `<your ip>`，检测其 ping 值是否合理。以上两方面结果要合理才能进入下一步，否则要排查原因。如果效果始终不好，可删除原 VPS，再新建一个 VPS 重试。

## 购买域名与域名解析

我们可以在 NameSilo 购买域名，至于域名解析，我们可以使用域名提供商本身进行解析，也可以使用其他NS服务商进行解析。Cloudflare 是用的比较多的一个国外的 NS 服务商，提供15年的SSL证书、免费CDN，同时可以防护DDoS攻击等。这也就是为什么国外很多人不用域名提供商而额外使用Cloudflare 进行域名解析的原因。下面阐述本部分流程：

- 进入 [NameSilo](https://www.namesilo.com/)，注册并登入账户

- 搜索域名：

  ![image-20230809174245800](https://cdn.staticaly.com/gh/Meiting-Wang/pictures@main/picgo/202308091742854.png)

  选择域名：

  ![image-20230809174330721](https://cdn.staticaly.com/gh/Meiting-Wang/pictures@main/picgo/202308091743742.png)

  选择相关服务与结账：

  ![image-20230809174754703](https://cdn.staticaly.com/gh/Meiting-Wang/pictures@main/picgo/202308091747746.png)

  选择支付方式：

  ![image-20230809175005589](https://cdn.staticaly.com/gh/Meiting-Wang/pictures@main/picgo/202308091750620.png)

  最终支付：

  ![image-20230809175109413](https://cdn.staticaly.com/gh/Meiting-Wang/pictures@main/picgo/202308091751447.png)

  至此，域名购买完毕。

- 使用 Namesilo 本身进行域名解析：进入其域名解析管理界面

  ![image-20230809180255098](https://cdn.staticaly.com/gh/Meiting-Wang/pictures@main/picgo/202308091802135.png)

  操作域名解析

  ![image-20230809180419753](https://cdn.staticaly.com/gh/Meiting-Wang/pictures@main/picgo/202308091804780.png)

  至此，设置完毕。一般来说，过一小段时间，域名就解析完成了。此时在你的电脑上，打开 cmd，输入 `ping <你的域名>`查看效果

- 当然，就像前面所说，我们也可以使用 [cloudflare](https://www.cloudflare.com/) 进行域名解析，流程如下：进入 [cloudflare](https://www.cloudflare.com/)，注册并登入账户；点击添加站点：

  ![image-20230809181322618](https://cdn.staticaly.com/gh/Meiting-Wang/pictures@main/picgo/202308091813641.png)

  选择计划：

  ![image-20230809181418197](https://cdn.staticaly.com/gh/Meiting-Wang/pictures@main/picgo/202308091814216.png)

  查看DNS记录：

  ![image-20230809181908672](https://cdn.staticaly.com/gh/Meiting-Wang/pictures@main/picgo/202308091819700.png)

  更换服务器：

  ![image-20230809182911197](https://cdn.staticaly.com/gh/Meiting-Wang/pictures@main/picgo/202308091829311.png)

  快速入门指南：

  ![image-20230809183649893](https://cdn.staticaly.com/gh/Meiting-Wang/pictures@main/picgo/202308091836912.png)

  等一段时间，回到主页，对应域名如果显示有效，则说明服务器转移成功：

  ![image-20230809184016588](https://cdn.staticaly.com/gh/Meiting-Wang/pictures@main/picgo/202308091840610.png)

  进入站点，设置DNS：

  ![image-20230809184333484](https://cdn.staticaly.com/gh/Meiting-Wang/pictures@main/picgo/202308091843511.png)

  至此，设置完毕。一般来说，过一小段时间，域名就解析完成了。此时在你的电脑上，打开 cmd，输入 `ping <你的域名>`查看效果

- 本部分的参考资料如下：

  - [youtube: namesilo域名注册和cloudflare域名解析教程，新手入门教学](https://www.youtube.com/watch?v=NW49jTk0w60)
  - [NameSilo注册与域名购买教程](https://www.vpsgo.com/namesilo-coupon-and-register.html)
  - [域名解析教程：Cloudflare解析与DNSPod解析](https://www.vpsgo.com/domain-ns-cloudflare-dnspod.html)

dsdsd

sfsdfsdf





























