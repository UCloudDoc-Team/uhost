# 用户自定义数据

用户自定义数据是指主机初次启动或每次启动时，系统自动运行的配置脚本，该脚本可通过控制台/API等，通过cloud-init注入主机内。支持的脚本类型包括：User-Data、Cloud Config、Include、Gzip压缩脚本、 Upstart Job等。

判断主机是否支持用户自定义数据，需要2个前提条件：镜像内部已安装了cloud-init（即镜像的CloudInitFeature属性=True），以及当前地域支持了元数据服务器。当符合上述2个条件时，主机创建页面会展示“自定义数据”选项。

## 创建时传入用户自定义数据

注意：脚本内容不能超过16 KB。

### User-data脚本

首行固定为#!，例如#!/bin/bash，或#!/bin/python等

仅在首次启动实例时执行一次。

Example. 主机启动开启Httpd服务

    #!/bin/bash
    service httpd start
    chkconfig httpd on

### Cloud Config脚本

首行固定为#cloud-config

根据调用模块的不同，启动频次也不同，详情请参考：

Example 1. 修改Hostname

    #cloud-config
    hostname: uhost1

Example 2. 修改数据盘挂载点到/opt/data

    #cloud-config
    mounts:
     - [ /dev/vdb, /opt/data ]


其他方式请参考 cloud-init官方文档

## 主机内获取用户自定义数据


