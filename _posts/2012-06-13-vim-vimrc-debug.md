---
layout:     post
title:      vimrc调试
comments:   true
category:   vim
tags:       [vim]
published:  true
---

当`vimrc`包含的命令比较多时, 难免有差错. 这时就需要使用各种方法, 调试`vimrc`了.
本文同样适用于, 那些想对`vimrc`有深入了解的vim用户.
如果你刚刚学会使用vim, 本文会为你以后的学习, 打下扎实的基础.

在Terminal中
------------

### 不加载vimrc

    $ vim -u NORC

### 不加载vimrc及plugin

    $ vim -N -u NONE

> 在不使用`vimrc`时, vim默认以compatible形式启动, 因此加上`-N`选项.

### 加载其他vimrc

    $ vim -u myvimrc

### 全程记录log

    $ vim -V9vim.log

> `-V20vim.log`由3部分组成(即, 选项:`-V`, 级别:`9`, log文件:`vim.log`), 之间无空格.  
> 不同的级别, log的详细程度不同.

### 加载vimrc前, 执行命令

    $ vim --cmd 'set verbose=9 verbosefile=vim.log'

### 加载vimrc后, 执行命令

    $ vim -c 'set binary'

### 使用环境变量作为vimrc

    $ VIMINIT='set number' vim

> 启动vim时, 传入环境变量`VIMINIT`, vim就会忽略`~/.vimrc`了.

在vim中
-------

### 查看vimrc文件名
    
    :echo $MYVIMRC

### 查看所有已加载的脚步

    :scriptnames

> `vimrc`会排在前面, 除非被你禁用了.

### 调试vimrc

    :debug source $MYVIMRC

说明
----

暂时想到这么多, 我会不断更新本文.
