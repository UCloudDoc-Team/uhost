# 安装Cloudera

## 安装Cloudera-Manager

到此链接下载 :

    http://archive.cloudera.com/cm4/installer/latest/cloudera-manager-installer.bin

执行以下脚本 :

    chmod u+x cloudera-manager-installer.bin

进入/etc/yum.repo.d/ :

    cat >cloudera-manager.repo <<\EOF
    [cloudera-manager]
    name=Cloudera Manager
    baseurl=http://cloudera-manager.mirror.ucloud.cn
    gpgcheck=0
    enabled=1
    EOF

执行 :

    cloudera-manager-installer.bin

## 安装Cloudera-CDH

“选择您想安装在主机上的 CDH 的特定版本。”

选择“自定义存储库”

输入http://cloudera-cdh4.mirror.ucloud.cn/
（如果需要安装CDN3，请输入http://cloudera-cdh3.mirror.ucloud.cn）

“选择您想安装在主机上的 Cloudera Manager 的特定版本。

选择“自定义存储库”

输入“<http://cloudera-manager.mirror.ucloud.cn/>”

注:我们的主机名称默认为10-4-4-1（例），在安装CDH的时候，请先修改hostanme，不要含有“-”，部分软件对此不兼容。
