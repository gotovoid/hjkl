---
layout: post
title: 增加firefox右击菜单
category: firefox
tags: [firefox]
---

## 工具
- `firefox`
- 高级文本编辑器: `vim`, `notepad++`等
- 压缩/解压缩工具: `zip`/`unzip`, `7z`等

## 修改`omni.ja`
### 备份`omni.ja`
    sudo cp /usr/lib/firefox/omni.ja{,.bk}
    
### 解压缩`omni.ja`
    mkdir ~/firefox && cd ~/firefox
    unzip /usr/lib/firefox/omni.ja -d omni
    # 7z x /usr/lib/firefox/omni.ja -oomni
    cd omni

### 编辑`browser.xul`
    vim ./chrome/browser/content/browser/browser.xul

{% highlight xml %}
<menupopup id="contentAreaContextMenu">
    <!-- SKIP -->
    <!-- SKIP -->
    <!-- SKIP -->
    <menuitem id="context-inspect"/>

    <!-- ADD by Kev++ BEGIN -->
    <menuseparator id="kev-separator"/>

    <menuitem id="context-toggle-proxy"
              label="Toggle Proxy"
              oncommand="var stat = gPrefService.getIntPref('network.proxy.type');
                         var port = gPrefService.getIntPref('network.proxy.socks_port');
                         this.setAttribute('label', 'Toggle Proxy: '+port.toString());
                         if(!stat)
                             this.setAttribute('checked', 'true');
                         else
                             this.removeAttribute('checked');
                         gPrefService.setIntPref('network.proxy.type', !stat);"
              />

    <menuitem id="context-restart"
              label="Restart"
              oncommand="const nsIAppStartup = Components.interfaces.nsIAppStartup;
                         Components.classes['@mozilla.org/toolkit/app-startup;1'].getService(nsIAppStartup)
                                   .quit(nsIAppStartup.eRestart | nsIAppStartup.eAttemptQuit);"
              />

    <menuitem id="context-quit"
              label="Quit"
              command="cmd_quitApplication"
              />
    <!-- ADD by Kev++ END -->

</menupopup>
{% endhighlight %}

> 说明: 把代码插入到不同的位置, 可以改变菜单项的排列顺序

### 压缩/覆盖`omni.ja`
    zip -r omni.ja *
    # 7z a -tzip -mx0 omni.ja *
    sudo mv omni.ja /usr/lib/firefox/

## 最终效果
    | ...          |
    |--------------|
    | Toggle Proxy |
    | Restart      |
    | *Quit*       |
    |--------------|

## 注意事项
一定要[启用/禁用]任意一个插件, 来重新加载`omni.ja`

## 参考
- <https://developer.mozilla.org/en/XUL/PopupGuide/Extensions>
- <http://superuser.com/questions/421800/how-to-append-customer-context-menuitem-to-the-last-postion-in-firefox>
- <http://superuser.com/questions/421809/how-to-add-a-proxy-on-off-context-menuitem-to-firefox>
- <http://kb.mozillazine.org/Firefox_:_Tips_:_Customize_context_menu>
- <http://kb.mozillazine.org/UserChrome.css_Element_Names/IDs>
- <https://developer.mozilla.org/en/FirefoxOverlayPoints/Menus>
- <http://www.rdrop.com/~half/Creations/Writings/TechNotes/firefox.menus.html>
