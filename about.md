---
layout:    default
title:     About
comments:  true
---

![vim](/img/love-vim.gif)
![gmail](/img/gmail.png)

---------------------------------

> Simplicity is the ultimate sophistication. — Leonardo Da Vinci

## less is more

- The basic problem is actually very complicated.
- It's amazing that computers only use `0` and `1`.

## I taught myself

- `vim` 4 years ago (2008)
- `python` 4 years ago (2008)
- `bash` 2 years ago (2010)
- `emacs` 1 month ago (2012)

I'm happy to do what I love! I'd love to learn more.

---------------------------------

## expressive haskell

    merge xs ys
        | null xs = ys
        | null ys = xs
        | otherwise = (x+y) : (merge xs' ys')
        where x:xs' = xs
              y:ys' = ys

    ones = repeat 1
    ints = 1 : (merge ints ones)
    fibs = 0 : 1 : (merge fibs (tail fibs))
    
    sieve (x:xs) = x : [y | y<-(sieve xs), (y `mod` x)/=0]
    primes = sieve [2..]
