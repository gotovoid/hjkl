---
layout:     post
title:      谈谈vim语法高亮
comments:   true
category:   vim
tags:       [vim]
published:  true
---

本文是[谈谈vim的语法侦测]({% post_url 2012-06-04-vim-filetype %})的续集.
讲解`:syntax`命令的用法, 以及内部实现.


涉及到的文件全部位于`$VIMRUNTIME/syntax/`目录下:

- syntax.vim
- manual.vim
- synload.vim
- syncolor.vim
- nosyntax.vim

----

    | 命令        | 实现                         | 说明                                |
    |-------------|------------------------------|-------------------------------------|
    | :syn on     | g:syntax_cmd = 'on'          | 监听FileType事件, 一旦ft有变化,     |
    |             | runtime! syntax/syntax.vim   | 立刻执行:set syntax=ft;             |
    |             |                              | 如果filetype.vim尚未执行, 则执行之; |
    |             |                              | 手动触发filetypedetect.BufRead;     |
    |-------------|------------------------------|-------------------------------------|
    | :syn enable | g:syntax_cmd = 'enable'      | :syn enable与:syn on的区别表现在,   |
    |             | runtime! syntax/syntax.vim   | 执行syncolor.vim                    |
    |-------------|------------------------------|-------------------------------------|
    | :syn manual | runtime! syntax/manual.vim   | 取消监听FileType事件,               |
    |             | g:syntax_manaul = 1          | ft与syn将失去关联.                  |
    |-------------|------------------------------|-------------------------------------|
    | :syn reset  | g:syntax_cmd = 'reset'       | syncolor.vim执行时,                 |
    |             | runtime! syntax/syncolor.vim | 会根据g:syntax_cmd的不同,           |
    |             |                              | 而执行不同的代码                    |
    |-------------|------------------------------|-------------------------------------|
    | :syn off    | runtime! syntax/nosyntax.vim | 取消与Syntax事件绑定的所有代码      |
    |             | unlet syntax_on              |                                     |
    |             | unlet syntax_manual          |                                     |
