# 自定义数据

自定义数据（UserData）是指主机初次启动或每次启动时，系统自动运行的配置脚本，该脚本可由控制台/API等传入元数据服务器，并由主机内的cloud-init程序获取。支持的脚本类型包括：User-Data、Cloud Config、Include、Gzip压缩脚本、 Upstart Job等。

判断主机是否支持用户自定义数据，需要2个前提条件：镜像内部已安装了cloud-init（即镜像的Feature中，包含CloudInit），以及当前地域支持了元数据服务器。当符合上述2个条件时，主机创建页面会展示“自定义数据”选项。

## 创建主机时传入自定义数据

注意：脚本内容不能超过16 KB。

### User-data脚本

首行固定为#!，例如#!/bin/bash，或#!/bin/python等

仅在首次启动实例时执行一次。

示例： 主机启动开启Httpd服务

    #!/bin/bash
    service httpd start
    chkconfig httpd on

### Cloud Config脚本

首行固定为#cloud-config

根据调用模块的不同，启动频次也不同，详情请参考[官方示例](https://cloudinit.readthedocs.io/en/latest/topics/modules.html)

示例 1：修改Hostname

    #cloud-config
    hostname: uhost1

示例 2： 修改数据盘挂载点到/opt/data

    #cloud-config
    mounts:
     - [ /dev/vdb, /opt/data ]

### 其他脚本类型

UHost还支持传入Include脚本、Gzip压缩脚本、 Upstart Job等脚本类型。

详情请参考 [Cloud-init官方文档](https://cloudinit.readthedocs.io/en/latest/topics/format.html)

## 主机内获取自定义数据

通过以下方式，可在主机内部获取用户自定义数据

    curl http://100.80.80.80/user-data

