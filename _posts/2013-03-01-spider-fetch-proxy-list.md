---
layout: post
title: 从网页中提取proxy列表
category: spider
tags: [spider]
---

从网上手动提取代理很耗时耗力, 写个自动抓取工具很有必要! 一劳永逸!

从<http://www.freeproxylists.net/>提取所有的(中国)HTTP代理(含翻页).

其中涉及到cookie及xpath等技术.

## 源代码

    #!/usr/bin/env python3
    # Extract HTTP Proxy List
    # by Kev++

    import sys
    from lxml import html
    from http.cookiejar import MozillaCookieJar
    from urllib.parse import unquote, urlencode
    from urllib.request import build_opener, HTTPCookieProcessor

    def fetch(cookie):
        cj = MozillaCookieJar()
        cj.load(cookie)
        opener = build_opener(HTTPCookieProcessor(cj))

        for pn in range(1, 10):
            url = 'http://www.freeproxylists.net/?' + urlencode({'c':'CN', 'pr':'HTTP', 'u':90, 'page': pn})
            data = opener.open(url).read().decode('utf-8')
            dom = html.fromstring(data)
            for e in dom.xpath('//table[@class="DataGrid"]//tr[@class="Odd" or @class="Even"][count(td)>1]'):
                x = e.xpath('./td[1]/script/text()')[0]
                l, r = x.find('"'), x.rfind('"')
                x = unquote(x[l+1:r])
                l, r = x.find('>'), x.rfind('<')
                ip = x[l+1:r]
                port = e.xpath('./td[2]/text()')[0]
                prot = e.xpath('./td[3]/text()')[0]
                print('{}:{}:{}'.format(prot, ip, port))
            if not dom.xpath('//div[@class="page"]/a[last() and contains(., "Next")]'):
                break

    if __name__=='__main__':
        fetch(sys.argv[1])

## COOKIE文件

    # Netscape HTTP Cookie File
    www.freeproxylists.net	FALSE	/	FALSE	1393663347	userno	20130228-014848
    www.freeproxylists.net	FALSE	/	FALSE	1393663347	refdomain	search.yahoo.com
    www.freeproxylists.net	FALSE	/	FALSE	1393663347	query	proxylist
    www.freeproxylists.net	FALSE	/	FALSE	1393663347	pv	13
    www.freeproxylists.net	FALSE	/	FALSE	1393643733	key	key
    www.freeproxylists.net	FALSE	/	FALSE	1393663347	hl	en
    www.freeproxylists.net	FALSE	/	FALSE	1393663347	from	link
    .freeproxylists.net	TRUE	/	FALSE	1377809030	__utmz	251962462.1362019453.1.1.utmcsr=yahoo|utmccn=(organic)|utmcmd=organic|utmctr=proxylist
    .freeproxylists.net	TRUE	/	FALSE	1425113030	__utmv	251962462.China
    .freeproxylists.net	TRUE	/	FALSE	0	__utmc	251962462
    .freeproxylists.net	TRUE	/	FALSE	1362042830	__utmb	251962462.14.10.1362040479
    .freeproxylists.net	TRUE	/	FALSE	1425113030	__utma	251962462.1608408579.1362019453.1362019453.1362040479.2
    www.freeproxylists.net	FALSE	/	FALSE	1425113030	__atuvc	10%7C9

## 运行结果

    HTTP:123.125.74.212:80
    HTTP:42.121.18.69:9088
    HTTP:211.142.236.137:80
    HTTP:122.72.80.46:80
    HTTP:122.72.28.15:80
    HTTP:58.211.121.20:80
    HTTP:122.72.80.107:80
    HTTP:61.132.225.35:80
    HTTP:122.72.28.24:80
    HTTP:211.151.171.207:80
    HTTP:211.142.236.137:8080
    HTTP:110.153.9.250:80
    HTTP:124.207.102.60:80
    HTTP:221.130.18.211:80
    HTTP:122.72.124.73:80
    HTTP:124.240.187.79:82
    HTTP:61.55.141.12:80
    HTTP:125.39.68.195:80
    HTTP:61.55.141.10:80
    HTTP:125.39.66.133:3128
    HTTP:125.39.25.202:8096
    HTTP:211.100.47.131:8990
    HTTP:60.195.251.213:8888
    HTTP:221.130.18.218:80
    HTTP:61.152.108.187:82
    HTTP:114.80.136.112:7780
    HTTP:222.185.143.254:80
    HTTP:180.95.129.231:80
    HTTP:211.142.236.132:81
    HTTP:221.3.153.74:80
    HTTP:122.72.80.108:80
    HTTP:14.17.29.112:80
    HTTP:211.151.171.206:80
    HTTP:116.255.148.5:3128
    HTTP:124.240.187.79:80
    HTTP:58.68.151.180:80
    HTTP:218.203.107.169:80
    HTTP:122.72.76.125:80
    HTTP:221.7.11.163:80
    HTTP:202.105.113.132:8080
    HTTP:202.96.155.251:8888
    HTTP:123.129.214.155:80
    HTTP:58.68.142.211:8080
    HTTP:218.61.8.124:88
    HTTP:118.244.190.5:80
    HTTP:61.135.209.203:81
    HTTP:122.72.28.19:80
    HTTP:120.203.214.182:86
    HTTP:118.244.190.6:80
    HTTP:183.221.250.137:80

