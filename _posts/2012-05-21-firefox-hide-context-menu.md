---
layout: post
title: 隐藏firefox右击菜单
category: firefox
tags: [firefox]
---

## 工具
- `firefox`
- 高级文本编辑器: `vim`, `notepad++`等

## 创建`userChrome.css`
    vi ~/.mozilla/firefox/*.default/chrome/userChrome.css

{% highlight css %}
/*
 * Path: 
 *      Ubuntu: ~/.mozilla/firefox/*.default/chrome/userChrome.css
 *      Window: %AppData%\Mozilla\Firefox\Profiles\*.default\chrome\userChrome.css
 */

#context-back,
#context-forward,
#context-reload,
#context-stop,
#context-sep-stop,
#context-selectall,
#context-openlink,
#context-bookmarklink,
#context-bookmarkpage,
#context-savepage,
#context-sendpage,
#context-sendlink,
#context-sendimage,
#context-setWallpaper,
#context-setDesktopBackground,
#context-sep-viewbgimage {
    display: none;
}

menuitem[label="Quit"] {
    font-weight: bold !important;
    text-shadow: 1px 1px 1px #000;
}
{% endhighlight %}

## 效果
    |------------------------------|
    | View Background Image        |
    |------------------------------|
    | View Page Source             |
    | View Page Info               |
    |------------------------------|
    | Inspect Element(Q)           |
    |------------------------------|
    | Toggle Proxy                 |
    | Restart                      |
    | *Quit*                       |
    |------------------------------|
    | Inspect Element with Firebug |
    |------------------------------|
