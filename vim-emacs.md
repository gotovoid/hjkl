---
layout:    default
title:     Vim Emacs
comments:  true
---

## File 

    VIM         EMACS
    ━━━━━━━━━━━━━━━━━
    :e file     C-x C-f file
    :w          C-x C-s
    :w file     C-x C-w file
    :wa         C-x s
    :r file     C-x i

## Motion 

    VIM         EMACS
    ━━━━━━━━━━━━━━━━━
    h           C-b
    j           C-n
    k           C-p
    l           C-f
    e           M-f
    b           M-b
    0           C-a
    ^           M-m
    $           C-e
    (           M-a
    )           M-e
    {           M-{
    }           M-}
    C-f         C-v
    C-b         M-v
    gg          M-<
    G           M->
    H           M-0 M-r
    M           M-r
    L           M-- M-r

## Change 

    VIM         EMACS
    ━━━━━━━━━━━━━━━━━
    o           C-e C-j
    O           C-a C-o
    x           C-d
    de          M-d
    dd          C-a C-k
                C-S-<BS>
                C-e C-0 C-k
    iC-w        M-<BS>
    yy          C-a C-k C-y
                C-a C-<SPACE> C-e M-w
    p           C-y
    u           C-x u
                C-/
                C-_
    >>          C-4 C-x <TAB>
    <<          C--4 C-x <TAB>
    R           <INS>
    dfx         M-z x
    C-n         M-/
    iC-q        C-q
    iC-v
    :retab!     M-x untabify

## Search/Replace 

    VIM         EMACS
    ━━━━━━━━━━━━━━━━━
    /           C-s
                M-C-s
    ?           C-r
                M-C-r
    n           C-s
    N           C-r
    :s///c      M-%
                M-C-%
    :vimgrep    M-x occur
                M-s o

## Visual

    VIM         EMACS
    ━━━━━━━━━━━━━━━━━
    v           C-<SPACE>
    gv          C-x C-x
    ggVG        C-x h
    vap         M-h
    vas         M-a C-<SPACE> M-e
    viw         M-b C-<SPACE> M-f

## Window/Buffer 

    VIM         EMACS
    ━━━━━━━━━━━━━━━━━
    :bd         C-x k
    C-^         C-x b
    :ls!        C-x C-b
    C-w c       C-x 0
    C-w q
    :q
    C-w o       C-x 1
    :on
    C-w s       C-x 2
    :sp
    C-w v       C-x 3
    :vsp
    :new file   C-x 4 f file
    :tabe file  C-x 5 f file
    C-w w       C-x o

## Setting 

    VIM         EMACS
    ━━━━━━━━━━━━━━━━━
    :set ft=foo M-x foo-mode
                M-x set-variable
                M-x customize

## Shell 

    VIM         EMACS
    ━━━━━━━━━━━━━━━━━
    :%w !cmd    M-|
    :%!cmd      C-u M-|
    :!cmd       M-!
    :r !cmd     C-u M-!

## Help 

    VIM         EMACS
    ━━━━━━━━━━━━━━━━━
    :h          C-h r
    :h foo      C-h a foo
                C-h v foo
    :h Ctrl-a   C-h k C-a
                C-h c C-a

## Config

    VIM         EMACS
    ━━━━━━━━━━━━━━━━━
    set nu      (global-linum-mode t)
    set cul     (global-hl-line-mode t)
    set wmnu    (ido-mode t)
    set list    (setq-default show-trailing-whitespace t)
    set ts=4    (setq-default tab-width 4)
    set et      (setq-default indent-tabs-mode nil)
    so code.vim (load "code.el")
