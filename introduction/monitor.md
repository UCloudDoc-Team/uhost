# 监控


我们为您的主机、网络等资源提供监控服务，您可以随时了解系统运行情况和资源使用状况，方便定位分析问题。

主机监控项默认提供：CPU使用率，磁盘读写，网卡出入带宽和包量。如您安装了我们的监控代理程序，还可以监控内存使用率，磁盘空间使用率等更多指标。

# 监控代理程序安装

当前，您可以在主机创建完成后，安装我们的监控代理程序，具体安装方式请参考：[监控代理操作指南](https://docs.ucloud.cn/cloudwatch/ublotagent/UboltAgent_Linux_Installation_Guide)

同时，如果您希望在创建主机时能附带安装和启动我们的监控代理程序，可以通过【创建页】-【高级设置】-【资源监控】，创建主机。

## 创建控制台操作指南

### 资源监控一键安装
操作位置：创建控制台-高级设置-监控资源。

- 限制条件：

  - 镜像：
    - CentOS 7.9 64位 （标准）
    - CentOS 7.6 64位 （快杰）
    - Ubuntu 22.04 64位
    - Ubuntu 20.04 64位
    - Ubuntu 18.04 64位
    - Debian 11.7 64位
    - RedHat 8.3 64位
    - Rocky 8.5 64位
   
步骤一：点击开关，开启资源监控

![image](https://www-s.ucloud.cn/2025/08/f0990c2bfac3edff1e926edddb4a97a3_1756176566236.png)


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


