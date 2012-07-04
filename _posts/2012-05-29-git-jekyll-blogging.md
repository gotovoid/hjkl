---
layout:     post
title:      使用github+jekyll写博客
comments:   true
category:   git
tags:       [git, jekyll]
published:  true
---

我曾经使用过很多的blog系统(baidu, sina, sohu, 163, qq, xiaonei...).
一直都是寄人篱下, 文章莫名奇妙被删也是家常便饭.
我也生怕这些网站, 总有一天会倒闭, blog变成了陪葬品.
多年来我苦不堪言, 因为我没有钱去购买blog空间.
最近, 发现了github的pages功能, 完美地解决了我的问题.

使用github写博客的好处:

- 完全免费
- 非常稳定
- 版本控制
- 随心所欲

## 安装软件
    # jekyll框架
    gem install jekyll
    # 解析markdown
    gem install rdiscount
    # 语法高亮
    pip install pygments

## 创建github项目

> 按照[官方文档](http://help.github.com/pages/)所述, 创建一个分支`gh-pages`(必须是这个名字).

    git clone git@github.com:gotovoid/hjkl.git

## 签出代码
    # 从github获取代码
    git fetch origin
    # 创建并切换到分支
    git checkout -b gh-pages origin/gh-pages

## 网站结构
    # 创建文件
    touch README.md _config.yml {index,about,404}.html
    # 创建目录
    mkdir _{includes,layouts,posts,site} css img js
    # 目录结构
    tree -F -L 1
        .
        ├── _includes/
        ├── _layouts/
        ├── _posts/
        ├── _site/
        ├── css/
        ├── img/
        ├── js/
        ├── _config.yml
        ├── index.html
        ├── about.md
        ├── 404.html
        └── README.md

        7 directories, 5 files

## 编辑配置
    vim _config.yml

{% highlight yaml %}
auto:        true
lsi:         false
pygments:    true
markdown:    rdiscount
{% endhighlight %}

## 编辑网页
    vim -p {index,about,404}.html

{% highlight html %}
<h1>hello, world</h1>
<h1>about me</h1>
<h1>404</h1>
{% endhighlight %}

## 评论模块
{% highlight html linenos %}
    <section id="comments">
        <div id="disqus_thread"></div>
        <script type="text/javascript">
            /* * * CONFIGURATION VARIABLES: EDIT BEFORE PASTING INTO YOUR WEBPAGE * * */
            var disqus_shortname = 'your-name'; // required: replace example with your forum shortname
            var disqus_developer = 1;

            /* * * DO NOT EDIT BELOW THIS LINE * * */
            (function() {
                var dsq = document.createElement('script'); dsq.type = 'text/javascript'; dsq.async = true;
                dsq.src = 'http://' + disqus_shortname + '.disqus.com/embed.js';
                (document.getElementsByTagName('head')[0] || document.getElementsByTagName('body')[0]).appendChild(dsq);
            })();
        </script>
        <noscript>Please enable JavaScript to view the <a href="http://disqus.com/?ref_noscript">comments powered by Disqus.</a></noscript>
        <a href="http://disqus.com" class="dsq-brlink">comments powered by <span class="logo-disqus">Disqus</span></a>
    </section>
{% endhighlight%}

## 测试网站
    jekyll --server

## CNAME(可选)
    echo hjkl.me > CNAME

## 提交代码
    echo _site/ > .gitignore
    git add .
    git commit -m 'create my site'
    git push
