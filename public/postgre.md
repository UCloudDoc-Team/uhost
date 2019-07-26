# PostgreSQL软件源配置

> Note
> 
> UCloud云平台的PostgreSQL软件源目前仅适用于CentOS 5.x|6.x|7.x 64位，和Redhat6.x|7.x 64
> 位操作系统。

在 **/etc/yum.repos.d/** 新建postgresql.repo文件并加入以下内容：

## postgresql 9.3版本

```
[PostgreSQL93]
name=postgresql93 Repository
baseurl=http://centos.mirror.ucloud.cn/postgresql/9.3/$releasever/$basearch
gpgcheck=0
enabled=1
```

## postgresql 9.4版本

```
[PostgreSQL94]
name=postgresql94 Repository
baseurl=http://centos.mirror.ucloud.cn/postgresql/9.4/$releasever/$basearch
gpgcheck=0
enabled=1
```

创建好repo文件之后，执行yum clean all && yum makecache，即可将新的仓库生效。

> Note
> 
> 各数据中心仓库域名有所区别，详见下表。


| 数据中心    | 仓库URL                                                     |
| ------- | --------------------------------------------------------- |
| 北京一可用区A | centos.mirror.ucloud.cn 或者 centos.mirrors.ucloud.cn       |
| 北京二可用区B | centos.mirror.cs.ucloud.cn 或者 centos.mirrors.cs.ucloud.cn |
| 北京二可用区C | centos.mirror.yg.ucloud.cn 或者 centos.mirrors.yg.ucloud.cn |
| 亚太      | centos.mirror.hk.ucloud.cn 或者 centos.mirrors.hk.ucloud.cn |
| 北美      | centos.mirror.la.ucloud.cn 或者 centos.mirrors.la.ucloud.cn |
