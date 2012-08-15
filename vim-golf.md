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

###001 四则运算
![vim-golf-001.gif](/img/vim-golf-001.gif)
###002 乘法口诀
![vim-golf-002.gif](/img/vim-golf-002.gif)
###003 合并列表
![vim-golf-003.gif](/img/vim-golf-003.gif)
###004 base64解码
![vim-golf-004.gif](/img/vim-golf-004.gif)
###005 列表=>表格
![vim-golf-005.gif](/img/vim-golf-005.gif)
###006 分组排序
![vim-golf-006.gif](/img/vim-golf-006.gif)
###007 提取数字
![vim-golf-007.gif](/img/vim-golf-007.gif)
###008 名言警句
![vim-golf-008.gif](/img/vim-golf-008.gif)
###009 交换单词
![vim-golf-009.gif](/img/vim-golf-009.gif)
###010 列表编号
![vim-golf-010.gif](/img/vim-golf-010.gif)
###011 寻找素数
![vim-golf-011.gif](/img/vim-golf-011.gif)
###012 Fibonacci
![vim-golf-012.gif](/img/vim-golf-012.gif)
###013 Factorial
![vim-golf-013.gif](/img/vim-golf-013.gif)
###014 冒泡排序
![vim-golf-014.gif](/img/vim-golf-014.gif)

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
