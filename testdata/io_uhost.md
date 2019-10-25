# 本地磁盘I/O性能测试



**注意：此文档仅为IO性能的基准值测试，由于本地磁盘为共享磁盘，其IO会有一定波动，使性能达不到文档中测试出的水准。若您希望更稳定的IO，建议您选择云盘。**

## 硬盘性能指标

**顺序读写** （吞吐量，常用单位为MB/s）：文件在硬盘上存储位置是连续的。

适用场景：大文件拷贝（比如视频音乐）。速度即使很高，对数据库性能也没有参考价值。

**4K随机读写** （IOPS，常用单位为次）：在硬盘上随机位置读写数据，每次4KB。

适用场景：操作系统运行、软件运行、数据库。

以下是使用通用I/O测试工具“fio”，并在指定数据块大小“4K、512K”、队列深度为“128”的条件下，对“UHost标准版机型”以及“UHost高性能SSD机型”这两种机型磁盘进行的I/O基准性能测试所得出的测试数据。

## 测试结果

### 测试1. 顺序读/写512K

![image](/images/seq512k.jpg)

（本地普通盘与本地SSD磁盘对比）

### 测试2. 随机读/写 4K

![image](/images/rand4k.jpg)

（本地普通盘与本地SSD磁盘对比）

**测试详情**

> 工具：fio
> 
> 官方网站：
> 
> <http://freecode.com/projects/fio>
> 
> <http://brick.kernel.dk/snaps/>

**注意:
性能测试建议直接通过写裸盘的方式进行测试，会得到较为真实的数据。但直接测试裸盘会破坏文件系统结构，导致数据丢失，请在测试前确认磁盘中数据已备份。**

块大小：4kb / 512kb

队列深度：128

fio.conf配置：

```
[global]
ioengine=libaio
iodepth=128
time_based
direct=1
thread=1
group_reporting
randrepeat=0
norandommap
numjobs=32
timeout=6000
runtime=120

[randread-4k]
rw=randread
bs=4k
filename=/dev/sdb   注：/dev/sdb是目标测试磁盘的设备名称
rwmixread=100
stonewall

[randwrite-4k]
rw=randwrite
bs=4k
filename=/dev/sdb
stonewall

[read-512k]
rw=read
bs=512k
filename=/dev/sdb
stonewall

[write-512k]
rw=write
bs=512k
filename=/dev/sdb
stonewall
```

使用方法：shell$\> fio fio.conf
