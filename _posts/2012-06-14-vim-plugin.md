---
layout:     post
title:      vim插件介绍
comments:   true
category:   vim
tags:       [vim, screencast]
published:  true
---

可以通过安装插件来扩展vim的功能. vim的插件, 其实就是用vimscript写的脚本.
当vim启动时, 会自动加载这些插件.

如果感觉到`vimrc`中某个函数, 功能很强大, 并且太占地方,
那么就可以把它提取出来, 包装成一个插件了.

vim有两种形式的插件:

1. 一般插件: 适用于所有类型的文件, 即, 无论编辑什么类型的文件, 都可以使用插件提供的功能.
2. 特种插件: 适用于特定类型的文件, 即, 只有在编辑特定类型的文件时, 该插件才生效.

> 这里的"文件类型", 指的是文件是什么类型的(如:`cpp`, `py`, `conf`等).

安装/卸载"一般插件"的方法:

- 安装插件: 把脚本`name.vim`丢进特定的目录
    - Linux: `~/.vim/plugin`
    - Windows: `C:\Program Files\vim\vimfiles\plugin`
- 卸载插件: 把刚才丢进去的脚本`name.vim`删除
    - Linux: `rm ~/.vim/plugin/name.vim`
    - Windows: `del C:\Program Files\vim\vimfiles\plugin\name.vim`

安装/卸载"特种插件"的方法, 与"一般插件"类似, 只是目录不同

- Linux: `~/.vim/ftplugin`
- Windows: `C:\Program Files\vim\vimfiles\ftplugin`

接下来, 我会介绍一些比较流行的vim插件:

- **pathogen**
- **sparkup**
- **fugitive**
- **vimwiki**
- nerdtree
- snipmate
- ...

---------

## pathogen

- 下载地址: <https://github.com/tpope/vim-pathogen>
- 安装路径:
    - Linux: `~/.vim/autoload/pathogen.vim`
    - Windows: `C:\Program Files\vim\vimfiles\autoload\pathogen.vim`
- vimrc配置:

        call pathogen#infect()

- 工作原理:
    - vim启动过程中, 会自动执行`runtimepath`(简称`rtp`)中的一系列脚本. `pathogen`正利用了这一知识点.
    - 它把`~/.vim/bundle/`中的相关文件夹名称, 按照一定的次序添加到了`rtp`中.
    - 这样的话, 每当vim启动时, 就会加载安装在`~/.vim/bundle/`中的插件了.
    - 称之为"病原体"(译名), 很恰当!
- 注意事项:
    - 该插件被安装到了`~/.vim/autoload`文件夹中, vim会对`autoload`中的脚本延迟加载.
    - 需把`filetype plugin indent on`及`syntax on`, 放到`call pathogen#infect()`后面.
        > 为了避免遗漏加载`~/.vim/bundle/*/filetype.vim`等.
    - 安装新插件到`~/.vim/bundle`后, 若该插件含`doc`, 则需运行`:Helptags`命令, 生成`tags`文件.

## tabular

- 下载地址: <https://github.com/godlygeek/tabular>
- 安装路径: 使用`pathogen`来管理该插件
    - Linux: `~/.vim/bundle/tabular`
    - Windows: `C:\Program Files\vim\vimfiles\bundle\tabular`

> 若不作特殊说明, 下文一律使用`pathogen`来管理新插件.

## sparkup

- 下载地址: <https://github.com/rstacruz/sparkup>
- 工作原理:
    - 按下<kbd>Ctrl-e</kbd>后, 以当前行为参数传递给`sparkup.py`脚本, 把返回的HTML替换掉原来的行.
    - 按下<kbd>Ctrl-n</kbd>后, 自动跳到空Tag/Attr里面.
- 注意事项: 该插件只能在编辑HTML时才会生效, 也可以通过`:set ft=html`强制生效.
- 图片资料:
    - <http://html5tutorial.net/wp-content/uploads/2009/09/html4-structure-div.gif>
    - <http://html5tutorial.net/wp-content/uploads/2009/09/html5-structure-div1.gif>
    - <http://media.smashingmagazine.com/wp-content/uploads/images/html5/html5_structure.png>

## surround

- 下载地址: <https://github.com/tpope/vim-surround>
- 工作原理:
    - 按下<kbd>ys</kbd>, 添加surround
    - 按下<kbd>cs</kbd>, 改变surround
    - 按下<kbd>ds</kbd>, 删除surround
    - 按下<kbd>S</kbd>, surround选中的
- 注意事项: 通过安装[repeat.vim](https://github.com/tpope/vim-repeat), 来支持<kbd>.</kbd>(repeat)操作

## command-T

- 下载地址: <http://www.vim.org/scripts/script.php?script_id=3025>
- 工作原理:
    - <kbd>:CommandT</kbd>, 打开搜索框, 查找file
    - <kbd>:CommandTBuffer</kbd>, 打开搜索框, 查找buffer
    - <kbd>Ctrl-k</kbd>/<kbd>Ctrl-j</kbd>, 在列表中, 上下导航
    - <kbd>Enter</kbd>, 在当前窗口, 打开选中的文件
    - <kbd>Ctrl-t</kbd>, 在新Tab中, 打开选中的文件
    - <kbd>Ctrl-s</kbd>/<kbd>Ctrl-v</kbd>, 分割当前窗口, 打开选中的文件
    - <kbd>Ctrl-c</kbd>/<kbd>Esc</kbd>, 不打开任何文件, 并关闭搜索框
- 注意事项: vim需要支持ruby扩展. 在vim中输入`:ruby 1`报错, 就表示不支持.

## yankring

- 下载地址: <http://www.vim.org/scripts/script.php?script_id=1234>
- 工作原理:
    - <kbd>:YRShow</kbd>, 打开YankRing窗口
    - <kbd>:YRClear</kbd>, 清空YankRing
    - <kbd>p</kbd>, 粘贴YankRing中最顶的一个
    - <kbd>Ctrl-p</kbd>, 粘贴YankRing中上一个
    - <kbd>Ctrl-n</kbd>, 粘贴YankRing中下一个

## fugitive

- 插件简介: 我的天哪, fugitive太强大了, 不会是非法的吧!
- 下载地址: <https://github.com/tpope/vim-fugitive>
- 工作原理:
    - <kbd>:Git</kbd>     , 运行git ...
    - <kbd>:Gstatus</kbd> , 运行git status
    - <kbd>:Gcommit</kbd> , 运行git commit
    - <kbd>:Gdiff</kbd>   , 运行git diff
    - <kbd>:Glog</kbd>    , 运行git log file
    - <kbd>:Ge</kbd>      , 运行e file
    - <kbd>:Gread</kbd>   , 运行git checkout file
    - <kbd>:Gwrite</kbd>  , 运行git add file
- 参考资料:
    - <http://marklodato.github.com/visual-git-guide/index-en.html>
    - <http://gitref.org/>

## minim

- 插件简介: 轻量级中文输入法
- 下载地址: <https://github.com/gotovoid/dot/raw/master/.vim/plugin/minim.vim>
- 工作原理: <kbd>Ctrl-x</kbd><kbd>Ctrl-u</kbd>, 调用插件中的MiniM函数, 以弹出菜单的形式显示候选词语.
- 严重警告: 不要输入敏感词, 否则后果自负!

## alternate

- 插件简介: 让你快速地在`*.{h,cpp}`文件之间切换
- 下载地址: <http://www.vim.org/scripts/script.php?script_id=31>
- 工作原理:
    - <kbd>:A</kbd>, 类似于`:e %:r.cpp`
    - <kbd>:AV</kbd>, 类似于`:vsplit`
    - <kbd>:AS</kbd>, 类似于`:split`
    - <kbd>:AT</kbd>, 类似于`:tabe`
    - <kbd>:let g:alternateExtensions_foo = 'bar,baz'</kbd>, 定义新的绑定: `foo <=> bar,baz`

## easymotion

- 插件简介: 先精确定位, 再跳上去.
- 下载地址: <https://github.com/Lokaltog/vim-easymotion>
- 工作原理:
    - 首先`:let mapleader=','`(最好在`vimrc`中设置)
    - 然后输入<kbd>,,f</kbd>{char}, 从光标位置处向后查找所有{char}, 并且临时把它们替换成a,b,c...
    - 最后输入<kbd>b</kbd>, 光标就跳到第二个{char}上了.

## vimwiki

- 插件简介: 个人日记本
- 下载地址: <http://code.google.com/p/vimwiki/downloads/list>
- 注意事项: 先把vim基本功练好, 再玩这个插件!

## gist
- 插件介绍: github代码片断manager
- 下载地址: <https://github.com/mattn/gist-vim>
- 注意事项: github提供的API有bug, 导致无法正确上传含有`%`(百分号)snippet
- 工作原理:
    - <kbd>:Gist</kbd>, 上传当前文件
    - <kbd>:Gist -l</kbd>, 列出所有gist
    - <kbd>:Gist -d</kbd>, 删除当前gist
    - <kbd>:w</kbd>, 更新当前gist
- 严重警告: github.com暂时无法访问, 原因未知.

--------

## 视频演示

- vim插件介绍
    - [下载](http://ubuntuone.com/3NAbwQUsuzJNxrThAMurk0)
- pathogen
    - [下载](http://ubuntuone.com/1QFrp0WLPDeVSehPzkPvHw)
- tabular
    - [下载](http://ubuntuone.com/2cjmijnIp6DBnBApC2px3N)
- sparkup
    - [下载](http://ubuntuone.com/6hBtYaH8ZWpwtTvniHokku)
- surround
    - [下载](http://ubuntuone.com/4VoeX3F4VqXihd4E9yfiAR)
- command-T
    - [下载](http://ubuntuone.com/1Dxrc54DawBv0cUfdC7FyE)
- yankring
    - [下载](http://ubuntuone.com/1tmePAIKKQ5Egh4vRMBi9m)
- fugitive
    - [下载](http://ubuntuone.com/5r0AAuhxEg7vnwCwciAKCz)
- minim(beta)
    - [下载](http://ubuntuone.com/3XSLL7z3wtySFWGkibiojJ)
- alternate
    - [下载](http://ubuntuone.com/6UVtcfYFxiKU2dIXvRTCLT)
- easymotion
    - [下载](http://ubuntuone.com/3OdOiQh4iXBykDRtXG3z5i)
- vimwiki
    - [下载1](http://ubuntuone.com/6k4KOqIGj5hfI2DmBHWcXJ)
    - [下载2](http://ubuntuone.com/1Br6gJacWwZODU8cdrFn23)

[优酷专辑](http://www.youku.com/playlist_show/id_17756150.html)

**...未完待续...**
