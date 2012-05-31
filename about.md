---
layout: default
title: About
comments: true
---

![flair](http://stackexchange.com/users/flair/141612.png)

![gmail](/img/gmail.png)

----

## 本站及本人
__godaddy__域名50RMB/年, __github__免费托管.  

本网站基于[jekyll][1]框架,
使用markdown写完文章后, 直接上传的github, 然后由github自动生成HTML.
因此全部页面都是静态的HTML, 没有后台数据库.
整个国内过程非常简单, 你不妨[尝试][1]一下!

讲述程序员自己的故事, 用行动证明自己的存在!  
少说一点废话, 多干一点实事.  
XXX制造问题, 程序员解决问题.

----

## 关于**命令行**
**命令行**刷新了我对_程序/软件_的理解: **命令行**是解决问题的最短路径!  
**命令行**让你看清事物的本质, 明确自己的目的, 最终完美地解决问题!  
如果你崇尚简约, 那么**命令行**是你杀手锏!

----

git push失败了吗?

## 突破封锁, 连接github
### SSH Tunnel
{% highlight bash %}
$ plink -N -L 2222:github.com:22 -pw 5736f    usassh@free.usassh.com
#             ---- -------------     -----    ------ ---------------
#              |        |              |         |         |
#              |        |              |         |         |
#              |        |              |         |         |
#             本地   github          SSH密码  SSH用户名 SSH服务器
{% endhighlight %}

### 修改配置
{% highlight bash %}
$ vim .git/config
[remote "origin"]
	fetch = +refs/heads/*:refs/remotes/origin/*
    url = ssh://git@localhost:2222/username/project.git
{% endhighlight %}

### 上传代码
{% highlight bash %}
$ git push
{% endhighlight %}

[1]: http://hjkl.me/github/2012/05/29/jekyll.html
