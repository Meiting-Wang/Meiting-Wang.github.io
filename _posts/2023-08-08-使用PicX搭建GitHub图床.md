---
title: 使用 PicX 搭建 GitHub 图床
tags: 图床 github
---

我们在写markdown语言的文章时，不可避免的要使用图片。为了使得文章轻量化以及便于给其他人阅读，我们需要一个图床来承载我们上传的图片，然后在本身的markdown中，只需附上对应图片的链接即可。在这里，我将展示使用 PicX 工具搭建图床的整个过程。

## PicX 简介

PicX 是一款基于 GitHub API 开发的图床工具，提供图片上传托管、生成图片链接和常用图片工具箱服务。相关的链接如下：

- GitHub 项目：[PicX](https://github.com/XPoet/picx)
- 官方文档入口：[快速开始](https://picx-docs.xpoet.cn/usage-guide/get-start.html)
- PicX 使用界面：[https://picx.xpoet.cn/](https://picx.xpoet.cn/)



## 图床搭建流程

- 点击[这里](https://github.com/new)建立用于储存上传图片的仓库

- 点击[这里](https://github.com/settings/tokens/new)申请 GitHub token，申请时注意勾上以下选项：

  - [x] repo

    - [x] repo:status

    - [x] repo_deployment

    - [x] public_repo

    - [x] repo:invite

    - [x] security_events

- [打开 PicX 使用界面](https://picx.xpoet.cn/#/config)>图床配置>输入Token>点击手动配置

- 依次操作：选择仓库>选择分支>选择目录>点击确定

- 点击我的设置，然后依次操作：图片名称设置>图片压缩设置>图片链接规则配置>图片链接格式设置

- 再点击上传图片，至此，我们就可以上传图片并同时获得图片的 markdown 链接了。

- 上传完图片后，我们还可以点击图床管理，然后进行以下操作：

  - 查看以上上传图片的属性
  - 复制以前上传图片的链接
  - 删除以前上传的图片（对应 Github 中仓库的文件也会被删除）
  - 批量复制图片链接与删除图片

> 更多使用细节，可参照[官方说明文档](https://picx-docs.xpoet.cn/usage-guide/get-start.html)。