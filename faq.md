# FAQ



## 主机机型概念1.0和2.0发生了哪些变化？

为了降低新用户对于机型的入门门槛，2019年5月，随新版本主机创建页上线，UCloud定义了主机机型概念2.0，将原先的8款机型合并到了3款。

![](/images/jietu20190519-191704.jpg)

新版机型与旧版对应关系：

| 原有机型      | 现有机型                                   |
| --------- | -------------------------------------- |
| 标准型N1     | 通用型N + IvyBridage/Haswell CPU          |
| 标准型N2     | 通用型N + Broadwell CPU                   |
| 标准型N3     | 通用型N + Skylake CPU                     |
| 高IO型I1    | 通用型N + IvyBridage/Haswell CPU + SSD本地盘 |
| 高IO型I2    | 通用型N + Broadwell CPU + SSD本地盘          |
| 高主频型C1    | 高主频型C                                  |
| GPU型-K80  | GPU型 + K80 GPU                         |
| GPU型-P40  | GPU型 + P40 GPU                         |
| GPU型-V100 | GPU型 + V100 GPU                        |

参照此表格，如果您之前的主力机型为N2，希望创建相同或更好的机型，在控制台上选择通用型N +
CPU平台≥Broadwell即可。后台会根据实际资源情况，分配到原机型N2的宿主机，或更新一代Skylake的宿主机（即原机型N3上）上。

通过将鼠标Hover在“机型”列上，您仍可以看到当前主机原有的机型命名。

![](/images/jietu20190519-191301.jpg)

您仍可以在新建主机时通过“返回旧版”，通过旧的产品概念进行创建；且公共API的现有字段并不会有任何变化，您仍可用之前的方式调用云主机相关API。

新版主机概念详见：详见[机型与CPU平台](/compute/uhost/introduction/uhost/type_new#cpu平台)

## 我该如何选择存储类型？

UCloud云主机可选三种类型的磁盘：云硬盘（UDisk），本地普通盘，和本地SSD盘。

其中云硬盘拥有3份冗余备份，可靠性高，宕机后可秒级恢复；本地盘系列则IO性能更强，但价格相对也更高。

上述机型在部分机房未上线，或因库存原因而限制申请。若您发现无法选择所需的磁盘，请咨询客户经理。

具体性能对比/价格对比请查看 [云主机磁盘简介](/compute/uhost/guide/disk)

## 在控制面板中设置的防火墙，是映射到了系统中的iptables么？

这个是单独的防火墙，和用户系统中的iptables是不一样的。我们建议用户使用后台的防火墙，和iptables实现的效果是一样的，而且操作方便。

## 如果我要安装的软件在UCloud提供的软件源中找不到如何处理？

如果您的云主机有外网IP，可安装第三方源。如使用的用户多，我们会添加到默认的软件源cache中。 如果第三方源中也没有，可自行下载源码编译。
如无外网IP，请向我们反馈，我们会不断更新软件源内容。

## 在SSD云主机上使用MySQL，如何发挥最佳性能？

在SSD云主机上使用MySQL数据库需要进行以下优化：innodb\_io\_capacity设为2000 (若使用MyISAM则无需此配置）

## 怎么将文件迁移到云主机呢？

在原服务器本地打包，然后使用scp或者ftp等方式传输到云主机。

## 云主机停机时是否收费？

云主机在停机时仍会照常收费，请确保将不使用的主机删除。

## 如何扩大SWAP分区呢？

    swapoff -a
    rm /swapfile
    dd if=/dev/zero of=/swapfile bs=1M count=1024
    chmod 600 /swapfile
    mkswap /swapfile
    swapon /swapfile

## 在云主机有一个测试页面，但用17ce去get这个页面，为什么速度很低呢？

17ce的Get属于一个并发测试，如果带宽只有2M的话，那么17ce的每个节点（大概有50个节点左右）只能分到几十K，所以会比较慢。

## CentOS中yum update很慢，如何处理？

将/etc/yum.repos.d/CentOS-Base.repo中6.3（或者其他版本号）改为$releasever，然后yum update。

## Gem经常很慢，不能用，如何更换成taobao的源？

``` 
gem sources --remove http://rubygems.org/
gem sources -a http://ruby.taobao.org/ 
gem sources -l  # 请确保只有 ruby.taobao.org  
gem install foo  
```

## 刚刚做了大并发测试，然后云主机就连不上了，这是为什么呢？

机房防火墙可能认定这是一次攻击行为，从而禁止了对本地IP的访问。如发生此类情况，请和技术支持联系。

## 上传文件到云主机速度很慢？

我们不对上传文件到云主机做速度限制，如果慢的话，可以了解下当地运营商是否对上行有做限制。（如深圳普通ADSL，上行速度限制为512kbps）

## 如何使用双线机房的两个IP做智能解析？

我们推荐使用DNSPod，登录后台后需要输入以下内容：

**主机记录**

主机记录就是域名前缀，常见用法有： www ： 解析后的域名为www.ucloud.cn @ ： 直接解析主域名ucloud.cn * ：
泛解析，匹配其他所有域名*.ucloud.cn

**记录类型** 

这边我们做A记录，选择A即可。

**线路类型 & 记录值** 

线路类型第一条选默认，后面记录值填写电信IP线路类型第二条选联通，后面记录值填写联通IP。

**例子**

![image](/images/dns.png)

## 如何在万网修改DNS地址到DNSPod ?

登陆 <http://diy.hichina.com> -\> 域名管理

![image](/images/wanwang01.png)

按照下图提示，填写DNSPod的2个DNS短地址（对应6台服务器）

f1g1ns1.dnspod.net

f1g1ns2.dnspod.net

![image](/images/wanwang02.png)

## 云主机是否可以更新内核?

可以更新. 和物理服务器一样, 使用yum update或apt-get upgrade linux-image即可

## CentOS上, 我如何制作自定义的内核rpm包?

确认当前内核版本号, 下载对应的SRPM包 :

    #确认当前版本号
    uname -r
    
    # 到valut.centos.org找到SRPM并下载
    # 注意事项
    # (1) 确认是否用了plus版本的内核, 是的话SRPM在/centosplus/Source/SPackages/
    # (2) 非plus版在以下两个目录: /updates/Source/SPackages, /os/Source/SPackages
    wget http://vault.centos.org/6.4/updates/Source/SPackages/kernel-2.6.32-358.14.1.el6.src.rpm

安装SRPM以及相关RPM工具 :

``` 
# 安装SRPM
rpm -ivh kernel-2.6.32-358.14.1.el6.src.rpm

# 安装相关RPM工具
yum install rpm-build redhat-rpm-config patchutils xmlto asciidoc elfutils-libelf-devel zlib-devel binutils-devel newt-devel python-devel perl-ExtUtils-Embed hmaccalc rng-tools kernel-firmware

# 启动rngd服务, 提供足够的熵值 cat /dev/null >/etc/sysconfig/rngd echo 'EXTRAOPTIONS="--rng-device /dev/urandom"' >/etc/sysconfig/rngd service rngd start

```

生成内核源码, 使用diff生成patch文件 :

    # 生成内核源码
    cd ~/rpmbuild/SPECS
    rpmbuild -bp kernel.spec
    
    # 修改并生成diff文件
    cd ~/rpmbuild/BUILD
    cp -r kernel-2.6.32-358.14.1.el6 kernel-2.6.32-358.14.1.el6.mine
    diff -urpN kernel-2.6.32-358.14.1.el6 kernel-2.6.32-358.14.1.el6.mine > this-patch-to-fix-that-bug.patch
    
    # 将patch拷贝到SOURCES下
    cp this-patch-to-fix-that-bug.patch ~/rpmbuild/SOURCES
    
    # 清理
    rm -rf ~/rpmbuild/BUILD/kernel-2.6.32-358.14.1.el6*


修改SPEC文件, 生成新的内核RPM包 :

    # 找到以下几行, 再后面添加一行
    # Source84: config-s390x-generic-rhel
    # Source85: config-powerpc64-debug-rhel
    # Source86: config-s390x-debug-rhel
    
    # 新添加行
    Source87: this-patch-to-fix-that-bug.patch
    Patch001: this-patch-to-fix-that-bug.patch
    
    # (可选) 修改changelog, 找到%changelog这行, 再后插入行:
    * Tue Aug 03 2013 Your Name<yourname@company.com> [2.6.32-358.14.1.el6.centos]
      - [XXX] path to fix that bug

打包生成新的内核RPM包 :

    # 执行SPEC, 生成过程很长请耐心等待.
    # 执行前, 请仔细review上述步骤, 避免出错重来
    rpmbuila -ba kernel.spec
    
    # 会生成若干个RPM包, 其中最关键的如下, 使用rpm -ivh安装即可
    # kernel-2.6.32-358.14.1.el6.x86_64.rpm
    # kernel-devel-2.6.32-358.14.1.el6.x86_64.rpm
    # kernel-headers-2.6.32-358.14.1.el6.x86_64.rpm

## CentOS系统安装软件包出现对kernel-devel依赖的问题，应该如何解决？

为了确保内核的稳定，默认情况下，我们在yum的配置文件/etc/yum.conf中加了exclude=kernel*
centos-release*，这样可以防止在装软件包时无意更新内核相关的东西。
如果确实需要安装此软件包，将/etc/yum.conf中的这行代码注释即可。

## /usr/bin/uga程序是什么？主机中的uga进程是什么？

UGA是UCloud提供的主机内置代理程序。仅仅用于帮助用户结合主机控制台功能执行自动化操作，提升用户体验。无法通过UGA查、增、删、改用户文件。[详情](/compute/uhost/guide/uga)

## 如何激活UHost上的Windows Server?

UCloud上创建的Windows云主机，默认是自动激活的，用户无需再操作。参考 [KMS激活说明](/compute/uhost/windows_op/kms)


若遇特殊原因，需要手动激活一下，则步骤如下：

1.KMS地址

首先定义下各个数据中心的KMS地址（$kms\_name）。步骤4中会用到$kms\_name，请用相应的地址替代。例如北京二可用区E的地址为hb06.kms.ucloud.cn。若需其他可用区地址，请联系技术支持。

- 进入命令目录

用管理员身份打开cmd -> cd C:\Windows\system32

![image](/images/02.png)

- 清除密钥并重启

执行 cscript.exe slmgr.vbs /rearm 来清除统一密钥，完成后重启操作系统。

![image](/images/03.png)

- 配置KMS

用管理员身份打开cmd -> cd C:\Windows\system32。执行cscript.exe slmgr.vbs /skms
$kms\_name(见步骤1)

![image](/images/04.png)

- 激活Windows

执行cscript.exe slmgr.vbs /ato 激活windows

![image](/images/05.png)
