# 更新CentOS系统

> Note
> 
> 本文提供的方法，以CentOS系列为例。可更新到UCloud软件源维护的最新系统版本。

通过命令：

```
cat /etc/centos-release
```

可查看您当前的系统内核版本。如需要升级，可以进行如下操作：

## Step 1 编辑yum.conf

在/etc/yum.conf中，注释：exclude kernel\* centos-release\*

## Step 2 升级所有软件包

输入命令：

```
yum update
```

此命令将升级CentOS系统和所有相关的软件包到UCloud软件源提供的最新版本。

等待升级完成。

## Step 3 确认升级完成

升级完成后，再次输入命令：

```
cat /etc/centos-release
```

此时会展示升级后的系统版本。
