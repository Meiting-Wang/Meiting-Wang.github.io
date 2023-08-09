---
title: 自定义 jekyll-TeXt-theme 博客的 Logo 和 Favicon
tags: blog-build jekyll-TeXt-theme jekyll
---

我们前面通过文章[利用 Github Pages + jekyll-TeXt-theme 初步搭建个人博客](https://meiting-wang.github.io/2023/08/04/%E5%88%A9%E7%94%A8GP%E5%92%8CJK%E5%88%9D%E6%AD%A5%E6%90%AD%E5%BB%BA%E4%B8%AA%E4%BA%BA%E5%8D%9A%E5%AE%A2.html)介绍了初步搭建博客的流程。这里我们依据官方文档 [Logo 和 Favicon](https://kitian616.github.io/jekyll-TeXt-theme/docs/zh/logo-and-favicon) 介绍如何去更改网站的 Logo 和 Favicon。

## 修改 Logo

我们可以通过替换 *_includes/svg/logo.svg* 来替换你的 Logo。我们可以在这个[免费网站](https://logo.com/)设计你的 Logo，设计完毕后你可以从中下载 Logo 的 png、webp、svg、ai 以及 pdf 文件版本。

## 修改 Favicon

我们可以使用 [realfavicongenerator](https://realfavicongenerator.net/) 生成我们需要的 Favicon，然后再将其放在对应位置中，具体流程如下：

- 打开 [realfavicongenerator](https://realfavicongenerator.net/) 后，点击 **Select your Favicon picture**，选择需要被用来制作 Favicon 的图片进入下一步：

  ![image-20230809025217476](https://cdn.staticaly.com/gh/Meiting-Wang/pictures@main/picgo/202308090252496.png)

- 选择将 Favicon 系列文件存放在根目录，点击 **Generate your Favicons and HTML code** 进入下一步（其他选项的保持默认）：

  ![image-20230809025552550](https://cdn.staticaly.com/gh/Meiting-Wang/pictures@main/picgo/202308090255572.png)

- 点击 **Favicon package** 下载 realfavicongenerator 为我们制作好的系列 Favicon 文件，并将其解压在本地文件夹根目录中（若有相同，则选择替换）；将图中 HTML 代码替换到 *_includes/head/favicon.html* 文件中；部署完网站后，可返回来点击 **Check your favicon** 测试结果：

  ![](https://cdn.staticaly.com/gh/Meiting-Wang/pictures@main/picgo/202308090305967.png)













































































