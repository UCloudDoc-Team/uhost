# CentOS 6.X下配置Keepalived VIP

## 一、申请内网VIP

1、用户登录控制台选择数据中心后，在Uhost的主标签下点击”弹性IP”功能按钮，点击”申请IP”按钮下的”申请内网IP”。

![image](/images/software/keep1.jpg)

2、选择需要申请的内网弹性IP的个数，点击”确定”后完成申请流程。

![image](/images/software/keep2.jpg)

3、页面返回后展示申请到的内网弹性IP信息。

![image](/images/software/keep3.jpg)

## 二、安装keepalived

CentOS下直接用yum安装

    # yum install -y keepalived

## 三、配置VIP

先解释下以下步骤中的几个变量（默认使用root权限）：

    $node1: 服务器A的内网IP

    $node2: 服务器B的内网IP

    $vip: 内网VIP

### 服务器A（node1）

1、编辑/etc/keepalived/keepalived.conf

    global_defs {
      router_id LVS_DEVEL
    }
    vrrp_instance VI_1 {
      state MASTER
      interface eth0
      #unicast peer 格式必须完全匹配！否则会起不来，必须写成三行。
      unicast_peer {
            $node2
      }
      virtual_router_id 51
      priority 100 advert_int 1
      authentication {
        auth_type PASS
        auth_pass 1111
      }
      virtual_ipaddress {
            $vip dev eth0
      }
    }

2、启动keepalived

``` 
  # service keepalived start
```

### 服务器B（node2）

1、编辑/etc/keepalived/keepalived.conf

    global_defs {
      router_id LVS_DEVEL
    }
    vrrp_instance VI_1 {
      state BACKUP
      interface eth0
      #unicast peer 格式必须完全匹配！否则会起不来，必须写成三行。
      unicast_peer {
          $node1
      }
      virtual_router_id 51
      priority 90
      advert_int 1
      authentication {
        auth_type PASS
        auth_pass 1111
      }
      virtual_ipaddress {
          $vip dev eth0
      }
    }

2、启动keepalived

``` 
  # service keepalived start
```

## 四、测试VIP

1、检查系统日志, 观察keepalived是否成功

``` 
  # tail /var/log/messsages
```

2、在node1上停止掉keepalived，然后在node1和node2上分别观察IP信息

``` 
  # service keepalived stop
```

``` 
  # ip a
```
