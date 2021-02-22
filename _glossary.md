# 名词解释
## 机型
  通用型 N：提供最灵活自由的CPU、内存、磁盘组合，能满足90%的基础业务诉求。<br> 
  高主频型 C：提供>=3.0GHz主频的CPU，CPU计算性能更高。<br>
  GPU型 G：满足需要GPU图形计算卡的异构计算需求，如人工智能，图形渲染，科学计算等。

## CPU平台
CPU平台属性是指云主机所在宿主机的CPU微架构版本。每代CPU平台主要升级了硬件架构。不同CPU平台的云主机价格相同，详情请查看[CPU平台](https://docs.ucloud.cn/uhost/introduction/uhost/type_new)
## 磁盘
分为云盘和本地盘两大类，云盘采用分布式多份副本机制，宿主机宕机后1分钟内可快速迁移；IO性能稳定，可按需挂载卸载数据盘。本地盘的磁盘与CPU/内存在同一台物理宿主机上，性能强，延迟低。

## 网络增强
网络增强特性分为1.0和2.0两个不同版本。网络增强1.0是UCloud利用多核CPU配合Linux内核对网卡驱动多队列的支持，开启网卡多队列而获得的云主机特性。满足新场景下通讯频繁、数据包体积小但数量大的需求。开启后，预期性能可从300,000 pps提升到1,000,000 pps。
网络增强2.0通过宿主机的智能网卡硬件支持，以及SR-IOV（Single-root I/O virtualization，单根I/O虚拟化）技术，进一步升级了云主机的网络性能，最高可达10,000,000 pps。目前此特性仅支持快杰系列机型。详细信息请查看[特性](https://docs.ucloud.cn/uhost/introduction/uhost/feature)。

## 热升级
主机CPU/内存热升级，包括CPU与内存均支持在线升级扩展。升级过程中云主机无需关机或重启，同时不会对主机上运行的应用和业务产生性能影响。详细信息请查看[特性](https://docs.ucloud.cn/uhost/introduction/uhost/feature)。

## 数据方舟
即UDataArk，是为UCloud云主机磁盘提供连续数据保护的服务。支持在线实时备份、具有精确到秒级的数据恢复能力。避免误操作、恶意破坏对数据造成的损失，有效保护您的珍贵数据。详情请查看[数据方舟](https://docs.ucloud.cn/uda/README)。

## 外网弹性IP
即EIP,详情请查看[外网弹性IP](https://docs.ucloud.cn/unet/eip/guide)。

## VPC
私有网络VPC（Virtual Private Cloud）是属于用户的、逻辑隔离的网络环境，详情请查看[私有网络UVPC](https://docs.ucloud.cn/vpc/introduction/subnet)。

## 快照
磁盘快照，即Usnap，是一种便捷高效的数据容灾手段，常用于数据备份、制作自定义镜像、应用容灾等。详情请查看[磁盘快照服务（USnap）](https://docs.ucloud.cn/usnap/common)。

## 硬件隔离组：
硬件隔离组能严格确保组内的每一台云主机都落在不同的物理机上。每个隔离组在单个可用区至多可以添加7台云主机。

## AnycastEIP
即利用UCloud的全球BGP宣告能力、覆盖全球的十余个海外节点以及节点间的专线资源，提供全球网络加速，详情请查看[AnycastEIP](https://docs.ucloud.cn/anycasteip/README)。
