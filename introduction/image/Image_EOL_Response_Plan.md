# 关于镜像结束生命周期（EOL）的应对方案

镜像结束生命周期（End of Life，EOL），是指其操作系统版本已停止维护。**官方停止维护后，UCloud 也将停止对相应基础镜像的更新、维护及相关操作系统技术支持，并在镜像选择时标注「EOL」。**

> **注意：**
EOL 不代表云主机停止运行或镜像立即下架，但操作系统停止维护后将无法获得包括问题修复和功能更新在内的软件维护和支持，建议您及时更换仍在维护期内的镜像版本。针对镜像 EOL 后的解决方案可参考本文档。

## 一、镜像版本维护时间

### Ubuntu

| 版本  | 停止标准维护时间 |
| --- | --- |
| Ubuntu 24.04 LTS | 2029-05-31 |
| Ubuntu 22.04 LTS | 2027-04-30 |
| Ubuntu 20.04 LTS | 2025-05-31 |
| Ubuntu 18.04 LTS | 2023-05-31 |
| Ubuntu 16.04 LTS | 2021-04-30 |
| Ubuntu 14.04 LTS | 2019-04-25 |

以上为标准维护期限，不包含 Ubuntu Pro 等延长维护服务。

详细信息请参见 [Ubuntu 官网](https://ubuntu.com/about/release-cycle)。

### CentOS

| 版本  | 停止维护时间 |
| --- | --- |
| CentOS Stream 9 | 2027-05-31 |
| CentOS 8 | 2021-12-31 |
| CentOS 7 | 2024-06-30 |
| CentOS 6 | 2020-11-30 |

CentOS Stream 持续交付面向 RHEL 后续版本的更新。迁移前，请充分测试业务兼容性。

详细信息请参见 [CentOS 官网](https://www.centos.org/download/)。

### Windows Server

| 版本  | 主流支持结束时间 | 延长支持结束时间 |
| --- | --- | --- |
| Windows Server 2022 | 2026-10-13 | 2031-10-14 |
| Windows Server 2019 | 2024-01-09 | 2029-01-09 |
| Windows Server 2016 | 2022-01-11 | 2027-01-12 |
| Windows Server 2012 | 2018-10-09 | 2023-10-10 |
| Windows Server 2008 | 2015-01-13 | 2020-01-14 |

说明：

- **主流支持**：微软提供安全更新、问题修复及产品改进等支持，结束后进入延长支持阶段。
- **延长支持**：以安全更新为主，通常不再提供新功能；结束后不再提供常规安全更新。

详细信息请参见 [Microsoft 官网](https://learn.microsoft.com/zh-cn/lifecycle/products/)。

### Debian

| 版本  | 常规支持结束时间 | 社区 LTS 结束时间 |
| --- | --- | --- |
| Debian 12 | 2026-06-10 | 2028-06-30 |
| Debian 11 | 2024-08-14 | 2026-08-31 |
| Debian 10 | 2022-09-10 | 2024-06-30 |
| Debian 9 | 2020-07-18 | 2022-06-30 |
| Debian 8 | 2018-06-17 | 2020-06-30 |

说明：

- **常规支持结束时间**：Debian 安全团队停止常规安全维护的时间，之后进入社区长期支持（LTS）阶段。
- **社区 LTS 结束时间**：LTS 团队停止提供安全更新的时间。LTS 只覆盖部分架构和软件包。

详细信息请参见 [Debian 官网](https://www.debian.org/releases/)。

### Red Hat Enterprise Linux

| 版本  | 对应大版本维护支持结束时间 | 固定小版本支持情况 |
| --- | --- | --- |
| Red Hat Enterprise Linux 9.6 | 2032-05-31 | EUS 至 2027-05-31，需相应订阅 |
| Red Hat Enterprise Linux 8.3 | 2029-05-31 | 该小版本于 2021-05-31 停止常规更新 |
| Red Hat Enterprise Linux 6.6 | 2020-11-30 | 该小版本 EUS 于 2016-10-31 结束 |

大版本维护期限不代表旧小版本可一直使用。延长支持的期限随订阅类型而异，以有效订阅及官方政策为准。

详细信息请参见 [Red Hat 官网](https://access.redhat.com/support/policy/updates/errata)。

### Rocky Linux

| 版本  | 停止维护时间 |
| --- | --- |
| Rocky Linux 10.1 | 2028-05-29 |
| Rocky Linux 9.7 | 2026-05-28 |
| Rocky Linux 9.6 | 2025-12-01 |
| Rocky Linux 9.5 | 2025-06-04 |
| Rocky Linux 9.4 | 2024-11-19 |
| Rocky Linux 9.2 | 2023-11-20 |
| Rocky Linux 9.1 | 2023-05-16 |
| Rocky Linux 8.5 | 2022-05-16 |

详细信息请参见 [Rocky Linux 官网](https://docs.rockylinux.org/10/releases/)。

### Kylin（银河麒麟）

| 版本  | 停止维护时间 |
| --- | --- |
| Kylin Server V10 SP3（aarch64） | 以麒麟软件官方公告为准 |

详细信息请参见 [麒麟软件官网](https://support.kylinos.cn/#/support/policies)。

## 二、应对建议

- **无需保留系统盘数据：** 备份重要数据后，通过[重装系统](https://docs.ucloud.cn/uhost/guide/common?id=%e9%87%8d%e8%a3%85%e7%b3%bb%e7%bb%9f)更换镜像。重装会清除原系统盘内容。
- **需要保留业务数据：** 建议使用UCloud服务器迁移中心（USMC）进行迁移，详见[产品说明](https://docs.ucloud.cn/usmc/introduction/concept)。
- **替代镜像选择：** CentOS Linux 用户可优先考虑仍在维护期内的 Rocky Linux，也可选择 Ubuntu、Debian 或具备有效订阅的Red Hat Enterprise Linux；Windows 用户应选择仍受支持的 Windows Server 版本。具体可选版本以控制台为准。
