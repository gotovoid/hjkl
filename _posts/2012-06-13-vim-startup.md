---
layout:     post
title:      vim启动流程
comments:   true
category:   vim
tags:       [vim]
published:  true
---

## vim启动过程中, 一共做了下列12件事:

1. 设置`shell`及`term`选项

2. 处理命令行参数
   > 有些参数, 需要在后续步骤中, 才真正执行

3. 执行环境变量或配置文件中的Ex命令:
    1. 根据命令行`-u XXX`参数的不同, 会执行下列不同的路径:
        1. 若命令行有`-u filename`参数, 则以`filename`为`vimrc`, 并跳到步骤`4`
        2. 若命令行有`-u NORC`参数, 则跳到步骤`4`
        3. 若命令行有`-u NONE`参数, 则跳到步骤`5`
    2. 若命令行有`-s`参数(Ex模式), 则只解析上述的`-u`参数中的`vimrc`, 并跳到步骤`4`
    3. 依次执行下列脚本:
        1. 如果命令行有`-y`参数(Easy模式), 则运行`source $VIMRUNTIME/evim.vim`
        2. 运行`source $VIM/vimrc`
        3. 依次搜索下列环境变量或配置文件(找到其中一个后, 就不继续找了):
            1. 环境变量: `VIMINIT`
            2. 用户vimrc: `$HOME/.vimrc`(Unix), `$HOME/_vimrc`(Win32), `$VIM/_vimrc`(Win32)
            3. 环境变量: `EXINIT`
            4. 用户exrc: 与vimrc类似, 仅文件名不同, 且默认使用compatible方式运行.
        4. 若`exrc`选项已设置, 则在当前目录下依此查找3个配置文件(找到一个就不找了):
            1. `.vimrc`(Unix), `_vimrc`(Win32)
            2. `_vimrc`(Unix), `.vimrc`(Win32)
            3. `.exrc`(Unix), `_exrc`(Win32)

4. 若满足下列条件, 则加载plugin脚本(即执行`:runtime! plugin/**/*.vim`)
    1. `loadplugins`选项未在`vimrc`中被重置
    2. 命令行无`--noplugin`参数
    3. 命令行无`-u NONE`参数
    4. vim具有`+eval`这个feature

5. 设置`shellpipe`及`shellredir`选项

6. 若命令行无`-n`参数, 则`set updatecount=0`

7. 若命令行有`-b`参数, 则`set binary`
    > 这一步, 似乎有问题!

8. 若命令行有`-g`参数, 则初始化GUI

9. 若`viminfo`选项不为空, 则读取`viminfo`配置文件

10. 若命令行有`-q`参数, 则读取制定的`quickfix`文件

11. 执行以下启动命令:
    1. 若命令行有`-t`参数, 则跳到指定tag
    2. 若命令行有`-c`或`+cmd`参数, 则执行指定的命令
    3. 把`vim_starting`这个feature设为`0`
    4. 若`insertmode`选项已设置, 则进入Insert模式
    5. 执行`VimEnter`自动命令


说明
----
- 想要获取更多信息, 请`:help startup`

