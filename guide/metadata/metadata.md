# 元数据

元数据（Metadata）是云主机UHost基本信息的集合，包括主机id，配置，镜像，ip等。实例的所有相关元数据可通过元数据服务器获取。

## 元数据服务器（Metadata Server）

元数据服务器是一个内网服务。通过该服务，能在主机内取得当前云主机实例的自身信息。

UCloud的元数据服务器地址为（各可用区一致）：
   
       http://100.80.80.80/meta-data/
       

## 元数据目录

（相对于：http://100.80.80.80/meta-data/latest/uhost）

 	/project-id          	项目ID
	/region           		地域
    /zone                   可用区
    /uhost-id               云主机ID
    /name                   云主机名称
    /remark                 云主机备注
    /tag                    云主机业务组
    /image-id               镜像ID
    /os-name                镜像操作系统名称
    /machine-type           机型
    /cpu                    CPU个数
    /memory                 内存容量（MB）
    /gpu                    GPU个数
    /isolation-group        硬件隔离组ID
    /net-capability         网络增强特性
    /hotplug                热升级特性
    /disks/N/               （数组）磁盘
        /disk-id            磁盘id
        /name               磁盘名称
		/is-boot            是否为系统盘
        /disk-type          磁盘类型
        /size               磁盘容量（GB）
        /drive              磁盘盘符
        /encrypted          是否为加密盘
        /backup-type        备份类型
    /network-interfaces/N/ （数组）虚拟网卡
        /vpc-id             VPC ID
        /subnet-id          子网ID
		/mac                MAC地址
        /ips/N/             （数组）IP地址
            /ip-id          （仅当为EIP时返回）EIP ID
            /ip-address     IP地址
            /type           IP类型
            /bandwitdh      带宽大小（MB）

## 查看元数据

通过以下命令，可获取元数据服务器相关目录层级下的数据或目录：

	[root@192-168-1-1]# curl http://100.80.80.80/meta-data/latest/uhost/uhost-id
	
	uhost-vjfsj2db

	
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


