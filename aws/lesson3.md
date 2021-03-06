# 1. VPC的介绍与初步使用(Amazon Virtual Private Cloud)

## 1.1 左侧菜单的介绍

* 您的VPC AWS 云中逻辑隔离的虚拟网络。从所选范围内定义 VPC 的 IP 地址空间。
  * 子网 VPC 的 IP 地址范围内的一个区段，其中可放置隔离的资源组。分为公有和私有，公有需要互联网网关。对于 IPv4，子网的大小下限为 /28（或 14 个 IP 地址）。子网的大小不能超过在其中创建它们的 VPC。
  * 路由表 
  * 互联网网关 公有 Internet 连接的 Amazon VPC 端。
  * 仅出口互联网网关 有状态网关，仅提供从 VPC 到 Internet 的 IPv6 流量传出访问权限。
  * DHCP选项集
  * 弹性IP
  * 终端节点 支持建立从您的 VPC 到 AWS 中托管的服务的私有连接，无需使用互联网网关、VPN、网络地址转换 (NAT) 设备或防火墙代理。
  * 终端节点服务
  * NAT网关 网络地址转换 (NAT) 服务，便于私有子网中的资源访问互联网。
  * 对等连接 对等连接使您可以通过私有 IP 地址在两个对等 VPC 之间路由流量。(两个vpc之间或两个账号之间连接)
* 安全性
  * 网络ACL
  * 安全组
* 虚拟专用网络 vpn
  * 客户网关
  * 虚拟私有网关 VPN 连接的 Amazon VPC 端。
  * 站点到站点的VPC连接
  * 客户端VPN终端节点
* 中转网关 尚未接触
  * 中转网关 尚未接触
  * 中转网关附件 尚未接触
  * 中转网关路由表 尚未接触
  * 网络管理器 尚未接触
* 流量镜像 尚未接触
  * 镜像会话 尚未接触
  * 镜像目标 尚未接触
  * 镜像筛选条件 尚未接触

## 1.2 建立VPC

### 1.2.1 填写基本情报

Name tag: 标识一个VPC的tag，两个VPC可以使用同一个tag，但是他们的VPC ID完全不同  
IPv4 CIDR block: 默认 VPC 分配有 172.31.0.0/16 的 CIDR 范围。自定义的话可以从10.0.0.0/16  
IPv6 CIDR block: 根据需求是否开启IPv6  
Tenancy: 作用未知，待补充，一般默认  

我会使用下面配置进行举例。
Name tag: test  
IPv4 CIDR block: 10.0.0.0/26  
IPv6 CIDR block: none  
Tenancy: default  

当你的情报填写无误创建成功后，会返回到一览界面，随着VPC的成功建立，一个与这个VPC相关联的路由表，网络ACL和安全组也随之创建。

### 1.2.2 为创建的VPC添加子网

由于子网最小的子网掩码是28，所以将「10.0.0.0/26」分为「10.0.0.0/28」，「10.0.0.16/28」，「10.0.0.32/28」，「10.0.0.48/28」4个网段。

### 1.2.3 路由表


## 2 注意事项及个人心得

部分疑问请先参照官网的[常见问题](https://aws.amazon.com/cn/vpc/faqs/?nc1=h_ls)

* 路由表和ACL都是管理出入站的
