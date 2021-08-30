# 域名加速

## 域名加速列表

云主机上无需额外配置，在访问以下域名时即可实现访问加速：

| 分类          | 域名                                                    |
| ------------- | ------------------------------------------------------- |
| **github**    | github.com                                              |
|               | *.github.com                                            |
|               | gist.githubusercontent.com                              |
|               | raw.githubusercontent.com                               |
| **dingtalk**  | *.trans.dingtalk.com                                    |
|               | trans.dingtalk.com                                      |
|               | zjk-cdn-trans.dingtalk.com                              |
|               | sh-cdn-trans.dingtalk.com                               |
|               | sz-cdn-trans.dingtalk.com                               |
| **baidu.com** | *.pcs.baidu.com                                         |
|               | pcs.baidu.com                                           |
|               | *.baidupcs.com                                          |
|               | baidupcs.com                                            |
| **nvidia**    | developer.download.nvidia.com                           |
|               | nvcr.io                                                 |
|               | *.nvcr.io                                               |
|               | helm.ngc.nvidia.com                                     |
|               | *.ngc.nvidia.com                                        |
| **docker**    | download.docker.com                                     |
| **go**        | golang.org                                              |
|               | go.googlesource.com                                     |
| **其他**       | conda.anaconda.org                                      |
|               | conda.io                                                |
|               | repo.anaconda.com                                       |


## 加速效果

测试数据如下，可实现百倍级别的加速。

### 加速前

加速前带宽10KB/s-50KB/s范围内。

```
[root@192-168-6-90 ~]# git clone https://github.com/dgraph-io/dgraph.git
Cloning into 'dgraph'...
remote: Enumerating objects: 162, done.
remote: Counting objects: 100% (162/162), done.
remote: Compressing objects: 100% (137/137), done.
Receiving objects:  10% (10713/98227), 5.32 MiB | 27.00 KiB/s
```

### 加速后

加速后带宽可至1MB/s-10MB/s范围内。

```
[root@192-168-6-90 ~]# git clone https://github.com/dgraph-io/dgraph.git
Cloning into 'dgraph'...
remote: Enumerating objects: 140, done.
remote: Counting objects: 100% (140/140), done.
remote: Compressing objects: 100% (118/118), done.
remote: Total 98205 (delta 60), reused 46 (delta 22), pack-reused 98065
Receiving objects: 100% (98205/98205), 436.16 MiB | 4.32 MiB/s, done.
```

# 加速原理

### 现象

主机上无需做额外配置，执行dig github.com时，会发现解析出一个内网IP地址，这是专门为实现域名加速而提供的服务地址。

```
dig github.com

...

;; ANSWER SECTION:
github.com.		312	IN	A	10.10.211.68

...
```

### 原理

以GitHub实现为例，clone代码时有两种方法，HTTPS和SSH。TSL/SSL加密在客户端和GitHub服务器之间进行，每个连接会生成唯一的加密密钥，且传输的内容是经过完整性校验，客户端会对服务端的主机名和证书进行有效性验证。SSH使用公私钥对进行认证和加密传输，客户端到GitHub服务端的连接是基于非对称加密，实现端到端的加密传输。 

