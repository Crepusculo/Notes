
<!-- toc orderedList:0 depthFrom:1 depthTo:6 -->

- [__A__](#__a__)
	- [ARP](#arp)
		- [ARP 代理](#arp-代理)
- [__C__](#__c__)
	- [CSMA](#csma)
- [__I__](#__i__)
	- [ICMP](#icmp)
	- [IGP](#igp)
- [__J__](#__j__)
	- [JavaBean](#javabean)
- [__O__](#__o__)
	- [OSPF](#ospf)
- [__P__](#__p__)
	- [POJO](#pojo)
	- [POP](#pop)
- [__R__](#__r__)
	- [RESTful](#restful)
	- [RIP](#rip)
- [__S__](#__s__)
	- [Spring](#spring)
	- [SpringBoot](#springboot)
	- [SpringMVC](#springmvc)
	- [Structs](#structs)

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
# __C__
## CSMA
Carrier Sense Multiple Access
载波侦听 多路访问
__载波侦听（英语：Carrier Sense，CS）__
指任何连接到介质的设备在欲发送帧前，必须对介质进行侦听，当确认其空闲时，才可以发送。
__多路访问（英语：Multiple Access，MA）__
指多个设备可以同时访问介质，一个设备发送的帧也可以被多个设备接收。
# __I__
## ICMP
Internet Control Message Protocol
网络消息控制协议
## IGP


# __J__
## JavaBean
# __O__
## OSPF
Open Shortest Path First
开放式最短路径优先

是对链路状态路由协议的一种实现，隶属内部网关协议（IGP）故运作于自治系统内部。

是

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
# __R__
## RESTful

## RIP
__Routing Information Protocol__
__路由信息协议__
| TCP/IP协议层 | 网络层 |
|---|---|
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
