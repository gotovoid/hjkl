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
> 下面以blob为例.


手动计算blob哈希
----------------
    $ mkdir hjkl && cd hjkl && git init && rm .git/hooks/*
    
    $ echo 'hello, world' > README
    
    $ wc -c README
    13 README
    
    $ printf 'blob 13\0hello, world\n' | sha1sum
    4b5fa63702dd96796042e92787f464e28f09f17d  -
    
    $ git add .

    $ xxd .git/index 
    0000000: 4449 5243 0000 0002 0000 0001 4fe4 7cee  DIRC........O.|.
    0000010: 2ed4 fad9 4fe4 7cee 2ed4 fad9 0000 0700  ....O.|.........
    0000020: 000e 632a 0000 81a4 0000 03e8 0000 03e8  ..c*............
    0000030: 0000 000d 4b5f a637 02dd 9679 6042 e927  ....K_.7...y`B.'
    0000040: 87f4 64e2 8f09 f17d 0006 5245 4144 4d45  ..d....}..README
    0000050: 0000 0000 47c2 c3e4 be7d 08a9 c34b 140f  ....G....}...K..
    0000060: bee5 7b4d 6e73 3ca6                      ..{Mns<.

    $ tree .git/objects/
    .git/objects/
    ├── 4b
    │   └── 5fa63702dd96796042e92787f464e28f09f17d
    ├── info
    └── pack

在.bashrc中定义alias
--------------------
    alias deflate='python -c "import sys; sys.stdout.write(sys.stdin.read().decode(\"zlib\"))"'

使用zlib解压缩
---------------
    $ python -c '
    > import zlib, sys
    > print(zlib.decompress(sys.stdin.read()))
    > ' < .git/objects/4b/5fa63702dd96796042e92787f464e28f09f17d

    $ deflate < .git/objects/4b/5fa63702dd96796042e92787f464e28f09f17d

使用hashlib验证
---------------
    $ python -c '
    > import hashlib, sys
    > print(hashlib.sha1(sys.stdin.read().decode("zlib")).digest().encode("hex"))
    > ' < .git/objects/4b/5fa63702dd96796042e92787f464e28f09f17d

    $ deflate < .git/objects/4b/5fa63702dd96796042e92787f464e28f09f17d | sha1sum

使用git自带命令
---------------
    $ git show --raw 4b5fa
    $ git cat-file -p 4b5fa

