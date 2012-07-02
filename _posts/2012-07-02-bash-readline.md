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

    C-a
    C-e

    C-b
    C-f

    M-b
    M-f

    C-space
    C-x x

    C-] x
    M-C-] x

## 删除

    <backspace>
    M-backspace

    C-h
    C-w

    C-d
    M-d

    C-u
    C-k

    M-\

## 粘贴

    C-y
    M-y

## 撤消

    C-_
    M-r

## 改变

    C-t
    M-t

    M-c
    M-l
    M-u

## 输入

    <Tab>

    C-l

    C-c

    C-v
    C-q

    M-#

    C-x C-e

## 重复

    M-3

    C-x (
    C-x )
    C-x e

## 历史

    history -c
    history -w
    history -r

    <Up>
    <Down>
    
    C-p
    C-n
    
    M-.

    C-r
    C-s

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
