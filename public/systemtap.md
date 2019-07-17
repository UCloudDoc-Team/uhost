# 安装Systemtap

## Ubuntu

添加Ubuntu ddebs源文件，在命令行粘贴如下命令：

    codename=$(lsb_release -c | awk  '{print $2}')
    sudo tee /etc/apt/sources.list.d/ddebs.list << EOF
    deb http://ddebs.ubuntu.com/ ${codename}      main restricted universe multiverse
    deb http://ddebs.ubuntu.com/ ${codename}-security main restricted universe multiverse
    deb http://ddebs.ubuntu.com/ ${codename}-updates  main restricted universe multiverse
    deb http://ddebs.ubuntu.com/ ${codename}-proposed main restricted universe multiverse
    EOF

其中在Ubuntu 11.10中把universe，multiverse删除，改为：

    codename=$(lsb_release -c | awk  '{print $2}')
    sudo tee /etc/apt/sources.list.d/ddebs.list << EOF
    deb http://ddebs.ubuntu.com/ ${codename}      main restricted
    deb http://ddebs.ubuntu.com/ ${codename}-security main restricted
    deb http://ddebs.ubuntu.com/ ${codename}-updates  main restricted
    deb http://ddebs.ubuntu.com/ ${codename}-proposed main restricted
    EOF

Ubuntu Key认证：

    sudo apt-key adv --keyserver keyserver.ubuntu.com --recv-keys ECDCAD72428D7C01

更新索引：

    sudo apt-get update -y

安装Systemtap：

``` 
sudo apt-get install -y systemtap gcc 
```

安装dbgsym：

    sudo apt-get install linux-image-$(uname -r)-dbgsym

验证Systemtap是否安装成功，正确显示hello world即安装成功：

    stap -e 'probe kernel.function("sys_open") {log("hello world") exit()}'

## CentOS

安装systemtap：

    yum install systemtap kernel-devel

下载debuginfo：

先查看系统内核版本：

    uname -rm

到http://debuginfo.centos.org/ 下载对应的RPM包，并安装：

    rpm -Uhv kernel-debuginfo-*rpm

验证Systemtap是否安装成功，正确显示hello world即安装成功：

    stap -e 'probe kernel.function("sys_open") {log("hello world") exit()}'
