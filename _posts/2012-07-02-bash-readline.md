---
layout:     post
title:      bash命令行编辑
comments:   true
category:   bash
tags:       [bash, beta, screencast]
published:  true
---

## 设置

    set +o vi
    set -o emacs

## 移动

    ←           →
    C-a         C-e
    C-b         C-f
    M-b         M-f
    C-]         M-C-]
    C-space     C-x-x

## 删除

    C-h         Backspace
    C-d         Delete
    C-w         M-Backspace(ESC Backspace)
    C-u         C-k
    M-d
    M-\

## 粘贴

    C-y         M-y

## 取消

    C-_         M-r

## 编辑

    C-t         M-t
    C-v         C-q
    M-c         M-l         M-u
    M-#
    C-x C-e

## 重复/宏

    M-num
    C-x (       C-x )       C-x e

## 历史(beta)

    history -c/w/r
    <Up>        <Down>
    C-p         C-n
    M-.
    C-r         C-s
    
    !!
    !-2
    !foo

    !!:0
    !!:^
    !!:0-4
    !!:*
    !!:$

    !!:p

    !#:$

    ^foo^bar
    !!:gs/foo/bar

## 参考

- <http://www.gnu.org/software/bash/manual/bashref.html#Command-Line-Editing>
- <http://www.catonmat.net/blog/bash-emacs-editing-mode-cheat-sheet/>
