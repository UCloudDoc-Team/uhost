# 优化DNS配置方法

## Step 1  配置冗余DNS Server地址

可防止DNS Server单点故障后，域名无法解析的情况。

以CentOS为例：

打开主机内/etc/resolv.conf文件，

若文件中只配置了1个IP，根据如下列表，替换为以下2个IP：

| 机房/可用区              | IP                                                 |
| ------------------------ | -------------------------------------------------- |
| 北京二可用区B            | 10.9.255.1，10.9.255.2                             |
| 北京二可用区C            | 10.10.255.1，10.10.255.2                           |
| 北京二可用区D            | 10.19.255.1，10.19.255.2                           |
| 北京二可用区E            | 10.42.255.1，10.42.255.2                           |
| 乌兰察布可用区A          | 100.65.128.2，100.65.128.3                         |
| 广东可用区B              | 10.13.255.1，10.13.255.2                           |
| 香港可用区A，香港可用区B | 10.8.255.1，10.8.255.2                             |
| 洛杉矶可用区A            | 10.11.255.1，10.11.255.2                           |
| 新加坡可用区B            | 10.35.224.212，10.35.250.52                        |
| 新加坡可用区A            | 10.35.255.1，10.35.255.2                           |
| 泰国曼谷可用区A          | 10.31.255.1，10.31.255.2                           |
| 华盛顿可用区A            | 10.27.255.1，10.27.255.2                           |
| 法兰克福可用区A          | 10.29.255.1，10.29.255.2                           |
| 韩国首尔可用区A          | 10.33.255.1，10.33.255.2                           |
| 俄罗斯莫斯科可用区A      | 10.39.255.1，10.39.255.2                           |
| 日本东京可用区A          | 10.40.255.1，10.40.255.1，10.40.255.2，10.40.255.2 |
| 台湾台北可用区A          | 10.41.255.1，10.41.255.1，10.41.255.2，10.41.255.2 |
| 阿联酋迪拜可用区A        | 10.44.255.1，10.44.255.2                           |
| 印尼雅加达可用区A        | 10.45.255.1，10.45.255.2                           |
| 印度孟买可用区A          | 10.47.255.1，10.47.255.2                           |
| 巴西圣保罗可用区A        | 10.49.255.1，10.49.255.2                           |
| 英国伦敦可用区A          | 10.50.255.1，10.50.255.2                           |
| 马尼拉可用区A            | 100.64.48.2，100.64.48.3                           |
| 泰国曼谷可用区B          | 10.31.255.11，10.31.255.10                         |
| 拉各斯可用区A            | 10.52.255.1，10.52.255.2                           |
| 越南胡志明可用区A        | 100.64.0.2，100.64.0.3                             |
| 上海二可用区B            | 10.23.255.1，10.23.255.2                           |


## Step 2  开启NSCD服务

在Linux中开启NSCD服务可在本地缓存DNS解析结果。在TTL时间内，无需去DNS服务器重复解析，从而加快DNS的解析速度，也缓解DNS服务器的压力。

以CentOS为例：

### 1、安装

    yum install nscd

### 2、增加配置文件 /etc/nscd.conf

内容如下：

```
#
# /etc/nscd.conf
#
# An example Name Service Cache config file.  This file is needed by nscd.
#
# Legal entries are:
#
#       logfile                 <file>
#       debug-level             <level>
#       threads                 <initial #threads to use>
#       max-threads             <maximum #threads to use>
#       server-user             <user to run server as instead of root>
#               server-user is ignored if nscd is started with -S parameters
#       stat-user               <user who is allowed to request statistics>
#       reload-count            unlimited|<number>
#       paranoia                <yes|no>
#       restart-interval        <time in seconds>
#
#       enable-cache            <service> <yes|no>
#       positive-time-to-live   <service> <time in seconds>
#       negative-time-to-live   <service> <time in seconds>
#       suggested-size          <service> <prime number>
#       check-files             <service> <yes|no>
#       persistent              <service> <yes|no>
#       shared                  <service> <yes|no>
#       max-db-size             <service> <number bytes>
#       auto-propagate          <service> <yes|no>
#
# Currently supported cache names (services): passwd, group, hosts, services
#
#   logfile                 /var/log/nscd.log
    threads                 4
    max-threads             32
    server-user             nscd
    stat-user               somebody
    debug-level             5
    reload-count            5
    paranoia                no
    restart-interval        3600


    enable-cache            hosts           yes
    enable-cache            passwd          no
    enable-cache            group           no
    enable-cache            services        no
    positive-time-to-live   hosts           5
    negative-time-to-live   hosts           20
    suggested-size          hosts           211
    check-files             hosts           yes
    persistent              hosts           yes
    shared                  hosts           yes
    max-db-size             hosts           33554432
```

### 3、启动服务

    service nscd start

### 4、添加开机自启动

    chkconfig nscd on

### 5、如需要停止服务

    service nscd stop
