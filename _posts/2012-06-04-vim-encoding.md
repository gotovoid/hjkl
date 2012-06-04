---
layout:     post
title:      谈谈vim文件编码
comments:   true
category:   vim
tags:       [vim]
published:  true
---

使用vim打开含中文的文件时, 由于配置不当, 就会出现乱码.
遇到这种情况, 不要慌. 把下面的设置, 放到你的vimrc中:

    set fencs=utf-8,chinese,latin1 fenc=utf-8 enc=utf-8

> 多个配置, 可以写在一行, 只需要写一个`set`即可.

下文详细分析这条配置.

----

准备测试文件
--------
我使用的是Ubuntu 12.04系统, 默认使用UTF8编码. 可以使用`iconv`把UTF8编码的文件转码成GBK.

    # 通过iconv把UTF8转码成GBK, 并且保存到文件file.txt中
    $ echo '你好, 世界!' | iconv -f UTF8 -t GBK > file.txt

> 简体中文有3种编码方式: GB2312, GBK, GB18030. 其中GB18030是最新版本, GBK使用最广泛.  
> Windows XP, 使用GBK作为简体中文编码方式.  
> 值得一提的是, 当软件把文本文件读到内存时, 需要转换编码方式, 一般以UTF8或其他unicode编码存储在内存中.  
> 因此, 在读入文本文件时, 编辑器就要知道文件的编码方式(ASCII, UTF8, GBK还是Latin1等等).  
> 高级编辑器一般会尝试不同的编码, 直到找到一个合适的(以不报错为标准).

用vim打开file.txt
-----------------

    # 为了不受vimrc/plugin的影响, 使用`-u NONE`不加载vimrc/plugin, vim将使用默认配置
    $ vim -u NONE file.txt

    ÄãºÃ, ÊÀ½ç!

vim没有报错, 因此vim认为解码成功; 由于看到乱码, 我们主观地认为vim解码失败.
这里涉及到"是/非"哲学问题, 不深入讨论.
因为我还没有对vim进行任何配置, vim可以决定用任何方式对文件解码.
不难发现, vim是用万能的latin1解码的.

查看与编码相关的设置
-------------------

    :set fencs?
        fileencodings=ucs-bom,utf-8,default,latin1

    :set fenc?
        fileencoding=latin1

    :set enc?
        encoding=utf-8

- `fencs` 打开文件时, vim会逐个地用`fencs`中提供的编码, 对文本进行解码, 直到找到合适的.
- `fenc` 上一步成功后, 会把那个合适的编码名称, 赋给`fenc`; 否则不进行赋值.
- `enc` 设置vim内部使用的编码方式, 建议使用UTF8.

分析问题原因
--------

在`fencs`中没有GBK, 因此vim是不会擅作主张, 使用GBK对文件进行解码的.
我们只需要把GBK设到`fencs`中, 并重新打开文件即可:

    :set fencs=utf-8,chinese,latin1
    :e!

其中, `fencs`中的编码名称的前后位置是很关键的, 如果你把latin1放在最前面, 会导致后面的编码永远没法起作用.
因为, latin1使用一个字节(8bit)对字符进行编码, 任何字节都是有效的latin1字符.
chinese是euc-cn的别名. 文件中的字属于常见字, 因此可以使用任意一种中文编码方式, 均可以顺利解码.

也可以使用更加简便的方式, 临时改变解码方式:

    :e ++enc=chinese

上述命令, 在对文件编码进行猜测时, 特别有用!
