---
layout:     post
title:      tmux教程
comments:   true
category:   tmux
tags:       [tmux, terminal, screencast, beta]
published:  true
---

介绍
-------
> `tmux` is a terminal multiplexer: it enables a number of terminals (or windows),
> each running a separate program, to be created, accessed, and controlled from a
> single screen. tmux may be detached from a screen and continue running in the
> background, then later reattached.

![img](http://upload.wikimedia.org/wikipedia/commons/thumb/5/50/Tmux.png/320px-Tmux.png)

`tmux`是个终端复用器：它让你在一个屏幕中, 创建/操作/控制若干终端（或窗口），
每个窗口都可以独立地运行程序。`tmux`可以脱离屏幕在后台继续运行，稍后可复位。

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
    &           Kill the current window.
    '           Prompt for a window index to select.'
    ,           Rename the current window.
    .           Prompt for an index to move the current window.
    0 to 9      Select windows 0 to 9.
    c           Create a new window.
    n           Change to the next window.
    p           Change to the previous window.
    M-n         Move to the next window with a bell or activity marker.
    M-o         Rotate the panes in the current window backwards.
    M-p         Move to the previous window with a bell or activity marker.

### pane
    C-o         Rotate the panes in the current window forwards.
    !           Break the current pane out of the window.
    "           Split the current pane into two, top and bottom."
    %           Split the current pane into two, left and right.
    ;           Move to the previously active pane.
    f           Prompt to search for text in open windows.
    i           Display some information about the current window.
    l           Move to the previously selected window.
    o           Select the next pane in the current window.
    q           Briefly display pane indexes.
    w           Choose the current window interactively.
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
    #           List all paste buffers.
    -           Delete the most recently copied buffer of text.
    =           Choose which buffer to paste interactively from a list.
    [           Enter copy mode to copy text or view the history.
    ]           Paste the most recently copied buffer of text.
    Page Up     Enter copy mode and scroll one page up.

### client/session
    $           Rename the current session.
    D           Choose a client to detach.
    d           Detach the current client.
    r           Force redraw of the attached client.
    s           Select a new session for the attached client interactively.
    L           Switch the attached client back to the last session.

配置文件
------------
我的配置: [~/.tmux.conf](https://raw.github.com/gotovoid/dot/master/.tmux.conf)

... 未完待续 ...

参考
----
- [官网](http://tmux.sourceforge.net/)
- [wiki](https://wiki.archlinux.org/index.php/Tmux)

视频
----
- [优酷](http://v.youku.com/v_show/id_XNDA1NTM1MDQ0.html)
- [下载](http://ubuntuone.com/7HUPgFOU7kbBPvkSjlsrpd)
