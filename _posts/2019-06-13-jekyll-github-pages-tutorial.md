---
layout: single
title: Jekyll + GitHub Pages 搭建博客教程
date: 2019-06-13 17:18 +0800 
categories: "教程"
tags: 
    - "Jekyll"
    - "GitHub Pages"
---

### 一、简单的方法

#### 1. ForkGitHub仓库

    在GitHub上fork这个[Repository][repo-link].（当然，首先你需要一个github账号）

#### 2. 修改仓库名

在repo的setting选项中修改Repository name为：<你的github用户名>.github.io. 以便你的博客可以在你的github.io的域名下访问，访问地址为：https://your-github-name.github.io
    
    ![renamm repo]({{ site.url }}/assets/img/rename-repo.png)

#### 3. 修改配置文件中必要的字段
    
    配置文件为: __config.yml， 你可以直接在github网站上修改也可以下载github desktop或者clone到本地，修改完之后push到github

    ```yml
    # Site Settings
    ...
    title                    : # 你的博客的名字
    title_separator          : "-"
    name                     : # 你的名字
    description              : # 描述
    url                      : # the base hostname & protocol for your site e.g. "https://mmistakes.github.io"
    baseurl                  : # the subpath of your site, e.g. "/blog"
    repository               : # GitHub username/repo-name e.g. "mmistakes/minimal-mistakes"
    teaser                   : # path of fallback teaser image, e.g. "/assets/images/500x300.png"
    logo                     : # path of logo image to display in the masthead, e.g. "/assets/images/88x88.png"
    ...
    comments:
        provider             : "disqus" # 不需要评论功能的话改为 false # false (default), , "discourse", "facebook", "staticman", "staticman_v2", "utterances", "custom"
        disqus:
            shortname        : # 你的diqus用户名 别用我的 # https://help.disqus.com/customer/portal/articles/466208-what-s-a-shortname-
    ...
    # Analytics
    analytics:
        provider             : "google" # 不需要的话改为false # false (default), "google", "google-universal", "custom"
            google:
                tracking_id  : # "UA-xxxxxxxxx-1" # 改用你自己的id 不要用我的
                anonymize_ip : # true, false (default)
    ```

    其他字段按需修改。修改完成以后，如果是在github网页上修改可以直接commit，其他方式需要commit以后push到github。不知道什么是commit？你可能需要补补课了，推荐这个[教程](https://www.liaoxuefeng.com/wiki/896043488029600)。（注意，如果是以SSH协议clone到本地来修改的话，push需要添加你的SSH Key到你的github账号，教程里面也有相关内容。如果嫌麻烦可以在clone的时候改为HTTPS协议，如图，点击Use HTTPS）

    ![ssh-https]({{site.url}}/assets/img/ssh-https.png)

#### 4. 开始写博客

    博客文件位于__posts目录下，一个文件代表一篇博客。文件名有讲究，合法的格式有两种：
    ```
    yyyy-mm-dd-Blog-Title.md
    yyyy-mm-dd-Blog-Title.textile
    ```
    注意yyyy表示年份，4位数字，mm和dd分别表示月和日，2位数字。从后缀名可以看出，jekyll支持两种文档格式：Markdown和Textile。
    每一篇博客必须以一段YAML头信息开始，之后你就可以用Markdown的方式写博客了，不熟悉Markdown语法的话可以参考[这里](https://markdown.tw)，很简单的。
    常用的YAML头信息字段如下：
    ```yml
    layout: single  # 注意，数星使用的主题的使用的single作为博客的layout而不是post
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

#### 5. 自定义

    数星使用的主题是[Minimal Mistakes](https://mademistakes.com/work/minimal-mistakes-jekyll-theme/)。请参考[文档](https://mmistakes.github.io/minimal-mistakes/docs/configuration/)进行自定义。


[repo-link]: https://github.com/kuangyl0212/kuangyl0212.github.io/fork