# 1. EC2的介绍与使用(Amazon Elastic Compute Cloud)

## 1.1 左侧菜单栏的介绍

* 事件
* 标签 每个AWS服务都有这个TAG功能，但在EC2这里，可以按照绑定标签的情况看到一览。比如，建立一个用户A标签，在接下来的操作中所新建的实例等添加该标签，方便日后区分和删除。
* 报告 EC2的使用状况的报告
* 限制 介绍了当前情况下的EC2的一些限制情况，如果不符合用户需求的话，可以[Service Quotas]或者[Support]中提出请求进行缓和。
* 实例
  * 实例 提供计算的实例
  * 实例类型 介绍了可选的CPU，内存等条件
  * 启动模板 预先配置好的EC2实例模板，以达到auto scaling时启动的实例相同
  * Spot请求 没用过，不知道
  * Savings plans 没用过，不知道
  * 预留实例 没用过，不知道
  * 专用主机 没用过，不知道
  * 预留容量 没用过，不知道
* 映像
  * AMI 系统镜像，比上面的模板相比缺少了VPC配置等
  * 捆绑任务 没用过，不知道
* ELASTIC BLOCK STORE
  * 卷 挂载到EC2上的硬盘
  * 快照 硬盘上的数据的一时版本
  * 生命周期管理器  没用过，不知道
* 网络与安全
  * 安全组 管理入站和出站的规则(即IP，端口的限制)
  * 弹性IP 没用过，不知道
  * 个置放群组 没用过，不知道
  * 密钥对 启动EC2实例时使用的密钥，可生成登陆密码
  * 网络接口 绑定后可以使EC2访问别的资源
* 负载均衡
  * 负载均衡器 将对负载均衡器发出的请求转发至目标群组或指定对象
  * 目标群组 可以是各种AWS服务或EC2的某个终端节点
* AUTO SCALING
  * 启动配置  没用过，不知道
  * Auto Scaling组 指定启动模板以达到Auto Scaling

## 1.2 启动实例

点击实例，右侧会出现实例状况一览。在右侧面板中，点击上方的启动实例按钮。

### 1.2.1 步骤1 选择AMI

选择列表左边的仅免费套餐的checkbox，然后选择合适的系统并点击选择

### 1.2.2 步骤2 选择实例类型

选择CPU和内存的界面，在这里也选择免费套餐，然后点击下一步

### 1.2.3 步骤3 配置实例

实例详细界面有很多可以配置的选项，对应的选项旁边的小叹号有具体说明，请自行取舍(VPC处选择默认，到VPC时再做补充)。此处的IAM角色可以参照上一节课的说明

### 1.2.4 步骤4 添加存储

即菜单中的EBS(Elastic Block Store)，酌情设置大小。  
※windows免费套餐的客户最多可获得 30GB 的 EBS 通用型(SSD)或磁存储器,linux为8GB

### 1.2.5 步骤5 添加标签

即菜单中的标签。

### 1.2.6 步骤6 配置安全组

选择现有的VPC安全组或者默认新建一个打开3389的远程连接端口的安全组。  
对于我所接触的项目来说一般配置一个「踏み台サーバ」，在这个服务器上可以连接其余的EC2实例。

### 1.2.7 审核

显示出你之前所选择的参数的一览，也可以在这个界面修改之前的参数。  
当你点击启动后，会弹出一个选择密钥的窗口，选择一个之前建好的密钥或者新建一个密钥，进行下一步

## 1.3 新建实例后的界面说明

点击查看实例后，回到主画面，然后看到右方实例一览列表中有一个新建实例，此时点击新建实例的checkbox，下方会显示出该当实例的配置信息等情报。

接下来介绍Windows的连接方式：  
点击上方的连接按钮，有RDP(Remote Desktop Protocol)和SSM(AWS Systems Manager)两种方式，后者在讲解该服务时说明。前者根据画面提示下载桌面连接程序后，点击下方获取密码，再将1.2.7节选择的密钥填入后，即可获取密码。默认用户名是administrator

Linux系统的连接方式：  
由于大部分Linux系统并没有GUI，所以多出一种浏览器的连接方式(谷歌浏览器的扩展商店也可以搜到SSH连接插件)。默认用户名是ec2-user

## 1.4 弹性IP

每回停止(STOP)实例的时候，公有IP地址会被回收，再启动就会被分配一个新的IP地址。如果想使用固定的共有IP，则可以使用弹性IP的功能。  
使用方式： 从Amazon的IPV4池或者VPC处建立的自己的IPV4池，又或者是在别处建立的自定义IPV4池中分配一个固定的共有IP。然后，在一览界面选择该弹性IP，点击右上角的Actions，关联弹性IP地址。可关联到EC2实例或者网络接口。

## 1.5 AMI做成

现将ec2停止，选择☑️该当ec2后点击操作，映像，输入映像名称创建。返回到ami可以观察到新创建的映像。创建ami时会同步创建卷的备份即快照。之后可以在创建ec2的第一步中选择我的ami后就可以看到刚才创建的ami。

## 2 注意事项

* 在项目过程中，搭建了两台EC2，安装了Apache和Tomcat服务器后发现无法通信，即使在同一个子网下也需要关闭防火墙才可以通信
* Apache和Tomcat之前使用AJP协议，在追加了负载均衡器后需要改成http或https协议
* 建好的EC2默认安装了AWS CLI ←需要EC2绑定角色或访问密钥才能调用别的服务
* 在使用启用粘性会话的负载均衡器的话，response中会被设置两次[AWS-Cookie](https://forums.aws.amazon.com/thread.jspa?messageID=751842)
* 使用负载均衡后需要在Apache的代理处，添加disablereuse属性，以提高负载均衡的利用率
``` XML
<IfModule proxy_http_module> 
  <Location /mieruka/webapp> 
    ProxyPass http://internal-DNS/mieruka/webapp disablereuse=on timeout=600 
    ProxyPassReverse http://internal-DNS/mieruka/webapp 
  </Location> 
</IfModule> 
```
[disablereuse](https://httpd.apache.org/docs/2.4/en/mod/mod_proxy.html#proxypass)的文档  
This parameter should be used when you want to force mod_proxy to immediately close a connection to the backend after being used, and thus, disable its persistent connection and pool for that backend. This helps in various situations where a firewall between Apache httpd and the backend server (regardless of protocol) tends to silently drop connections or when backends themselves may be under round- robin DNS. When connection reuse is enabled each backend domain is resolved (with a DNS query) only once per child process and cached for all further connections until the child is recycled. To disable connection reuse, set this property value to On
