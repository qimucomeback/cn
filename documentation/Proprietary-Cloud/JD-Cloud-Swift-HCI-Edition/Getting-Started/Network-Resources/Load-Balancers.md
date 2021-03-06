# 负载均衡

京东云敏捷专有云平台提供虚拟负载均衡服务LBaaS（LoadBalanceasaService），负载均衡建立在现有网络结构之上，它提供了一种廉价有效透明的方法扩展网络设备和服务器的带宽、增加吞吐量、加强网络数据处理能力、提高网络的灵活性和可用性。京东云敏捷专有云平台通过管理一个或多个虚拟负载均衡设备，实现业务级别的负载均衡功能。

面对高并发业务场景时，可以将外部访问流量按照一定的负载均衡规则分发至不同的云主机上，有效平衡业务负载压力，确保资源池中的云主机均处于最优的负载状态，提高整个集群的资源利用率与服务效率。

![Load-Balancers-1](../../../../../image/JD-Cloud-Swift-HCI-Edition/Load-Balancers-1.png)

### 负载均衡相关特性描述

#### 虚拟负载均衡高可用
平台支持虚拟负载均衡的创建、编辑、删除与详情列表查看等生命周期管理操作，同时采用高可用设计，保障负载均衡可以稳定、可靠、持续地提供流量分配服务。

#### 监听器
同一负载均衡支持定义多个监听器，监听器支持TCP、HTTP、HTTPS等多种协议类型；同时可定义端口号，此端口为监听器上用来接收请求并向后端服务器转发请求的端口；支持设置外部访问的最大连接数，确保进入资源池的流量在可控范围之内。

#### 资源池服务
平台提供的负载均衡资源池中可添加一到多台云主机，为外部流量提供相同的服务，资源池支持手动弹性伸缩，以匹配外部流量变化，伸缩过程中不影响其对外部提供服务的能力，确保实现资源利用的最大化。平台支持云主机的添加、编辑、删除与查看详情列表等全生命周期操作；向资源池中添加云主机时可设置端口与权重信息，负载均衡会使用该端口向云主机加权转发报文。
虚拟负载均衡服务后端资源池中的云主机均不暴露在外部网络中，用户只需通过IP访问虚拟负载均衡器，而无需清楚内部提供服务的资源池信息，实现对资源的安全保护。

#### 健康检查
负载均衡服务支持对资源池中的云主机进行定期健康检查，支持的检查方式有PING、TCP、HTTP、HTTPS等，一旦检测到云主机运行异常，则不会再将流量分配给这些异常的云主机，直至检测到运行正常后再恢复流量转发，保证服务的可用性。

#### 浮动IP绑定/解绑
平台支持对负载均衡绑定浮动IP，用户可自主选择是否绑定、解绑公网IP并自由切换，灵活搭建内网、公网负载均衡，适应不同场景下的业务需求；通过公网IP绑定的方式，可隐藏内部网络结构，提高系统安全性。

#### 多种负载均衡策略
针对不同资源池，用户可选择不同的负载均衡方式，平台支持的负载均衡方式为轮询、最少连接数、源IP等。用户可以根据实际业务流量情况与应用场景自行选择策略，实现最优的流量分配。