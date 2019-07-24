# 防火墙启用教程

#### 教程纲要：

开启windows防火墙，并添加远程桌面连接、ICMP v4和ICMP v6多播侦听程序至信任规则中；

windows防火墙可以阻止一些恶意程序攻击，防止某些端口被远程访问；

开启windows防火墙以后ping功能和远程桌面登陆将失效。

> 注：
> 
> 1. 要使用windows防火墙之前需先开启Windows Firewall服务；
> 
> 2. ICMP v4需要手动创建，ICMP v6和远程桌面可以直接添加到信任规则中。


### 开启Windows Firewall服务

将启动类型设置为自动：

![image](/images/software/windows_firewall1.png)

### 启用Windows防火墙

![image](/images/software/windows_firewall2.png)

将远程桌面、ICMP v4和v6的多播侦听程序加入防火墙规则中，其中ICMP v4需要手动创建，ICMP v6和远程桌面可以直接添加到信任规则中。

（1）创建ICMP v4规则：

进入“高级安全Windows 防火墙”，在“入站规则”中点击“新建规则”

![image](/images/software/windows_firewall3.png)

选择自定义规则，点击下一步：

![image](/images/software/windows_firewall4.png)

选择“此程序路径”，并输入“System”，点击下一步：

![image](/images/software/windows_firewall5.png)

在协议类型下拉框中，选择“ICMPv4”，其余均默认，点击下一步：

![image](/images/software/windows_firewall6.png)

在作用域中可以根据自身网络环境要求，在本地或远程IP地址中输入指定的IP地址，也可以选择任何IP地址：

![image](/images/software/windows_firewall7.png)

选择“允许连接”，点击下一步：

![image](/images/software/windows_firewall8.png)

选择作用域的应用规则时使用默认设置，点击下一步：

![image](/images/software/windows_firewall9.png)

输入该规则名称，例如：ICMPv4，点击完成：

![image](/images/software/windows_firewall10.png)

（2）ICMPv6和远程桌面规则可以在入站规则的默认规则中找到，直接启用这些规则即可在防火墙中看到：

![image](/images/software/windows_firewall11.png)

启用后，就可以ping通和远程登录服务器了。

同理，可以仿照以上步骤设置其它防火墙规则。
