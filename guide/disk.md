# 磁盘 
关于磁盘的不同操作场景请对应查找相关操作指南

- [查看硬盘分区](#查看硬盘分区)

- [系统盘扩容](#系统盘扩容)

- [数据盘扩容](#数据盘扩容)

- [挂载云硬盘](#挂载云硬盘)

- [卸载云硬盘](#卸载云硬盘)

- [本地磁盘缩容](#本地磁盘缩容)

- [磁盘快照](#磁盘快照)

  


## 查看硬盘分区

登陆云主机后，使用`fdisk -l`命令查看云主机的硬盘分区（Ubuntu中需要root权限）。

![image](/images/udisk_use1.png)

    系统盘：/dev/vda
    
    数据盘1：/dev/vdb
    
    数据盘2：/dev/vdc

## 系统盘扩容

### 1. 扩容规则

不同磁盘类型，遵循不同的磁盘扩容规则：

| 类型 | 磁盘上限 | 支持扩容操作 |
| --- | - | --- |
| 本地磁盘 (普通本地盘，SSD本地盘) | 100GB | 更改配置 |
| 云盘 |  500GB | 创建主机、更改配置、重装系统 |

### 2. 扩容步骤

#### 创建/重装主机时扩容：

1. 在创建/重装主机页面，选择系统盘大小；
2. 等待创建/重装完毕，此时底层块设备已扩容完成；
3. 进入主机查看文件系统是否已扩容完毕。

#### 创建后通过更改配置扩容：

!> 本地系统盘扩容时间较长，扩容至100G可能需要关机等待30分钟。

1. 选择“更改配置” -> “更改磁盘容量” -> 系统盘；<br>
2. 等待扩容结束，主机进入关机状态，此时底层块设备已扩容完成；<br>
3. 开机，进入主机查看文件系统是否已扩容完毕。<br>

#### 查看文件系统是否扩容完毕：
<!-- tabs:start -->

#### ** Linux **

    df -TH
    
#### ** Windows **

    这台电脑->查看C盘大小是否与控制台一致
   
<!-- tabs:end -->

?> 如文件系统并未扩容完毕，则需要执行**系统内扩容步骤**。

### 3. 系统内扩容步骤

<!-- tabs:start -->
#### ** Linux **

* 步骤1：安装growpart

Cloud-init支持版镜像中已默认安装growpart，其余版本需要自行安装，过程如下：

CentOS：

    yum install -y epel-release
    yum install -y cloud-utils

Ubuntu：

    sudo apt-get install cloud-initramfs-growroot
    
    
* 步骤2：扩容分区表

```
LANG=en_US.UTF-8
growpart /dev/vda 1
```

?> CentOS6和Debian8，可能会遇到内核以及工具链不支持热重载分区表的情况，如遇此情况，扩容分区表后需重启一次操作系统。

* 步骤3：扩容文件系统

```
resize2fs /dev/vda1 (ext4文件系统)
xfs_growfs /dev/vda1 (xfs文件系统) 或xfs_growfs /
```

* 步骤4：确认

查看是否扩容完成：

    df -TH
    
#### ** Windows **
在“计算机管理”中选择扩展卷，即可完成扩容。具体操作步骤如下：

![](/images/guide/sysdisk_step1.jpg)

![](/images/guide/sysdisk_step2.jpg)

![](/images/guide/sysdisk_step3.jpg)

![](/images/guide/sysdisk_step4.jpg)

![](/images/guide/sysdisk_step5.jpg)

![](/images/guide/sysdisk_step6.jpg)

![](/images/guide/sysdisk_step7.jpg)

![](/images/guide/sysdisk_step8.jpg)

<!-- tabs:end -->
    

## 数据盘扩容

### 1. 扩容步骤

#### 磁盘类型：本地盘和云硬盘

![](/images/reconfignew.png)

在控制台选择“更改配置”，关机升级后，重新开机即可。

?> 如文件系统并未扩容完毕，则需要执行**系统内扩容步骤**。

### 2. 系统内扩容步骤

 <!-- tabs:start -->
#### ** Linux **

* 查看数据盘的文件系统类型（升级操作需要针对ext4和xfs两种文件系统采取不同的操作） 
```
df -ihT
```

![image](/images/ext4.png)

![image](/images/xfs.png)

* 针对ext4文件格式的操作系统（如CentOS6）  

``` 
e2fsck -f /dev/vdb
resize2fs /dev/vdb
``` 

* 针对xfs文件格式的操作系统（如CentOS7）  

``` 
xfs_repair /dev/vdb
xfs_growfs /data
``` 

* 确认是否扩容成功 
```
df -TH
```

#### ** Windows **
在主机上操作，cmd中输入`diskpart.exe`，`list volume`，选择要扩展大小的逻辑卷，输入要扩展大小extend
\[size=n\]， 或extend将所有未分配大小扩展到选择的逻辑卷。

![image](/images/disk_extend.png)
    
<!-- tabs:end -->

### 3. 扩容前无本地数据盘的主机

<!-- tabs:start -->
#### ** Linux **
升级后，需在云主机内做如下操作：

1. 可选择ext4或xfs两种文件系统格式来格式化数据盘

2. 将数据盘设置为ext4文件格式（CentOS6的默认文件系统格式）：
``` 
mkfs -t ext4 /dev/vdb 
mount /dev/vdb /data/
```

3. 编辑/etc/fstab，将对应配置写入fstab

``` 
/dev/vdb   /data  ext4  defaults,noatime 0 0
```

4. 将数据盘设置为xfs格式（CentOS7的默认文件系统格式）：
```
mkfs.xfs /dev/vdb
mount -t xfs /dev/vdb /data
```

5. 编辑/etc/fstab，加入如下内容
```
/dev/vdb /data xfs defaults,noatime 0 0  
```


#### ** Windows **
在主机上操作，cmd中输入`diskpart.exe`

1. 输入`list disk`，`select disk n` (请根据实际情况，填写n的具体数值），选中数据盘;
2. 输入`create partition primary`，创建分区;
3. 输入`list volume`，可看到创建的卷。输入`format fs=ntfs quick` 进行分区;
4. 输入`assign`,分配驱动器号;
5. 输入`exit`退出，系统中已可看到已创建的磁盘。

![image](/images/create_new_disk.png)

<!-- tabs:end -->


## 挂载云硬盘

在控制台主机管理页面->挂载云硬盘，进行挂载操作。

您还可以使用[udisk attach](cli/cmd/ucloud/udisk/attach)（UCloud CLI）命令挂载云硬盘，并指定可用区和云主机实例ID。请使用 --udisk-id参数指定云硬盘资源ID。
例如：
```
ucloud udisk attach --udisk-id bsm-bagfqw5u --zone cn-bj2-05 --uhost-id uhost-bh0fvsnh/UHost
```
以上示例输出如下：
```
udisk[bsm-bagfqw5u] is attaching to uhost uhost[uhost-bh0fvsnh]...done
```
然后在云主机内做如下操作：

    mkdir /udisk
    mount /dev/vdc /udisk
    df -h

## 卸载云硬盘

> 您只能操作卸载数据盘，系统盘不能被卸载。同时本地盘也不支持卸载，不支持单独释放。

### 1. 系统内卸载云盘
<!-- tabs:start -->
#### ** Linux **
Linux操作系统执行以下语句：

    umount /dev/vdc

#### ** Windows **

首先在磁盘管理器中选中云磁盘，右键选择“脱机”。

![image](/images/udisk_windows_1.png)

然后在设备管理器中选中云硬盘，右键点击“卸载”。

![image](/images/udisk_windows_2.png)

这两个操作相当于在Windows系统中对云硬盘进行了dismount操作。

> 如果只有一个C盘，此时第二个便是云硬盘，建议在扩容前对云硬盘进行备份（如快照和克隆）。<br>
> 在控制台云硬盘列表页选择需要扩容的云硬盘，将其卸载。这时云硬盘状态会从“已挂载”变为“可用”。

<!-- tabs:end -->
### 2. 控制台操作

在控制台主机管理页面->云盘管理->卸载，进行卸载操作。

您还可以使用[udisk detach](cli/cmd/ucloud/udisk/detach)（UCloud CLI）命令卸载云硬盘，并指定可用区。请使用 --udisk-id参数指定云硬盘资源ID。
例如：
```
ucloud udisk detach --udisk-id bsm-bagfqw5u --zone cn-bj2-05
```
以上示例输出如下：
```
Please confirm that you have already unmounted file system corresponding to this hard drive,(See "https://docs.ucloud.cn/udisk/userguide/umount" for help), otherwise it will cause file system damage and UHost cannot be normally shut down. Sure to detach? (y/n):y
udisk[bsm-bagfqw5u] is detaching from uhost[uhost-bh0fvsnh]…done
```



## 本地磁盘缩容

控制台不支持本地磁盘的“缩容”，但可通过以下步骤变相实现“缩容”。

!> 请注意，此操作会完全抹去数据，请先进行数据备份后操作！！！

### 1. 删除本地盘

?> 本地盘的删除需要关机进行。
首先进入系统内部进行卸载操作，操作步骤：
<!-- tabs:start -->
#### ** Linux **

``` 
umount /dev/vdc
``` 

#### ** Windows **

首先在磁盘管理器中选中云磁盘，右键选择“脱机”。

![image](/images/udisk_windows_1.png)

然后在设备管理器中选中云硬盘，右键点击“卸载”。

![image](/images/udisk_windows_2.png)

在系统内完成卸载后，请在控制台选择 指定主机-\>详情-\>磁盘与恢复-\>删除本地盘。

![](/images/guide/jietu20181227-174630.jpg)
<!-- tabs:end -->

### 2. 添加本地盘

请在控制台选择 指定主机-\>详情-\>磁盘与恢复-\>新建本地盘，选择适合大小。

![](/images/guide/jietu20181227-174714.jpg)

新建后，请进入主机内部进行如下操作：
<!-- tabs:start -->

#### **Linux**

升级后，需在云主机内做如下操作：

1. 可选择ext4或xfs两种文件系统格式来格式化数据盘

2. 将数据盘设置为ext4文件格式（CentOS6的默认文件系统格式）：

``` 
mkfs -t ext4 /dev/vdb 
mount /dev/vdb /data/
```

3. 编辑/etc/fstab，将对应配置写入fstab

``` 
/dev/vdb   /data  ext4  defaults,noatime 0 0
```

4. 将数据盘设置为xfs格式（CentOS7的默认文件系统格式）：

``` 
mkfs.xfs /dev/vdb
mount -t xfs /dev/vdb /data
``` 

5. 编辑/etc/fstab，加入如下内容

``` 
/dev/vdb /data xfs defaults,noatime 0 0
``` 

#### ** Windows **

在主机上操作，cmd中输入`diskpart.exe`

1. 输入`list disk`，`select disk n`(请根据实际情况，填写n的具体数值），选中数据盘。
2. 输入`create partition primary`，创建分区。
3. 输入`list volume`，可看到创建的卷。输入`format fs=ntfs quick` 进行分区
4. 输入 `assign`。分配驱动器号。
5. 输入`exit`退出。系统中已可看到已创建的磁盘。

![image](/images/create_new_disk.png)

> 同理，云盘亦不支持直接“缩容”，但可以在卸载后新建容量较小的云盘，直接挂载。<br>
  如您还想了解更多磁盘相关功能及信息，请阅读[云硬盘UDisk](udisk/userguide/create)。

<!-- tabs:end -->

## 磁盘快照
磁盘快照服务（USnap）是基于数据方舟CDP技术为全系列云硬盘数据盘（普通/SSD/RSSD）提供了创建快照的能力。快照是一种便捷高效的数据容灾手段，常用于数据备份、制作自定义镜像、应用容灾等。

如您需要了解更多更多快照相关操作及功能，请阅读[磁盘快照服务 USnap](https://docs.ucloud.cn/usnap/README)。

