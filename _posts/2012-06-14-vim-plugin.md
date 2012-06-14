---
layout:     post
title:      vim插件
comments:   true
category:   vim
tags:       [vim]
published:  true
---

可以通过安装插件来扩展vim的功能.
vim的插件, 其实就是用vimscript写的脚本.
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

接下来, 我会介绍一些比较著名的vim插件:

- pathogen
- nerdtree
- snipmate
- sparkup/zencode
- surround
- ...

我想问一下大家, 要不要制作一系列关于`vim插件`的视频.
也许, 通过看视频演示, 才能快速地了解插件的用途.

...等待大家答复中...

视频演示
--------

- vim插件介绍
    - [下载](http://ubuntuone.com/3NAbwQUsuzJNxrThAMurk0)
    - [优酷](http://v.youku.com/v_show/id_XNDEzMDc1NDMy.html)
