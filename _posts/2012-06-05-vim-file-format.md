---
layout:     post
title:      谈谈vim文件格式
comments:   true
category:   vim
tags:       [vim]
published:  true
---

在Windows下, 用notepad打开某些C++代码文件时,
经常会出现, 文件中没有任何换行, 所有的字符都挤在一行.
出现这种问题的原因是, 在保存文本文件时, Linux与Windows使用不同的换行符.

Linux使用`\n`作为换行符, 而Windows使用`\r\n`.   
其实, Linux与Windows的文本文件的区别, 就这么点.  
总之, 只要解决了`换行`问题, 就解决了文本文件的跨平台问题.  
notepad认为, 来自于Linux的文本文件, 没有包含任何换行符, 因此就把所以字符用一行显示了.  
如果在Linux下, 查看Windows下的文本文件, 每一行后面都多了个`^M`(即`\r`).

幸好, vim有自动侦测文件格式的功能. 你需要把下面的配置, 写入vimrc:

    set ffs=unix,dos ff=unix

- `fileformats(ffs)` - vim会首先使用unix, 失败后, 再用dos的换行符格式, 解读文件. 并且把相应的值赋给`ff`.
- `fileformat(ff)` - 创建新文件时, 选用`ff`所指定的换行符, 保存文件. 即使在Windows下, 我也`set ff=unix`.

在最新版`vim73`中, 可以使用默认值. 通过`:set ffs? ff?`查看.

检验是否配置正确
----------------

### 创建一个dos格式的文本:

    $ echo -ne 'hello\r\nworld\r\n' > dos.txt
    $ vim dos.txt

运行命令:

    :set ffs? ff?
      fileformats=unix,dos
      fileformat=dos

### 创建一个unix格式的文本:

    $ echo -ne 'hello\nworld\n' > unix.txt
    $ vim unix.txt

运行命令:

    :set ffs? ff?
      fileformats=unix,dos
      fileformat=unix

强制使用某种文件格式
--------------------

如果有多个人修改同一个文件的话, 就会导致在一个文件中, 可能同时包含两种格式的换行符.  
作为一个程序员, 你不解决, 还指望谁来解决.

### 创建一个dos/unix混合格式的文本:

    $ echo -ne 'hello\nworld\r\n' > dx.txt
    $ vim dx.txt

运行下列命令, 就可以解决问题:

    :e ++ff=unix
    :%s/\r//
    :w

> 使用`:e ++ff=unix`命令, 以`unix`格式重新打开文件. 如果当前`ff`已经是`unix`, 则不需要再打开一次.  
> 通过`:%s/\r//`命令, 把所有的`\r`字符删除.  
> 如果你想把文件保存为`dos`格式, 先要`:set ff=dos`, 然后再`:w`.  
> 也可以用`:w ++ff=dos`(此命令不改变编辑器的`ff`设置, 如果再运行一次`:w`, 文件又变成了`unix`格式).

另外, 也可以使用`dos2unix`/`unix2dos`等命令行工具, 转化文件格式:

    $ dos2unix dos.txt
    $ unix2dos unix.txt

说明
----
- 所谓的dos格式, 并不一定要在Windows系统下, 才能创建. 我用`echo`命令, 演示了如何创建各种格式的文本.  
- 除了dos及unix格式外, 还有mac格式. 有兴趣的朋友可以阅读<https://ccrma.stanford.edu/~craig/utility/flip/>.
