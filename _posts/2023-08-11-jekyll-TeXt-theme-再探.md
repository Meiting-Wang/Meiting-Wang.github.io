---
title: jekyll-TeXt-theme 再探
show_author_profile: true
tags: jekyll blog-build jekyll-TeXt-theme
---

依据以下资料：

- [jekyll-TeXt-theme中文官方教程](https://kitian616.github.io/jekyll-TeXt-theme/docs/zh/quick-start)
- [Yulei's blog-用 Github pages 和 Jekyll 搭建博客](https://yuleii.github.io/2020/06/09/build-blog-with-github-pages-and-jekyll.html)
- [error's blog-使用 GitHub Page + Jekyll + TeXt theme 制作博客](https://zhuanlan.zhihu.com/p/385384830)

本文对 jekyll-TeXt-theme 再做进一步使用，并将其形成文档于此。

## Jekyll 目录结构

| 文件或文件夹 | 含义                          |
| :----------- | :---------------------------- |
| _posts/      | 博客内容                      |
| _pages/      | 其他需要生成的网页，如About页 |
| _layouts/    | 网页排版模板                  |
| _includes/   | 模板包含的HTML片段等          |
| _data/       | 动态数据                      |
| _sites/      | 最终生成的静态网页            |
| _config.yml  | 网站全局配置信息              |
| index.html   | 网站入口                      |

## 网站配置

我们可以在根目录的*_config.yml*文件中对网站进行全局配置，常用的变量有：

| 变量              | 含义         | 示例                              |
| :---------------- | :----------- | :-------------------------------- |
| `text_skin`       | 网站皮肤     | `text_skin: default`              |
| `highlight_theme` | 代码高亮主题 | `highlight_theme: default`        |
| `title`           | 网站的标题   | `title: Meiting-Wang`             |
| `description`     | 网站描述     | `description: Truth sets us free` |
| `lang`            | 网站的语言   | `lang: zh`                        |
| `timezone`        | 网站时区     | `timezone: Asia/Shanghai`         |
| author            | 网站作者     | --                                |
|                   |              |                                   |
|                   |              |                                   |
|                   |              |                                   |
|                   |              |                                   |
|                   |              |                                   |
|                   |              |                                   |

## YAML 头信息

YAML 头信息必须放在文章开头部分，以实现对文章的局部设定，例如：

```markdown
---
title: Document - Writing Posts
mathjax: true
---
```

在这里可以设置在_config.yml文件中预定义的变量和针对文章特有的变量，常用的变量有：

| 变量                  | 含义                   | 示例                        |
| --------------------- | ---------------------- | --------------------------- |
| `show_author_profile` | 在文章末尾展示作者信息 | `show_author_profile: true` |
|                       |                        |                             |
|                       |                        |                             |

