---
layout:     post
title:      打造markdown编辑器
comments:   true
category:   vim
tags:       [vim, screencast]
published:  true
---

网上有很多在线markdown编辑器, 当你在文本框内输入markdown后, 在右侧就同步显示相对应的HTML.  
根据该原理, 可以制作一个vim版的markdown编辑器. 由于vim不是web浏览器, 就在右侧显示HTML代码吧!

# 工具

- vim - 高级文本编辑器
- firefox - 网页浏览器
- markdown - markdown解析器
- pandoc - 增强版markdown解析器
- tidy - HTML格式化工具

# 配置

{% highlight vim %}
" vimrc4md
" Kev++@2012-06-27

" 基本配置
set nocompatible
set autoread
set expandtab tabstop=4 softtabstop=4 shiftwidth=4
set laststatus=2
set t_Co=256

" 转换Markdown为HTML
let mapleader = ','
nnoremap <leader>f  :silent! !firefox %<CR>
nnoremap <C-m>      !!markdown<CR>
vnoremap <C-m>      !markdown<CR>
nnoremap <C-p>      !!pandoc<CR>
vnoremap <C-p>      !pandoc<CR>

" 启用语法侦测
syntax on

" 自动化命令
au FileType markdown        let &l:mp='pandoc % \| tidy -q -i -utf8 --doctype omit --tidy-mark 0 --show-errors 0 -o %:r.html'
au FileType markdown        nnoremap <buffer> <F5> :write \| silent make \| redraw!<CR>
au BufWrite *.markdown      exe "normal \<F5>"

" 提取文章标题
com! -bar TOC call TOC()
fun! TOC()
    call setloclist(0, [])
    let save_cursor = getpos(".")
    call cursor(1, 1)
    let flag = 'cW'
    while search("^#", flag) > 0
        let flag = 'W'
        let msg = printf('%s:%d:%s', expand('%'), line('.'), substitute(getline('.'), '#', '»', 'g'))
        laddexpr msg
    endwhile
    call setpos('.', save_cursor)
    silent! call ToggleLocationList()
endfun

" 配置插件
let g:alternateExtensions_html = 'markdown'
let g:alternateExtensions_markdown = 'html'
set rtp+=~/.vim/bundle/powerline/
set rtp+=~/.vim/bundle/alternate/
let g:Powerline_symbols = 'fancy'

{% endhighlight %}

## 视频演示

- 下载
- 优酷
