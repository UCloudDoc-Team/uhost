# KMS激活方式说明

本文主要阐述了Windows主机在UCloud云环境中，如何实现自动激活。

## 背景

用户在使用Windows系统时都必需先进行激活，然后才能正常使用，安装应用软件，部署业务环境等等。

由此用户在购买所有Windows系统的UHost时均已包含系统版权费用，在主机初始化过程中，UCloud平台自动激活系统，具体过程如下阐述。

## 采用KMS方式激活

微软在Windows XP、Windows Server 2003的时候采用的是VOL(volume licensing for
organizations)团体批量许可证方式激活系统， 到了Windows Vista后采用了MAK(Multiple Activation
Key)多次激活密钥方式和KMS(Key Management Service)密钥管理服务方式来激活。

他们之间的区别在于MAK是一种以计数的方式，在每次系统重装后输入MAK密钥激活时，这个密钥就被计算到最大激活次数内，当激活次数达到最大激活次数后，这个密钥将无法再次激活；
而KMS是以Server-Client的方式来管理密钥，客户端可以通过局域网与服务端通讯，密钥安装在服务端上，并以密钥管理服务的方式来管理所有与之通讯的客户端主机，如下图所示：

![image](/images/software/kms01.png)

KVM运作机制如下：

1. KMS Server安装密钥后通过公网连接微软授权许可服务器激活自身KMS服务；
2. Client在初始化时内网访问 KMS地址通过DNS Server解析到KMS Server IP；
3. DNS Server定期内网保持与KMS Server集群通讯，如果当探测到一台KMS Server异常时，则自动将域名解析到另一台KMS Server上；
4. KMS Server与Client通过默认端口1688通讯，并自动激活Client端系统，每180天会再次联系KMS Server激活。

## 客户端激活

UHost在初始化完成便可自动激活系统，整个过程用户无感知也无需任何干预。用户远程登陆主机后，可以通过slmgr.vbs
/dlv命令查看激活信息，如下图：

![image](/images/software/kms02.png)

Uhost所在机房：北京二可用区C

Uhost安装系统：Windows server 2008 datacenter r2

若需查询各机房KMS地址，请联系技术支持。

## 常见问题与解答

### Q: 请问你们提供的Windows云主机是否都是正版的呢？

A：我们UCloud提供的所有Windows平台的主机均已向微软购买了官方正版授权许可，您在购买我们Windows版本的主机时就已经包含了系统版权费用，因此您无需再另外购买系统序列号。
主机在初始化时就已经通过内网的KMS服务自动激活，并且每180天会自动激活一次，您可以在主机内部通过cmd命令slmgr.vbs /dlv
查看具体激活信息。

### Q: 如果我要在这些Windows云主机上另外安装其他收费软件是否可以呢？

A：您可以在UCloud的UHost主机内安装收费软件，但是软件所需的版权费用需要用户自行向软件提供商支付，UCloud不会干涉用户在主机内的任何操作，如果您使用盗版软件由此引发的法律责任全部由客户自行承担。

### Q:我在UCloud的一个机房创建了一台Windows主机并制作成了镜像，提交工单后你们帮我把这个镜像迁移到了另一个机房，但是我现在通过这个镜像生成一个新的UHost后系统提示“产品未激活”，请问我该如何解决？

A：由于您的镜像进行了跨机房迁移，因此系统内部的KMS地址发生了变化，镜像里的KMS信息仍然还是记录前一个机房，需要手动激活一次即可解决。
具体操作可以参考我们的 [FAQ文档](/compute/uhost/faq#如何激活UHost上的Windows_Server)。

## 总结

采用KMS方式统一管理系统激活，通过内网随时保持服务端与客户端的通讯，极大地方便了在云环境下的自动化部署与快速生成主机，为客户大批量动态增减资源时，省去了系统激活、环境初始化等一系列重复劳动。

## 参考文档

[微软官网：Windows激活FAQ](http://windows.microsoft.com/en-us/windows/activating-windows-faq#1TC=windows-7)
