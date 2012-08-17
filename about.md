---
layout:    default
title:     About
comments:  true
---

![flair](http://stackoverflow.com/users/flair/348785.png)
![vim](/img/love-vim.gif)
![gmail](/img/gmail.png)

> [vim官网](http://www.vim.org/)被墙，我憎恨中共!  
> 中共的本质是独裁!  
> 天朝山寨奇异国必亡!  
> 穷则独善其身, 达则兼济天下!  

---------------------------------
      
    1   1   1   1   1
    1   2   3   4   5
    1   3   6   10  15
    1   4   10  20  35
    1   5   15  35  ?

    $ python
    >>> def f(n,m):
    ...   if n==1 or m==1:
    ...     return 1
    ...   else:
    ...     return f(n,m-1)+f(n-1,m)
    ... 
    >>> f(5,5)
    ?
    
    $ scheme
    >>> (define s1 (cons-stream 1 s1))
    >>> (define s2 (cons-stream 1 (add-streams (cdr-stream s1) s2)))
    >>> (define s3 (cons-stream 1 (add-streams (cdr-stream s2) s3)))
    >>> (define s4 (cons-stream 1 (add-streams (cdr-stream s3) s4)))
    >>> (define s5 (cons-stream 1 (add-streams (cdr-stream s4) s5)))
    >>> (stream-ref s5 5)
    ?
