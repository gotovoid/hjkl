---
layout:     post
title:      理解UTC时间
comments:   true
category:   basic
tags:       [basic, utc]
published:  true
---

基本概念

- Unix time, the number of seconds since 00:00:00 UTC on January 1, 1970.
- Unix timestamp is a floating point number expressed in seconds since the epoch, in UTC.

在linux中，可以用date命令, 转换时间格式; 但是时间中隐含的时区往往被忽视;
在进行时间处理时, 建议统一使用UTC时间.

    # 把Local时间转换成UNIX时间
    $ date -d '2009-05-13 12:34:15' +%s
    1242189255

    # 上述命令，隐含了系统预设时区CST(China Standard Time)
    $ date -d '2009-05-13 12:34:15 CST' +%s
    $ date -d '2009-05-13 12:34:15 +0800' +%s
    1242189255

    # 可以指明是UTC时间(Coordinated Universal Time)
    $ date -d '2009-05-13 12:34:15 UTC' +%s
    $ date -ud '2009-05-13 12:34:15' +%s
    $ TZ=UTC date -d '2009-05-13 12:34:15' +%s
    1242218055

    # 可以看出UTC与CST之间差了+08:00
    # 中国人吃午饭时，英国人才起床
    $ echo $(((1242218055-1242189255)/3600))
    8

    # 把UNIX时间转换成Local时间
    $ date -d @1242189255 +'%F %T'
    2009-05-13 12:34:15

    # 把UNIX时间转换成UTC时间
    $ date -ud @1242218055 +'%F %T'
    2009-05-13 12:34:15


一个完整的时间戳包含3个部分:

- date
- time
- utcoffset [+HHMM or -HHMM]

也就是说:

    1970-01-01 06:00:00 +0500 == 1970-01-01 01:00:00 +0000 == UNIX timestamp:3600

    $ python3
    >>> from datetime import datetime
    >>> from calendar import timegm
    >>> tm = '1970-01-01 06:00:00 +0500'
    >>> fmt = '%Y-%m-%d %H:%M:%S %z'
    >>> timegm(datetime.strptime(tm, fmt).utctimetuple())
    3600


    $ python3
    >>> from datetime import datetime, timezone, timedelta
    >>> from calendar import timegm
    >>> dt = datetime(1970, 1, 1, 6, 0)
    >>> tz = timezone(timedelta(hours=5))
    >>> timegm(dt.replace(tzinfo=tz).utctimetuple())
    3600


参考: <https://wiki.archlinux.org/index.php/Time>

