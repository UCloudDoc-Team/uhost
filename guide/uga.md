

# UGA

## 我在/usr/bin/下找到了uga程序，什么是uga？

UGA（UCloud Guest
Agent）是UCloud提供的主机内置代理程序。**仅仅用于帮助用户结合主机控制台功能执行自动化操作，提升用户体验。无法通过UGA查，增，删，改用户文件。**

## UGA能帮助用户进行什么操作？

UGA将帮助您自动进行如下操作，免去手动输入命令。包括：

  - 自动配置4层ULB下主机的IP
  - 无需关机修改密码
  - 自动挂载与卸载UDisk，免于手动输入命令
  - 扩容磁盘免于手动输入命令
  - 自动伸缩
  - 容器等服务的节点，通过UGA实现自动化操作

（以上功能在逐步灰度中，部分用户可能无法操作）

## UGA的原理是什么？

主机内的UGA通过监听外部指定的特殊信号，执行命令。

我们定义了UGA可接收命令的白名单，因此无法通过UGA执行查，增，删，改用户信息的操作。

UGA基于Qemu提供的开源Guest Agent。若希望了解更多，可移步 [Qemu Guest
Agent官方文档](http://wiki.qemu.org/Features/QAPI/GuestAgent#Guest_Agent)

## 如何查看UGA操作的历史记录？

UGA的操作Log位于/var/log/uga.log下。可以查看通过UGA执行的全部命令。

## 如何判断系统内的UGA是UCloud提供的，而非其他人员恶意伪造？

您可以通过UGA程序的MD5判断真伪。

验证方法：

1）执行以下命令，

    md5sum /usr/bin/uga

2）判断生成的MD5是否与以下MD5一致：

    64位uga    a0de274b27ba4f2c7c23fb895c177e6f
    32位uga    1aa5d0d6635926be7e415fc1d126dab7

若一致，则该UGA就是UCloud预装的原版程序。

## 如何卸载UGA？

**我们不建议您卸载UGA。卸载UGA将导致上述功能不可用。**

若您希望卸载UGA，可以执行以下命令：

Centos / Ubuntu / Redhat：

> 1.删除文件/etc/init/uga.conf 文件， kill init 进程
> 
> 2.kill uga进程，确认uga进程不再重启
>
> 3.chattr -i /usr/bin/uga 去除属性(immutable)
>
> 4.删除文件 /usr/bin/uga

Debian：

> 1.修改/etc/inittab文件，注释行： uga:2345respawn:/usr/bin/uga 并保存
>
> 2.init q 重启inittab
>
> 3.查看uga进程不再运行
>
> 4.chattr -i /usr/bin/uga 去除属性(immutable)
>
> 5.删除文件/usr/bin/uga
