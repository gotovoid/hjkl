---
layout:     post
title:      使用Google Chart API绘制3D饼图
comments:   true
category:   plot
tags:       [plot, chart, google, curl]
published:  true
---

基于Web Sevice的软件已经非常普及了, 桌面应用在日常生活中的比重变得越来越小.  
最终, 只要安装一个Web Browser, 就可以使用电脑了. 也许, 未来的操作系统就是一个Web Browser.  
本文介绍, 怎样使用命令行工具[curl][1]通过[Google Charts API][2]生成3D饼图.  
所生成的拼图, 与wikipedia上的对比, 发现一个事实:

> IE浏览器的市场份额, 半年就降了近10%!

数据源
-----------

    Browser Usage on Wikimedia
    ==========================
    浏览器              份额
    ------             ------
    IE                  34.2
    Firefox             23.6
    Chrome              20.6
    Safari              11.2
    Opera               5.0
    Android             1.9
    Other               3.5

> 这是我半年前记录的数据, 再看看现在的[状况][3]!

命令行
-----------

    curl -v -G -o browers.png \
    --data-urlencode 'chtt=Browser Usage on Wikimedia' \
    --data           'cht=p3' \
    --data           'chs=450x200' \
    --data           'chd=t:34.2,23.6,20.6,11.2,5.0,1.9,3.5' \
    --data-urlencode 'chl=IE|Firefox|Chrome|Safari|Opera|Android|Other' \
    --data-urlencode 'chdl=34.2%|23.6%|20.6%|11.2%|5.0%|1.9%|3.5%' \
    'http://chart.apis.google.com/chart'

说明
-----
    -v                      开启啰嗦模式
    -G                      使用GET命令
    -o FILE                 输出到文件
    --date DATA             query-string数据(简称: -d)
    --data-urlencode DATA   query-string数据(进行url编码)

    | 参数 | 说明       | 补充                           |
    |------+------------+--------------------------------|
    | chd  | data       | 以`t:`为前缀, 用`逗号`分割字段 |
    | chdl | data label | 用`竖线`分割字段               |
    | chl  | label      | 用`竖线`分割字段               |
    | chs  | size       |                                |
    | cht  | type       |                                |
    | chtt | title      |                                |

结果
----
### 半年前
![半年前](http://chart.apis.google.com/chart?chtt=Browser%20Usage%20on%20Wikimedia&cht=p3&chs=450x200&chd=t:34.2,23.6,20.6,11.2,5.0,1.9,3.5&chl=IE|Firefox|Chrome|Safari|Opera|Android|Other&chdl=34.2%25|23.6%25|20.6%25|11.2%25|5.0%25|1.9%25|3.5%25)

### 半年后
![半年后](http://upload.wikimedia.org/wikipedia/commons/thumb/0/08/Wikimedia_browser_share_pie_chart_3.png/220px-Wikimedia_browser_share_pie_chart_3.png)

[1]: http://curl.haxx.se/
[2]: https://developers.google.com/chart/image/
[3]: http://en.wikipedia.org/wiki/Usage_share_of_web_browsers
