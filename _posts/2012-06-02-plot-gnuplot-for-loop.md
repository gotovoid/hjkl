---
layout:     post
title:      使用gnuplot的for循环制作动画
comments:   true
category:   plot
tags:       [plot, gnuplot, random]
published:  true
---

gnuplot 4.6增加了`for...loop`, 为制作动画提供了方便.  
为了增加编程的乐趣, 我写了一个随机生成圆点的gif动画.  
如果你对gnuplot还不了解, 请阅读关于[plot](http://hjkl.me/tagcloud.html#cat-plot)的相关文章.

脚本
----
{% highlight gnuplot %}
#!/usr/bin/env gnuplot
# rnd.plt
# generate random dots

!mkdir -p rnd

set term svg
unset border
unset tics
rnd(x) = int(rand(0)*2**24)
do for [i=0:99] {
    file = sprintf('rnd/%02d.svg', i)
    set out file
    plot '<seq 10' using (rnd(0)):(rnd(0)):(10*rand(0)):(rnd(0)) \
        with points pt 7 ps var lc rgb var notitle
}

!convert rnd/*.svg rnd.gif
!rm -r rnd
{% endhighlight %}

运行
----
    chmod +x rnd.plt
    ./rnd.plt
    firefox rnd.gif

结果
----
![rnd.gif](/img/rnd.gif)
    
参考
----
- <http://gnuplot.sourceforge.net/demo_4.6/rgb_variable.html>
- <http://www.gnuplotting.org/gnuplot-4-6-do/>
