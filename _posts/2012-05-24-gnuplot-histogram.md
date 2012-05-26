---
layout: default
title: 使用gunplot绘制直方图
category: gnuplot
tags: [gnuplot, visualization]
---

## 工具介绍
- `vim`/`gvim` - 高级文本编辑器
- `gnuplot` - 通用绘图工具
- `display` - 图片浏览器(需安装`ImageMagick`)

## 获取数据
Google搜索: ["What's your favorite text editor?"](https://spreadsheets.google.com/spreadsheet/viewanalytics?formkey=dHhwMm9jS1l6RTh4Q3RBZU1GRWE1R0E6MQ)

    VIM          1368  48%
    EMACS        610   21%
    gEdit        307   11%
    Geany        66    2%
    jEdit        47    2%
    Kate         54    2%
    Bluefish     12    0%
    Notepad++    687   24%
    Textpad      77    3%
    UltraEdit    54    2%
    Coda         74    3%
    TextMate     511   18%
    SublimeText  10    0%

> 注意: 预处理数据时, 需要把最后一行中的~~Sublime Text~~中间的空格去掉了.

## 编写脚本
{% highlight gnuplot %}
#!/usr/bin/env gnuplot

set terminal png
set output 'editor.png'
set title "What's your favorite text editor?" font 'Ubuntu,16'
set xtics scale 0 rotate by -45
set style fill solid 0.25 noborder
set box 0.5
set rmargin 5
set bmargin 5
set grid y

plot 'editor.csv' using 2:xtic(1) with boxes linecolor rgb 'blue' title 'Votes',\
     '' using 0:($2+50):3 with labels notitle
{% endhighlight %}

## 代码解释
{% highlight gnuplot %}
#!/usr/bin/env gnuplot

# 输出类型
set terminal png

# 输出文件名
set output 'editor.png'

# 标题及其字体
set title "What's your favorite text editor?" font 'Ubuntu,16'

# X轴刻度标签顺时针旋转45°, 并且隐藏刻度线
set xtics scale 0 rotate by -45

# 填充颜色, 并隐藏边框
set style fill solid 0.25 noborder

# 矩形框的宽度
set box 0.5

# 右边距
set rmargin 5

# 下边距
set bmargin 5

# 显示Y轴网格
set grid y

# 先绘制boxes, 再绘制labels
plot 'editor.csv' using 2:xtic(1) with boxes linecolor rgb 'blue' title 'Votes',\
     '' using 0:($2+50):3 with labels notitle
{% endhighlight %}

## 运行脚本
    chmod +x editor.plt
    ./editor.plt
    display editor.png

![editor](/img/editor.png)

## 视频演示
- [优酷](http://v.youku.com/v_show/id_XNDAxNzkxMDY4.html)
- [下载](http://ubuntuone.com/7a4Z0uA7X1DsWrIF9rymiX)
