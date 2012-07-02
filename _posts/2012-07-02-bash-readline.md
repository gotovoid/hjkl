---
layout:     post
title:      bash命令行编辑
comments:   true
category:   bash
tags:       [bash]
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
    C-] x
    M-C-] x

## 删除

    backspace
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

    C-v
    C-q

    C-x C-e

## 重复

    M-3

## 历史

    history -c
    history -w
    history -r

    <Up>
    <Down>

    C-r
    C-s

    !!
    !-2
    !!:0
    !!:^
    !!:0-4
    !!:*
    !!:$
    !#:$

    ^foo^bar
    !!:gs/foo/bar

