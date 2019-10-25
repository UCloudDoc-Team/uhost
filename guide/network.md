

# 网络

## 管理外网弹性IP

主机的外网带宽，外网IP信息，集中在关联产品——外网弹性IP（EIP）中管理。

云主机可绑定多个EIP，并设置出口。

此外，此处也可修改EIP带宽。修改EIP带宽无需重启，立即生效。

![](/images/guide/common05.png)

备注：弹性IP是独立产品，有独立的订单与计费周期。

详细信息请查看： [EIP文档](/network/unet/eip)

注意事项：大数据主机无法绑定外网弹性IP，若需出外网，请查看[教程](#外网访问配置)。

## 更换防火墙管理

UCloud为云主机提供防火墙功能，类似于IPsec/IPtables的功能，为云主机提供访问控制功能。

详情面板中，可选择更换防火墙。

![](/images/guide/common04.png)

若需要在当前数据中心增加新的防火墙，可以在产品与服务-\>基础网络-\>防火墙，找到对应的产品面板，进行操作。

详细信息请查看防火墙部分： [防火墙管理](..//../../network/firewall/index)

## 外网访问配置

> 因架构原因，大数据机型无法通过EIP进行外网访问。若希望外网访问，可以通过配置虚拟路由器及端口转发，并修改主机内网网关的方式实现外网对此两种机型的访问，操作方法如下：

1.选择UNet-\>弹性IP，申请外网弹性IP，该IP为对此两种机型的访问入口：

![image](/images/bigdata1.png)

2.选择UNet-\>路由器，并创建转发路由器：

![image](/images/bigdata2.png)

3.选择UNet-\>弹性IP，并将刚刚申请的弹性IP绑定到转发路由器上：

![image](/images/bigdata3.png)

4.配置主机中的路由，将路由指向转发路由器，并修改网络设备端口中的网关设置：

**Linux系统中**

```
ip route change default via $router_ip
```

> Note
> 
> 这里的$router\_ip为10.9.31.156，即转发路由器的内网IP地址。

修改/etc/sysconfig/network-scripts/ifcfg-eth\* 中GATEWAY

```
GATEWAY=$router_ip
```

**windows系统**

```
route change 0.0.0.0 mask 0.0.0.0 $router_ip [if n] /p
```

n为网卡号码，单网卡不需要输入中括号中内容。可以通过在cmd中执行route print结果中的第一列查看。

![image](/images/route_print.jpg)

> Note
> 
> 这里的$router\_ip为10.9.31.156，即转发路由器的内网IP地址。 /p参数保证路由配置在服务重启后不会失效。

5.选择UNet-\>路由器-\>点击路由器ID-\>端口转发-\>添加转发规则，填入源端口(外网端口)及需要转发的主机内网IP及主机端口：

![image](/images/bigdata4.png)

![image](/images/bigdata5.png)

> Note
> 
> 为了安全起见，这里尽量使用非常规端口作为转发端口。
