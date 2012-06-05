---
layout:     post
title:      谈谈vim空格缩进
comments:   true
category:   vim
tags:       [vim]
published:  true
---

`Tab(\t)`是制表符, 由于编辑器的配置各不相同, 从而导致显示出不同的效果.
`Tab(\t)`与空格符, 是无法通过肉眼区分的, 如果在一个文件中混搭两者, 必然会出现问题.
由于`Tab(\t)`的配置依赖行, 以及不可预测性, 建议使用4个(或8个)空格代替它.
使用空格可以确保在不同编辑器中显示完全相同的效果.

在vimrc中, 需要写入:

    set shiftwidth=4 tabstop=4 softtabstop=4 expandtab
    set listchars=precedes:«,extends:»,tab:▸·,trail:∙,eol:¶

第一句: 设置Tab的宽度, 以及把Tab自动转化为空格
第二句: 当运行`:set list`命令时, 把隐形的`Tab`及行尾的空格显示出来.

----

解释命令
--------

    :set expandtab

> 按下<kbd>Tab</kbd>键后, 自动把`Tab`转化成指定数目(由`tabstop`决定)的空格

    :set tabstop=4

> 定义`Tab`的宽度为4, 在insert模式下, 通过<kbd>Ctrl-v</kbd><kbd>Tab</kbd>强制输入`Tab`查看效果.

    :set shiftwidth=4

> 自动语法缩进, 或者按下<kbd>&lt;&lt;</kbd>键后, 缩进的宽度为4

    :set softtabstop=4

> 按下<kbd>Backspace</kbd>键后, 自动删除4个空白. 让人觉得在删除`Tab`.  
> 为了查看效果, 可以首先运行`:set noet ts=8 sw=4 sts=4 list`, 然后输入<kbd>Tab</kbd>, 最后按下<kbd>Backspace</kbd>.  
> 可以发现, 删除了4个空白, 并且把宽度为8的`Tab`, 变成了4个空格.


    :set listchars=precedes:«,extends:»,tab:▸·,trail:∙,eol:¶

> 运行`:set list`命令后, 会把`Tab`显示成`▸·`, 把行尾空格显示成`∙`, 行尾添加`¶`.  
> 运行`:set nowrap`命令后, 对于超出屏幕范围的行, 会在左边界显示`«`, 右边界显示`»`.  

手动转化
-------

打开一个文件后, 发现Tab与空格混用, 可以使用下面的命令解决:

{% highlight cpp %}
int main()
{
∙∙∙∙while(1) {
▸···printf("hello, world!\n");
∙∙∙∙}
}
{% endhighlight %}

    :set ts=8

{% highlight cpp %}
int main()
{
∙∙∙∙while(1) {
▸·······printf("hello, world!\n");
∙∙∙∙}
}
{% endhighlight %}

    :set et
    :retab!

{% highlight cpp %}
int main()
{
∙∙∙∙while(1) {
∙∙∙∙∙∙∙∙printf("hello, world!\n");
∙∙∙∙}
}
{% endhighlight %}

> 这个过程是可逆的, 在`:retab!`之前, `:set noet`即可.

注意事项
--------

- `Tab(\t)`在编辑器中看起来像是4个字符, 但是保存到文件时, 只是一个字符.
- 在写python代码时, 建议使用`:set expandtab`, 把问题扼杀在摇篮里.
