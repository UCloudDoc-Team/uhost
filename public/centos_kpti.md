

# CentOS KPTI关闭方法

为了解决近期爆出的MeltDown漏洞带来的安全风险，UCloud的官方CentOS
6.x与7.x镜像均已更新，新版本镜像默认开启了KPTI（内核页表隔离），以修复该漏洞。请见[Meltdown漏洞详情](https://meltdownattack.com/)

然而，根据测试，开启KPTI可能对虚机性能产生5%-30%的影响。计算类业务影响较小，IO/内存类业务则影响较大。

您可以根据实际情况判断是否关闭KPTI，以在承担安全风险的前提下，恢复性能。

## Centos 6.x

1） 关闭KPTI

``` 
vim /boot/grub/grub.conf 
```

在 kernel 行追加

``` 
nopti 
```

重启虚机生效

2） 验证是否已关闭

输入命令：

``` 
dmesg | grep isolation 
```

若展示以下信息，则表明KPTI仍是开启的。

    x86/pti: Kernel page table isolation enabled

如果关闭成功 上面的这一行信息则不会展示。

## CentOS 7.x

1） 关闭KPTI

输入命令：

    vim /boot/grub2/grub.cfg

在/boot/vmlinuz-\* 行追加

    nopti

重启虚机生效

2） 验证是否已关闭

输入命令：

``` 
dmesg | grep isolation 
```

若展示以下信息，则表明KPTI仍是开启的。

    x86/pti: Unmapping kernel while in userspace

如果关闭成功 上面的这一行信息则不会展示。
