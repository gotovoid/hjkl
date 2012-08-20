---
layout:    default
title:     Vim Plugin
comments:  true
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
- **nerdtree**
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
    - 若不作特殊说明, 下文一律使用`pathogen`来管理新插件.

## tabular

- 插件介绍: 快速对齐
- 下载地址: <https://github.com/godlygeek/tabular>
- 使用方法:
    - 按下<kbd>:Tabularize /=</kbd>, 对`=`进行左对齐
    - 按下<kbd>:Tabularize /=/r1c1l0</kbd>
        - 对`=`前进行右对齐(后面跟一个空格)
        - 对`=`进行居中对齐(后面跟一个空格)
        - 对`=`后进行左对齐(后面不跟空格)


## sparkup

- 插件介绍: zencoding
- 下载地址: <https://github.com/rstacruz/sparkup>
- 使用方法:
    - 按下<kbd>Ctrl-e</kbd>后, 以当前行为参数传递给`sparkup.py`脚本, 把返回的HTML替换掉原来的行.
    - 按下<kbd>Ctrl-n</kbd>后, 自动跳到空Tag/Attr里面.
- 图片资料:
    - <http://html5tutorial.net/wp-content/uploads/2009/09/html4-structure-div.gif>
    - <http://html5tutorial.net/wp-content/uploads/2009/09/html5-structure-div1.gif>
    - <http://media.smashingmagazine.com/wp-content/uploads/images/html5/html5_structure.png>
- 注意事项: 该插件只能在编辑HTML时才会生效, 也可以通过`:set ft=html`强制生效.

## surround

- 插件介绍: 把文本包围起来
- 下载地址: <https://github.com/tpope/vim-surround>
- 使用方法:
    - 按下<kbd>ys</kbd>, 添加surround
    - 按下<kbd>cs</kbd>, 改变surround
    - 按下<kbd>ds</kbd>, 删除surround
    - 按下<kbd>S</kbd>, surround选中的
- 注意事项: 通过安装[repeat.vim](https://github.com/tpope/vim-repeat), 来支持<kbd>.</kbd>(repeat)操作

## command-T

- 插件介绍: 模糊文件查找
- 下载地址: <http://www.vim.org/scripts/script.php?script_id=3025>
- 使用方法:
    - <kbd>:CommandT</kbd>, 打开搜索框, 查找file
    - <kbd>:CommandTBuffer</kbd>, 打开搜索框, 查找buffer
    - <kbd>Ctrl-k</kbd>/<kbd>Ctrl-j</kbd>, 在列表中, 上下导航
    - <kbd>Enter</kbd>, 在当前窗口, 打开选中的文件
    - <kbd>Ctrl-t</kbd>, 在新Tab中, 打开选中的文件
    - <kbd>Ctrl-s</kbd>/<kbd>Ctrl-v</kbd>, 分割当前窗口, 打开选中的文件
    - <kbd>Ctrl-c</kbd>/<kbd>Esc</kbd>, 不打开任何文件, 并关闭搜索框
- 注意事项: vim需要支持ruby扩展. 在vim中输入`:ruby 1`报错, 就表示不支持.

## yankring

- 插件介绍: 一个粘贴板队列
- 下载地址: <http://www.vim.org/scripts/script.php?script_id=1234>
- 使用方法:
    - <kbd>:YRShow</kbd>, 打开YankRing窗口
    - <kbd>:YRClear</kbd>, 清空YankRing
    - <kbd>p</kbd>, 粘贴YankRing中最顶的一个
    - <kbd>Ctrl-p</kbd>, 粘贴YankRing中上一个
    - <kbd>Ctrl-n</kbd>, 粘贴YankRing中下一个

## fugitive

- 插件介绍: 我的天哪, fugitive太强大了, 不会是非法的吧!
- 下载地址: <https://github.com/tpope/vim-fugitive>
- 使用方法:
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

- 插件介绍: 轻量级中文输入法
- 下载地址: <https://github.com/gotovoid/dot/raw/master/.vim/plugin/minim.vim>
- 使用方法: <kbd>Ctrl-x</kbd><kbd>Ctrl-u</kbd>, 调用插件中的MiniM函数, 以弹出菜单的形式显示候选词语.
- 严重警告: 不要输入敏感词, 否则后果自负!

## alternate

- 插件介绍: 让你快速地在`*.{h,cpp}`文件之间切换
- 下载地址: <http://www.vim.org/scripts/script.php?script_id=31>
- 使用方法:
    - <kbd>:A</kbd>, 类似于`:e %:r.cpp`
    - <kbd>:AV</kbd>, 类似于`:vsplit`
    - <kbd>:AS</kbd>, 类似于`:split`
    - <kbd>:AT</kbd>, 类似于`:tabe`
    - <kbd>:let g:alternateExtensions_foo = 'bar,baz'</kbd>, 定义新的绑定: `foo <=> bar,baz`

## easymotion

- 插件介绍: 先精确定位, 再跳上去.
- 下载地址: <https://github.com/Lokaltog/vim-easymotion>
- 使用方法:
    - 首先`:let mapleader=','`(最好在`vimrc`中设置)
    - 然后输入<kbd>,,f</kbd>{char}, 从光标位置处向后查找所有{char}, 并且临时把它们替换成a,b,c...
    - 最后输入<kbd>b</kbd>, 光标就跳到第二个{char}上了.

## vimwiki

- 插件介绍: 个人日记本
- 下载地址: <http://code.google.com/p/vimwiki/downloads/list>
- 注意事项: 先把vim基本功练好, 再玩这个插件!

## gist

- 插件介绍: github代码片断管理及分享
- 下载地址: <https://github.com/mattn/gist-vim>
- 使用方法:
    - <kbd>:Gist</kbd>, 上传当前文件
    - <kbd>:Gist -l</kbd>, 列出所有gist
    - <kbd>:Gist -d</kbd>, 删除当前gist
    - <kbd>:w</kbd>, 更新当前gist

## gundo

- 插件介绍: 以可视化的方式显示Undo Tree
- 下载地址: <http://sjl.bitbucket.org/gundo.vim/>
- 使用方法:
    - <kbd>:GundoToggle</kbd>, 显示/隐藏Undo Tree
    - <kbd>:GundoRenderGraph</kbd>, 刷新Undo Tree
- 注意事项: 本插件需要python

## nerdtree

- 插件介绍: 在vim左侧显示目录结构, 给打开文件提供了方便
- 下载地址: <https://github.com/scrooloose/nerdtree>

## file:line

- 插件介绍: 打开文件, 并且把光标置于指定行与列
- 下载地址: <https://github.com/bogado/file-line>

## space

- 插件介绍: 智能地改变<kbd>Space</kbd>的功能, 便捷地跳到下一个位置
- 下载地址: <https://github.com/spiiph/vim-space>
- 使用方法:
    - 使用<kbd>/search</kbd>, <kbd>fx</kbd>, <kbd>]c</kbd>等命令后, 动态改变<kbd>Space</kbd>的功能
    - <kbd>Space</kbd>, 跳到下一个位置
    - <kbd>Shift-Space</kbd>, 跳到前一个位置

--------

## 视频演示

<table><tbody>
        <tr id="header-file" class="changerow"><td colspan="4">Files</td></tr>
        <tr id="fusgqDkXWR9QDWaOoYtL6E0EA" class="file published" title="File (published)">
            <td class="files-td-name" id="vim-plugin-alternate.mp4">
                <a id="yui_3_5_1_2_1345450292603_490" href="http://ubuntuone.com/2DQmmjZrkoWcj87RyobCSo" target="_blank">vim-plugin-alternate.mp4</a>
            </td>
            <td class="files-td-size">
                12.7 MB
            </td>
        </tr>
        <tr id="fusP__4cfaXTiCJvCIDH8Mxkg" class="file published" title="File (published)">
            <td class="files-td-name" id="vim-plugin-commandt.mp4">
                <a href="http://ubuntuone.com/6V1VCmjV8Ip4i4fWnLbqxi" target="_blank">vim-plugin-commandt.mp4</a>
            </td>
            <td class="files-td-size">
                20.3 MB
            </td>
        </tr>
        <tr id="fusaE48TSSNR8yDcNkmGZs5PA" class="file published" title="File (published)">
            <td class="files-td-name" id="vim-plugin-ctrlp.mp4">
                <a href="http://ubuntuone.com/6EULQ171CI1zDFE50k3SC5" target="_blank">vim-plugin-ctrlp.mp4</a>
            </td>
            <td class="files-td-size">
                15.6 MB
            </td>
        </tr>
        <tr id="fusFad2HmBASqaEknj_PiB-bg" class="file published" title="File (published)">
            <td class="files-td-name" id="vim-plugin-esaymotion.mp4">
                <a href="http://ubuntuone.com/2jrZHJczywoEOR17CRNDJG" target="_blank">vim-plugin-esaymotion.mp4</a>
            </td>
            <td class="files-td-size">
                7.5 MB
            </td>
        </tr>
        <tr id="fus_Ra_MztEQjibAoVYIim4cg" class="file published" title="File (published)">
            <td class="files-td-name" id="vim-plugin-fileline.mp4">
                <a href="http://ubuntuone.com/1OCQNPduDyoycQpVCUemDP" target="_blank">vim-plugin-fileline.mp4</a>
            </td>
            <td class="files-td-size">
                7.3 MB
            </td>
        </tr>
        <tr id="fus0iqQ02ZeSVyMiqXQjhNTdg" class="file published" title="File (published)">
            <td class="files-td-name" id="vim-plugin-fugitive.mp4">
                <a href="http://ubuntuone.com/5CrzdLv8uDXPQ6Ug9JM8dd" target="_blank">vim-plugin-fugitive.mp4</a>
            </td>
            <td class="files-td-size">
                29.6 MB
            </td>
        </tr>
        <tr id="fusOTGaXc5JSZOk64ZJNFNhww" class="file published" title="File (published)">
            <td class="files-td-name" id="vim-plugin-gist.mp4">
                <a href="http://ubuntuone.com/4WzqWgepRiPOftZdmeHjli" target="_blank">vim-plugin-gist.mp4</a>
            </td>
            <td class="files-td-size">
                20.2 MB
            </td>
        </tr>
        <tr id="fusCiHQx155T-eHLZTx-7xkDg" class="file published" title="File (published)">
            <td class="files-td-name" id="vim-plugin-gundo.mp4">
                <a href="http://ubuntuone.com/47hQCxnszNc0qi5HtSNLJY" target="_blank">vim-plugin-gundo.mp4</a>
            </td>
            <td class="files-td-size">
                16.9 MB
            </td>
        </tr>
        <tr id="fusDt3vhbLnQ5C7azL-xYYpBQ" class="file published" title="File (published)">
            <td class="files-td-name" id="vim-plugin-intro.mp4">
                <a href="http://ubuntuone.com/2S6SDfQLtnwZSEmBpQCLg2" target="_blank">vim-plugin-intro.mp4</a>
            </td>
            <td class="files-td-size">
                7.5 MB
            </td>
        </tr>
        <tr id="fuswWXk1A6tT2SwdkiKWjAVGQ" class="file published" title="File (published)">
            <td class="files-td-name" id="vim-plugin-minim.mp4">
                <a href="http://ubuntuone.com/6leaNidZweQZnwVwjawo1V" target="_blank">vim-plugin-minim.mp4</a>
            </td>
            <td class="files-td-size">
                12.3 MB
            </td>
        </tr>
        <tr id="fusdO7kc6q1SPmRK6cbaCT5ZQ" class="file published" title="File (published)">
            <td class="files-td-name" id="vim-plugin-nerdtree.mp4">
                <a href="http://ubuntuone.com/3qRJNRHUmWpjS8jhcMwP1N" target="_blank">vim-plugin-nerdtree.mp4</a>
            </td>
            <td class="files-td-size">
                24.7 MB
            </td>
        </tr>
        <tr id="fusRc1-iMypT3mpxHvoyyUOOg" class="file published" title="File (published)">
            <td class="files-td-name" id="vim-plugin-pathogen.mp4">
                <a href="http://ubuntuone.com/4W5zsHdTUrdNaAnoPphx4F" target="_blank">vim-plugin-pathogen.mp4</a>
            </td>
            <td class="files-td-size">
                12.4 MB
            </td>
        </tr>
        <tr id="fusOeM18p3kQ8WI6F4LL3ny7Q" class="file published" title="File (published)">
            <td class="files-td-name" id="vim-plugin-space.mp4">
                <a href="http://ubuntuone.com/14wbQI5EC8VkA6HlsMh476" target="_blank">vim-plugin-space.mp4</a>
            </td>
            <td class="files-td-size">
                6.9 MB
            </td>
        </tr>
        <tr id="fusd-s54t0KTn-em13TetDKxg" class="file published" title="File (published)">
            <td class="files-td-name" id="vim-plugin-sparkup.mp4">
                <a href="http://ubuntuone.com/6dRS6SWspB930HX5JXkMfN" target="_blank">vim-plugin-sparkup.mp4</a>
            </td>
            <td class="files-td-size">
                18.0 MB
            </td>
        </tr>
        <tr id="fusNv1YtBFxS2S8Ie-G4BYL1A" class="file published" title="File (published)">
            <td class="files-td-name" id="vim-plugin-surround.mp4">
                <a href="http://ubuntuone.com/5GFZ86Y40G7i7RSMSC7uLh" target="_blank">vim-plugin-surround.mp4</a>
            </td>
            <td class="files-td-size">
                11.4 MB
            </td>
        </tr>
        <tr id="fusLBhlAvx5TxW9eJqIKGZ2bw" class="file published" title="File (published)">
            <td class="files-td-name" id="vim-plugin-tabular.mp4">
                <a href="http://ubuntuone.com/1g7GgouswR2bvQARF2WSmy" target="_blank">vim-plugin-tabular.mp4</a>
            </td>
            <td class="files-td-size">
                31.7 MB
            </td>
        </tr>
        <tr id="fusHC6eSrqgQCaE7c4Rcbi91g" class="file published" title="File (published)">
            <td class="files-td-name" id="vim-plugin-taglist.mp4">
                <a href="http://ubuntuone.com/6bSFVGcXCyuukbo6TyUvHK" target="_blank">vim-plugin-taglist.mp4</a>
            </td>
            <td class="files-td-size">
                13.1 MB
            </td>
        </tr>
        <tr id="fusa3EZNM2HQkid8dv6oB-9eQ" class="file published" title="File (published)">
            <td class="files-td-name" id="vim-plugin-vimwiki-1.mp4">
                <a href="http://ubuntuone.com/3PF5Geod2dq7oEtH9NePbL" target="_blank">vim-plugin-vimwiki-1.mp4</a>
            </td>
            <td class="files-td-size">
                39.9 MB
            </td>
        </tr>
        <tr id="fusaZf97OrSTbynhAxZsVerCQ" class="file published" title="File (published)">
            <td class="files-td-name" id="vim-plugin-vimwiki-2.mp4">
                <a href="http://ubuntuone.com/2n6QAQnuNoj085cMRmmWeO" target="_blank">vim-plugin-vimwiki-2.mp4</a>
            </td>
            <td class="files-td-size">
                36.4 MB
            </td>
        </tr>
        <tr id="fus11EtgzGAQ-2pHy9ZFfCyUw" class="file published" title="File (published)">
            <td class="files-td-name" id="vim-plugin-yankring.mp4">
                <a href="http://ubuntuone.com/4vlNxWhxsEQc2tUGTsMKW5" target="_blank">vim-plugin-yankring.mp4</a>
            </td>
            <td class="files-td-size">
                14.0 MB
            </td>
        </tr>
</table></tbody>

## [优酷专辑](http://www.youku.com/playlist_show/id_17756150.html)

**...未完待续...**
