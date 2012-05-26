---
layout: post
title: 免费SSH看Youtube
category: ssh
tags: [ssh, plink, gfw, screencast]
---

## 工具介绍
- `plink`/`ssh` - SSH客户端
- `firefox` - 网页浏览器
- `vim` - 高级文本编辑器

## 安装plink
- Windows: [下载plink.exe](http://the.earth.li/~sgtatham/putty/latest/x86/plink.exe)
- Ubuntu:
    sudo apt-get install putty-tools

## 使用plink

    # 需要手动输入密码
    ssh -N -D 8888 freessh@jp.uudaili.com

    # plink的优点: 提供了`-pw`选项
    plink -N -D 8888 -pw 84601359 freessh@jp.uudaili.com

## bash脚本
{% highlight bash %}
#!/usr/bin/env bash
# gfw.sh
# free ssh

while :
do
    clear
    echo "Connecting ..."
    arr=($(
            curl -s http://ssh.emdao.com/freessh.php |
                iconv -f gbk -t utf8 |
                    grep -Po '(?<=: ).*(?=<br)'
    ))
    host=${arr[0]}
    user=${arr[1]}
    pass=${arr[2]}
    port=8888
    clear
    echo "HOST: $host"
    echo "USER: $user"
    echo "PASS: $pass"
    echo "PORT: $port"
    echo "TIME: $(date +'%F %T')"
    plink -N -D $port -pw $pass $user@$host &>/dev/null
done
{% endhighlight %}

另一个脚本

{% highlight bash %}
#!/usr/bin/env bash
# gfw2.sh
# free ssh

cat >gfw.yql << "_EOF_"
SELECT content
FROM html
WHERE url='https://www.usassh.com/free.php'
    AND xpath='//font[@color="red"][not(contains(text(), "。"))]'
LIMIT 1
_EOF_

while :
do
    clear
    echo "Connecting ..."
    host=free.usassh.com
    user=usassh
    pass=$(curl -s --data-urlencode 'q@gfw.yql' http://query.yahooapis.com/v1/public/yql |
            xmlstarlet sel -t -m //font -v .)
    port=9999
    if [[ -z $pass ]]
    then
        continue
    fi
    clear
    echo "HOST: $host"
    echo "USER: $user"
    echo "PASS: $pass"
    echo "PORT: $port"
    echo "TIME: $(date +'%F %T')"
    plink -N -D $port -pw $pass $user@$host &>/dev/null
done

rm gfw.yql
{% endhighlight %}

## 运行脚本
    chmod +x gfw.sh
    ./gfw.sh

###output:
    HOST: jp.uudaili.com
    USER: freessh
    PASS: 24670538
    PORT: 8888
    TIME: 2012-05-25 08:11:09

## 设置firefox
- Edit->Preferences->Advanced->Network->Settings...<br>
  Manual proxy configuration:<br>
  SOCKS Host: 127.0.0.1     Port: 8888
- 在地址栏中输入: _about:config_
- System Settings -> Network -> Network proxy

## 视频演示
- [优酷](http://v.youku.com/v_show/id_XNDAxOTkzNzcy.html)
- [下载](http://ubuntuone.com/4kBLIAdLhlBc0l3PcIUe09)

## 免费SSH
<iframe src="http://ssh.emdao.com/freessh.php" style="background-color: white;"></iframe>

