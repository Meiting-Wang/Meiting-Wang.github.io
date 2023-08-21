---
title: Typora 与 Picgo 的结合
permalink: /3c8b48eb133ed3dca5f38a5c790525ae
category: Post
tags: 
  - 图床
---

在文章[使用 PicGo 搭建 GitHub 图床](https://meiting-wang.github.io/22eff2fef46c2db79a045167bc3b620b.html)，我们介绍了使用 PicGo 搭建 GitHub 图床的过程。事实上，PicGo还可以与很多其他的软件进行结合。在这里，我们将对 PicGo 与 markdown 编辑器 Typora 的结合进行阐述。

<!--more-->

## 设置流程

- 按照文章[使用 PicGo 搭建 GitHub 图床](https://meiting-wang.github.io/22eff2fef46c2db79a045167bc3b620b.html)配置软件 PicGo
- 打开软件 Typora
- 进入文件>偏好设置>图像
  - **插入图片时**：选择**上传图片**，并在“对本地位置的图片应用上述规则”前打钩
  - **上传服务设定**：**上传服务**选择 **PicGo(app)**；**PicGo 路径**选择 **PicGo.exe 文件的路径**
  - 上面设置完毕后，点击**验证图片上传选项**，验证以上选项是否生效。
  - 本部分设置好后如下图所示：
  
    ![image-20230808215648644](https://cdn.staticaly.com/gh/Meiting-Wang/pictures@main/picgo/202308082156676.png){:.shadow}
- 至此，设置完毕

## 使用流程

我们可以通过以下两种方式进行使用：

- 将图片拖拽至 Typora 编辑器中，图片将自动完成上传，并在编辑器中生成 Markdown 图片链接；
- 复制图片后，ctrl+v 将图片粘贴至 Typora 编辑器中，图片将自动完成上传，并在编辑器中生成 Markdown 图片链接。
