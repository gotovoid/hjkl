---
layout: post
title: 在firefox中使用vi/emacs快捷键
category: firefox
tags: [firefox, vim, emacs, shortcuts]
---

## 工具
- `firefox`
- 高级文本编辑器: `vim`, `notepad++`等
- 压缩/解压缩工具: `zip`/`unzip`, `7z`等

## 修改`omni.ja`
### 解压缩`omni.ja`
    mkdir ~/firefox && cd ~/firefox
    cp /usr/lib/firefox/omni.ja .
    unzip omni.ja -d omni
    cd omni

### 编辑`platformHTMLBindings.xml`
    vim ./chrome/toolkit/content/global/platformHTMLBindings.xml

{% highlight xml %}
<?xml version="1.0"?>

<bindings id="htmlBindings"
   xmlns="http://www.mozilla.org/xbl"
   xmlns:xul="http://www.mozilla.org/keymaster/gatekeeper/there.is.only.xul">
 
  <binding id="inputFields">
    <handlers>

      <!--Emacs BEGIN-->
      <handler event="keypress" key="a" modifiers="control" command="cmd_beginLine"/>
      <handler event="keypress" key="e" modifiers="control" command="cmd_endLine"/>
      <handler event="keypress" key="b" modifiers="control" command="cmd_charPrevious"/>
      <handler event="keypress" key="f" modifiers="control" command="cmd_charNext"/>
      <handler event="keypress" key="h" modifiers="control" command="cmd_deleteCharBackward"/>
      <handler event="keypress" key="d" modifiers="control" command="cmd_deleteCharForward"/>
      <handler event="keypress" key="w" modifiers="control" command="cmd_deleteWordBackward"/>
      <handler event="keypress" key="u" modifiers="control" command="cmd_deleteToBeginningOfLine"/>
      <handler event="keypress" key="k" modifiers="control" command="cmd_deleteToEndOfLine"/>
      <!--Emacs End-->

    </handlers>
  </binding>

  <binding id="browser">
    <handlers>

      <!-- VIM BEGIN -->
      <handler event="keypress" key="h" command="cmd_scrollLeft"/>
      <handler event="keypress" key="j" command="cmd_scrollLineDown"/>
      <handler event="keypress" key="k" command="cmd_scrollLineUp"/>
      <handler event="keypress" key="l" command="cmd_scrollRight"/>
      <handler event="keypress" key="g" command="cmd_scrollTop"/>
      <handler event="keypress" key="g" modifiers="shift" command="cmd_scrollBottom"/>
      <handler event="keypress" key="b" command="cmd_movePageUp"/>
      <handler event="keypress" key="f" command="cmd_movePageDown"/>
      <handler event="keypress" key="w" command="cmd_selectWordNext"/>
      <handler event="keypress" key="w" modifiers="shift" command="cmd_selectWordPrevious"/>
      <handler event="keypress" key="v" command="cmd_selectEndLine"/>
      <handler event="keypress" key="v" modifiers="shift" command="cmd_selectBeginLine"/>
      <handler event="keypress" key="h" modifiers="shift" command="cmd_selectCharPrevious" />
      <handler event="keypress" key="l" modifiers="shift" command="cmd_selectCharNext" />
      <handler event="keypress" key="c" command="cmd_copy" />
      <!-- VIM ENG -->

    </handlers>
  </binding>

</bindings>
{% endhighlight %}

### 压缩/覆盖`omni.ja`
    zip -r omni.ja *
    sudo mv omni.ja /usr/lib/firefox/

## 效果
### 在文本框中
- <kbd>C-a</kbd> 光标跳到行首
- <kbd>C-e</kbd> 光标跳到行尾
- <kbd>C-b</kbd> 光标向左移动一位
- <kbd>C-f</kbd> 光标向右移动一位
- <kbd>C-h</kbd> 删除光标前一个字符
- <kbd>C-d</kbd> 删除光标后一个字符
- <kbd>C-w</kbd> 删除光标前一个单词
- <kbd>C-u</kbd> 删除到行首
- <kbd>C-k</kbd> 删除到行尾

### 在页面中
- <kbd>h</kbd><kbd>j</kbd><kbd>k</kbd><kbd>l</kbd> 分别向左/下/上/右托动页面
- <kbd>g</kbd> 跳到页首
- <kbd>G</kbd> 跳到页尾
- <kbd>b</kbd> 向上翻页
- <kbd>f</kbd> 向下翻页
- <kbd>w</kbd> 向后选择单词
- <kbd>W</kbd> 向前选择单词
- <kbd>v</kbd> 向后选择到行尾
- <kbd>V</kbd> 向前选择到行首
- <kbd>H</kbd> 向前选择字符
- <kbd>L</kbd> 向后选择字符
- <kbd>c</kbd> 复制选中的内容

## 注意事项
一定要[启用/禁用]任意一个插件, 来重新加载`omni.ja`
