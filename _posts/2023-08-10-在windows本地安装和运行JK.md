---
title: 在 Windows 系统本地安装和运行 Jekyll
tags: jekyll blog-build
---

为了在本地调试由 Jekyll 生成的网站效果，有必要在自己的系统上安装 Jekyll。依据

- [在 Windows 系统上安装 Jekyll](https://www.xjtu-blacksmith.cn/notes/install-jekyll-on-windows)
- [用 Github pages 和 Jekyll 搭建博客](https://yuleii.github.io/2020/06/09/build-blog-with-github-pages-and-jekyll.html)
- [使用 GitHub Page + Jekyll + TeXt theme 制作博客](https://zhuanlan.zhihu.com/p/385384830)
- [飞鸿影-搭建jekyll博客](https://www.cnblogs.com/52fhy/p/5096251.html)

这里将阐述在 windows 本地安装 Jekyll 的过程。

## 准备工作

安装过程需要 git bash 访问外网，所以需先按照文章 [Git 的配置与代理设置](https://meiting-wang.github.io/2023/08/04/git%E7%9A%84%E9%85%8D%E7%BD%AE%E4%B8%8E%E4%BB%A3%E7%90%86%E8%AE%BE%E7%BD%AE.html)在 windows 本地安装并部署好 Git。

## 安装 Ruby 环境

Jekyll 是由 Ruby 语言开发而成的网站搭建工具，所以我们首先安装 Ruby 环境。

- 点击[这里](https://rubyinstaller.org/downloads/)下载最新版的 Ruby（建议下载最新版的 x64 版本）并安装，完毕后按照后续提示完成更新
- 打开任意一种命令行工具（包括命令提示符 cmd、powershell、Git Bash 等等），用 `ruby -v` 命令检查 Ruby 是否正确安装
- 运行`gem update --system`更新 RubyGems

## 安装 Jekyll 和 Bundler

- 用`gem install jekyll bundler`分别安装 Jekyll 与一个名为 Bundler 的程序——后者用于自动安装其他所需的程序。

- 在 git bash 中使用`cd`命令将目录切换到网站项目本地仓库的根目录中

- 运行`bundle install`——这将使得 Bundler 程序为你目前所在网站安装所需要的各种必要工具

## 在本地运行 Jekyll  主题

- 运行 `bundle exec jekyll serve` 或 `jekyll serve --watch` 命令，这将使得 Jekyll 在 Bundler 的保障下开始运行，开启一个「本地服务器」预览网站。

- 不要关闭命令行程序。 打开浏览器，在浏览器中输入 `127.0.0.1:4000` 或 `localhost:4000`，你就能看到由你编写的代码所生成的网站（文章的更改能立即生效；对于网站元素的更改需要重启 jekyll 服务后才能生效）。

- 只要命令行程序没有关闭，本地网页就能一直访问。

## 常见问题

- 如果出现了`...Failed to open TCP connection to rubygems.org:443...`的错误，将`https://gems.ruby-china.com`设置为默认的 RubyGems 镜像源可解决问题，运行代码为：`gem sources --add https://gems.ruby-china.com/ --remove https://rubygems.org/`。相关资料参见 [timezone data could be found问题和RubyGems默认镜像源设置](https://blog.csdn.net/shysea2019/article/details/130647010)
- 如果出现了`Jekyll 4.3.2 | Error: No source of timezone data could be found`类似的错误。我们需要做以下操作：
  - 在 git bash 命令行中运行 `gem install tzinfo-data`
  - 在本地网站仓库根目录下 `Gemfile` 文件的内容中添加一行 `gem 'tzinfo-data', platforms: [:mingw, :mswin, :x64_mingw]`，然后在 git bash 命令行中运行 `bundle update`
  - 通过以上操作，就可解决网站的时区问题了。相关资料参见：(1)[Resolving TZInfo::DataSourceNotFound Errors](https://github.com/tzinfo/tzinfo/wiki/Resolving-TZInfo::DataSourceNotFound-Errors); (2)[解决 Jekyll 的 post 时区问题](https://blog.jasongzy.com/jekyll-timezone.html); (3)[timezone data could be found问题和RubyGems默认镜像源设置](https://blog.csdn.net/shysea2019/article/details/130647010)











