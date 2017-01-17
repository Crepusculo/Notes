
<!-- toc orderedList:0 depthFrom:1 depthTo:6 -->

* [__A__](#__a__)
	* [ARP](#arp)
		* [ARP 代理](#arp-代理)
	* [ARQ](#arq)
		* [SR Selective Repeat](#sr-selective-repeat)
		* [GBN Go Back N](#gbn-go-back-n)
		* [Stop-and-wait](#stop-and-wait)
* [__C__](#__c__)
	* [CSMA](#csma)
* [__D__](#__d__)
	* [DHCP](#dhcp)
* [__F__](#__f__)
	* [FEC](#fec)
	* [FDM](#fdm)
* [__H__](#__h__)
	* [HDLC](#hdlc)
* [__I__](#__i__)
	* [ICMP](#icmp)
	* [IS-IS](#is-is)
	* [IGMP](#igmp)
	* [IGP](#igp)
* [__J__](#__j__)
	* [JavaBean](#javabean)
	* [JAAS](#jaas)
	* [JDBC](#jdbc)
	* [JNDI](#jndi)
	* [JTA](#jta)
	* [JPA](#jpa)
* [__O__](#__o__)
	* [OSPF](#ospf)
* [__P__](#__p__)
	* [POJO](#pojo)
	* [POP](#pop)
	* [PPP](#ppp)
* [__R__](#__r__)
	* [RESTful](#restful)
	* [RIP](#rip)
* [__S__](#__s__)
	* [Spring](#spring)
	* [SpringBoot](#springboot)
	* [SpringMVC](#springmvc)
	* [Structs](#structs)
* [__T__](#__t__)
	* [TDM](#tdm)

<!-- tocstop -->

# __A__
## ARP
__Adress Resolution Protocol__
__地址解析协议__
| 简介  | IP -> MAC  |
|---|---|
| __功能__  | 基本功能为透过目标设备的 __IP__ 地址，查询目标设备的 MAC 地址，以保证通信的顺利进行  |
| | |
在IPv6中被 [NDP(邻居发现协议)](#NDP) 替代
### ARP 代理
当发送主机和目的主机不在同一个局域网中时，即便知道目的主机的 MAC 地址，两者也不能直接通信，必须经过路由转发才可以。所以此时，发送主机通过 ARP 协议获得的将不是目的主机的真实 MAC 地址，而是一台可以通往局域网外的路由器的 MAC 地址。于是此后发送主机发往目的主机的所有帧，都将发往该路由器，通过它向外发送。这种情况称为 __ARP 代理（ARP Proxy）__。
## ARQ
__Automatic Repeat-reQuest__
### SR Selective Repeat
### GBN Go Back N
### Stop-and-wait
# __C__
## CSMA
Carrier Sense Multiple Access
载波侦听 多路访问
__载波侦听（英语：Carrier Sense，CS）__
指任何连接到介质的设备在欲发送帧前，必须对介质进行侦听，当确认其空闲时，才可以发送。
__多路访问（英语：Multiple Access，MA）__
指多个设备可以同时访问介质，一个设备发送的帧也可以被多个设备接收。
# __D__
## DHCP
__Dynamic Host Configuration Protocol__
__动态主机设置协议__
是一个局域网的网络协议，__使用UDP工作__
+ 用于内部网络或网络服务供应商自动分配 IP 地址给用户
+ 用于内部网络管理员作为对所有电脑作中央管理的手段
# __F__
## FEC
Forward Error
## FDM
__Frequecy_division multiplexing__
__频分多路复用__
# __H__
## HDLC
__High-Level Data Link Control__
__高级数据链路控制__
# __I__
## ICMP
__Internet Control Message Protocol__
__网络消息控制协议__

网络层

通常用于返回的错误信息或是分析路由。ICMP 错误消息总是包括了源数据并返回给发送者。

每个 ICMP 消息都是直接封装在一个 IP 数据包中的，因此，和 UDP 一样，ICMP 是不可靠的。
## IS-IS
__Intermediate system to intermediate system__
__中间系统到中间系统__
协议是一种基于链路状态算法的路由协议，这意味着作为中间系统的路由器，必须完全知晓自己所在区域内部所有其它的路由器和它们的链路状态。
## IGMP
__Internet Group Management Protocol__
__因特网组管理协议__
是用于管理网路协议多播组成员的一种通信协议。IP 主机和相邻的路由器利用 IGMP 来创建多播组的组成员。
## IGP


# __J__
## JavaBean
## JAAS
## JDBC
## JNDI
## JTA
## JPA
# __O__
## OSPF
Open Shortest Path First
开放式最短路径优先

是对__链路状态路由协议__的一种实现，隶属内部网关协议（IGP）故运作于自治系统内部。

是用 Dijkstra 实现的
是 RIP 的一种替代

|| 链路状态 Link-state | 距离矢量 Distance vector |
|--|---|---|
| __路由器信息__ | 只将它所直连的链路状态与邻居共享, 这个邻居是指一个域内 (domain), 或一个区域内 (area) 的所有路由器！ |会将所有它知道的路由信息与邻居共享, 但是只与直连邻居共享！|
| 回路 | 链路状态路由协议均使用了强健的 SPF 算法，如 OSPF 的 dijkstra，不易产生路由环路，或是一些错误的路由信息。|所有距离矢量路由协议均使用 Bellman-Ford(Ford-Fulkerson) 算法，容易产生路由环路（loop）和计数到无穷大（counting to infinity）的问题。
| |更新的是 “拓扑”！每台路由器上都有完全相同的拓扑，他们各自分别进行 SPF 算法，计算出路由条目！一条重要链路的变化，不必再发送所有被波及的路由条目，只需发送一条链路通告，告知其它路由器本链路发生故障即可。其它路由器会根据链路状态，改变自已的拓扑数据库，重新计算路由条目。|更新的是 “路由条目”！一条重要的链路如果发生变化，意味着需通告多条涉及到的路由条目！|
| | 链路状态路由协议更新是非周期性的（nonperiodic），部分的（partial） | 距离矢量路由协议发送周期性更新、完整路由表更新（periodic & full）
# __P__
## POJO
Plain Ordinary Java Object
简单JAVA对象

POJO 是一个简单的普通的 Java 对象，它不包含业务逻辑或持久逻辑等，但不是 JavaBean、EntityBean 等，不具有任何特殊角色和不继承或不实现任何其它 Java 框架的类或接口。
>"We wondered why people were so against using regular objects in their systems and concluded that it was because simple objects lacked a fancy name. So we gave them one, and it's caught on very nicely."
>----Martin Fowler
[JavaBean](#javabean)
[VO]
[dto]

## POP
__Post Office Protocol__
__邮局协议__
| TCP/IP协议层 | 应用层 |
|---|---|
| __功能__  | POP 支持离线邮件处理。其具体过程是：邮件发送到服务器上，电子邮件客户端调用邮件客户机程序以连接服务器，并下载所有未阅读的电子邮件。这种离线访问模式是一种存储转发服务，将邮件从邮件服务器端送到个人终端机器上，一般是 PC 机或 MAC。一旦邮件发送到 PC 机或 MAC 上，邮件服务器上的邮件将会被删除。但目前的 POP3 邮件服务器大都可以 “只下载邮件，服务器端并不删除”，也就是改进的 POP3 协议。 |

## PPP
__Point-Point Protocol__

# __R__
## RESTful

## RIP
__Routing Information Protocol__
__路由信息协议__
| TCP/IP协议层 | 网络层 |
|---|---|
| __算法__  | __距离向量算法__
| __替代__  | [OSPF](#OSPF) \ [IS-IS](#IS-IS)  |
| __功能__  | 可以通过不断的交换信息让路由器动态的适应网络连接的变化，这些信息包括每个路由器可以到达哪些网络，这些网络有多远等。|
| __运作原理__|同一自治系统 (A.S.) 中的 路由器每 30 秒会与相邻的路由器 交换子讯息，以动态的建立路由表。|
__RIP封包格式__
```
0                   1                   2                   3
0 1 2 3 4 5 6 7 8 9 0 1 2 3 4 5 6 7 8 9 0 1 2 3 4 5 6 7 8 9 0 1
+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+
| command (1)   | version (1)   |      must be zero (2)         |
+---------------+---------------+-------------------------------+
| address family identifier (2) |      must be zero (2)         |
+-------------------------------+-------------------------------+
|                         IP address (4)                        |
+---------------------------------------------------------------+
|                        must be zero (4)                       |
+---------------------------------------------------------------+
|                        must be zero (4)                       |
+---------------------------------------------------------------+
|                          metric (4)                           |
+---------------------------------------------------------------+
```
RIP 允许最大的 hop 数为 15
# __S__
## Spring
## SpringBoot
## SpringMVC
## Structs
# __T__
## TDM
__Time-division Multiplexing__
__时分多路复用__
高速信道根据时间划分成多个时隙供多个低速信道轮流使用，在一个时隙内，只能有一个低速信道占有高速信道的资源。
