# 关于镜像结束生命周期（EOL）的应对方案
镜像EOL是指镜像结束了生命周期（由于第三方支持、开源计划等原因），UCloud同时停止对使用相应镜像的技术支持，并在选择镜像版本时标注「EOL」提示该镜像已结束生命周期。针对镜像EOL后的解决方案可参考本文档，如无涉及相关镜像可联系我们提供方案。

## 一、CentOS Linux停止维护后的应对方案
依据CentOS官方公告所知，其将停止维护CentOS Linux项目，UCloud所提供的基础镜像CentOS Linux源于CentOS官方，故在官方停止维护后UCloud也将停止对该基础镜像的维护。
<br>
本文主要就CentOS官方公告内容及影响、UCloud基础镜像应对方案及应对建议进行介绍。

### CentOS官方公告内容
2020年12月08日，CentOS官方宣布了停止维护CentOS Linux 的计划，并推出了CentOS Stream项目。具体信息请阅读[CentOS官方公告](https://www.centos.org/cl-vs-cs/)。因此对CentOS Linux镜像存在以下影响：
- CentOS Linux 7作为RHEL 7的复刻版本已于2020年08月06日停止更新，但会延续当前的支持计划，于2024年06月30日停止维护（EOL）；
- CentOS Linux 8作为RHEL 8的复刻版本，生命周期缩短，已于2021年12月31日停止更新并停止维护（EOL）。

基于以上官方变更计划，CentOS Linux 7和CentOS Linux 8用户将无法获得包括问题修复和功能更新在内的任何软件维护和支持。
CentOS官方建议停止维护后，可以将环境迁移至CentOS Stream版本；对于生产环境或部署关键业务的系统，建议使用稳定的Red Hat Enterprise Linux。对此，用户需评估以下问题：

- CentOS Stream是一个滚动发行的版本，仅为RHEL前置测试版，运用于生产环境时，可能存在一定风险。

### UCloud基础镜像应对方案
基于CentOS官方公告，UCloud的应对方案如下：
- UCloud对于CentOS操作系统的服务支持将和CentOS官方日期保持同步。对CentOS Linux 7的服务支持将持续至2024年06月30日。
- CentOS Linux 8已于2021年12月31日停止维护，UCloud已停止对该基础镜像的更新和维护。但暂不会下线CentOS Linux 8，所以对于正在使用相关镜像的云主机用户不会受到影响；

### 应对建议
您可以根据业务情况选择适用的操作系统替代CentOS Linux，具体操作说明如下：
- 无需保留系统盘数据：可通过重装操作系统进行更换，具体操作详见[操作指南](https://docs.ucloud.cn/uhost/guide/common?id=%e9%87%8d%e8%a3%85%e7%b3%bb%e7%bb%9f)；
- 如需保留系统盘数据：建议使用UCloud服务器迁移中心（USMC)进行迁移，详见[产品说明](https://docs.ucloud.cn/usmc/introduction/concept)；
- UCloud建议您使用Rocky Linux镜像。


UCloud基础镜像中还提供了其他多种基础镜像可选，您可以根据业务的实际情况，选择适用的操作系统替代CentOS Linux。具体说明如下：

| 镜像名称 | 概述 |
| ----------- | ---------|
|Red Hat Enterprise Linux | Red Hat Enterprise Linux是Red Hat公司提供的企业版操作系统，UCloud基础镜像中目前支持RedHat 8.3 64位版本。|
|Rocky Linux  | Rocky Linux 是一个社区化的企业级操作系统，Rocky Linux与CentOS一样，提供了适用于服务器的稳定版本，旨在作为CentOS完全兼容的替代版本。 |
|Debian、Ubuntu等其他操作系统 | Linux的其他发行版操作系统，不同操作系统在使用习惯和应用兼容性上存在一定差异。|
