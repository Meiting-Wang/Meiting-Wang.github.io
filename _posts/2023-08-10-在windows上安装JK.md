---
title: 在 Windows 系统上安装 Jekyll
tags: jekyll
---

为了在本地调试由 Jekyll 生成的网站效果，有必要在自己的系统上安装 Jekyll。借鉴了[在 Windows 系统上安装 Jekyll](https://www.xjtu-blacksmith.cn/notes/install-jekyll-on-windows)，这里将阐述在 windows 本地安装 Jekyll 的过程。

## 准备工作

安装过程需要 git bash 访问外网，所以需先按照文章 [Git 的配置与代理设置](https://meiting-wang.github.io/2023/08/04/git%E7%9A%84%E9%85%8D%E7%BD%AE%E4%B8%8E%E4%BB%A3%E7%90%86%E8%AE%BE%E7%BD%AE.html)在 windows 本地安装并部署好 Git。

## 安装 Ruby 环境

Jekyll 是由 Ruby 语言开发而成的网站搭建工具，所以我们首先安装 Ruby 环境。

- 点击[这里](https://rubyinstaller.org/downloads/)下载最新版的 Ruby（建议下载最新版的 x64 版本）并安装
- 按照后续提示完成更新
- 打开任意一种命令行工具（包括命令提示符 cmd、powershell、Git Bash 等等），用 `ruby -v` 命令检查 Ruby 是否正确安装
- 运行`gem update --system`更新 RubyGems。如果由于网络问题命令运行终端，则可在[这里](https://rubygems.org/pages/download)下载最新版本的 RubyGems，然后解压 > 管理员运行 git bash > cd 到前面解压的文件夹内 > 运行`ruby setup.rb`完成更新。

## 安装 Jekyll 和 Bundler

- 用`gem install jekyll bundler`分别安装 Jekyll 与一个名为 Bundler 的程序——后者用于自动安装其他所需的程序。

























