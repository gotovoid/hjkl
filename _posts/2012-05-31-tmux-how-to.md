---
layout:     post
title:      tmux介绍
comments:   true
category:   tool
tags:       [tool, tmux, screencast, beta]
published:  true
---

介绍
-------
> `tmux` is a terminal multiplexer: it enables a number of terminals (or windows),
> each running a separate program, to be created, accessed, and controlled from a
> single screen. tmux may be detached from a screen and continue running in the
> background, then later reattached.

> `tmux`是个终端复用器：它让你在一个屏幕中, 创建/操作/控制若干终端（或窗口），
> 每个窗口都可以独立地运行程序。`tmux`可以脱离屏幕在后台继续运行，稍后可重新挂载。

术语
-------
- `session` - 直接运行`tmux`命令, 会创建一个session;
  也可以通过运行`tmux attach -t session-name`命令, 连接到已有的session.
- `client` - tmux是基于C/S架构的软件, 你所操作的界面属于client,
  服务器(即server)会管理所有的client; 不同的client可以连接到相同的session.
- `window` - 参考firefox的`Tab`
- `pane` - 参考vim的`:split`

命令
----
- `bind`(bind-key) - 绑定快捷键
- `unbind`(unbind-key) - 取消快捷键
- `set`(set-option) - 设置(用`set -u`来unset)
- `setw`(set-window-option) - 设置窗口

默认快捷键
----------
### other
    C-b         Send the prefix key (C-b) through to the application.
    C-z         Suspend the tmux client.
    :           Enter the tmux command prompt.
    ?           List all key bindings.
    t           Show the time.
    ~           Show previous messages from tmux, if any.

### window
    c           Create a new window.
    n           Change to the next window.
    p           Change to the previous window.
    l           Move to the previously selected window.
    f           Prompt to search for text in open windows.
    w           Choose the current window interactively.
    i           Display some information about the current window.
    &           Kill the current window.
    '           Prompt for a window index to select.'
    ,           Rename the current window.
    .           Prompt for an index to move the current window.
    0 to 9      Select windows 0 to 9.

### pane
    "           Split the current pane into two, top and bottom."
    %           Split the current pane into two, left and right.
    C-o         Rotate the panes in the current window forwards.
    !           Break the current pane out of the window.
    ;           Move to the previously active pane.
    o           Select the next pane in the current window.
    q           Briefly display pane indexes.
    x           Kill the current pane.
    {           Swap the current pane with the previous pane.
    }           Swap the current pane with the next pane.
    ↑↓←→        Change to the pane above, below, to the left,
                or to the right of the current pane.
    C-↑↓←→      Resize the current pane in steps of one cell.
    M-↑↓←→      Resize the current pane in steps of five cells.
    M-1 to M-5  Arrange panes in one of the five preset layouts:
                even-horizontal, even-vertical, main-horizontal, main-vertical, or tiled.

### copy/paste
    [           Enter copy mode to copy text or view the history.
    ]           Paste the most recently copied buffer of text.
    =           Choose which buffer to paste interactively from a list.
    #           List all paste buffers.
    -           Delete the most recently copied buffer of text.
    Page Up     Enter copy mode and scroll one page up.

### client/session
    d           Detach the current client.
    $           Rename the current session.
    D           Choose a client to detach.
    s           Select a new session for the attached client interactively.
    L           Switch the attached client back to the last session.
    r           Force redraw of the attached client.

实战演练
--------
### Window

tmux的window与firefox/vim的Tab, 本质上是一样的, 只是名字不同而已.
至于叫什么名字, 萝卜青菜各有所爱.
我假设你已经见过firefox/vim了, 我就不费力气解释了.

    # 新建一个Tab
    tmux new-window (prefix + c)
    # 根据索引选择Tab
    tmux select-window -t :0-9 (prefix + 0-9)
    # 重命名Tab
    tmux rename-window (prefix + ,)
        rename the current window

### Pane

pane是tmux的亮点(cool), 如果要向别人推销tmux的话, 我猜pane是最能吸引眼球的.
特别是, 通过鼠标点击的傻瓜方式, 在不同的pane之间进行切换, 不得不让人感到愉悦!
彻底打败了GNU screen.

    # 水平分割
    tmux split-window (prefix + ")
    # 竖直分割
    tmux split-window -h (prefix + %)
    # 交换pane
    tmux swap-pane -[UDLR] (prefix + { or })
    # 选择pane
    tmux select-pane -[UDLR]
    # 选择下一个pane
    tmux select-pane -t :.+

### Session

你可以把一组功能类似的window, 组织成是一个session.
这样做的好处是, 可以很明确地知道自己在干嘛(play OR work).
比如, 你可以定义这两个:

- work - 包含几个用vim打开的文件, 一个clock, 也许还有emacs
- play - 包含一个mpg321, 一个还未完成的curl命令(准备批量下载图片)

<br>

    # 创建一个名称为session_name的session
    tmux new -s session_name
    # 挂载一个已经存在的名称为session_name的session
    tmux attach -t session_name
    # 切换到一个已经存在的名称为session_name的session
    tmux switch -t session_name
    # 列出所有已经存在的session
    tmux list-sessions
    # 卸载当前挂载的session
    tmux detach (prefix + d)

配置文件
------------

    # 重新绑定prefix
    # xmodmap -e 'keycode 66 = Insert' &> /dev/null # 映射CapsLock为Insert
    unbind C-b
    set -g prefix IC
    bind IC send-prefix

    # 重新加载配置文件
    bind F5 source-file ~/.tmux.conf

    # 使用<Tab>快速地切换pane
    bind -r Tab select-pane -t :.+

    # 在copy时使用vi快捷键
    setw -g mode-keys vi

    # 启用鼠标
    set -g mouse-resize-pane on
    set -g mouse-select-pane on
    set -g mouse-select-window on

... 未完待续 ...

参考
----
- <http://tmux.sourceforge.net/>
- <https://wiki.archlinux.org/index.php/Tmux>
- 我的配置: [~/.tmux.conf](https://raw.github.com/gotovoid/dot/master/.tmux.conf)

视频
----
- [优酷](http://v.youku.com/v_show/id_XNDA1NTM1MDQ0.html)
- [下载](http://ubuntuone.com/7HUPgFOU7kbBPvkSjlsrpd)

![img](http://upload.wikimedia.org/wikipedia/commons/thumb/5/50/Tmux.png/320px-Tmux.png)
![cartoon](http://media.pragprog.com/images/cms/bhtmux-cartoon.jpg)
