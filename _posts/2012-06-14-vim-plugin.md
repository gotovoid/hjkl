---
layout:     post
title:      vim插件
comments:   true
category:   vim
tags:       [vim, screencast]
published:  true
---

可以通过安装插件来扩展vim的功能. vim的插件, 其实就是用vimscript写的脚本.
当vim启动时, 会自动加载这些插件.

如果感觉到`vimrc`中某个函数, 功能很强大, 并且太占地方,
那么就可以把它提取出来, 包装成一个插件了.

vim有两种形式的插件:

1. 一般插件: 适用于所有类型的文件, 即, 无论编辑什么类型的文件, 都可以使用插件提供的功能.
2. 特种插件: 适用于特定类型的文件, 即, 只有在编辑特定类型的文件时, 该插件才生效.

> 这里的"文件类型", 指的是文件是什么类型的(如:`cpp`, `py`, `conf`等).

安装/卸载"一般插件"的方法:

- 安装插件: 把脚本`name.vim`丢进特定的目录
    - Linux: `~/.vim/plugin`
    - Windows: `C:\Program Files\vim\vimfiles\plugin`
- 卸载插件: 把刚才丢进去的脚本`name.vim`删除
    - Linux: `rm ~/.vim/plugin/name.vim`
    - Windows: `del C:\Program Files\vim\vimfiles\plugin\name.vim`

安装/卸载"特种插件"的方法, 与"一般插件"类似, 只是目录不同

- Linux: `~/.vim/ftplugin`
- Windows: `C:\Program Files\vim\vimfiles\ftplugin`

接下来, 我会介绍一些比较流行的vim插件:

- **pathogen**
- **tabular**
- nerdtree
- snipmate
- sparkup/zencoding
- surround
- ...

---------

pathogen
--------
- 下载地址: <https://github.com/tpope/vim-pathogen>
- 安装路径:
    - Linux: `~/.vim/autoload/pathogen.vim`
    - Windows: `C:\Program Files\vim\vimfiles\autoload\pathogen.vim`
- vimrc配置:

        call pathogen#infect()

- 工作原理:
    - vim启动过程中, 会自动执行`runtimepath`(简称`rtp`)中的一系列脚本. `pathogen`正利用了这一知识点.
    - 它把`~/.vim/bundle/`中的相关文件夹名称, 按照一定的次序添加到了`rtp`中.
    - 这样的话, 每当vim启动时, 就会加载安装在`~/.vim/bundle/`中的插件了.
    - 称之为"病原体"(译名), 很恰当!
- 注意事项:
    - 该插件被安装到了`~/.vim/autoload`文件夹中, vim会对`autoload`中的脚本延迟加载.
    - 需把`filetype plugin indent on`及`syntax on`, 放到`call pathogen#infect()`后面.
        > 为了避免遗漏加载`~/.vim/bundle/*/filetype.vim`等.
    - 安装新插件到`~/.vim/bundle`后, 若该插件含`doc`, 则需运行`:Helptags`命令, 生成`tags`文件.

tabular
-------
- 下载地址: <https://github.com/godlygeek/tabular>
- 安装路径: 使用`pathogen`来管理该插件
    - Linux: `~/.vim/bundle/tabular`
    - Windows: `C:\Program Files\vim\vimfiles\bundle\tabular`

> 若不作特殊说明, 下文一律使用`pathogen`来管理新插件.

--------

视频演示
--------

- vim插件介绍
    - [下载](http://ubuntuone.com/3NAbwQUsuzJNxrThAMurk0)
    - [优酷](http://v.youku.com/v_show/id_XNDEzMDc1NDMy.html)
- pathogen
    - [下载](http://ubuntuone.com/1QFrp0WLPDeVSehPzkPvHw)
    - [优酷](http://v.youku.com/v_show/id_XNDE0MTIxMTk2.html)
- tabular
    - 下载
    - 优酷


**...未完待续...**
