---
layout:     post
title:      vimrc入门
comments:   true
category:   vim
tags:       [vim]
published:  true
---

在*nix系统中, 功能比较多的软件, 通常都有一个或多个配置文件.
如果软件名为`xxx`, 那么其配置文件名通常为`xxxrc`(`rc`是`run command`的简称).
系统范围内的配置一般位于`/etc/xxx/xxxrc`, 而用户配置则位于`~/.xxxrc`.

比如, 安装完vim后, 其系统配置为`/etc/vim/vimrc`, 用户配置为`~/.vimrc`.
其中, `~/.vimrc`需要自己创建, 因为它不是必须的, 没有它, vim照样可以运行.

值得注意的是, 修改`/etc/vim/vimrc`, 会影响到计算机上的所有用户.
并且, 在vim升级时, 也可能被覆盖掉. 因此不建议直接修改`/etc/vim/vimrc`.

如果你的登陆名为`hjkl`, 你的`HOME`目录一般为`/home/hjkl`(简写为`~`).
只要在`HOME`目录下, 创建`.vimrc`即可(注意: 该文件是隐藏的).
网上大家所讨论的`vimrc`, 一般就是指`~/.vimrc`.
如果不作特殊说明, 下文所说的`vimrc`, 也指`~/.vimrc`.

如果你还没有创建`~/.vimrc`, 你可以参考这个简单范本:

    " 使用非兼容模式(该设置会影响其他设置, 需要放在第一行)
    set nocompatible
    " 在左侧显示行号
    set number
    " 启用文件类型侦测功能, 并且加载与之对应的plugin及indent脚本
    filetype plugin indent on
    " 启用语法高亮功能
    syntax on

`vimrc`中包含的所有命令, 都可以通过`:command args`的形式在vim中手动运行.
`vimrc`的目的是为了, 减轻用户的负担, 自动运行其中的命令, 而不需要手动干预.

在启动vim时, vim会自动逐行运行`vimrc`中的命令(行业术语称之为`source`).
vim启动完毕后, 无论是打开新文件, 分割Window, 而是打开新Tabpage, `vimrc`都不会再次被运行了.
如果你修改了`vimrc`, 需要手动运行`:source ~/.vimrc`后, 你的修改才生效.

vim提供了几百个`option`(随着新版本发布, 会不断增加), 都可以通过`:set`命令来进行设置.
如果你没有设置某个`option`, 那么该`option`将采用默认值(请查看帮助文档).

另外, 你可以在`vimrc`中定义函数, 例如:

    fun! IncFontSize(inc)
        if !exists('+guifont')
            return
        endif
        let s:defaultfont = 'Ubuntu Mono 12'
        if a:inc==0 || empty(&guifont)
            let &guifont = s:defaultfont
            return
        endif
        let &guifont = substitute(&guifont, '\d\+$', '\=submatch(0)+'.a:inc, '')
    endfun
    
我定义了一个函数`IncFontSize()`, 你可以在vim中输入`:call IncFontSize(1)`来增大字体.

你也可以定义一些键盘快捷键, 来执行指定的命令, 例如:

    nnoremap <C-kPlus>     : call IncFontSize(+1)<CR>
    nnoremap <C-kMinus>    : call IncFontSize(-1)<CR>
    nnoremap <C-k0>        : call IncFontSize(0)<CR>

定义了快捷键后, 你就可以按<kbd>Ctrl-kPlus</kbd>/<kbd>Ctrl-kMinus</kbd>/<kbd>Ctrl-k0</kbd>,
来调用函数`IncFontSize()`对字体进行"增大/缩小/复位"了.

> kPlus/kMinus/k0指的是, 键盘右侧数字键区的+/-/0键.

本文简要地介绍了`vimrc`的作用, 以及如何自定义`vimrc`.
如果你有什么疑惑的话, 请留言, 我很乐意解答.
