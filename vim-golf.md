---
layout:    default
title:     Vim Golf
comments:  true
---

    ╻ ╻╻┏┳┓┏━╸┏━┓╻  ┏━╸
    ┃┏┛┃┃┃┃┃╺┓┃ ┃┃  ┣╸ 
    ┗┛ ╹╹ ╹┗━┛┗━┛┗━╸╹  
    write less, do more!

---------------------------------------------------

![vim-golf-001.gif](/img/vim-golf-001.gif)

![vim-golf-002.gif](/img/vim-golf-002.gif)

![vim-golf-003.gif](/img/vim-golf-003.gif)

![vim-golf-004.gif](/img/vim-golf-004.gif)

---------------------------------------------------

## 技术交流

- 豆瓣HJKL小组: <http://www.douban.com/group/hjkl/>

## 制作vim-golf

### 录制屏幕

    recordMyDesktop: Advanced » Performance
    ---------------------------------------
    参数                        值
    ---------------------------------------
    Frames Per Second           10
    Encode One the Fly          ✓
    Zero Compression            ✓
    Quick Subsampling           ✗
    Full shots at every frame   ✓

### 视频编码

    $ ffmpeg -i input.ogv -vcodec libx264 output.mp4

### 动画制作

#### 脚本

    #!/bin/bash
    # NAME:     gif (convert video to gif)
    # USAGE:    ./gif video.fmt

    tmp=/tmp/$RANDOM
    mkdir -p $tmp
    ffmpeg -i "${1:?input is empty}" -r 4 $tmp/%06d.png
    for i in $tmp/*.png
    do
        convert $i $i.jpg
    done
    convert -delay 25 -loop 0 -fuzz 15% -layers Optimize $tmp/*.jpg "$1.gif"
    rm -rf $tmp

#### 运行

    $ chmod +x gif
    $ ./gif video.fmt
    $ display video.fmt.gif
