---
layout:     post
title:      谈谈vim的语法侦测
comments:   true
category:   vim
tags:       [vim]
published:  true
---

介绍
---

在`vimrc`文件中, 往往会有下面两句配置:

    filetype plugin indent on
    syntax on

这两句都是与语法高亮相关的.

第一句的作用是, 启用语法检测功能, 并且在语法检测成功后, 加载与该语法相关的ftplugin及indent脚本.
打开/新建文件时, vim会根据文件名及扩展名, 推测文件类型.
如果无法推测的话, 会尝试根据文件内容(如第一行), 进一步推测文件类型.

这是为什么当你打开一个没有扩展名的python脚本文件时, vim仍然可以识别的原因.

    $ vim hello
    #!/usr/bin/env python
    def hello():
        print("hello, world!")
        
第二句的作用是, 启用语法高亮. 具体细节本文暂不讨论, 我会专门写一篇文章.

----

在Ubuntu 12.04系统中, vim被安装到/usr/share/vim/vim73目录下;
在Windows XP系统中, vim被安装到C:\Program Files\vim\vim73目录下.
值得我们注意的文件有`filetype.vim`及`indent.vim`, 下面我就来简单介绍这两个文件.

filetype.vim
-------------

用来侦测文件类型(即, 判断是C++还是java代码, 还是其他).
打开该文件后, 可以看到很多这样的语句:

    " awk "
    au BufNewFile,BufRead *.awk             setf awk
    " Java "
    au BufNewFile,BufRead *.java,*.jav      setf java
    " Makefile "
    au BufNewFile,BufRead [mM]akefile*      call s:StarSetf('make')


这些语句是用来根据文件名/扩展名, 推测文件类型的. 

indent.vim
----------

用来控制与语法相关的缩进的. 定义了`s:LoadIndent`函数, 并且注册了`FileType`事件.
只要`filetype`设置发生改变, 就会自动运行`s:LoadIndent`函数.
在`s:LoadIndent`函数中, 首先判断所需要执行的动作(启用/停用语法缩进功能), 然后执行相应动作.
值得注意的是`runtime! indent/name.vim`, `runtime!`命令会到`runtimepath`中, 查找所有的`indent/name.vim`,
并且逐个运行这些`name.vim`, 其中`runtimepath`类似与Windows/Linux的`PATH`环境变量.

可以通过以下命令察看`filetype(ft)`/`runtimepath(rtp)`的值:

    :set ft?
    :set rtp?
    
- `ft`是当前buffer的语法类型名称(java, cpp, python等等), `ft`也可能为空.
- `rtp`由一些用逗号分割的路径组成, 其实`pathogen.vim`插件, 就是通过操作`rtp`来实现vim插件管理的.

应用
----

在vimrc中, 要加上那两句后, 往往就可以解决大部分与语法高亮相关的问题了. 但是不排除有特殊情况发生.

如果打开一个python文件后, 发现识别语法类型失败, 或者张冠李戴. 可以通过下面的的命令手动解决:

    :set ft=python

说明
----
本文涉及到vim的内部运作流程, 如果你没看懂, 也没关系.
如果你想要写个像样的vim插件, 最好还是深入了解一下.
由于动手实践的地方比较多, 计划把本文制作成视频, 也许会更容易理解.

