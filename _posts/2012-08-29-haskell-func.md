---
layout:     post
title:      函数式编程
comments:   true
category:   haskell
tags:       [haskell]
published:  true
---

## 转换进制

    >>> let bin n = if n==0 then "" else bin (n `div` 2) ++ show (n `mod` 2)
    >>> bin 234
    "11101010"

## 分组排序

    >>> import qualified Data.List as L
    >>> import Data.Function
    >>> L.groupBy ((==) `on` length) ["a","b","cd","hello","world"]
    [["a","b"],["cd"],["hello","world"]]
    >>> L.sortBy (compare `on` last) ["a","b","cd","hello","world"] 
    ["a","b","cd","world","hello"]

## 计数统计

    >>> import qualified Data.Map as M
    >>> M.toList $ foldr (flip (M.insertWith (+)) 1) (M.fromList []) [1,3,2,4,2,1,5,2,2,4]
    [(1,2),(2,4),(3,1),(4,2),(5,1)]

## 因式分解

    >>> let fun n = let m = (head.filter ((==0).(mod n))) [2..] in if m==n then [m] else m:fun (div n m)
    >>> fun 234
    [2,3,3,13]

