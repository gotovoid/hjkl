---
layout: post
title: 理解regex
category: basic
tags: [basic, regex]
---

正则表达式(regex), 是个值得掌握的工具!

组成元素
------

    Combination
        concatenation
        alternation
        grouping
            (non-)captured
            atomic

    Character
        ordinary character
        character class
            range
            negation
            shorthand
            dot

    Quantifier
        *       -   [0, +∞)
        +       -   [1, +∞)
        {N}     -   [N, N]
        {N,M}   -   [N, M]
        {N,}    -   [N, +∞)
        
        greedy(*)
        lazy(*?)
        possessive(*+)

    Anchor
        line boundary
        word boundary
        look around

    Other
        atom
        backreference
        mode

多行模式
------

    MULTI-LINE MODE (OFF)
        ^ - 匹配字符串之首
        $ - 匹配字符串之尾(若末尾的字符为newline，则也会匹配该newline之前)
        
        例：
            "·h·e·l·l·o·\n·w·o·r·l·d·\n·\n·\n·"
             ^                            $  $
        
    MULTI-LINE MODE (ON)
        ^ - 匹配字符串之首，或者newline之后
        $ - 匹配字符串之尾，或者newline之前
        
        例：
            "·h·e·l·l·o·\n·w·o·r·l·d·\n··\n··\n··"
             ^         $  ^         $  ^$  ^$  ^$

等价关系
------

    r'^x$'      ===     r'^^^x$$$'
    r'\bx\b'    ===     r'\b\b\bx\b\b\b'
    r'\b\B'     ===     r'(?!)'

常见错误
------

    r'x$*'
    r'(x*)*'
        sre_constants.error: nothing to repeat

    r'x**'
        sre_constants.error: multiple repeat

    r'x\1'
    r'(?:x)\1'
    r'(?=x)\1'
        sre_constants.error: bogus escape: '\\1'

    r'(x\1)'
        sre_constants.error: cannot refer to open group

