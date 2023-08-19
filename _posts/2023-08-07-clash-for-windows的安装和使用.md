---
title: Clash for Windows 的安装和使用
permalink: /7556294033efd547cd34592d06782ef4
tags: fq
---

Clash for Windows 是一个用于 windows 上的魔法上网软件，配置和使用方法要比 v2rayN 复杂。这里一切从简，给出 Clash for Windows 的下载地址和使用教程。

<!--more-->

## 项目网站与软件下载地址

- Clash for Windows 的 GitHub 项目网站为：[https://github.com/Fndroid/clash_for_windows_pkg](https://github.com/Fndroid/clash_for_windows_pkg)
- Clash for Windows 的 下载地址为：[https://github.com/Fndroid/clash_for_windows_pkg/releases](https://github.com/Fndroid/clash_for_windows_pkg/releases)

在 releases 中选择 *Clash.for.Windows-x.xx.xx-win.7z* 文件进行下载。

## 软件的使用

软件本身是一个绿色软件，但后期更新后会变成一个安装型软件，所以这里建议先安装一个老版本，然后使用更新变成安装型版本（安装路径为：`C:\Users\wmt\AppData\Local\Programs\Clash for Windows`）：

![](https://cdn.staticaly.com/gh/Meiting-Wang/pictures@main/picgo/202308192101834.png){:.shadow}

软件的汉化（如果无需汉化，则可略过这一步）：进入这里，下载版本匹配的 Releases。详细的，下载对应版本的 *app.7z* 或 *app.zip* 文件(两个压缩包内容一样)后，解压压缩包，然后替换下列路径中的 *app.asar* 文件：`C:\Users\wmt\AppData\Local\Programs\Clash for Windows\resources`

![](https://cdn.staticaly.com/gh/Meiting-Wang/pictures@main/picgo/202308192117245.png){:.shadow}

接下来我们需要有一个 clash 订阅链接。如果你本身有则可以略过这一步，然而如果你只有节点链接或其他软件的订阅链接如 v2ray，则你需要先将其转化为 clash 订阅。方法为：进入 [https://acl4ssr-sub.github.io/](https://acl4ssr-sub.github.io/)，然后

![](https://cdn.staticaly.com/gh/Meiting-Wang/pictures@main/picgo/202308192131178.png){:.shadow}

下载订阅链接。下载完毕后可以右键对其进行设置、代理图形化、规则图形化、更新、复制、更新、打开所在文件夹等操作。

![](https://cdn.staticaly.com/gh/Meiting-Wang/pictures@main/picgo/202308192135182.png){:.shadow}

来到代理界面，选择对应代理方式和规则：

![](https://cdn.staticaly.com/gh/Meiting-Wang/pictures@main/picgo/202308192144660.png){:.shadow}

回到主页，打开系统代理，即可实现科学上网：

![](https://cdn.staticaly.com/gh/Meiting-Wang/pictures@main/picgo/202308192146629.png){:.shadow}

## 常见问题

- 每次更新之后都需要重新汉化
- clash 订阅文件下载下来事实上为一个 *.yaml* 文件。有时我们为实现特定的功能而需要的对配置文件进行修改，这里提供两个模板（形成思想来源于前面订阅转化后的文件内容）：
  - 只包含节点系列：[config3.yaml](https://raw.githubusercontent.com/Meiting-Wang/resource/master/config3.yaml)
  - 只包含机场订阅链接：[config4.yaml](https://raw.githubusercontent.com/Meiting-Wang/resource/master/config4.yaml)
  - 配置文件的更多细节可参考以下资料：
    - [youtube: 「#74」让你意想不到的 clash 客户端终极懒人用法！ rule-provider、 proxy-provider 轻松实现自动更新节点、规则、机场订阅链接](https://www.youtube.com/watch?v=IVlnvBQXEgE)
    - [blog: 什么是 rule-provider、proxy-provider？怎么用？](https://www.jamesdailylife.com/rule-proxy-provider)
