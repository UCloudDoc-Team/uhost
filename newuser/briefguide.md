# 创建第一台主机

## 选购一台uhost主机

?> 如果您尚未注册ucloud账号，请先注册账号。

操作流程：
> - 选择地域可用区
> - 选择镜像、CPU及内存
> - 配置网络
> - 配置管理相关项目
> - 选择付费方式并支付

首先登录并前往[控制台页面](https://console.ucloud.cn/)，选择uhost产品，点击创建主机，进入主机配置信息页面。

![img](/images/newuser/console.png)<br>
### 1.选择可用区
![img](/images/newuser/region.png)<br>

> 不同地域之间内网不互通。

### 2.选择镜像、CPU及内存
分为基础配置和自定义配置两种，基础配置为已封装的组合及标准镜像，可快速完成系统的基础配置；自定义配置支持自定义配置机型、cpu平台、镜像、cpu、内存、磁盘、是否开启网络增强、开启热升级等。

![基础配置](/images/newuser/image01.png)<br>

> 1.基础配置默认机型为通用型N，镜像支持目前仅支持ucloud提供的标准镜像，如您还有其他需求，请切换至自定义配置；<br>
> 2.推荐配置目前组合展示四款（1核1G、1核2G、2核4G、4核8G），如您还有其他需求，请切换至自定义配置。
          
![自定义配置](/images/newuser/image02.png)<br>

> 1.可自定义选择[机型](https://docs.ucloud.cn/uhost/introduction/uhost/type_new)、CPU、内存、[磁盘类型及大小](https://docs.ucloud.cn/uhost/introduction/disk)；<br>
> 2.可选择是否开启网络增强以及热升级特性，部分镜像及机型可能不支持网络增强和热升级特性，如您想详情了解，请阅读[云主机特性](https://docs.ucloud.cn/uhost/introduction/uhost/feature)；<br>
> 3.CPU平台是指云主机所在宿主机的CPU微架构版本，每代CPU平台主要升级了硬件架构。如您想详情了解，请阅读[CPU平台](https://docs.ucloud.cn/uhost/introduction/uhost/type_new)。

### 3.配置网络
分为基础网络和自定义网络两种方式。基础网络默认为您绑定外网弹性IP，防火墙策略；自定义网络包括所属vpc、所属子网段、外网弹性IP以及防火墙。防火墙策略展示初始展示“Web推荐”和“非Web推荐”的两种，若有特殊需求可新建防火墙策略，详细操作请阅读[防火墙操作指南](https://docs.ucloud.cn/unet/firewall/guide)。

![img](/images/newuser/net01.png)

在基础网络模式下，默认外网弹性IP带宽为1Mb，防火墙策略有“Web推荐”和“非Web推荐”两种，如果uhost需开启http或https服务，请选择“Wed推荐”。若以上配置不满足您的需求，请选择自定义网络。

![img](/images/newuser/net02.png)

> 带宽提供带宽计费、流量计费以及共享带宽三种计费模式，如您想详细了解计费价格，请阅读[带宽计费](https://docs.ucloud.cn/unet/README)。

### 4.管理员设置
初次建立的登录用户名为默认值，根据镜像类型的选择有所不同，不可更改。依次设置密码、主机名称、是否加入业务组、是否开启硬件隔离组等。密码可根据要求自行设计，也可以系统随机生成。其中隔离组是云主机的逻辑分组，如您想详细了解，请阅读[硬件隔离组](https://docs.ucloud.cn/uhost/guide/isolationgroup)。

![img](/images/newuser/admin01.png)

### 5.选择付费方式并支付
系统默认付费方式为月付，时间默认为购买至月末。系统同时还支持月付、年付、以及按时支付三种方式。以上三种均为预付费，系统会提前扣取下一阶段的费用。点击【立即购买】，完成支付，返回至控制台页面，即可在列表中看到新购买的uhost信息。

![img](/images/newuser/order01.png)<br>

> 选择付费方式：“月付”——>“购买至月末”即表示该订单付款至当前月末，下一期订单从下个月1号零点开始计算。

## 连接uhost主机

连接uhost主机方式分为控制台登录和第三方客户端登录。第三放客户端软件（例如：xshell、PuTTY、SecureCRT等）登录时需开放对应的防火墙端口以及外网ip。
### 1.控制台登录 
点击页面【登录】按钮，录入购买是设置的用户名及密码，即可在网页端登录。

![img](/images/newuser/login01.png)<br>

![img](/images/newuser/shell.png)

> 当云主机状态从“初始化”变为“运行”，即代表初始化完成。

### 2.第三方客户端登录
若云主机配置的镜像为Linux环境，可通过SecureCRT/XShell等工具连接登录，如下图。

![img](/images/newuser/login02.png)

> uhost主机登录界面会因为系统选择的镜像不同有所不同，但登录步骤一致。

## 使用CLI命令创建主机
单击控制台上右上角shell图标（如下图所示），或者直接录入[网址](https://shell.ucloud.cn)启动CLI shell，窗口（或页面）打开后，您需要等待后台分配虚拟机，预计耗时10~20秒。
![img](/images/newuser/CLI.png) <br>


> 当Cloud Shell启动时，会自动创建一台虚拟机，同一个账户的不同会话会共享一台虚拟机。不同账户的虚拟机相互隔离，保障安全。输入以下命令即可完整主机的建立，通过修改API接口参数配置，完成迅速搭建主机的需求（例如：通过修改等效 CLI 命令行的 count 参数，可在 CloudShell 中批量创建超过10台云主机）。

    ucloud uhost create --cpu "4" --charge-type "Month" --os-disk-backup-type "NONE" --os-disk-size-gb "20" --os-disk-type "CLOUD_RSSD" --data-disk-backup-type "NONE" --data-disk-size-gb "20" --data-disk-type "CLOUD_RSSD" --gpu "0" --hot-plug "false" --image-id "uimage-x3wyyb" --machine-type "O" --memory-gb "8" --minimal-cpu-platform "Intel/Auto" --name "UHost" --net-capability "Ultra" --create-eip-bandwidth-mb "1" --create-eip-line "Bgp" --create-eip-traffic-mode "Bandwidth" --password "x1\`:/]F'iE}U" --project-id "org-e543cf" --quantity "0" --region "cn-bj2" --firewall-id "1118814" --subnet-id "subnet-idoejvcs" --vpc-id "uvnet-qk4wyw0c" --group "Default" --zone "cn-bj2-02" --count "1"





