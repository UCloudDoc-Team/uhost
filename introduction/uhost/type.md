

# 机型与规格

*注意：2019年5月上线新版主机创建页后，主机机型概念已升级到2.0版本。此文档描述的1.0版本概念将不再沿用。请参照
[机型与CPU平台](/compute/uhost/introduction/uhost/type_new)
进行选型。控制台列表展示的机型也已全部采用了2.0版本机型概念，新旧版机型概念对比参照
[FAQ](/compute/uhost/faq#主机机型概念10和20发生了哪些变化)。*

以下为1.0版主机概念的文档：

### 规格族简述

UCloud云主机根据应用场景将主机区分为：**标准型N、高IO型I、高主频型C、GPU型G**总计4种规格族，并支持总计3个系列的10种机型。

|       | 特点                   | 适用场景                |
| ----- | -------------------- | ------------------- |
| 标准型N  | 配置自由灵活，选择丰富          | 企业级应用，游戏，内存服务，数据分析等 |
| 高主频型C | 采用3.2GHz主频的CPU，计算性能强 | 高频交易，数据处理，图形渲染等     |
| 高IO型I | 采用本地SSD磁盘，IO性能高      | 中大型数据库，核心业务服务器等     |
| GPU型G | 搭载K80，P40或V100 GPU   | 人工智能，科学计算，图形渲染等     |

价格详情请参见：[主机价格](https://docs.ucloud.cn/compute/uhost/price)

### 标准型 N

* 机型特点：配置自由灵活，可选性价比出众的SSD云盘与IO优化技术加持的本地磁盘，满足通用场景。
* 适用场景：企业级应用，游戏，内存服务，数据分析等

**系列3 N3 (公测中)**

* 物理CPU: Intel Xeon Gold 6126 V5 (Skylake) - 2.6GHz
* CPU与内存配比为 1:1-1:8
* 配置范围：1核1G - 32核256G
* 支持网络增强，热升级
* 系统盘：
  
``` 
本地普通盘：默认大小Linux 20GB，Windows 40GB，支持创建后扩容到100GB，支持数据方舟
SSD云盘：默认大小Linux 20GB，Windows 40GB，支持扩容到500GB
```

* 数据盘：
  
``` 
本地普通盘：20GB～2000GB，支持数据方舟
普通云盘：20GB～8000GB，支持快照与数据方舟
SSD云盘：20GB～4000GB
```

**系列2 N2**

* 物理CPU: Intel Xeon E5-2650 V4 (Broadwell)
* CPU与内存配比为 1:1-1:4
* 配置范围：1核1G - 32核128G
* 支持网络增强，热升级
* 系统盘：
  
``` 
本地普通盘：默认大小Linux 20GB，Windows 40GB，支持创建后扩容到100GB，支持数据方舟
SSD云盘：默认大小Linux 20GB，Windows 40GB，支持扩容到500GB
```

* 数据盘：

``` 
本地普通盘：20GB～2000GB，支持IO加速技术，数据方舟
普通云盘：20GB～8000GB，支持快照与数据方舟
SSD云盘：20GB～4000GB
```

**系列1 N1**

* 物理CPU: Intel Xeon E5-2630 V3 (Haswell) / V2 (Ivy Bridge)
* CPU与内存配比为 1:1-1:4
* 配置范围：1核1G - 16核64G
* 支持网络增强
* 系统盘：

``` 
本地普通盘：默认大小Linux 20GB，Windows 40GB，支持创建后扩容到100GB，支持数据方舟
```

* 数据盘：

``` 
本地普通盘：20GB～2000GB，支持数据方舟
```

### 高主频型 C

* 机型特点：主频达3.2GHz，配置自由灵活，可选高性能的SSD本地磁盘。
* 适用场景：高频交易，数据处理，图形渲染

**系列3 C1 (公测中)**

* 物理CPU: Intel Xeon Gold 6146 V5 (Skylake) - 3.2GHz
* CPU与内存配比为 1:1-1:8
* 配置范围：1核1G - 32核256G
* 支持网络增强，热升级
* 系统盘：

``` 
本地SSD盘：默认大小Linux 20GB，Windows 40GB，支持创建后扩容到100GB
SSD云盘：默认大小Linux 20GB，Windows 40GB，支持扩容到500GB
```

* 数据盘：
  
``` 
本地SSD盘：20GB～1000GB
SSD云盘：20GB～4000GB
```

### 高IO型 I

* 机型特点：附带高性能、低延迟的SSD本地磁盘，提供UCloud最佳的IO性能
* 适用场景：高频交易，中大型数据库，核心业务服务器

**系列2 I2**

* 物理CPU: Intel Xeon E5-2650 V4 (Broadwell)
* CPU与内存配比为 1:1-1:4
* 配置范围：1核1G - 32核128G
* 支持网络增强，热升级
* 系统盘：
  
``` 
本地SSD盘：默认大小Linux 20GB，Windows 40GB，支持创建后扩容到100GB
SSD云盘：默认大小Linux 20GB，Windows 40GB，支持扩容到500GB
```

* 数据盘：
  
``` 
本地SSD盘：20GB～1000GB
SSD云盘：20GB～4000GB
```

**系列1 I1**

* 物理CPU: Intel Xeon E5-2630 V3 (Haswell) / V2 (Ivy Bridge)
* CPU与内存配比为 1:1-1:4
* 配置范围：1核1G - 16核64G
* 支持网络增强
* 系统盘：
  
``` 
本地SSD盘：默认大小Linux 20GB，Windows 40GB，支持创建后扩容到100GB
```

* 数据盘：

``` 
本地SSD盘：20GB～1000GB
```

### GPU机型 G

* 机型特点：搭载Nvidia Tesla系列企业级GPU卡
* 适用场景：人工智能，科学计算，图形渲染

**系列2 GPU-V100**

* 物理CPU: Intel Xeon E5-2650 V4 (Broadwell) 
* 采用NVIDIA Tesla V100 GPU
* CPU与内存配比为 1:2-1:4
* 配置范围：4核8G 1颗GPU - 32核128G 4颗GPU
* 支持网络增强
* 系统盘：
  
``` 
本地SSD盘：默认大小Linux 20GB，Windows 40GB，支持创建后扩容到100GB
SSD云盘：默认大小Linux 20GB，Windows 40GB，支持扩容到500GB
```

* 数据盘：
  
``` 
本地SSD盘：20GB～1000GB
SSD云盘：20GB～4000GB
```

**系列2 GPU-P40**

* 物理CPU: Intel Xeon E5-2650 V4 (Broadwell) 
* 采用NVIDIA Tesla P40 GPU
* CPU与内存配比为 1:2-1:4
* 配置范围：4核8G 1颗GPU - 32核128G 4颗GPU
* 支持网络增强
* 系统盘：
  
``` 
本地SSD盘：默认大小Linux 20GB，Windows 40GB，支持创建后扩容到100GB
SSD云盘：默认大小Linux 20GB，Windows 40GB，支持扩容到500GB
```

* 数据盘：
  
``` 
本地SSD盘：20GB～1000GB
SSD云盘：20GB～4000GB
```

**系列1 GPU-K80**

* 物理CPU: Intel Xeon E5-2630 V3 (Haswell) 
* 采用NVIDIA Tesla K80 GPU
* CPU与内存配比为 1:2-1:4
* 配置范围：4核8G 1颗GPU - 16核64G 2颗GPU
* 支持网络增强
* 系统盘：
  
``` 
本地SSD盘：默认大小Linux 20GB，Windows 40GB，支持创建后扩容到100GB
```

* 数据盘：
  
``` 
本地SSD盘：20GB～1000GB
```

具体GPU卡的性能对比见 [GPU机型说明](https://docs.ucloud.cn/ai/gpu/type)

### 大数据型 D

``` 
目前大数据机型已停止对新客户开放
``` 

* 机型特点：附带3T/4T独立磁盘
* 适用场景：Hadoop/Spark等大数据应用

**系列1 D1**

* 物理CPU: Intel Xeon E5-2630 V3 (Haswell) / V2 (Ivy Bridge)
* 配置范围：4核8G，8核16G
* 系统盘：本地普通盘，默认大小Linux 20GB，Windows 40GB（赠送），暂不支持扩容
* 数据盘：本地独享磁盘（无Raid，**硬盘损坏后数据可能无法恢复**，请谨慎选择），3TB/4TB

### 后续阅读

[主机磁盘简介](/compute/uhost/introduction/disk)

[特性简介：网络增强、热升级与数据方舟](/compute/uhost/introduction/uhost/feature)
