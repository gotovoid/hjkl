---
layout:     post
title:      解压缩git对象
comments:   true
category:   git
tags:       [git]
published:  true
---

> git使用zlib对blob/tree/commit/tag等对象进行压缩后, 统一存储在`.git/objects`目录下.
> 为了满足好奇的心, 我打算手动解压缩这些对象, 并且重新计算sha1哈希, 进行校验.

切换到obj目录
-------------

    $ cd .git/objects/a5
    $ ls
    0c564e401a1883414226893cbc6c3fd833edc7

使用git自带命令
---------------

    $ git show --raw a50c56
    $ git cat-file -p a50c56

使用zlib解压缩
---------------

    $ python -c '
    > import zlib, sys
    > print(zlib.decompress(sys.stdin.read()))
    > ' <0c564e401a1883414226893cbc6c3fd833edc7


使用hashlib验证
---------------
    $ python -c '
    > import hashlib, sys
    > print(hashlib.sha1(sys.stdin.read().decode("zlib")).digest().encode("hex"))
    > ' <0c564e401a1883414226893cbc6c3fd833edc7
    a50c564e401a1883414226893cbc6c3fd833edc7

