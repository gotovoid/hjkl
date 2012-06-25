---
layout: post
title: vim视频播放器
category: c4f
tags: [c4f, vim, ascii]
comments:   true
published:  true
---

在C++中, 可以在main函数里面调用其他函数, 来实现我们想要的功能.  
同样地, 在linux中, 通过组合不同的tool, 就可以构造出新的tool.  
vim不仅可以自由地与外部tool交互, 而且有自己的scripting语言.  
我之所以喜欢vim, 是因为vim有数不清的玩法, 永远不会玩腻了!  
下面我就来实现一个非常简单的ascii播放器.

## 工具介绍
- vim - 高级text editor
- ffmpeg - 从flv中提取jpg/mp3
- jp2a  - 把jpg转换成ascii
- mpg321 - 命令行player

## 输入文件
- [bad-apple.flv](http://v.youku.com/v_show/id_XMzQxNDY0MDY0.html)
- [下载](http://ubuntuone.com/125AH5y0lHQd2kbxvmZPqu)

## bash版
### 代码
{% highlight bash %}
    #!/bin/bash
    # ┏┓ ┏━┓╺┳┓   ┏━┓┏━┓┏━┓╻  ┏━╸
    # ┣┻┓┣━┫ ┃┃   ┣━┫┣━┛┣━┛┃  ┣╸ 
    # ┗━┛╹ ╹╺┻┛   ╹ ╹╹  ╹  ┗━╸┗━╸
    # by Kev++

    video=${1:?input is empty}
    audio=${video%.*}.mp3
    image=./tmp/img

    [ -e $image ] || { mkdir -p $image && ffmpeg -i $video -r 10 $image/%05d.jpg; }
    [ -e $audio ] || ffmpeg -i $video -vn $audio

    mpg321 $audio &
    for i in $image/*.jpg; do jp2a $i; sleep 0.08; done
{% endhighlight %}

### 运行
    $ chmod +x bad-apple.sh
    $ ./bad-apple.sh bad-apple.flv

## vim版
{% highlight vim %}
    " ┏┓ ┏━┓╺┳┓   ┏━┓┏━┓┏━┓╻  ┏━╸
    " ┣┻┓┣━┫ ┃┃   ┣━┫┣━┛┣━┛┃  ┣╸ 
    " ┗━┛╹ ╹╺┻┛   ╹ ╹╹  ╹  ┗━╸┗━╸
    " by Kev++
    
    if empty(glob('./tmp'))
        finish
    endif
    
    fun! Display(cmd, delay)
        %d
        exe a:cmd
        redraw
        exe 'sleep' a:delay
    endfun
    
    for i in range(3, 1, -1)
        call Display('r!toilet -f mono12 '.i, 1)
    endfor
    
    call system('mpg321 tmp/*.mp3&')
    
    silent! argdel *
    argadd ./tmp/img/*.jpg
    for i in argv()
        call Display('r!jp2a '.i, '80m')
    endfor
    argdel *
    
    call Display('r!toilet -f mono12 END', 3)
    
    undo
{% endhighlight %}

### 运行
    $ vim -u NONE +so% bad-apple.vim
    
> 运行该vim脚本前, 请使用ffmpeg生成`./tmp/img/*.jpg`

## 视频演示
- [下载](#)
- [在线](#)
