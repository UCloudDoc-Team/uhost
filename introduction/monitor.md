# 监控


我们为您的主机、网络等资源提供监控服务，您可以随时了解系统运行情况和资源使用状况，方便定位分析问题。

主机监控项默认提供：CPU使用率，磁盘读写，网卡出入带宽和包量。如您安装了我们的监控代理程序，还可以监控内存使用率，磁盘空间使用率等更多指标。

## 监控代理程序安装


当前，您可以在主机创建完成后，安装我们的监控代理程序，具体安装方式请参考：[监控代理操作指南](https://docs.ucloud.cn/cloudwatch/ublotagent/UboltAgent_Linux_Installation_Guide)

同时，如果您希望在创建主机时能附带安装和启动我们的监控代理程序，可以通过【创建页】-【高级设置】-【资源监控】，创建主机。

### 创建控制台操作指南 —— 资源监控一键安装
操作位置：创建控制台 - 高级设置 - 资源监控。

- 限制条件：

  - 镜像（基础镜像或从基础镜像衍生的自制镜像）：
    - CentOS 7.9 64位 （标准）
    - CentOS 7.6 64位 （快杰）
    - Ubuntu 22.04 64位
    - Ubuntu 20.04 64位
    - Ubuntu 18.04 64位
    - Debian 11.7 64位
    - RedHat 8.3 64位
    - Rocky 8.5 64位
  - GPU云主机选择上述镜像需要在创建页勾选安装GPU驱动。

    
#### 步骤一：点击开关，开启资源监控

![](https://www-s.ucloud.cn/2025/08/f0990c2bfac3edff1e926edddb4a97a3_1756176566236.png)


#### 步骤二：确认是否成功预安装

##### 查看进程是否启动

执行命令如下：

```bash
ps -ef | grep uboltagent
```

若执行结果如下图所示，说明 UboltAgent 相关进程已正常启动，则已经成功安装 UboltAgent。

![](https://www-s.ucloud.cn/2025/08/75e68ccc76bea93419e60e0f461b6922_1756177473974.png)

##### 查看服务状态

执行命令如下：

```bash
service uboltagent status
# 或者
systemctl status uboltagent
```

若执行结果如下图所示，说明 UboltAgent 服务状态正常。

![](https://www-s.ucloud.cn/2025/08/730834ab849436670aa3f9a60c5ddac2_1756177473992.png)

##### 登录云监控确认

等待约5分钟，进入云主机详情页 - 监控信息，查看相关指标图表数据是否正常展示。

![](https://www-s.ucloud.cn/2025/08/1dde6fe8f8589958c9c7442364300618_1756177474081.png)

---

### API操作指南
#### 步骤一：通过设置UserData字段，指定安装监控agent，输入以下base64编码

```
I2Nsb3VkLWNvbmZpZwpwYWNrYWdlczoKICAtIGN1cmwKcnVuY21kOgotICdjdXJsIC1PIGh0dHA6Ly91bW9uLmFwaS5zZXJ2aWNlLnVjbG91ZC5jbi9zdGF0aWMvY2xvdWR3YXRjaC9pbnN0YWxsX3Vib2x0YWdlbnQuc2ggJiYgc3VkbyBzaCBpbnN0YWxsX3Vib2x0YWdlbnQuc2gn
```
> 请确认镜像版本后安装。

#### 步骤二：确认是否成功预安装

同创建控制台预安装检查方式。

