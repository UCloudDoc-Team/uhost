

# 使用 Packer 创建并导入本地镜像

## 概述

Packer 是 Hashicorp 公司推出的自动化打包镜像的轻量级开源工具（[详细介绍可参考上篇文档](https://docs.ucloud.cn/compute/uhost/guide/image/packer)）。UCloud 通过对的 Packer 的集成，目前已支持一键导入自制的本地镜像到 UCloud 云平台中。

## 相关链接

[镜像导入官方参考文档地址](https://www.packer.io/docs/post-processors/ucloud-import.html)

用于查询 UCloud import Post-Processors 的各种参数

[Packer官方下载页面](https://www.packer.io/downloads.html?spm=a2c4g.11186623.2.13.7186682bskvY7M)

用于安装 Packer

[开源仓库地址](https://github.com/hashicorp/packer)

欢迎为 UCloud Packer Builder 贡献代码

## 镜像导入示例

下面将使用 Packer 制作并导入一个 CentOS 镜像。如下图所示:

![](/images/guide/image/packer-import.png)

Packer 首先利用 [QEMU Builder](https://www.packer.io/docs/builders/qemu.html) 制作了一个 RAW 镜像，存放在本地配置的目录下，之后利用 *ucloud-import* [Post-Processors 后处理器](https://www.packer.io/docs/post-processors/index.html) 将本地的镜像存放到用户配置的 UFile 中，并自动化导入到 UCloud 云平台中。

### 环境配置

**安装 Packer**

- 参照[官方安装文档](https://www.packer.io/intro/getting-started/install.html#alternative-installation-methods)安装 Packer

**配置默认用户**

设置密钥   UCLOUD\_PUBLIC\_KEY, UCLOUD\_PRIVATE\_ KEY 并设置项目ID UCLOUD\_PROJECT\_ID 为全局环境变量（推荐），或在 json 文件中显式指定 public\_key、 private\_key、 project\_id。

**安装QEMU**

- 参照[官方安装文档](https://www.qemu.org/download/), 其中使用命令行安装，MacOS: *brew install qemu*, CentOs: *yum install qemu-kvm*, Ubuntu: *apt-get install qemu*

**创建一个 UFile 的 bucket 空间**

- 参照[官方文档](https://docs.ucloud.cn/storage_cdn/ufile/guide/bucket/devguide)


### 编写 JSON 文件 

让我们基于 MacOs 系统使用 QEMU 创建并导入一个 CentOS 6.10 的自定义镜像为例，[示例链接](https://github.com/hashicorp/packer/tree/master/examples/ucloud/local)。首先创建一个干净的空文件夹作为工作区，并且切换到该目录下，编写一个 JSON 规格文件(eg：local.json)，如下 ：

```json
{"variables": {
  "ucloud_public_key": "{{env `UCLOUD_PUBLIC_KEY`}}",
  "ucloud_private_key": "{{env `UCLOUD_PRIVATE_KEY`}}",
  "ucloud_project_id": "{{env `UCLOUD_PROJECT_ID`}}",
  "disk_size": "4096",
  "iso_checksum": "0da4a1206e7642906e33c0f155d2f835",
  "iso_checksum_type": "md5",
  "iso_name": "CentOS-6.10-x86_64-minimal.iso",
  "ks_path": "centos-6.10/ks.cfg",
  "mirror": "http://mirrors.ustc.edu.cn/centos",
  "mirror_directory": "6.10/isos/x86_64",
  "template": "centos-6.10-x86_64"
},
  "builders":[
    {
      "type": "qemu",
      "boot_command": [
        "<tab> text ks=http://{{ .HTTPIP }}:{{ .HTTPPort }}/{{user `ks_path`}}<enter><wait>"
      ],
      "boot_wait": "10s",
      "disk_size": "{{user `disk_size`}}",
      "http_directory": "http",
      "iso_checksum": "{{user `iso_checksum`}}",
      "iso_checksum_type": "{{user `iso_checksum_type`}}",
      "iso_url": "{{user `mirror`}}/{{user `mirror_directory`}}/{{user `iso_name`}}",
      "output_directory": "packer-{{user `template`}}-qemu",
      "shutdown_command": "echo 'packer'|sudo -S shutdown -P now",
      "ssh_password": "ucloud_packer",
      "ssh_port": 22,
      "ssh_username": "root",
      "ssh_timeout": "10000s",
      "vm_name": "{{ user `template` }}.raw",
      "net_device": "virtio-net",
      "disk_interface": "virtio",
      "format": "raw",
      "use_default_display": "false",
      "qemuargs": [
        ["-display", "cocoa"]
      ]
    }
  ],
  "post-processors":[
    {
      "type":"ucloud-import",
      "public_key": "{{user `ucloud_public_key`}}",
      "private_key": "{{user `ucloud_private_key`}}",
      "project_id": "{{user `ucloud_project_id`}}",
      "region":"cn-bj2",
      "ufile_bucket_name": "packer-test",
      "image_name": "packer_import_test",
      "image_os_type": "CentOS",
      "image_os_name": "CentOS 6.10 64位",
      "format": "raw"
    }
  ]
}
```
如上定义了一个 *qemu* Builder 构建器 和一个 *ucloud-import* [Post-Processors 后处理器](https://www.packer.io/docs/post-processors/index.html)，其中配置了UFile bucket name 等信息。

### 编写 Kickstart 文件

  根据如上 JSON 文件 QEMU 中配置的 http\_directory 和 boot\_command，则需要 JSON 文件目录下创建一个 ./http/centos-6.10/ 目录用来存放 Kickstart 文件即 ks.cfg, 如下：（[Kickstart参考文档](https://access.redhat.com/documentation/zh-cn/red_hat_enterprise_linux/6/html/installation_guide/ch-kickstart2)）
```
install
cdrom
lang en_US.UTF-8
keyboard us
network --bootproto=dhcp
rootpw ucloud_packer
firewall --disabled
selinux --permissive
timezone UTC
unsupported_hardware
bootloader --location=mbr
text
skipx
zerombr
clearpart --all
autopart
auth --enableshadow --passalgo=sha512
firstboot --disabled
reboot

%packages --nobase --ignoremissing
sudo
gcc
make
%end
```
  
### 执行命令行

 通过执行命令 *packer build local.json* 可以实现一键创建并导入自定义镜像。
