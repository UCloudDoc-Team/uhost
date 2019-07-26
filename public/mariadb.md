# MariaDB软件源配置

> Note
> 
> UCloud云平台的MariaDB软件源目前仅适用于CentOS6.x 64位和Redhat6.x 64位操作系统。

## MariaDB 5.5

在 **/etc/yum.repos.d/** 新建mariadb.repo文件并加入以下内容：

```
[mariadb5]
name=mariadb5 Repository
baseurl=http://mariadb5.mirror.ucloud.cn
gpgcheck=0
enabled=1
```

创建好repo文件之后，执行yum clean all && yum makecache，即可将新的仓库生效。

> Note
> 
> 各数据中心仓库域名有所区别，详见下表。


| 数据中心    | 仓库url                                                         |
| ------- | ------------------------------------------------------------- |
| 北京一可用区A | mariadb5.mirror.ucloud.cn 或者 mariadb5.mirrors.ucloud.cn       |
| 北京二可用区B | mariadb5.mirror.cs.ucloud.cn 或者 mariadb5.mirrors.cs.ucloud.cn |
| 北京二可用区C | mariadb5.mirror.yg.ucloud.cn 或者 mariadb5.mirrors.yg.ucloud.cn |
| 华南双线    | mariadb5.mirror.gz.ucloud.cn 或者 mariadb5.mirrors.gz.ucloud.cn |
| 亚太      | mariadb5.mirror.hk.ucloud.cn 或者 mariadb5.mirrors.hk.ucloud.cn |
| 北美      | mariadb5.mirror.la.ucloud.cn 或者 mariadb5.mirrors.la.ucloud.cn |

## MariaDB 10.0

在 **/etc/yum.repos.d/** 新建mariadb.repo文件并加入以下内容：

```
[mariadb100]
name=mariadb100 Repository
baseurl=http://mariadb100.mirror.ucloud.cn
gpgcheck=0
enabled=1
```

创建好repo文件之后，执行yum clean all && yum makecache，即可将新的仓库生效。

> Note
> 
> 各数据中心仓库域名有所区别，详见下表。


| 数据中心    | 仓库url                                                             |
| ------- | ----------------------------------------------------------------- |
| 北京一可用区A | mariadb100.mirror.ucloud.cn 或者 mariadb100.mirrors.ucloud.cn       |
| 北京二可用区B | mariadb100.mirror.cs.ucloud.cn 或者 mariadb100.mirrors.cs.ucloud.cn |
| 北京二可用区C | mariadb100.mirror.yg.ucloud.cn 或者 mariadb100.mirrors.yg.ucloud.cn |
| 华南双线    | mariadb100.mirror.gz.ucloud.cn 或者 mariadb100.mirrors.gz.ucloud.cn |
| 亚太      | mariadb100.mirror.hk.ucloud.cn 或者 mariadb100.mirrors.hk.ucloud.cn |
| 北美      | mariadb100.mirror.la.ucloud.cn 或者 mariadb100.mirrors.la.ucloud.cn |

## MariaDB 10.1

在 **/etc/yum.repos.d/** 新建mariadb.repo文件并加入以下内容：

```
[mariadb101]
name=mariadb101 Repository
baseurl=http://mariadb101.mirror.ucloud.cn
gpgcheck=0
enabled=1
```

创建好repo文件之后，执行yum clean all && yum makecache，即可将新的仓库生效。

> Note
> 
> 各数据中心仓库域名有所区别，详见下表。


| 数据中心    | 仓库url                                                             |
| ------- | ----------------------------------------------------------------- |
| 北京一可用区A | mariadb101.mirror.ucloud.cn 或者 mariadb101.mirrors.ucloud.cn       |
| 北京二可用区B | mariadb101.mirror.cs.ucloud.cn 或者 mariadb101.mirrors.cs.ucloud.cn |
| 北京二可用区C | mariadb101.mirror.yg.ucloud.cn 或者 mariadb101.mirrors.yg.ucloud.cn |
| 华南双线    | mariadb101.mirror.gz.ucloud.cn 或者 mariadb101.mirrors.gz.ucloud.cn |
| 亚太      | mariadb101.mirror.hk.ucloud.cn 或者 mariadb101.mirrors.hk.ucloud.cn |
| 北美      | mariadb101.mirror.la.ucloud.cn 或者 mariadb101.mirrors.la.ucloud.cn |
