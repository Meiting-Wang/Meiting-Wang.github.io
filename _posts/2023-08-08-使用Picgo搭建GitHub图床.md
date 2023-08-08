---
title: 使用 PicGo 搭建 GitHub 图床
tags: 图床 github picgo
---

在文章[使用 PicX 搭建 GitHub 图床](https://meiting-wang.github.io/2023/08/08/%E4%BD%BF%E7%94%A8PicX%E6%90%AD%E5%BB%BAGitHub%E5%9B%BE%E5%BA%8A.html)，我们介绍了使用 PicX 搭建 GitHub 图床的过程。然而，该方法只能在网页端进行操作，并且该方法在流程上略显复杂，即每次上传图片时都要经历以下过程：截图(或复制图片)>打开网页端picx>上传图片>得到markdown链接>将链接复制到本地markdown编辑器中。那么能不能有其他的方案？这是可以有的，这里我们将介绍另外一种方案：使用 PicGo 搭建 GitHub 图床。

## PicGo 简介

![image-20230808182141743](https://cdn.staticaly.com/gh/Meiting-Wang/pictures@main/picgo/image-20230808182141743.png)

PicGo 是一款用于快速上传图片并获取图片 URL 链接的工具。相关的链接如下：

- GitHub 项目：[PicGo](https://github.com/Molunerfinn/PicGo)
- 官方文档入口：[PicGo is Here](https://picgo.github.io/PicGo-Doc/zh/guide/)
- 软件下载入口：[releases](https://github.com/Molunerfinn/PicGo/releases)

## 图床搭建流程

- 点击[这里](https://github.com/new)建立用于储存上传图片的仓库

- 点击[这里](https://github.com/settings/tokens/new)申请 GitHub token，申请时注意勾上以下选项：

  - [x] repo

    - [x] repo:status

    - [x] repo_deployment

    - [x] public_repo

    - [x] repo:invite

    - [x] security_events

- 点击[这里](https://github.com/Molunerfinn/PicGo/releases)下载并安装软件

- 设置软件-上传区：链接格式-markdown

- 设置软件-图床设置-GitHub:

  |      项目      |                           示例                            |
  | :------------: | :-------------------------------------------------------: |
  |   图床配置名   |                         `Default`                         |
  |   设定仓库名   |                  `Meiting-Wang/pictures`                  |
  |   设定分支名   |                          `main`                           |
  |   设置Token    |                `填入前面申请得到的 Token`                 |
  |  设定储存路径  |                         `picgo/`                          |
  | 设定自定义域名 | `https://cdn.staticaly.com/gh/Meiting-Wang/pictures@main` |
  
  











- [打开 PicX 使用界面](https://picx.xpoet.cn/#/config)>图床配置>输入Token>点击手动配置

- 依次操作：选择仓库>选择分支>选择目录>点击确定

- 点击我的设置，然后依次进行设置：图片名称设置>图片压缩设置>图片链接规则配置>图片链接格式设置

  > 这里值得注意的是，github 本身的链接规则为`https://github.com/{{owner}}/{{repo}}/raw/{{branch}}/{{path}}`。此时，国内用户在不科学上网的情况下，可能会无法访问，所以，我们需要其他的CDN加速来进行访问。在 PicX 操作界面上，我们可以很方便的选择其他 CDN 加速链接。官方对此的说明参见[这里](https://picx-docs.xpoet.cn/usage-guide/settings.html#%E5%9B%BE%E7%89%87%E9%93%BE%E6%8E%A5%E8%A7%84%E5%88%99%E9%85%8D%E7%BD%AE)。

- 再点击上传图片，至此，我们就可以上传图片并同时获得图片的 markdown 链接了。

- 上传完图片后，我们还可以点击图床管理，然后进行以下操作：

  - 查看以上上传图片的属性
  - 复制以前上传图片的链接
  - 删除以前上传的图片（对应 Github 中仓库的文件也会被删除）
  - 批量复制图片链接与删除图片

> 更多使用细节，可参照[官方说明文档](https://picx-docs.xpoet.cn/usage-guide/get-start.html)。



