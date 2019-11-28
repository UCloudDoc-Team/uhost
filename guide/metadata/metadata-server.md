# 元数据

元数据（Metadata）是云主机UHost基本信息的集合，包括主机id，配置，镜像，ip等。实例的所有相关元数据可通过元数据服务器获取。

## 元数据服务器（Metadata Server）

元数据服务器是一个内网服务。通过该服务，能在主机内取得当前云主机实例的自身信息。

UCloud的元数据服务器地址为（各可用区一致）：

	http://100.80.80.80/meta-data/

## 元数据项

（相对于：http://100.80.80.80/meta-data/latest/uhost）

| 元数据项 | 说明 |
| -- | -- |
| /project-id | 项目ID |
| /region | 地域 |
| /zone   | 可用区 |
| /uhost-id  | 云主机ID |
| /name | 云主机名称 |
| /remark | 云主机备注 |
| /tag  | 云主机业务组 |
| /image-id | 镜像ID |
| /os-name | 镜像操作系统名称 |
| /machine-type | 机型 |
| /cpu | CPU个数 |
| /memory | 内存容量（MB）|
| /gpu | GPU个数 |
| /isolation-group | 硬件隔离组ID |
| /net-capability | 网络增强特性 |
| /hotplug | 热升级特性 |
| /disks/N/ |（数组）磁盘 |
| /disks/N/disk-id | 磁盘id |
| /disks/N/name | 磁盘名称 |
| /disks/N/is-boot | 是否为系统盘 |
| /disks/N/disk-type | 磁盘类型 |
| /disks/N/size | 磁盘容量（GB）|
| /disks/N/drive | 磁盘盘符 |
| /disks/N/encrypted | 是否为加密盘 |
| /disks/N/backup-type | 备份类型 |
| /network-interfaces/N/ |（数组）虚拟网卡 |
| /network-interfaces/N/vpc-id | VPC ID |
| /network-interfaces/N/subnet-id | 子网ID |
| /network-interfaces/N/mac | MAC地址 |
| /network-interfaces/N/ips/N/ |（数组）IP地址 |
| /network-interfaces/N/ips/N/ip-id |（仅当为EIP时有效）EIP ID |
| /network-interfaces/N/ips/N/ip-address | IP地址 |
| /network-interfaces/N/ips/N/type | IP类型 |
| /network-interfaces/N/ips/N/bandwitdh | 带宽大小（MB）|

## 查看元数据

通过以下命令，可获取元数据服务器相关目录层级下的对应项目信息：

	[root@192-168-1-1]# curl http://100.80.80.80/meta-data/latest/uhost/uhost-id
	
	uhost-vjfsj2db

通过以下命令，可获取元数据服务器的对应目录层级：
	
	[root@192-168-1-1]# curl http://100.80.80.80/meta-data/latest/uhost/disks/0/
	
	/backup-type 
	/encrypted 
	/disk-id
	/disk-type
	/drive
	/is-boot
	/name
	/size


## 已发布可用区

 - 泰国曼谷可用区A
 - 越南胡志明可用区A

（其他可用区发布中）
