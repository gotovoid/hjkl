---
layout: post
title: 调整firefox右击菜单顺序
category: firefox
tags: [firefox]
---

## 说明
如果需要改变`firefox`自带的菜单顺序, 可以直接修改`omni.ja`的`browser.xul`文件, 详情请参考[[firefox-add-context-menu]];

本文以`firebug`为例, 介绍怎样调整`firebug`提供的`Inspect Element with Firebug`菜单的相对位置.

## 工具
- `firefox`
- `firebug`
- 高级文本编辑器: `vim`, `notepad++`等
- 压缩/解压缩工具: `zip`/`unzip`, `7z`等

## 解压缩`firebug.xpi`
    mkdir firefox && cd firefox
    cp ~/.mozilla/firefox/*.default/extensions/firebug@software.joehewitt.com.xpi .
    unzip firebug@software.joehewitt.com.xpi -d firebug
    cd firebug

## 编辑`browserMenuOverlay.xul`
    vim ./content/firebug/firefox/browserMenuOverlay.xul

{% highlight xml %}
<!-- Firefox page context menu -->
<menupopup id="contentAreaContextMenu">
    <menuitem id="menu_firebugInspect" label="firebug.InspectElementWithFirebug"
              command="cmd_inspect" class="menuitem-iconic fbInternational"
              insertafter="context-inspect" />
</menupopup>
{% endhighlight %}

## 压缩/覆盖`firebug.xpi`
    zip -r firebug@software.joehewitt.com.xpi *
    mv firebug@software.joehewitt.com.xpi * ~/.mozilla/firefox/*.default/extensions/

## 效果
    |------------------------------|
    | View Background Image        |
    |------------------------------|
    | View Page Source             |
    | View Page Info               |
    |------------------------------|
    | Inspect Element(Q)           |
    | Inspect Element with Firebug |
    |------------------------------|
    | Toggle Proxy                 |
    | Restart                      |
    | *Quit*                       |
    |------------------------------|
