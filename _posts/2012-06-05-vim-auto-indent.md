---
layout:     post
title:      谈谈vim自动缩进
comments:   true
category:   vim
tags:       [vim]
published:  true
---

如果你是程序员, 你就能理解为什么代码要"自动缩进(autoindent)"了.

### 缩进前

{% highlight cpp %}
int main()
{
if(1)
printf("hello, world!");
else
printf("你好, 时间!");
}
{% endhighlight %}

### 缩进后

{% highlight cpp %}
int main()
{
    if(1)
        printf("hello, world!");
    else
        printf("你好, 时间!");
}
{% endhighlight %}

缩进后的代码, 更容易查看. 编译器不关心代码的缩进, 但是人关心. 如果手动输入这么多空格的话, 即耗时又无聊.  
其实, vim提供了很多关于自动缩进的设置, 当你按下<kbd>o</kbd>/<kbd>Enter</kbd>后, vim会进行适当的缩进.  
各种设置方案有利有弊, 根据具体情况选择适合的即可.

----

:set ai
-------

`autoindent(ai)`, 自动缩进. 这是vim提供的最简单的缩进方式, 适应于yaml, txt等.

{% highlight cpp %}
int main()
{
    if(1)█

{% endhighlight %}

### 按回车

{% highlight cpp %}
int main()
{
    if(1)
    █

{% endhighlight %}

:set si
------

`smartindent(si)`, 智能缩进. 比`ai`稍微高级一点, 识别`{,},if,else`等上下文相关的几个关键字.  
与其用阉割版的`si`, 不如直接用`cin`.

{% highlight cpp %}
int main()
{
    if(1)█

{% endhighlight %}

### 按回车

{% highlight cpp %}
int main()
{

    if(1)
        █

{% endhighlight %}

:set cin
--------

`cindent(si)`, C缩进. 功能最强悍, 适用于C系列语言(C/C++/C#/Java).

{% highlight cpp %}
int main()
{
    if(1)
        printf("hello, world"█


{% endhighlight %}

### 按回车

{% highlight cpp %}
int main()
{
    if(1)
        printf("hello, world"
            █

{% endhighlight %}

:set indentexpr
--------------
自定义缩进, 可以满足个性化需求, 编写难度大, 而且已经有现成的了.  
`$VIMRUNTIME/indent/*.vim`包含了几百个文件, 都是用来搞自定义的.  
启用方式, 请参考[谈谈vim语法侦测](http://hjkl.me/vim/2012/06/04/vim-filetype.html).  
以python为例:

{% highlight python %}
def hello():█
{% endhighlight %}

### 按回车

{% highlight python %}
def hello():
    █
{% endhighlight %}


小技巧
--------

如果*.cpp代码没有缩进, 用<kbd>gg=G</kbd>重新缩进.
也可以选中某些行, 按下<kbd>=</kbd>局部缩进.
