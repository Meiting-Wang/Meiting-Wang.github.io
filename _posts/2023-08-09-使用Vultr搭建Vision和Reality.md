---
title: 使用 Vultr 搭建 Vision 和 Reality
permalink: /75b32ec5e51d9b04395b260863918235
tags: 
  - fq
---

依据以下资料：

- mack-a的博客文章：[2023-03-29：搭建最新的Vision和Reality防止VPS端口封禁](https://www.v2ray-agent.com/archives/1680104902581)
- 奶油之家的博客文章：[2023-07-23：一键搭建Xray新协议Reality VPS](https://naiyous.com/732.html)
- 一瓶奶油的视频教程：[2023-07-23：轻松一键搭建xray新协议reality vps实现科学上网](https://www.youtube.com/watch?v=sVupcPFLvxs&t=256s)

本人于2023年8月9日使用 Vultr 亲自搭建 Vision 和 Reality 魔法上网节点。

<!--more-->

## 准备工作

- 通过文章 [Vultr VPS 的购买流程](https://meiting-wang.github.io/341802df0825bf94ec83797e798304e2.html)阐述的流程购买一台 Vultr VPS。
- 通过文章[域名的购买与解析](https://meiting-wang.github.io/72172e804af8cdb9ebf8e08675613d12.html)阐述的流程购买一个合适的域名并做好域名的解析。
- 通过文章 [FinalShell 的使用](https://meiting-wang.github.io/8be7596dcbd4c56c22960bc900fafe91)阐述的流程使用 FinalShell 接入 Vultr VPS

## 搭建 Vision 和 Reality

本部分操作均在 FinalShell 中进行，流程如下：

- 放行端口（一般情况下，默认 443 和 80 端口都是开放的，无需此项操作。如果是其他自定义端口，就需要用到以下命令）

  - Debian 或 Ubuntu 系统

    ```bash
    ufw allow <端口号>
    ```

  - CentOS 系统

    ```bash
    firewall-cmd --zone=public --add-port=<端口号>/tcp --permanent
    ```

- 下载脚本

  ```sh
  wget -P /root -N --no-check-certificate "https://raw.githubusercontent.com/mack-a/v2ray-agent/master/install.sh" && chmod 700 /root/install.sh && /root/install.sh
  ```

- 安装 Vision 和 Reality 协议（依据作者文档，这里有两种安装方式，一种需要域名，一种无需域名。这里只展示需要域名的方式），这部分依次选择为（该过程会同时安装 Vision_TLS、Reality+TCP+uTLS+Vision 和 Reality+gRPC+uTLS）：

  - 2-任意组合安装 
  - 1-Xray-core 
  - 7-VLESS+Reality+uTLS+Vision[推荐] 
  - 输入要配置的域名 
  - 使用默认端口（直接回车）
  - 1-letsencrypt[默认] 
  - UUID 随机（直接回车）
  - 是否使用TLS+Vision端口 ？(输入 y，然后回车) 
  - 搭建完成


## 节点的使用

- **使用 I**：上述搭建完成后，FinalShell 界面上会立即出现对应节点的链接，我们只需要复制其中的通用格式至对应的魔法上网软件即可使用：

  |         协议类型          |              通用格式              |
  | :-----------------------: | :--------------------------------: |
  |   VLESS+TCP+TLS_Vision    | vless://......VLESS_TCP/TLS_Vision |
  | VLESS+reality+uTLS+Vision | vless://......vless_reality_vision |
  |  VLESS+reality+uTLS+gRPC  |  vless://......vless_reality_grpc  |

- **使用 II**：如果后期忘了对应节点的通用格式链接，我们还可以回到 FinalShell，重新打开对应 VPS > 输入**vasma** > 选择**7-账号管理** > 选择**1-查看账号**。即可重新输出上面系列通用格式。

- **使用 III**：回到 FinalShell > 输入**vasma** > 选择**7-账号管理** > 选择**2-查看订阅** > **使用随机的 Salt**（如果非第一次这么使用，则选择**使用上次生成的 Salt**）。此时会生成订阅链接和二维码，将订阅链接添加至魔法上网软件（移动端可直接扫描二维码进行快速添加）并更新订阅后即可实现魔法上网。

  > Windows 和 Android 采用默认订阅即可。



































