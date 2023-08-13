---
title: jekyll-TeXt-theme 再探
tags: jekyll blog-build jekyll-TeXt-theme
---

依据以下资料：

- [jekyll-TeXt-theme中文官方教程](https://kitian616.github.io/jekyll-TeXt-theme/docs/zh/quick-start)
- [Yulei's blog-用 Github pages 和 Jekyll 搭建博客](https://yuleii.github.io/2020/06/09/build-blog-with-github-pages-and-jekyll.html)
- [error's blog-使用 GitHub Page + Jekyll + TeXt theme 制作博客](https://zhuanlan.zhihu.com/p/385384830)

本文对 jekyll-TeXt-theme 再做进一步使用，并将其形成文档于此。

<!--more-->

## Jekyll 目录结构

| 文件或文件夹  | 含义                          |
| :------------ | :---------------------------- |
| *_posts/*     | 博客内容                      |
| *_pages/*     | 其他需要生成的网页，如About页 |
| *_layouts/*   | 网页排版模板                  |
| *_includes/*  | 模板包含的HTML片段等          |
| *_data/*      | 动态数据                      |
| *_sites/*     | 最终生成的静态网页            |
| *_config.yml* | 网站全局配置信息              |
| *index.html*  | 网站入口                      |

## 网站配置

我们可以在根目录的 *_config.yml* 文件中对网站进行全局配置，常用的变量有：

| 变量                 | 含义               | 示例                                              |
| :------------------- | :----------------- | :------------------------------------------------ |
| `text_skin`          | 网站皮肤           | `text_skin: default`                              |
| `highlight_theme`    | 代码高亮主题       | `highlight_theme: default`                        |
| `title`              | 网站的标题         | `title: Meiting-Wang`                             |
| `description`        | 网站描述           | `description: Truth sets us free`                 |
| `lang`               | 网站的语言         | `lang: zh`                                        |
| `timezone`           | 网站时区           | `timezone: Asia/Shanghai`                         |
| `author`             | 网站作者           | `--`                                              |
| `repository`         | GitHub 源码仓库    | `repository: Meiting-Wang/Meiting-Wang.github.io` |
| `repository_tree`    | GitHub 仓库分支    | `repository_tree: main`                           |
| `toc: selectors`     | 文章目录           | `toc: selectors: h1,h2,h3`                        |
| `mathjax`            | 数学公式           | `mathjax: true`                                   |
| `mathjax_autoNumber` | 数学公式的自动编号 | `mathjax_autoNumber: true`                        |
| `mermaid`            | 文档图形           | `mermaid: true`                                   |
| `chart`              | 统计图表           | `chart: true`                                     |
| `paginate`           | 每页显示的文章数   | `paginate: 8`                                     |
| `comments`           | 评论               | `--`                                              |
| `pageview`           | 文章点击量         | `--`                                              |

## YAML 头信息

YAML 头信息必须放在文章开头部分，以实现对文章的局部设定，例如：

```markdown
---
title: Document - Writing Posts
mathjax: true
---
```

在这里可以设置在_config.yml文件中预定义的变量和针对文章特有的变量，常用的变量有：

| 变量                  | 含义                   | 示例                               |
| --------------------- | ---------------------- | ---------------------------------- |
| `show_author_profile` | 在文章末尾展示作者信息 | `show_author_profile: true`        |
| `permalink`           | 永久链接               | `permalink: /docs/en/quick-start:` |

## 导航栏配置

在 TeXt 中有两种导航栏：**头部导航栏**（Header Navigation）和**侧边栏导航栏**（Sidebar Navigation），它们均在 *_data/navigation.yml* 中配置。

### 头部导航栏

头部导航栏在 *_data/navigation.yml* 文件的 `header` 项定义，它是一个包含标题和 URL 项的数组。我自己设置的头部导航栏如下：

```yaml
header:
  - title:      LaTeX
    url:        /latex/begin
  - title:      Stata
    url:        /stata/begin
  - titles:
      # @start locale config
      en      : &EN       Archive
      en-GB   : *EN
      en-US   : *EN
      en-CA   : *EN
      en-AU   : *EN
      zh-Hans : &ZH_HANS  归档
      zh      : *ZH_HANS
      zh-CN   : *ZH_HANS
      zh-SG   : *ZH_HANS
      zh-Hant : &ZH_HANT  歸檔
      zh-TW   : *ZH_HANT
      zh-HK   : *ZH_HANT
      ko      : &KO       아카이브
      ko-KR   : *KO
      fr      : &FR       Archives
      fr-BE   : *FR
      fr-CA   : *FR
      fr-CH   : *FR
      fr-FR   : *FR
      fr-LU   : *FR
      tr      : &TR       Arşivdekiler
      # @end locale config
    url: /archive.html
  - titles:
      # @start locale config
      en      : &EN       About
      en-GB   : *EN
      en-US   : *EN
      en-CA   : *EN
      en-AU   : *EN
      zh-Hans : &ZH_HANS  关于
      zh      : *ZH_HANS
      zh-CN   : *ZH_HANS
      zh-SG   : *ZH_HANS
      zh-Hant : &ZH_HANT  關於
      zh-TW   : *ZH_HANT
      zh-HK   : *ZH_HANT
      ko      : &KO       소개
      ko-KR   : *KO
      fr      : &FR       À propos
      fr-BE   : *FR
      fr-CA   : *FR
      fr-CH   : *FR
      fr-FR   : *FR
      fr-LU   : *FR
      tr      : &TR       Hakkında
      # @end locale config
    url: /about.html
  - title:      GitHub
    url:        https://github.com/Meiting-Wang/Meiting-Wang.github.io
```

### 侧边导航栏

要想在某篇文章或页面中使用侧边栏导航栏，首先你需要在 *_data/navigation.yml* 中定义一个导航栏，如我想设置导航栏 `latexs-nav` 和 `statas-nav`：

```yaml
latexs-nav:
  - title:      LaTeX 开始
    children:
      - title:  LaTeX 开始 1
        url:    /latex/begin
      - title:  LaTeX 开始 2
        url:    /latex/begin2
      - title:  LaTeX 开始 3
        url:    /latex/begin3
  - title:      LaTeX 其次
    children:
      - title:  LaTeX 其次 1
        url:    /latex/next
      - title:  LaTeX 其次 2
        url:    /latex/next2
      - title:  LaTeX 其次 3
        url:    /latex/next3

statas-nav:
  - title:      Stata 开始
    children:
      - title:  Stata 开始 1
        url:    /stata/begin
      - title:  Stata 开始 2
        url:    /stata/begin2
      - title:  Stata 开始 3
        url:    /stata/begin3
  - title:      Stata 其次
    children:
      - title:  Stata 其次 1
        url:    /stata/next
      - title:  Stata 其次 2
        url:    /stata/next2
      - title:  Stata 其次 3
        url:    /stata/next3
```

然后在文章的 YAML 头信息中放入以下内容，即可将定义的导航栏作为该文章的导航栏，如我需要在某篇文章中将上面定义的 `latexs-nav` 作为侧边导航栏：

```yaml
sidebar:
  nav: latexs-nav
```

## 撰写普通博客

普通博客所有的文章都在 */_posts* 文件夹中。这些文件可以用 Markdown 或 HTML 编写。撰写一篇普通博客，无非就是在 */_posts* 文件中创建一个新文件。Jekyll 要求一篇普通博客的文件名需遵循以下格式：

```text
年-月-日-标题.MARKUP
```

下面是一些合法的文件名的例子：

```text
2011-12-31-new-years-eve-is-awesome.md
2012-09-12-how-to-write-a-blog.markdown
```

所有博客文章顶部必须有一段 YAML 头信息(YAML front-matter)，如

```yaml
---
layout: article
title: Document - Writing Posts
mathjax: true
---
```

然而，一般而言，我们可以在 *_config.yaml* 为这类普通博客全局设定一些默认值，如：

```yaml
defaults: #为对应的部分设置默认值
  ## posts
  - scope:
      path: ""
      type: posts
    values:
      layout: article
      sharing: true
      license: true
      aside:
        toc: true
      show_edit_on_github: true
      show_subscribe: true
      pageview: false
```

当然，优先级为局部设定（文章本身的 YAML 头信息）>全局设定。

## 撰写 Docs

撰写这类文章会与前面撰写普通博客不一样，而且一般都会伴随着头部导航栏和侧边导航栏。下面以我想部署一个 LaTeX Docs 为例，给出流程（示例）：

- 在根目录下新建 *_latex* 文件夹

- 在里面写一些文章，它们的 YAML 头信息为

  ```yaml
  # 第一篇文章
  ---
  title: LaTeX 开始 1
  permalink: /latex/begin
  date: 2023-08-12
  ---
  
  # 第二篇文章
  ---
  title: LaTeX 开始 2
  permalink: /latex/begin2
  date: 2023-08-12
  ---
  
  # 第三篇文章
  ---
  title: LaTeX 开始 3
  permalink: /latex/begin3
  date: 2023-08-12
  ---
  
  # 第四篇文章
  ---
  title: LaTeX 其次 1
  permalink: /latex/next
  date: 2023-08-13
  ---
  
  # 第五篇文章
  ---
  title: LaTeX 其次 2
  permalink: /latex/next2
  date: 2023-08-13
  ---
  
  # 第六篇文章
  ---
  title: LaTeX 其次 3
  permalink: /latex/next3
  date: 2023-08-13
  ---
  ```

- 在 *_data/navigation.yml* 文件中为以上文章部署一个头部导航栏：

  ```yaml
  header:
    - title:      LaTeX
      url:        /latex/begin
  ```

- 在 *_data/navigation.yml* 文件中为以上文章部署侧边导航栏 `latexs-nav`：

  ```yaml
  latexs-nav:
    - title:      LaTeX 开始
      children:
        - title:  LaTeX 开始 1
          url:    /latex/begin
        - title:  LaTeX 开始 2
          url:    /latex/begin2
        - title:  LaTeX 开始 3
          url:    /latex/begin3
    - title:      LaTeX 其次
      children:
        - title:  LaTeX 其次 1
          url:    /latex/next
        - title:  LaTeX 其次 2
          url:    /latex/next2
        - title:  LaTeX 其次 3
          url:    /latex/next3
  ```

- 在 *_config.yaml* 上面系列文章添加 collections:

  ```yaml
  collections:
    latex:
      output: true
  ```

- 为目录 */_latex* 下所有文章设置以下默认格式：

  ```yaml
  defaults: #为对应的部分设置默认值
    ## _latex
    - scope:
        path: "_latex"
      values:
        layout: article
        nav_key: latex
        sidebar:
          nav: latexs-nav
        license: true
        aside:
          toc: true
        show_edit_on_github: true
        show_date: true
        # lightbox: true
  ```

- 至此，LaTeX Docs 部署完毕，编译后效果如下：

  ![image-20230813183916358](https://cdn.staticaly.com/gh/Meiting-Wang/pictures@main/picgo/202308131839412.png){:.shadow}



















































































