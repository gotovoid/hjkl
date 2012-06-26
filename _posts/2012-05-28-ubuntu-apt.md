---
layout:    post
title:     使用APT软件包管理器
category:  tool
tags:      [tool, apt]
---

## 安装
    # 安装
    apt-get install <package>

##卸载
    # 卸载
    apt-get remove <package>
    # 完全卸载
    apt-get purge <package>

## 升级
    # 更新
    apt-cache update
    # 升级
    apt-cache upgrade

## 查询
    # 查找
    apt-cache search <pattern>
    # 描述
    apt-cache show <package>
    # 详情
    apt-cache showpkg <package>
    # 依赖
    apt-cache depands <package>
    # 归属
    apt-file search <file>
    # 归属(仅限已安装文件)
    dpkg -S <file>
    # 已安装package列表
    dpkg -l [<package>]

----

通过`apt-get install package`的时候, APT会从网上把`package.deb`软件包下载到缓存.  
**缓存**是为了下次重新安装package时, 不用再重新下载它. 缓存的路径为: `/var/cache/apt/archives/`.  
随着时间的推移, 这个文件夹会越来越大, 其中可能会有包含已经过期的软件包.

比如说, 当你安装gvim7.3后, 又安装了gvim7.4, 那么缓存会同时包含了2个不同版本的gvim.  
然而, gvim7.3已经属于过期软件了, 留在那里只会浪费磁盘空间.

下面介绍如何清理APT缓存的软件包

### 清理已过期的软件包

    sudo apt-get autoclean

### 清空所有软件包

    sudo apt-get clean

>如果你卸载package后, 又重新安装, 则会重新下载


## 参考：
- https://help.ubuntu.com/community/Repositories/CommandLine
- https://help.ubuntu.com/community/AptGet/Howto
