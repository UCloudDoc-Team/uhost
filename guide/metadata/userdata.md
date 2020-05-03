# 自定义数据

自定义数据（UserData）是指主机初次启动或每次启动时，系统自动运行的配置脚本，该脚本可由控制台/API等传入元数据服务器，并由主机内的cloud-init程序获取。

判断主机是否支持用户自定义数据，需要确认镜像内部已安装了cloud-init（对于UCloud提供的官方镜像，或基于UCloud镜像制作的自定义镜像，可通过镜像的Feature数组中是否包含CloudInit项，来判断系统中是否安装该程序），当符合条件时，主机创建页面会展示“自定义数据”选项。

## Cloud-Init

Cloud-init是由Linux发行版Ubuntu的母公司Canonical推出的一款开源软件，此软件可被安装在主流的Linux发行版上（Ubuntu，CentOS，Debian，等），主要的用途是在云计算平台上帮助用户初始化其创建的云主机。

用户自定义数据（Userdata）是Cloud-Init默认提供的机制，多云通用。

## 创建主机时传入自定义数据

通过控制台/API，可以在创建主机时传入自定义数据。支持的脚本类型包括：User-Data、Cloud Config、Include、Gzip压缩脚本、 Upstart Job等。

注意：脚本内容不能超过16 KB。

### User-data脚本

首行固定为#!，例如#!/bin/bash，或#!/bin/python等

仅在首次启动实例时执行一次。

**示例 1：**在主机创建完成后输出Hello World

```bash
#!/bin/sh
echo “Hello World!”
```

创建完成后，将能在/var/log/cloud-init-output.log日志文件的末尾看到”Hello World!”字样。

**示例 2： **主机启动开启Httpd服务

```bash
#!/bin/bash

service httpd start
chkconfig httpd on
```

### Cloud Config脚本

首行固定为#cloud-config

表明你提供的是一段由Cloud-Init原生定义的一套yaml格式的专用配置数据，它几乎囊括了所有与操作系统配置相关的抽象描述。

详情请参考[官方示例](https://cloudinit.readthedocs.io/en/latest/topics/modules.html)

**示例 1：** 修改Hostname

```yaml
#cloud-config

hostname: uhost1
```

**示例 2：** 修改数据盘挂载点到/opt/data

```yaml
#cloud-config

mounts:
  - [ /dev/vdb, /opt/data ]
```

**示例 3：** 主机创建后自动执行一次yum update或者apt-get upgrade
   
```yaml
#cloud-config

package_upgrade: true
```

**示例 4：** 创建主机时配置密钥
   
```yaml
#cloud-config

ssh_authorized_keys:
  - ssh-rsa AAAAB3NzaC1yc2EAAAABIwAAAGEA3FSyQwBI6Z+nCSjUUk8EEAnnkhXlukKoUPND/RRClWz2s5TCzIkd3Ou5+Cyz71X0XmazM3l5WgeErvtIwQMyT1KjNoMhoJMrJnWqQPOt5Q8zWd9qG7PBl9+eiH5qV7NZ mykey@host

```

### 其他脚本类型

UHost还支持传入Include脚本、Gzip压缩脚本、 Upstart Job等脚本类型。

详情请参考 [Cloud-init官方文档](https://cloudinit.readthedocs.io/en/latest/topics/format.html)

## 主机内获取自定义数据

通过以下方式，可在主机内部获取用户自定义数据

```bash
curl http://100.80.80.80/user-data
```

