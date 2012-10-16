---
layout: post
title: 在vim中运行外部程序
category: vim
tags: [vim, shell, python]
---

本文介绍如何在vim中调用外部程序：

## 运行外部程序
    :!cmd
    :silent !cmd
    ------------
    :!mkdir fold
    :silent !rm #☆

## 使用外部filter程序★
    !!cmd
    !{motion}cmd
    :{range}!cmd
    ------------
    !!base64 -d
    !Gcat -n
    :%!sort

## 读入外部程序结果★
    :[addr]r!cmd
    ------------
    :0r!seq 10
    :r!date +'\%F \%T'☆

## 以指定输入调用外部程序
    :[range]w !cmd†
    ------------
    :w !wc -w

## 使用python命令★‡
    :py cmd
    ------------
    :py from vim import *
    :py from random import shuffle
    :py shuffle(current.buffer)

注:

- ★ 可能会改变buffer
- ☆ 需对%及#进行转意
- † w后的空格不可省略
- ‡ 需指定版本的python
