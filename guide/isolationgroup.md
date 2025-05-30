

# 硬件隔离组


硬件隔离组是云主机的逻辑分组，能确保组内的每一台云主机都落在不同的物理机上。每个隔离组在单个可用区至多可以添加7台云主机。

## 加入隔离组

### 创建主机

在创建主机过程中，可选加入硬件隔离组。

![](https://www-s.ucloud.cn/2025/05/4772c15a0c2de681615d28011d003b89_1746759010220.png)

> 可选择加入硬件隔离组条件：当前可用区在隔离组内的主机数必须<7台。

若当前没有隔离组，可以点选“创建隔离组”，进入隔离组页面完成创建后，选择刷新此弹窗。

您还可以使用[uhost create](cli/cmd/ucloud/uhost/create)（UCloud CLI）命令创建主机。请使用 --isolation-group参数指定隔离组。
例如：
```
ucloud uhost create --isolation-group ig-rhcq22xt/ig --memory-gb 1 --cpu 1 --password test1234 --zone cn-bj2-05 --image-id uimage-35pn5v/CentOS 7.6 64位
```
以上示例输出如下：
```
uhost[uhost-bh0fvsnh] is initializing...done
```

### 已有主机

已有主机已支持加入硬件隔离组。

![](https://www-s.ucloud.cn/2025/05/cc385ad027433d5776aa1daabf4f500d_1746758884465.png)

> 可选择加入硬件隔离组条件：当前可用区在隔离组内的主机数必须<7台，且目标主机为关机状态。


## 查看隔离组

通过硬件隔离组Tab，可以查看全部隔离组。

在主机里列表，亦可以在“自定义列表”中将“硬件隔离组”列展开。支持通过隔离组筛选主机。

您还可以使用[isolation-group list](cli/cmd/ucloud/uhost/isolation-group/list)（UCloud CLI）命令查看隔离组。
例如：
```
ucloud uhost isolation-group list
```
以上示例输出如下：
```
ResourceID   Name  Remark  UHostCount
ig-rhcq22xt  ig    ig      cn-bj2-05:1
```
