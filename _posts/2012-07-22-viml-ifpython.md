---
layout:     post
title:      使用python开发vim插件
category:   viml
tags:       [viml, python]
comments:   true
published:  true
---

一个麻雀虽小五脏俱全的天气预报函数`Weather(city)`, 使用自定义命令`:W beijing`可以调用之.  
可以把这段脚本放到`.vimrc`里面, 也可以放到`~/.vim/plugin/weather.vim`里面.


## 嵌入HERE-DOC

{% highlight vim %}
" Weather report
com! -nargs=1 W echo Weather(<f-args>)
fun! Weather(city)
    if !has('python')
        echoerr 'python is not supported!'
        return
    endif
python <<_EOF_
try:
    import vim
    import xml.etree.ElementTree as ET
    from urllib2 import urlopen
    from urllib import urlencode
    url = 'http://www.google.com/ig/api?' + urlencode({'hl':'zh-cn', 'weather':vim.eval('a:city')})
    xml = ET.XML(unicode(urlopen(url, timeout=5).read() ,'gb2312').encode('utf-8')).find('.//forecast_conditions')
    if xml is None:
        raise Exception('city not found!')
    weather = {x.tag:x.get('data').encode('utf-8') for x in xml.getchildren()}
    vim.command('return "%s(%s°C~%s°C)"' % (weather['condition'], weather['low'], weather['high']))
except Exception, e:
    vim.command('return "Error: %s"' % e)
_EOF_
endfun
{% endhighlight %}

## 注意事项

- 参考帮助文档`:help if_python.txt`查看接口细节
- 确保python很快就执行完毕, 否则vim会卡住不动
- 确保返回给vim的字符为UTF-8编码, 否则会出现乱码
- 使用到网络时, 最好加上异常处理
