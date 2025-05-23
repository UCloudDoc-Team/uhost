

# 镜像

镜像（Image）是云主机实例运行环境的模板，包含了操作系统和预装软件以及配置。

镜像分为四类。

其一是 “标准镜像” ，由UCloud官方提供，包括了各种 Linux、Windows 等操作系统。

其二是 “自制镜像” ，是由用户通过云主机来自行创建的专用镜像，只有用户本人可见。

其三是“共享镜像”，是由已有的自制镜像同地域跨项目共享，被共享项目可以快速创建运行同一镜像环境的云主机。具体请参考[共享镜像](/uhost/guide/image/sharingimage.md)。

其四是 “云市场镜像” ，基于 UCloud 云市场平台，由独立软件供应商（ISV）向用户提供各类软件镜像和相关服务，详情请参考[云市场-商品列表](https://docs.ucloud.cn/umarketplace/description/product_list)。

## 快杰专用镜像

[快杰云主机系列](/uhost/introduction/uhost/type_new#机型)由于采用了[网络增强2.0](/uhost/introduction/feature/feature.md#特性)与[RSSD云盘](/uhost/introduction/disk#磁盘比对概览)技术，针对Linux镜像，对镜像的内核有一定要求，即至少为4.19内核。因此，对于`CentOS 8.0` 以下 / `Ubuntu 20.04` 以下 / `Debian 10.0` 以下的标准镜像，UCloud将其均升级到了4.19内核，取代了其原生内核。该高版本内核不会影响上层应用程序的使用，并且通常比低版本内核的安全性更高。

对于上传后无法支持快杰云主机的镜像，请联系技术支持指导内核版本的升级。

针对 Windows 镜像，则无此类内核版本要求。

## 标准镜像筛选

[获取镜像列表 - DescribeImage](https://docs.ucloud.cn/api/uhost-api/describe_image)

|产品类型 |机型类别 |筛选条件|备注|
|----------- |------------ |------------- |-----------------------|
|云主机|快杰机型|镜像Features包含RssdAttachable，过滤Vgpu_AMD、Vgpu_NVIDIA|快杰机型需要专用镜像，通过RssdAttachable来识别|
|云主机|ARM机型|镜像Features包含RssdAttachable、Aarch64_Type，过滤Vgpu_AMD、Vgpu_NVIDIA|ARM机型是快杰系列里的一种，属于快杰O型Ampere版|
|云主机|非快杰机型|ImageName不能包含“高内核”，过滤Vgpu_AMD、Vgpu_NVIDIA|伪代码演示：!ImageName.includes(“高内核”)|


