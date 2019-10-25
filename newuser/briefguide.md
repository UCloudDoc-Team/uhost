# 创建第一台主机



此文档适合于2019年5月后新上线的新版主机创建页。

## 五步快捷创建

### 1 选择地域和可用区

![](/images/newuser/region01.png)

请注意不同地域之间内网不互通。

### 2 选择镜像和主机配置

![](/images/newuser/image01.png)

1）基础配置下只支持UCloud提供的标准镜像，若需选择自制镜像，请切换至自定义配置；

2）默认推荐三款常用配置，系统盘与数据盘均为SSD云盘（部分可用区为普通本地盘），若无法满足您的需求，请切换至自定义配置下自行组合搭配。

### 3 设置基础网络

![](/images/newuser/unet01.png)

1）默认为您绑定1Mb的[外网弹性IP](https://docs.ucloud.cn/network/unet/eip)，若暂无绑定外网IP的需求，可切换至自定义网络；

2）防火墙有两种模式可供选择，若云主机希望开启http或https服务，请选择“Web推荐”。

### 4 设置主机管理信息

![](/images/newuser/management01.png)

1）登录用户名为默认值，根据镜像类型的选择有所不同；

2）密码可根据要求自行设置，或选择系统随机生成。

### 5 选择计费方式

![](/images/newuser/order01.png)

支持月付、年付以及按时三种计费模式。其中“月付“-”购至月末”即购买至本月底，下个月账单从1号开始结算。

选择合适的计费方式后点击“立即购买”支付即可。

## 自定义创建

### 1 选择地域和可用区

![](/images/newuser/region01.png)

与快捷创建模式下相同。

### 2 选择镜像和主机配置

![](/images/newuser/image02.png)

1）可选择标准镜像或自制镜像，使用自制镜像需先在云主机管理面板-镜像管理中导入镜像；

2）可自定义选择[机型](https://docs.ucloud.cn/compute/uhost/introduction/uhost/type_new)、CPU、内存、[磁盘类型及大小](https://docs.ucloud.cn/compute/uhost/introduction/disk)。

### 3 选择主机特性和CPU平台

![](/images/newuser/cpu_platform.png)

1）可选择是否开启网络增强以及热升级特性，详情参见：[特性](https://docs.ucloud.cn/compute/uhost/introduction/uhost/feature)；

2）CPU平台为新推出的选型概念，可选择最低CPU平台或后台自动分配，详情参见：[CPU平台](https://docs.ucloud.cn/compute/uhost/introduction/uhost/type_new)。

### 4 设置自定义网络

![](/images/newuser/unet02.png)

1）可选择VPC和子网，也提供新建VPC和子网的链接可完成快速创建后刷新；

2）带宽提供带宽计费、流量计费以及共享带宽三种计费模式，之间的差别参见：[带宽计费模式](https://docs.ucloud.cn/network/unet/index)。

### 5 设置主机管理信息

![](/images/newuser/management02.png)

自定义模式下新增主机名称、业务组以及硬件隔离组的设置，其中隔离组是云主机的逻辑分组，详情参见：[硬件隔离组](https://docs.ucloud.cn/compute/uhost/guide/isolationgroup)。

### 6 选择计费方式

![](/images/newuser/order01.png)

与快捷创建模式下相同。

## 登录您的主机

1）当云主机状态从“初始化”变为“运行”，即代表初始化完成；

![](/images/newuser/uhost01.png)

2）在相应主机下，点击“登录”，弹出主机显示终端窗口；

![](/images/newuser/uhost02.png)

3）根据提示，输入管理员用户名与密码，进入系统，进行后续操作。

> NOTE:
> 
> Linux系统与Windows系统界面不同，但登录步骤类似。

![](/images/uhost_login_linux.png)

（Linux系统下登录）

![](/images/uhost_login_windows.png)

（Windows系统下登录）
