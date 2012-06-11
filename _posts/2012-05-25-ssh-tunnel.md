---
layout: post
title: 免费SSH看Youtube
category: ssh
tags: [ssh, plink, gfw, screencast]
---

## 工具介绍
- `plink`/`ssh` - SSH命令行客户端, 也可以使用GUI工具`putty`.
- `firefox` - 网页浏览器
- `vim` - 高级文本编辑器

## 安装plink
- Windows: [下载plink.exe](http://the.earth.li/~sgtatham/putty/latest/x86/plink.exe)
- Ubuntu:
    sudo apt-get install putty-tools

## 使用plink

    # Ubuntu自带的ssh, 需要手动输入密码
    ssh -N -D 8888 freessh@jp.uudaili.com

    # plink的优点是, 提供了`-pw`选项
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

## 设置方法
- Edit->Preferences->Advanced->Network->Settings...<br>
  Manual proxy configuration: SOCKS Host: 127.0.0.1 Port: 8888
- 在firefox地址栏中输入: _about:config_, 并且查找**proxy**
- 对于Ubuntu系统: System Settings -> Network -> Network proxy

> 设置方法很多, 选择自己喜欢的即可.

----

## 翻墙连接github的方法
创建一个本地端口`2222`(任意), 重定向到`github.com:22`.
与`翻墙看Youtube`的唯一的区别在于, 在命令行中使用`-L`(local)选项.  

### 被墙症状
    $ git push
    ssh: connect to host github.com port 22: Connection timed out
    fatal: The remote end hung up unexpectedly

### 命令行
{% highlight bash %}
$ plink -N -L 2222:github.com:22 -pw 5736f    usassh@free.usassh.com
#             ---- -------------     -----    ------ ---------------
#              |        |              |         |         |
#              |        |              |         |         |
#              |        |              |         |         |
#             本地   github          SSH密码  SSH用户名 SSH服务器
{% endhighlight %}

### 修改配置
    $ vim .git/config
    
{% highlight conf %}
[remote "origin"]
	fetch = +refs/heads/*:refs/remotes/origin/*
    url = ssh://git@localhost:2222/username/project.git
{% endhighlight %}

### 上传代码
    $ git push

## 视频演示
- [优酷](http://v.youku.com/v_show/id_XNDAxOTkzNzcy.html)
- [下载](http://ubuntuone.com/4kBLIAdLhlBc0l3PcIUe09)

## 免费SSH
<iframe src="http://ssh.emdao.com/freessh.php" style="background-color: white;"></iframe>

