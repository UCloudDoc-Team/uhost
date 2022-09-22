# 监控


我们为您的主机、网络等资源提供监控服务，您可以随时了解系统运行情况和资源使用状况，方便定位分析问题。

主机监控项默认提供：CPU使用率，磁盘读写，网卡出入带宽和包量。如您安装了我们的监控代理程序，还可以监控内存使用率，磁盘空间使用率等更多指标。

# 监控代理程序安装

当前，您可以在主机创建完成后，安装我们的监控代理程序，具体安装方式请参考：[监控代理操作指南](https://docs.ucloud.cn/umon/agent)

同时，如果您希望在创建主机时能附带安装和启动我们的监控代理程序，可以参考以下方式，创建主机。

- 限制条件：

  - 机型：快杰机型

  - 镜像：CentOS镜像

  - 可用区：快杰机型所支持的可用区

## 创建控制台操作指南
&ensp; 操作位置：创建控制台下拉到最底部，更多设置卡片中的自定义数据。

![image](https://user-images.githubusercontent.com/91523214/191237686-ab92ed1a-741e-442d-b0a5-77011984a506.png)

步骤一：输入cloud-config脚本

&ensp; 除CentOS 8.0/8.2/8.3镜像版本外，输入以下脚本

```
#config
packages:
- uma
```
&ensp; CentOS 8.0/8.2/8.3镜像版本，输入以下脚本
```
#cloud-config
 packages:
 - uma-py3
```
步骤二：确认是否成功预安装

&ensp; 方法1：通过命令行确认：预安装成功会返回结果，反之则无返回
```
#rpm -qa | grep uma
```
&ensp; 方法2: 在管理控制台，相应云主机的详情页中，确认监控信息模块的数据，若已安装监控agent会展示监控数据
![image](https://user-images.githubusercontent.com/91523214/191244019-8a6cbdea-a3e5-4dec-b1df-c332864ed092.png)



## API操作指南
步骤一：通过设置UserData字段，指定安装监控agent，输入base64编码

&ensp; 除CentOS 8.0/8.2/8.3镜像版本外，输入以下编码

```
I2Nsb3VkLWNvbmZpZwpwYWNrYWdlczoKICAtIHVtYQ==
```
&ensp; CentOS 8.0/8.2/8.3镜像版本，输入以下脚本
```
I2Nsb3VkLWNvbmZpZwpwYWNrYWdlczoKICAtIHVtYS1weTM=
```

步骤二：确认是否成功预安装

&ensp; 方法1：通过命令行确认：预安装成功会返回结果，反之则无返回
```
#rpm -qa | grep uma
```
&ensp; 方法2: 在管理控制台，相应云主机的详情页中，确认监控信息模块的数据，若已安装监控agent会展示监控数据
![image](https://user-images.githubusercontent.com/91523214/191244019-8a6cbdea-a3e5-4dec-b1df-c332864ed092.png)


