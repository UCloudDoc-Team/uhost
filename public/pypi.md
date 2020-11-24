# UCloud PyPI私有源配置

PyPI是Python官方的第三方库的仓库。

为解决默认官方源在国内的访问速度受限，并发请求受限，经常出现丢包、超时等问题，UCloud PyPI私有源提供纯内网访问，在UCloud云主机上，无需外网IP地址即可获取所需的Python Package。

## 1、全局配置
在~/.pip/pip.conf文件中配置以下内容：

``` 
[global]
index-url = https://pypi.internal-mirrors.ucloud.cn/simple
``` 

## 2、指定源安装Python Package

``` 
pip3 install flask -i https://pypi.internal-mirrors.ucloud.cn/simple
``` 
