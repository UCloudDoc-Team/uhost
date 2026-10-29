# 导入镜像

将所需镜像上传至对象存储 US3，再通过控制台导入为自制镜像，用于创建云主机或为兼容的已有主机重装系统。
**注意，请将镜像添加至公开存储空间。**

## 操作步骤

### 1. 上传镜像至 US3

1. 将符合上述要求的镜像文件上传至 US3 **公开存储空间**。将镜像上传至US3。因镜像容量通常较大，需要使用客户端或SDK上传。[查看说明](https://docs.ucloud.cn/ufile/quick/quick_start)
2. 上传完成后，获取镜像文件的完整访问地址，确认可正常访问；不要使用存储空间或控制台管理页面的地址。

### 2. 导入镜像

1. 登录 UCloud 控制台，切换至目标项目和地域。
  
2. 进入【云主机】>【镜像管理】>【自制镜像】，点击【导入镜像】。
  <img width="807" height="551" alt="image" src="https://github.com/user-attachments/assets/e88592bb-7665-4cdc-9e93-c28f3e69daa1" />

3. 填写镜像名称、描述和 US3 文件地址，选择与文件一致的操作系统平台、版本及镜像格式，点击【确定】。
<img width="812" height="763" alt="image" src="https://github.com/user-attachments/assets/02d8597f-f815-4a7f-b993-0a430ef27a1c" />


### 3. 查看结果并使用

1. 在【自制镜像】列表中查看进度，等待镜像状态变为【可用】。若失败，按页面错误提示检查文件地址、格式和镜像配置。
  
2. 使用镜像创建测试主机，检查启动、登录、网络和磁盘是否正常，再用于正式部署。重装已有主机会替换系统盘内容，操作前须备份数据并确认兼容性。
  
3. 商业操作系统及软件需自行确认授权。
  

## 操作须知

| 检查项 | Linux 镜像 | Windows 镜像 |
| --- | --- | --- |
| 操作系统 | 基于 CentOS、Red Hat、Ubuntu、OpenSUSE、SUSE 发行版的镜像 | Microsoft Windows Server |
| 系统位数 | 支持 32 位和 64 位 | 支持 32 位和 64 位，支持激活 |
| 镜像格式 | raw、vhd、qcow2、vmdk | raw、vhd、qcow2、vmdk |
| 分区与文件系统 | 使用 MBR 分区的ext3或ext4文件系统（不支持GPT分区） | 使用 MBR 分区的NTFS文件系统（不支持GPT分区） |
| 系统盘大小 | 建议不超过 50 GB | 建议不超过 50 GB |
| 驱动  | 必须安装 KVM 虚拟化平台的 virtio 驱动 | 若镜像自带 virtio 驱动时，会以 virtio 启动；若镜像不带该驱动时，会以 IDE 启动 |
| 内核限制 | 建议使用原生内核，修改内核可能导致导入失败；若镜像为Redhat，需要用户自行购买license。 | —   |
| 磁盘范围 | 仅支持系统盘镜像，不支持数据盘 | 仅支持系统盘镜像，不支持数据盘 |

## 其他类型镜像

当您的镜像不在UCloud支持的镜像范围内时，可以选择上传为“其他”类型镜像。
<img width="807" height="765" alt="image" src="https://github.com/user-attachments/assets/b4d97e2b-ac60-4b7d-ad67-a41990857f5f" />

##
