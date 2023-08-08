---
title: 使用 Vultr 搭建最新的 Vision 和 Reality
tags: fq Vultr
---

依据以下资料：

- mack-a的博客文章：[2023-03-29：搭建最新的Vision和Reality防止VPS端口封禁](https://www.v2ray-agent.com/archives/1680104902581)
- 奶油之家的博客文章：[2023-07-23：一键搭建Xray新协议Reality VPS](https://naiyous.com/732.html)
- 一瓶奶油的视频教程：[2023-07-23：轻松一键搭建xray新协议reality vps实现科学上网](https://www.youtube.com/watch?v=sVupcPFLvxs&t=256s)

本人于2023年8月9日使用 Vultr 亲自搭建最新的 Vision 和 Reality 科学上网节点。

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

## 购买 VPS

