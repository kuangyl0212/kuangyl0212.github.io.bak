# 数星

这是一个使用[Jekyll][jekyll-home] + [GitHub Pages][gh-home] 搭建的个人博客，使用主题[minimal-mistakes][mm-home]

下面简要介绍一下如何使用

### 1. ForkGitHub仓库

在GitHub上fork这个[Repository][repo-link].（当然，首先你需要一个github账号）

### 2. 修改仓库名

在repo的setting选项中修改Repository name为：<你的github用户名>.github.io. 以便你的博客可以在你的github.io的域名下访问，访问地址为：https://your-github-name.github.io
    
![renamm repo]({{ site.url }}/assets/images/rename-repo.png)

### 3. 修改配置文件中必要的字段
    
配置文件为: __config.yml， 你可以直接在github网站上修改也可以下载github desktop或者clone到本地，修改完之后push到github

```yml
# Site Settings
...
name                     : # 你的博客的名字
description              : # 描述
url                      : # the base hostname & protocol for your site e.g. "https://mmistakes.github.io"
baseurl                  : # the subpath of your site, e.g. "/blog"
repository               : # GitHub username/repo-name e.g. "mmistakes/minimal-mistakes"
logo                     : # path of logo image to display in the masthead, e.g. "/assets/images/88x88.png"
disqus                   : # 填你的disqus shortname
# SEO Related
google_site_verification : # 
bing_site_verification   : #

include: ["_pages"]
permalink: /:title/

# Plugins
plugins: 
  - jekyll-feed
  - jekyll-sitemap
  - jekyll-paginate
  - jekyll-seo-tag
  
authors:
    forest:
      name:           # 你的名字
      en_name:        # 英文名（用于链接跳转）
      site:           # 你的主页 如 https://kuangyl0212.github.io
      avatar:         #/assets/images/avatar1.jpg
      bio:            # 你的口号^_^||"万物皆备于我，反身而诚，乐莫大焉！"
      email:          # 邮箱
      twitter:        # 推特


# Archives
#  Type
#  - GitHub Pages compatible archive pages built with Liquid ~> type: liquid (default)
#  - Jekyll Archives plugin archive pages ~> type: jekyll-archives
#  Path (examples)
#  - Archive page should exist at path when using Liquid method or you can
#    expect broken links (especially with breadcrumbs enabled)
#  - <base_path>/tags/my-awesome-tag/index.html ~> path: /tags/
#  - <base_path/categories/my-awesome-category/index.html ~> path: /categories/
#  - <base_path/my-awesome-category/index.html ~> path: /
category_archive:
  type: liquid
  path: /categories/
tag_archive:
  type: liquid
  path: /tags/
# https://github.com/jekyll/jekyll-archives
# jekyll-archives:
#   enabled:
#     - categories
#     - tags
#   layouts:
#     category: archive-taxonomy
#     tag: archive-taxonomy
#   permalinks:
#     category: /categories/:name/
#     tag: /tags/:name/

# Defaults
defaults:

  # all posts
  - scope:
      path: "_posts"
    values:
      layout: post
      author: # 填上你的英文名
      avatar: /assets/images/avatar1.jpg
      
  # all pages
  - scope:
      path: "_pages"
    values:
      layout: page
      
# Syntax
markdown: kramdown
highlighter: rouge

# Paginate
paginate: 10



# Exclude metadata and development time dependencies (like Grunt plugins)
exclude: [README.markdown, package.json, grunt.js, Gruntfile.js, Gruntfile.coffee, node_modules]
```

其他字段按需修改。修改完成以后，如果是在github网页上修改可以直接commit，其他方式需要commit以后push到github。不知道什么是commit？你可能需要补补课了，推荐这个[教程](https://www.liaoxuefeng.com/wiki/896043488029600)。（注意，如果是以SSH协议clone到本地来修改的话，push需要添加你的SSH Key到你的github账号，教程里面也有相关内容。如果嫌麻烦可以在clone的时候改为HTTPS协议，如图，点击Use HTTPS）

![ssh-https]({{site.url}}/assets/images/ssh-https.png)

### 4. 开始写博客

博客文件位于__posts目录下，一个文件代表一篇博客。文件名有讲究，合法的格式有两种：
```
yyyy-mm-dd-Blog-Title.md
yyyy-mm-dd-Blog-Title.textile
```
注意yyyy表示年份，4位数字，mm和dd分别表示月和日，2位数字。从后缀名可以看出，jekyll支持两种文档格式：Markdown和Textile。
每一篇博客必须以一段YAML头信息开始，之后你就可以用Markdown的方式写博客了，不熟悉Markdown语法的话可以参考[这里](https://markdown.tw)，很简单的。
常用的YAML头信息字段如下：
```yml
layout: post  
title:  #"Blog Title"
date:   # yyyy-mm-dd hh:mm:ss +0800
excerpt: # 摘要
categories: # 分类
    - #cat1
    - #cat2
    #...
tags: # 标签
    - #tag1
    - #tag2
    #...
toc: true   # 这是由主题提供的目录
```
其他字段请参考[文档](http://jekyllcn.com/docs/frontmatter/)，更多撰写博客的操作请参考[这里](http://jekyllcn.com/docs/posts/)

博客写完之后提交方式和提交配置文件修改一致，不再赘述。

### 5. 自定义

数星使用的主题是[Mundana](https://github.com/wowthemesnet/mundana-theme-jekyll)。请参考[文档](https://bootstrapstarter.com/bootstrap-templates/mundana-theme-jekyll/)进行自定义。


[repo-link]: https://github.com/kuangyl0212/kuangyl0212.github.io/fork