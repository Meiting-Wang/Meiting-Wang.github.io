---
title: Typora与Picgo的结合
tags: 图床 picgo typora
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
  
  自定义域名有如下规则可以使用：
  
  |     类型      |                           CDN规则                            |
  | :-----------: | :----------------------------------------------------------: |
  |   Staticaly   | `https://cdn.staticaly.com/gh/{{owner}}/{{repo}}@{{branch}}` |
  | ChinaJsDelivr |  `https://jsd.cdn.zzko.cn/gh/{{owner}}/{{repo}}@{{branch}}`  |
  |   jsDelivr    | `https://cdn.jsdelivr.net/gh/{{owner}}/{{repo}}@{{branch}}`  |
  |    GitHub     |    `https://github.com/{{owner}}/{{repo}}/raw/{{branch}}`    |
  
  > 相关说明参见 PicX 图床使用指南中的[图片链接规则配置](https://picx-docs.xpoet.cn/usage-guide/settings.html#%E5%9B%BE%E7%89%87%E9%93%BE%E6%8E%A5%E8%A7%84%E5%88%99%E9%85%8D%E7%BD%AE)。
  
- 设置软件-PicGo 设置:

  |       项目        |     示例      |
  | :---------------: | :-----------: |
  |    设置快捷键     | `shift+alt+a` |
  |   打开更新助手    |     `开`      |
  | 接受beta版本更新  |     `开`      |
  |     开机自启      |     `开`      |
  |   时间戳重命名    |     `开`      |
  | 上传后自定复制URL |     `开`      |
  | 请选择显示的图床  |   `GitHub`    |

- 至此，使用 PicGo 搭建 GitHub 图床完毕。

## 图床的使用

完成上述布置后，我们就可以上传图片并获得对应的 markdown 链接了：

- 将现有图片拖拽至上传区完成上传
- 复制现有的图片或复制截图后按alt+shift+a完成快捷上传

> 更多使用与说明参见[官方说明文档](https://picgo.github.io/PicGo-Doc/zh/guide/#picgo-is-here)。



















