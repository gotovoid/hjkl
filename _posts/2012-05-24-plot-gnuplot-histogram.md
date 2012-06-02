---
layout: post
title: 使用gunplot绘制直方图
category: plot
tags: [plot, gnuplot, chart, screencast]
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

----

## 附录

如果数据中第一行为column name, 并且数据是用"逗号"分割的. 例如:

    # Usage share data from Wikimedia visitor log analysis report
    #
    Period,IE,Firefox,Chrome,Safari,Opera,Mozilla,Mobile
    April 2009,57.37,30.71,1.93,3.86,2.57,0.68,1.9
    May 2009,57.30,30.43,2.28,3.76,2.65,0.66,2.0
    June 2009,56.35,30.82,2.45,4.04,2.61,0.64,2.1
    July 2009,54.55,31.52,2.77,4.51,2.38,0.70,2.4
    August 2009,55.60,30.25,2.97,4.57,2.97,0.71,2.3
    September 2009,55.77,29.78,3.12,4.72,2.62,0.67,2.2
    October 2009,54.72,30.17,3.41,4.82,2.76,0.65,2.2
    November 2009,54.43,29.96,3.73,4.96,2.82,0.63,2.3
    December 2009,52.24,30.45,4.34,5.14,3.08,0.57,3.0
    January 2010,51.01,30.85,4.81,5.13,3.18,0.56,3.1
    February 2010,50.29,30.96,5.28,5.27,3.29,0.60,3.0
    March 2010,50.43,30.44,5.75,5.14,3.30,0.62,3.0
    April 2010,48.96,30.84,6.37,5.09,3.40,0.69,3.3
    May 2010,48.25,30.87,6.93,4.99,3.46,0.62,3.5
    June 2010,47.50,30.90,7.39,4.95,3.43,0.59,3.9
    July 2010,47.74,30.43,7.52,5.18,2.89,0.53,4.5
    August 2010,47.22,29.49,8.36,5.31,2.88,0.59,4.6
    September 2010,46.45,29.33,9.00,5.49,3.19,0.54,4.5
    October 2010,44.72,29.67,9.71,5.57,3.48,0.53,4.7
    November 2010,44.46,29.17,10.29,5.61,3.37,0.53,4.9
    December 2010,42.12,28.82,11.18,5.70,3.67,0.52,6.4

{% highlight gnuplot %}
#!/usr/bin/env gnuplot

set title 'Usage share data from Wikimedia visitor log analysis report' font 'Ubuntu,14'
set term wxt size 800,600
set out 'browser.png'
set datafile sep ','
set border 3
set key autotitle col under nobox
set style data hist
set style hist rows
set boxwidth 0.5
set style fill solid 0.5 noborder
set xtics scale 0 rotate by -45 font 'Ubuntu,9'
set ytics scale 0 font 'Ubuntu,9'
set format y '%g%%'
set rmargin 5
set bmargin 8
set grid y

# plot rowstacked histogram
plot 'browser.csv' u 2:xtic(1), for [i=3:8] '' u i

# 暂停3秒
pause 3

unset key
set key autotitle columnheader vertical right out box
unset format
set style hist columns
set xtics norotate font 'Ubuntu,11'

# plot columnstacked histogram
plot 'browser.csv' u 2:key(1), for [i=3:8] '' u i
{% endhighlight %}

## 视频演示
- [优酷](http://v.youku.com/v_show/id_XNDAxNzkxMDY4.html)
- [下载](http://ubuntuone.com/7a4Z0uA7X1DsWrIF9rymiX)
