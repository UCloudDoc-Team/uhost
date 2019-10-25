

# 使用 Packer 创建自定义镜像

**注意:** 使用 Packer 创建自定义镜像的过程中会创建临时资源，临时资源会在构建结束后自动删除，故需要耗费一定资费。

## 概述

Packer 是 Hashicorp 公司推出的自动化打包镜像的轻量级开源工具，云厂商通过构建自己的 Builder 集成 Packer 中去，即可凭借单一配置文件，高效并行的为多云平台创建一致性的镜像。Packer 可以运行在常用的主流操作系统上，它不是 Chef、Puppet 等软件的替代品，而是集成并使用这些自动化配置工具在镜像上预装软件等。再配合 UCloud Terraform、UCloud CLI 等工具，可以在多云的DevOps场景下，实现基础设施即代码（IaC），持续集成和快速交付。

如下图所示，Packer 通过在 Provisioner 中集成 Chef、Shell、Puppet 等工具，制作包含各类软件的不可变镜像，供多云平台的云主机、Docker 等使用。

![](/images/guide/image/packer介绍.png)

### Packer与传统控制台创建镜像的对比

|            |                        控制台创建镜像                        |                        Packer创建镜像                        |
| -------- | ---------------------------------------------------------- | ---------------------------------------------------------- |
|  使用方式  |                          控制台点击                          |                       使用配置文件构建                       |
|  可复用性  | 低。每次都需执行相同操作，且无法保证镜像一致性，无法版本化管理 |           高。配置文件拷贝、修改即可，可版本化管理           |
| 操作复杂度 | 高。先使用基础镜像创建云主机，并自行登陆到云主机中进行部署，之后手动制作镜像 | 低。执行配置文件，自动执行预配置自动化脚本，然后自动构建镜像 |
|  创建时间  |   长。流程化操作，需要人工值守，无法准确等待每个流程的执行   |  短。自动化工作流操作，完善的轮询等待机制，无缝衔接每个流程  |

### Packer 创建镜像的生命周期
![](/images/guide/image/packer生命周期.png)
1.	用户通过构建JSON 模版，执行packer build 命令调用UCloud Builder；
2.	参数提前校验保证可用性；
3.	创建云主机、EIP等相关临时资源（若配置为内网环境则无需EIP）；
4.	通过SSH或 WinRM 等连接主机，执行 Provisioner 进程；
5.	关闭云主机，并创建镜像；
6.	复制镜像；
7.	删除主机、EIP等临时资源；
8.	执行后处理进程（如本地镜像导入等）。

## 快速开始

### 相关链接

[官方参考文档地址](https://www.packer.io/docs/builders/ucloud-uhost.html)

用于查询 UCloud Packer Builder 的各种参数

[官方下载页面](https://www.packer.io/downloads.html?spm=a2c4g.11186623.2.13.7186682bskvY7M)

用于安装 Packer

[开源仓库地址](https://github.com/hashicorp/packer)

欢迎为 UCloud Packer Builder 贡献代码

### 环境配置

**安装 Packer**

- 参照[官方安装文档](https://www.packer.io/intro/getting-started/install.html#alternative-installation-methods)安装 Packer
- 安装 [Cloud CLI 工具](https://docs.ucloud.cn/developer/cli/intro)（非必要，便于查询基础镜像等信息）
- 安装 [Terraform](https://docs.ucloud.cn/compute/terraform/quickstart)（非必要，便于使用 packer制作的镜像进行资源编排）

**配置默认用户**

设置密钥   UCLOUD\_PUBLIC\_KEY   ， UCLOUD\_PRIVATE\_ KEY 并设置项目ID UCLOUD\_PROJECT\_ID 为全局环境变量（推荐），或在 json 文件中显式指定 public\_key、 private\_key、 project\_id。

### 编写 JSON 文件

让我们以构建一个安装了 nginx 的自定义镜像为例。首先创建一个干净的空文件夹作为工作区，并且切换到该目录下，编写一个 JSON 规格文件(eg：test.json)，如下：

```json
{
  "variables": {
    "ucloud_public_key": "{{env `UCLOUD_PUBLIC_KEY`}}",
    "ucloud_private_key": "{{env `UCLOUD_PRIVATE_KEY`}}",
    "ucloud_project_id": "{{env `UCLOUD_PROJECT_ID`}}"
  },
  "builders": [
    {
      "type": "ucloud-uhost",
      "public_key": "{{user `ucloud_public_key`}}",
      "private_key": "{{user `ucloud_private_key`}}",
      "project_id": "{{user `ucloud_project_id`}}",
      "region": "cn-bj2",
      "availability_zone": "cn-bj2-02",
      "instance_type": "n-basic-2",
      "source_image_id": "uimage-f1chxn",
      "ssh_username": "root",
      "image_name": "packer-test-basic-bj"
    }
  ],
  "provisioners": [
    {
      "type": "shell",
      "inline": [
        "yum install -y nginx"
      ]
    }
  ]
}
```

如上定义了一个 *ucloud-uhost* Builders 构建器 和一个 [provisioners 配置器](https://www.packer.io/docs/provisioners/index.html?spm=a2c4g.11186623.2.18.589f682bpAI1YK) ，通过执行命令 *packer build test.json* 可以实现一键构建自定义镜像。

![](/images/guide/image/packer演示.gif)
