---
title: 域名的购买与解析
tags: fq DNS
---

我们可以在 NameSilo 购买域名，至于域名解析，我们可以使用域名提供商本身进行解析，也可以使用其他NS服务商进行解析。Cloudflare 是用的比较多的一个国外的 NS 服务商，提供15年的SSL证书、免费CDN，同时可以防护DDoS攻击等。这也就是为什么国外很多人不用域名提供商而额外使用Cloudflare 进行域名解析的原因。下面阐述本部分流程：

## NameSilo 域名购买

- 进入 [NameSilo](https://www.namesilo.com/)，注册并登入账户

- 搜索域名：

  ![image-20230809174245800](https://cdn.staticaly.com/gh/Meiting-Wang/pictures@main/picgo/202308091742854.png)

- 选择域名：

  ![image-20230809174330721](https://cdn.staticaly.com/gh/Meiting-Wang/pictures@main/picgo/202308091743742.png)

- 选择相关服务与结账：

  ![image-20230809174754703](https://cdn.staticaly.com/gh/Meiting-Wang/pictures@main/picgo/202308091747746.png)

- 选择支付方式：

  ![image-20230809175005589](https://cdn.staticaly.com/gh/Meiting-Wang/pictures@main/picgo/202308091750620.png)

- 最终支付：

  ![image-20230809175109413](https://cdn.staticaly.com/gh/Meiting-Wang/pictures@main/picgo/202308091751447.png)

- 至此，域名购买完毕。

## NameSilo 域名解析

- 进入其域名解析管理界面

  ![image-20230809180255098](https://cdn.staticaly.com/gh/Meiting-Wang/pictures@main/picgo/202308091802135.png)

- 操作域名解析

  ![image-20230809180419753](https://cdn.staticaly.com/gh/Meiting-Wang/pictures@main/picgo/202308091804780.png)

  至此，设置完毕。一般来说，过一小段时间，域名就解析完成了。此时在你的电脑上，打开 cmd，输入 `ping <你的域名>`查看效果

## CLOUDFLARE 域名解析

就像前面所说，我们也可以使用 [cloudflare](https://www.cloudflare.com/) 进行域名解析，流程如下：

- 进入 [cloudflare](https://www.cloudflare.com/)，注册并登入账户

- 点击添加站点：

  ![image-20230809181322618](https://cdn.staticaly.com/gh/Meiting-Wang/pictures@main/picgo/202308091813641.png)

- 选择计划：

  ![image-20230809181418197](https://cdn.staticaly.com/gh/Meiting-Wang/pictures@main/picgo/202308091814216.png)

- 查看DNS记录：

  ![image-20230809181908672](https://cdn.staticaly.com/gh/Meiting-Wang/pictures@main/picgo/202308091819700.png)

- 更换解析服务器服务器（NameSilo to CLOUDFLARE）：

  ![image-20230809182911197](https://cdn.staticaly.com/gh/Meiting-Wang/pictures@main/picgo/202308091829311.png)



- 快速入门指南：

  ![image-20230809183649893](https://cdn.staticaly.com/gh/Meiting-Wang/pictures@main/picgo/202308091836912.png)

- 等一段时间，回到主页，对应域名如果显示有效，则说明服务器转移成功：

  ![image-20230809184016588](https://cdn.staticaly.com/gh/Meiting-Wang/pictures@main/picgo/202308091840610.png)

- 进入站点，设置DNS：

  ![image-20230809184333484](https://cdn.staticaly.com/gh/Meiting-Wang/pictures@main/picgo/202308091843511.png)

- 至此，设置完毕。一般来说，过一小段时间，域名就解析完成了。此时在你的电脑上，打开 cmd，输入 `ping <你的域名>`查看效果

## 参考资料

- [youtube: namesilo域名注册和cloudflare域名解析教程，新手入门教学](https://www.youtube.com/watch?v=NW49jTk0w60)
- [NameSilo注册与域名购买教程](https://www.vpsgo.com/namesilo-coupon-and-register.html)
- [域名解析教程：Cloudflare解析与DNSPod解析](https://www.vpsgo.com/domain-ns-cloudflare-dnspod.html)































