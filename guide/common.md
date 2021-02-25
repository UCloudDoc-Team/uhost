# 主机
## 创建主机
如您想详细了解如何创建一台主机，请参考[快速上手创建云主机](uhost/newuser/briefguide.md)。<br>

## 管理主机
如果您登录[uhost控制台](https://console.ucloud.cn/uhost/uhost)，可以进行主机登录、关闭、重启以及断电操作。<br>

![img](/images/common/manage00.png)<br>

> 关机和重启都是虚机层面的，如果遇到重启或者关机无效的情况，可以使用断电操作，断电是宿主层面的关机，相当于强制关闭电源，较为彻底。<br>

如果您点击【详情】，将进入主机详情页面，展示当前选择主机的基本信息、配置信息、付费信息以及监控相关信息。

![img](/images/common/manage01.png)

![img](/images/common/manage02.png)

### 基本信息模块
![img](/images/common/manage03.png)<br>

基本信息模块包括资源ID、资源名、业务组、可用区以及内网ip等基本信息，其中资源名称、业务组名称可即时更改。

### 配置信息模块
![img](/images/common/manage04.png)<br>

配置信息模块包含机型、cpu平台、机型、CPU及内存等主机配置相关信息，点击【更改配置】，进入配置更改页面，支持更改内存和CPU规格、调整磁盘容量、升级外网弹性IP带宽。
### 更改规格
**操作路径**<br>
> 1. 选择云主机<br>
> 2. 点击选择【更改配置】，其后点击【更改规格】，点击【继续】进入下一页面<br>
> 3. 分别选择CPU和内存需要升级数据<br>
> 4. 点击【确定】，补缴差价，完成支付<br>

![img](/images/common/manage06.png)<br>

![img](/images/common/manage07.png)<br>

同时，您还可以使用[uhost resize](https://docs.ucloud.cn/cli/cmd/ucloud/uhost/resize)（UCloud CLI）命令升级配置，并指定实例ID。
请使用 --cpu参数和 --memory-gb参数按如下方式指定CPU核数和内存大小。
例如：
```
ucloud uhost resize --uhost-id uhost-0a3gcvih --cpu 2 --memory-gb 4
```

以上示例输出如下：
```
Resize uhost must be after stop it. Do you want to stop this uhost? (y/n):y
uhost[uhost-0a3gcvih] is shutting down...done
UHost:[uhost-0a3gcvih] resized...done
```
### 调整磁盘容量
**操作路径**<br>
> 1. 选择云主机<br>
> 2. 点击选择【更改配置】，其后点击【调整磁盘容量】，选择您想调整的磁盘，点击【继续】进入下一页面<br>
> 3. 选择调整磁盘的容量值<br>
> 4. 点击【确定】，补缴差价，完成支付<br>

![img](/images/common/manage08.png)<br>

![img](/images/common/manage09.png)<br>

?> 若当前磁盘支持在线扩容，扩容后无需重启主机，但需要进入主机内部进行相关配置，详情见[磁盘配置](https://docs.ucloud.cn/uhost/guide/disk)

### 升级外网弹性IP带宽
**操作路径**<br>
> 1. 选择云主机<br>
> 2. 点击选择【更改配置】，其后点击【升级外网弹性IP带宽】，选择需要升级的ip地址，点击【继续】进入下一页<br>
> 3. 调整您所需的带宽值<br>
> 4. 点击【确定】，补缴差价，完成支付<br>


![img](/images/common/manage10.png)<br>

![img](/images/common/manage11.png)<br>

### 付费信息模块
![img](/images/common/manage05.png)<br>

付费信息模块包含创建时间、到期时间以及付费方式，点击【付费】，支持一键续费。

## 删除主机

您可以登录[uhost控制台](https://console.ucloud.cn/uhost/uhost),选择主机，点击【删除主机】，即可删除当前主机。<br>
同时，您还可以使用[uhost delete](https://docs.ucloud.cn/cli/cmd/ucloud/uhost/delete)（UCloud CLI）命令删除主机，并指定实例ID。
例如：
```
ucloud uhost delete --uhost-id uhost-0a3gcvih
```

以上示例输出如下：
```
Are you sure you want to delete the host(s)? (y/n):y
uhost[uhost-0a3gcvih] is shutting down...done
uhost[uhost-0a3gcvih] deleted
```

> 1. 如您通过控制台删除云主机，主机关联的EIP与UDisk将被同步删除，不会继续计费。如果使用API，由字段ReleaseEIP和ReleaseUDisk决定是否同步删除EIP与UDisk，请参考[TerminateUHostInstance](https://docs.ucloud.cn/api/uhost-api/terminate_uhost_instance)。<br>
> 2. 资源删除后，系统将自动退还租约中的剩余费用，如您想了解具体的退费规则，请阅读[退费明细](https://docs.ucloud.cn/charge/refund)。<br>
 
## 网络配置
控制台主机列表页面提供更改外网防火墙、绑定弹性IP、挂载云硬盘入口。<br>
**操作路径**<br>
> 1. 选择主机<br>
> 2. 点击【…】，下拉框选择【关联产品操作】<br>
> 3. 点击【更换外网防火墙】/【绑定弹性IP】操作<br>

### 更换外网防火墙
如您需要重新调整外网防火墙策略，请阅读[防火墙操作指南](https://docs.ucloud.cn/unet/firewall/guide)

### 绑定弹性IP
如您需要重新绑定外网弹性IP，请阅读[外网弹性IP操作指南](https://docs.ucloud.cn/unet/firewall/guide)

## 磁盘配置 
**操作路径**<br>
> 1. 选择主机<br>
> 2. 点击【…】，下拉框选择【关联产品操作】<br>
> 3. 点击【挂载云硬盘】操作<br>

如您需要详细了解云硬盘相关信息，请阅读[云硬盘操作指南](https://docs.ucloud.cn/udisk/userguide/mount)

## 更多操作
除以上功能外，控制台列表还支持更改业务组、制作镜像等更多操作。

![img](/images/common/manage12.png)<br>

### 更改业务组
**操作路径**<br>
> 1. 选择主机<br>
> 2. 点击【…】，下拉框选择【更多操作】<br>
> 3. 点击【更改业务组】操作<br>

![img](/images/common/group01.png)<br>

您可对云主机进行分组，使得某些操作能以业务组为单位进行，省去逐个操作的繁琐，便于资源集中管理。后续查看监控数据或修改规则时，即可以组为单位进行操作。

### 查看/修改自定义数据
**操作路径**<br>
> 1. 选择主机<br>
> 2. 点击【…】，下拉框选择【更多操作】<br>
> 3. 点击【查看/修改自定义数据】<br>
如您需要详细了解元数据及自定义数据相关操作，请阅读[元数据及自定义数据](https://docs.ucloud.cn/uhost/guide/metadata/metadata-server)

### 制作镜像
**操作路径**<br>
> 1. 选择主机<br>
> 2. 点击【…】，下拉框选择【更多操作】<br>
> 3. 点击【制作镜像】<br>
如您需要详细了解镜像相关操作，请阅读[镜像操作指南](https://docs.ucloud.cn/uhost/guide/image/upload_image)

### 重置密码
**操作路径**<br>
> 1. 选择主机<br>
> 2. 点击【…】，下拉框选择【更多操作】<br>
> 3. 点击【重置密码】<br>

![img](/images/common/pwd.png)<br>

同时，您还可以使用[uhost reset-password](https://docs.ucloud.cn/cli/cmd/ucloud/uhost/reset-password)（UCloud CLI）命令重置主机密码，并指定可用区和实例ID。
请使用 --password参数按如下方式指定主机密码。
例如：


```
ucloud uhost reset-password --zone cn-bj2-05 --uhost-id uhost-0a3gcvih --password test12345
```


以上示例输出如下：
```
uhost[uhost-0a3gcvih] will be stopped, can we do this? (y/n):y
uhost[uhost-0a3gcvih] is shutting down...done
uhost[uhost-0a3gcvih] reset password
```

!> 1. 目前仍需要关机进行密码的重置；<br>
   2. 若主机修改了默认账户，则重置密码可能无法生效。<br>

## 重装系统
**操作路径**<br>
> 1. 选择主机<br>
> 2. 点击【…】，下拉框选择【更多操作】<br>
> 3. 点击【重装系统】<br>

![img](/images/common/reset.png)<br>


> 1. 如您重装系统时，系统盘大小和原主机不一致，相当于系统盘大小变配，需补足差价或发起退费, 详情请查看[退费说明](https://docs.ucloud.cn/charge/refund)。<br>
> 2. 重装主机重装系统需要在关机条件下进行，不会引起内网和外网IP的变更。<br>
> 3. 重装系统时请注意文件系统的变更，如CentOS 6.x重装为7.x，或Linux与Windows互相重装，可能引起数据盘无法识别。<br>
> 4. 开启网络增强的云主机无法重装为不支持网络增强的系统（如Windows）。<br>

## 主机NTP配置操作指南
### 各地域NTP服务器IP

| 地域    | 可用区  | NTP服务器1       | NTP服务器2       | NTP服务器3           |
| ----- | ---- | ------------- | ------------- | ----------------- |
| 北京一   | 可用区A | 10.255.255.1  | 10.255.255.2  | 0.cn.pool.ntp.org |
| 北京二   | 可用区B | 10.9.255.1    | 10.9.255.2    | 0.cn.pool.ntp.org |
| 北京二   | 可用区C | 10.10.255.1   | 10.10.255.2   | 0.cn.pool.ntp.org |
| 北京二   | 可用区D | 10.19.255.1   | 10.19.255.2   | 0.cn.pool.ntp.org |
| 北京二   | 可用区E | 10.42.255.1   | 10.42.255.2   | 0.cn.pool.ntp.org |
| 广州    | 可用区B | 10.13.255.1   | 10.13.255.2   | 0.cn.pool.ntp.org |
| 上海金融云 | 可用区A | 10.15.255.1   | 10.15.255.2   | 0.cn.pool.ntp.org |
| 上海二   | 可用区A | 10.23.255.101 | 10.23.255.102 | 0.cn.pool.ntp.org |
| 上海二   | 可用区B | 10.23.255.101 | 10.23.255.102 | 0.cn.pool.ntp.org |
| 香港    | 可用区A | 10.8.255.1    | 10.8.255.2    | 0.cn.pool.ntp.org |
| 香港    | 可用区B | 10.8.255.1    | 10.8.255.2    | 0.cn.pool.ntp.org |
| 洛杉矶   | 可用区A | 10.11.255.1   | 10.11.255.2   | 0.cn.pool.ntp.org |
| 华盛顿   | 可用区A | 10.27.255.101 | 10.27.255.102 | 0.cn.pool.ntp.org |
| 新加坡   | 可用区A | 10.35.255.1   | 10.35.255.2   | 0.cn.pool.ntp.org |
| 曼谷    | 可用区A | 10.31.255.101 | 10.31.255.102 | 0.cn.pool.ntp.org |
| 高雄    | 可用区A | 10.37.255.101 | 10.37.255.102 | 0.cn.pool.ntp.org |
| 台北    | 可用区A | 10.41.255.1   | 10.41.255.2   | 0.cn.pool.ntp.org |
| 雅加达   | 可用区A | 10.45.255.1   | 10.45.255.2   | 0.cn.pool.ntp.org |
| 孟买    | 可用区A | 10.47.255.1   | 10.47.255.2   | 0.cn.pool.ntp.org |
| 首尔    | 可用区A | 10.33.255.101 | 10.33.255.102 | 0.cn.pool.ntp.org |
| 东京    | 可用区A | 10.40.255.1   | 10.40.255.2   | 0.cn.pool.ntp.org |
| 法兰克福  | 可用区A | 10.29.255.101 | 10.29.255.102 | 0.cn.pool.ntp.org |
| 莫斯科   | 可用区A | 10.39.255.1   | 10.39.255.2   | 0.cn.pool.ntp.org |
| 迪拜    | 可用区A | 10.44.255.1   | 10.44.255.2   | 0.cn.pool.ntp.org |
| 圣保罗   | 可用区A | 10.49.255.1   | 10.49.255.2   | 0.cn.pool.ntp.org |


> 每台机器至少配置两个UCloud NTP server IP 和 一个外部NTP server, 分别对应下述文档中的 upstream1,upstream2, 和offical\_upstream3.

### 各操作系统修改NTP
 <!-- tabs:start -->
#### ** CentOS/Ubuntu/Redhat/Debian/Gentoo **
> NTP配置文件位置: /etc/ntp.conf <br>
 * **修改方法**

根据所在可用区添加对应的NTP服务器IP

```
restrict区域:
添加 restrict 10.255.255.1
添加 restrict 10.255.255.2

server区域:
原配置:
server 0.asia.pool.ntp.org
server 1.asia.pool.ntp.org
server 2.asia.pool.ntp.org
server 3.asia.pool.ntp.org (3.gentoo.pool.ntp.org)
替换为:
server 10.255.255.1 iburst minpoll 3 maxpoll 4 prefer
server 10.255.255.2 iburst minpoll 3 maxpoll 4 prefer
server 0.cn.pool.ntp.org iburst minpoll 3 maxpoll 4

作用: 缩短对时轮询周期，并首选UCloud的NTP服务
```

添加微调参数

```
添加 tinker dispersion 100
添加 tinker step 1800
添加 tinker stepout 3600

作用: 加速微调，控制微调范围
```

* **测试方法**

重启ntp服务

```
CentOS/Redhat/Gentoo:
# service ntpd restart

Ubuntu:
# sudo service ntp restart

Debian:
# service ntp restart
```

查看NTP server IP

```
# ntpq -pn
如显示表格中UCloud server IP,则表示ntp配置正确
```
 
?> 确保机器在能够跳跃对时的情况下，先执行ntpdate或者date命令来设置时间，再启动ntp对时服务。

```
具体操作:
# service ntpd stop
# ntpdate upstream1 或 # date -s "Y-m-D H:M:S"
# service ntpd start
```
    
#### ** OpenSUSE **
> NTP配置文件位置: /etc/ntp.conf <br>
* **修改方法**<br>
添加 restrict参数

```
restrict -4 default kod notrap nomodify nopeer noquery
restrict -6 default kod notrap nomodify nopeer noquery
```

根据所在可用区添加对应的NTP服务IP

```
restrict区域
添加 restrict 10.255.255.1
添加 restrict 10.255.255.2

server区域
原配置:
server 0.asia.pool.ntp.org
server 1.asia.pool.ntp.org
server 3.asia.pool.ntp.org (3.gentoo.pool.ntp.org)
替换为:
server 10.255.255.1 iburst minpoll 3 maxpoll 4 prefer
server 10.255.255.2 iburst minpoll 3 maxpoll 4 prefer
server 0.cn.pool.ntp.org iburst minpoll 3 maxpoll 4

作用: 缩短对时轮询周期，并首选UCloud的NTP服务
```

添加微调参数

```
添加 tinker dispersion 100
添加 tinker step 1800
添加 tinker stepout 3600

作用: 加速微调，控制微调范围
```
* **测试方法**<br>
重启ntp服务

```
# service ntp restart
```

查看NTP server IP

```
# ntpq -pn
如显示表格中UCloud server IP,则表示ntp配置正确
```

?> 确保机器在能够跳跃对时的情况下，先执行ntpdate或者date命令来设置时间，再启动ntp对时服务。

```
具体操作:
# service ntpd stop
# ntpdate upstream1 或 # date -s "Y-m-D H:M:S"
# service ntpd start
```

可以下载并运行脚本以完成配置，参见
[mod\_ntp.sh](http://static.ucloud.cn/1314eec96e414fcb3daca5124dee4112.sh)
    
#### ** Windows **
* **修改方法**<br>

修改Windows Time服务为自动启动 <br>
```
 1.在终端里输入"services.msc"，弹出服务列表，找到"Windows Time"将启动类型改为"自动"，并启动该服务；（如已启动则忽略）。
 2.针对2008和2012用户，64位机器，需要在终端中输入`sc triggerinfo w32time start/networkon stop/networkoff`
 （以上命令为cmd命令，不可运行于powershell）。
```

修改组策略<br>

 1. 启动Windows NTP客户端<br>
```
    1.在终端中输入"gpedit.msc"，弹出组策略编辑器。
    2."计算机配置\\管理模板\\系统\\Windows时间服务\\时间提供程序\\配置Windows NTP客户端"，将其状态修改为"已启用"。
```

 2. 配置Windows NTP客户端参数<br>
```
    1.配置对应可用区的"NtpServer"值为"upstream1,0x9 upstream2, 0x9official_upstream3,0x9"。
    2.修改"类型"值为NTP。
    3.修改"SpecialPollInterval"为30-60s之间的数值。
```
 3. 启用全局配置(计算机配置管理模板系统Windows时间服务全局配置设置)

```
修改"MaxAllowPhaseOffset"为3600
修改"MaxNegPhaseCorrection"为3600
修改"MaxPosPhaseCorrection"为3600
修改"PhaseCorrectRate"值为"7"
修改"MinPollInterval"值为"3"
修改"MaxPollInterval"值为"4"
```
* **测试方法**

 1. 命令行执行 gpupdate /force 强制更新组策略；<br>
 2. 按照以上配置完成后，确保机器可以跳跃对时的情况下，能够在终端执行"w32tm/resync"使客户端向服务器端发送时钟同步请求，完成立即对时； <br> 
 3. 在终端命令行中输入"w32tm /query /status" 查看同步信息。

<!-- tabs:end -->





