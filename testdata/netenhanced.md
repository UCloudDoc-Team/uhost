# 网络增强性能数据



**注意：此文档仅为性能基准的测试，测试通过UDP协议+小包/大包，带来的最大性能值。具体业务场景下的包量受到上层应用、通信协议等多种因素影响，请以实际的业务压测结果为准。**

## 网络性能测试指标

**包量** （常用单位: pps）: 每秒能处理的网络包的数量。是网络增强特性提升的核心指标。

**带宽** （常用单位: mb/s）：网络带宽是指一个固定的时间内（1秒），能通过的最大位数据。

**TCP\_RR** （常用单位: 次/秒）：测试同一个TCP连接中的多次TCP
request和response的响应效率，这种应用场景常常出现在数据库应用中。

**TCP\_CRR** （常用单位:
次/秒）：测试多个TCP连接中的request和response的响应效率，每个TCP请求、响应都建立一个新的TCP连接。最典型的应用是HTTP网页访问请求，每个请求响应都在一个单独的TCP连接中进行。

## 测试数据

### 测试环境

**测试机：**

镜像：CentOS 7.2 64位

规格：1）8核CPU 16G内存 2）16核CPU 32G内存

**辅助机：**

镜像：CentOS 7.2 64位

规格：8核CPU 16G内存 * 8台

### 测试1. 包量测试

采用UDP_STREAM，小包（1byte）测试。

![](/images/testdata/pps_compare.png)

* 网络增强能显著提升包量。UDP测试情况下，峰值包处理能力可达100万pps以上，是未开启网络增强情况下的3倍。
* UCloud的包量能力与规格大小无关。

### 测试2. 带宽测试

采用UDP_STREAM，大包（1400bytes）测试。

![](/images/testdata/bps_compare.png)

网络增强能显著提升带宽，但在出向测试时，达到了内网的最大带宽瓶颈（10G），因此无法进一步提升。

### 测试3. TCP_RR与TCP_CRR

![](/images/testdata/tcp_compare.png)

由于来回路径没有改变，单链只能走一个核和一个通道，是否开启网络增强并无差异。因此开启网络增强不能显著提升TCP_RR与TCP_CRR。

## 测试方法参考

### 测试准备

1）准备测试机与辅助机

创建1台测试机，以及8台辅助机。

2）安装netperf

在测试机和辅助机上执行以下命令安装iperf：

``` 
wget -c "https://codeload.github.com/HewlettPackard/netperf/tar.gz/netperf-2.5.0" -O netperf-2.5.0.tar.gz
tar -zxvf netperf-2.5.0.tar.gz
cd netperf-netperf-2.5.0
./configure && make && make install && cd ..
```

3）开启测试机网络增强功能

在测试机上，参考文档开启网络增强功能：<https://docs.ucloud.cn/compute/uhost/guide/common>

确认网络增强是否开启，执行命令：

``` 
ethtool -l eth0
``` 

获取结果：

``` 
Channel parameters for eth0:
Pre-set maximums: 
RX: 0 
TX: 0 
Other:0 
Combined: 4 //最多支持设置的队列数：4 
Current hardware settings: 
RX: 0 
TX: 0
Other: 0 
Combined: 4 //当前生效的队列数：4 
``` 

### TCP网络性能
#### 入向

1.在测试机启动netserver进程，-p参数指定不同的端口：

``` 
netserver -p 11001 
netserver -p 11002 
netserver -p 11003
netserver -p 11004 
netserver -p 11005 
netserver -p 11006 
netserver -p 11007 
netserver -p 11008
``` 

2.在辅助机上启动netperf进程，分别指定到测试机的不同端口上：

``` 
netperf -H 172.0.0.1 -p 11001 -t TCP\_STREAM -l 310 #第一台 
netperf -H 172.0.0.1 -p 11002 -t TCP\_STREAM -l 310 #第二台 
netperf -H 172.0.0.1 -p 11003 -t TCP\_STREAM -l 310 #第三台 
netperf -H 172.0.0.1 -p 11004 -t TCP\_STREAM -l 310 #第四台 
netperf -H 172.0.0.1 -p 11005 -t TCP\_STREAM -l 310 #第五台 
netperf -H 172.0.0.1 -p 11006 -t TCP\_STREAM -l 310 #第六台
netperf -H 172.0.0.1 -p 11007 -t TCP\_STREAM -l 310 #第七台 
netperf -H 172.0.0.1 -p 11008 -t TCP\_STREAM -l 310 #第八台 
``` 

**NOTE：** 

netperf可以指定不同的数据包大小，测试最好使用大包、中包、小包分别测试：

大包：不指定参数，在缺省情况下，netperf向发送的测试分组大小设置为本地系统所使用的socket发送缓冲大小

中包：使用 -- -m 512 指定数据大小为512bytes

小包：使用 -- -m 1 指定数据大小为1bytes

3.在测试机上执行命令：

``` 
sar -n DEV 1 300 
``` 

查看测试结果。

#### 出向

1.在所有辅助机内启动 1 个 netserver 进程，-p参数指定端口：

``` 
netserver -p 11010 
``` 

2.在测试机上启动 8 个 netperf 进程，分别指定到不同辅助机的netserver端口上：

``` 
netperf -H 172.0.1.1 -p 11010 -t TCP\_STREAM -l 310 #指定第一台
netperf -H 172.0.1.2 -p 11010 -t TCP\_STREAM -l 310 #指定第二台 
netperf -H 172.0.1.3 -p 11010 -t TCP\_STREAM -l 310 #指定第三台 
netperf -H 172.0.1.4 -p 11010 -t TCP\_STREAM -l 310 #指定第四台 
netperf -H 172.0.1.5 -p 11010 -t TCP\_STREAM -l 310 #指定第五台 
netperf -H 172.0.1.6 -p 11010 -t TCP\_STREAM -l 310 #指定第六台 
netperf -H 172.0.1.7 -p 11010 -t TCP\_STREAM -l 310 #指定第七台 
netperf -H 172.0.1.8 -p 11010 -t TCP\_STREAM -l 310 #指定第八台 
``` 

**NOTE：**

netperf可以指定不同的数据包大小，测试最好使用大包、中包、小包分别测试：

大包：不指定参数，在缺省情况下，netperf向发送的测试分组大小设置为本地系统所使用的socket发送缓冲大小。

中包：使用 -- -m 512 指定数据大小为512bytes。

小包：使用 -- -m 1 指定数据大小为1bytes。

3.在测试机上执行命令：

``` 
sar -n DEV 1 300
``` 

查看测试结果。

### UDP网络性能 
#### 入向 

1.在测试机启动netserver进程，-p参数指定不同的端口：

``` 
netserver -p 11001 
netserver -p 11002 
netserver -p 11003
netserver -p 11004 
netserver -p 11005 
netserver -p 11006 
netserver -p 11007 
netserver -p 11008 
``` 

2.在辅助机上启动netperf进程，分别指定到测试机的不同端口上：

``` 
netperf taskset -c 0 -H 10.0.0.75 -p 11001 -t UDP\_STREAM -l 310 -- -m 1400 #第一台 
netperf taskset -c 1 -H 10.0.0.75 -p 11002 -t UDP\_STREAM -l 310 -- -m 1400 #第二台 
netperf taskset -c 2 -H 10.0.0.75 -p 11003 -t UDP\_STREAM -l 310 -- -m 1400 #第三台 
netperf taskset -c 3 -H 10.0.0.75 -p 11004 -t UDP\_STREAM -l 310 -- -m 1400 #第四台 
netperf -H 172.0.0.1 -p 11005 -t UDP\_STREAM -l 310 -- -m 1400 #第五台 
netperf -H 172.0.0.1 -p 11006 -t UDP\_STREAM -l 310 -- -m 1400 #第六台 
netperf -H 172.0.0.1 -p 11007 -t UDP\_STREAM -l 310 -- -m 1400 #第七台
netperf -H 172.0.0.1 -p 11008 -t UDP\_STREAM -l 310 -- -m 1400 #第八台 
``` 

**NOTE：** 

netperf可以指定不同的数据包大小，测试最好使用大包、中包、小包分别测试：

大包：使用 -- -m 1400 指定数据大小为1400bytes

中包：使用 -- -m 512 指定数据大小为512bytes

小包：使用 -- -m 1 指定数据大小为1bytes

3.在测试机上执行命令：

``` 
sar -n DEV 1 300 
``` 

查看测试结果。

#### 出向

1.在所有辅助机内启动 1 个 netserver 进程，-p参数指定端口：

``` 
netserver -p 11010
``` 

2.在测试机上启动 8 个 netperf 进程，分别指定到不同辅助机的netserver端口上：

``` 
netperf -H 172.0.1.1 -p 11010 -t UDP\_STREAM -l 310 -- -m 1400 #指定第一台 
netperf -H 172.0.1.2 -p 11010 -t UDP\_STREAM -l 310 -- -m 1400 #指定第二台 
netperf -H 172.0.1.3 -p 11010 -t UDP\_STREAM -l 310 -- -m 1400 #指定第三台 
netperf -H 172.0.1.4 -p 11010 -t UDP\_STREAM -l 310 -- -m 1400 #指定第四台 
netperf -H 172.0.1.5 -p 11010 -t UDP\_STREAM -l 310 -- -m 1400 #指定第五台 
netperf -H 172.0.1.6 -p 11010 -t UDP\_STREAM -l 310 -- -m 1400 #指定第六台 
netperf -H 172.0.1.7 -p 11010 -t UDP\_STREAM -l 310 -- -m 1400 #指定第七台 
netperf -H 172.0.1.8 -p 11010 -t UDP\_STREAM -l 310 -- -m 1400 #指定第八台
``` 

**NOTE：** 

netperf可以指定不同的数据包大小，测试最好使用大包、中包、小包分别测试：

大包：使用 -- -m 1400 指定数据大小为1400bytes

中包：使用 -- -m 512 指定数据大小为512bytes

小包：使用 -- -m 1 指定数据大小为1bytes

3.在测试机上执行命令：

``` 
sar -n DEV 1 300
``` 

查看测试结果。

### TCP_RR 

1.在辅助机启动 1 个 netserver 进程，-p参数指定端口：

``` 
netserver -p 11010
``` 

2.在测试机执行命令：

``` 
netperf -H 172.0.1.1 -p 11010 -t TCP\_RR -l 300
``` 

3.查看测试结果。

### TCP\_CRR

1.在辅助机启动 1 个 netserver 进程，-p参数指定端口：

``` 
netserver -p 11010
``` 

2.在测试机执行命令：

``` 
netperf -H 172.0.1.1 -p 11010 -t TCP\_CRR -l 300
``` 

3.查看测试结果。
