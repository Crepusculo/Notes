
<!-- MDTOC maxdepth:6 firsth1:1 numbering:0 flatten:0 bullets:1 updateOnSave:1 -->

- [PPT Summary](#ppt-summary)   
- [Introduction](#introduction)   
   - [Computer Network](#computer-network)   
   - [The network edge](#the-network-edge)   
      - [The network core](#the-network-core)   
         - [[!important] Circuit-switching](#important-circuit-switching)   
         - [[!important] Package-switching](#important-package-switching)   
      - [Internet Structure: network of networks](#internet-structure-network-of-networks)   
   - [Local Area Networks, LANs](#local-area-networks-lans)   
   - [Wide Area Networks, WANs](#wide-area-networks-wans)   
   - [Network Software](#network-software)   
      - [Protocol Hierarchies](#protocol-hierarchies)   
      - [Design Issues for the Layers](#design-issues-for-the-layers)   
      - [Connection-Oriented and Connectionless Services](#connection-oriented-and-connectionless-services)   
      - [Service Primitives](#service-primitives)   
      - [The Relationship of Services to Protocols](#the-relationship-of-services-to-protocols)   
- [Reference Models](#reference-models)   
   - [The OSI Reference Model](#the-osi-reference-model)   
   - [The TCP/IP Reference Model](#the-tcpip-reference-model)   
   - [A Comparison of OSI and TCP/IP](#a-comparison-of-osi-and-tcpip)   
   - [A Critique of the OSI Model and Protocols](#a-critique-of-the-osi-model-and-protocols)   
   - [A Critique of the TCP/IP Reference Model](#a-critique-of-the-tcpip-reference-model)   
- [Architecture of the Internet](#architecture-of-the-internet)   

<!-- /MDTOC -->

# PPT Summary
+ Why computer networking: computer network applications
+ The concept of Computer Network, and the categories of computer networks
+ Network architecture, protocol stack network reference model,
+ Some important concepts: layer, protocol, service, interface, service primitive
+ Connection-oriented service vs. connectionless service

# Introduction

## Computer Network
**Computer Network**: a collection of autonomous computers interconnected by a single technology
 - Interconnected: be able to exchange information,
 - the connection could be via  copper wire, fiber optics, microwaves, infrared, and communication satellites
 - Single technology:
   - Internet is not a single network but a network of networks
   - World Wide Web is a distributed system that runs on top of the Internet

autonomous $n.$ 自主性

## The network edge
- end systems (hosts):
    - run application programs
    - e.g. Web, email
    - at “edge of network”
- client/server model
    - client host requests, receives service from always-on server
    - e.g. Web browser/server; email client/server

### The network core
- mesh of interconnected routers
- the fundamental question: how is data transferred through net?
    - **circuit switching:**
     dedicated circuit per call: telephone net
    - **packet-switching:**
     data sent thru net in discrete “chunks”

mesh $n.$ 网格 / circuit $n.$ 电路

#### [!important] Circuit-switching
#### [!important] Package-switching

### Internet Structure: network of networks
ISP

## Local Area Networks, LANs
LANs are distinguished from other kinds of networks by three characterisitcs:
1)  their size,
2)  their transmission technology, and
3)  their topology

Two broadcast networks: **(a) Bus**; **(b) Ring**
![Two broadcast networks](..\Resource\computer_works_intro_1.jpg)

## Wide Area Networks, WANs
WAN: spans a large geographical area, often a country or continent.
- Communication subnet,
    - sub net: consists of two distinct components: **(1). transmission lines** and **(2). switching elements**
- Hosts

span $v.$ 跨越 / continent $n.$ 大陆

## Network Software
+ Protocol Hierarchies
+ Design Issues for the Layers
+ Connection-Oriented and Connectionless Services
+ Service Primitives
+ The Relationship of Services to Protocols

protocal $n.$ 协议 / hierarchies $n.$ 层次 / issue $n.$ 问题,议题 / oriented $adj.$ 面向 / primitives $n.$  原语

### Protocol Hierarchies

![](..\Resource\computer_works_intro_2.jpg)

Layers, protocals, and interfaces

- **协议栈**
- To reduce their design complexity, most networks are organized as a stack of layers or levels, each one built upon the one below it.
- **同层通话**
- Layer $n$ on one machine carries on a conversation with layer $n$ on another machine. The rules and conventions used in this conversation are collectively known as the layer n protocol
- **约定**
- Basically, a protocol is an agreement between the communicating parties on how communication is to proceed
- **同层对等**
- The entities comprising the corresponding layers on different machines are called peers.
- **层间接口**
- Between each pair of adjacent layers is an interface.
- **所谓网络架构**
- A set of layers and protocols is called a network architecture.
- **协议栈**
- A list of protocols used by a certain system, one protocol per layer, is called a protocol stack.

![computer_works_intro_3](..\Resource\computer_works_intro_2.jpg)Example information flow supporting virtual communication in layer 5.

entity $n.$ 实体 / comprise $v.$ 包括 / corresponding $adj.$ 对应的 / peer $n.$ 对等体 / adjacent $v.$ 相邻

### Design Issues for the Layers
Some of the key design issues that occur in computer networks:
- Addressing
- Error Control
- Flow Control
- Multiplexing ( 复用 )
- Routing

### Connection-Oriented and Connectionless Services
Layers can offer two different types of services to the layers above them:
- **Connection-oriented service**:
- **建立连接的服务**
    - Modeled after the telephone system
    - to use a connection-oriented network service, the service user first establishes a connection, uses the connection, and then release the connection
- **Connectionless service**:
- **无连接服务**
    - Modeled after the postal system
    - Each message carries the full destination address, and each one is routed through the system independent of all the others.

| Type | Service | Example |
|---|:--|:--|
| Connection-oriented |　Reliable message stream | sequence of pages
|                       | Reliable byte stream     | Remote login
|                       | Unreliable connection    | Digitzed voice
| Connection-less     |  Unreliable datagram      | Electronic junk mail
|                       | Acknowledge datagram     | Registered mail
|                       | Request-reply            | Database query
Six different types of service.

digitzed $adj.$ 数字化的 / datagram $n.$ 数据报

### Service Primitives
服务原语

A service is formally specified by a set of **primitives** (operations) available to a user process to access the service.

The set of primitives available depends on the nature of the service being provided.

比如POST啊GET啊之类乱七八糟都是 "nature of the service being provided"

![Resource\computer_works_intro_4.jpg](..\Resource\computer_works_intro_4.jpg)
Packets sent in a simple client-server interaction on a connection-oriented network

### The Relationship of Services to Protocols
![Resource\computer_works_intro_5.jpg](..\Resource\computer_works_intro_5.jpg)
The relationship between a service and a protocol.

# Reference Models
+ The OSI Reference Model
+ The TCP/IP Reference Model
+ A Comparison of OSI and TCP/IP
+ A Critique of the OSI Model and Protocols
+ A Critique of the TCP/IP Reference Model

## The OSI Reference Model
![Resource\computer_works_intro_6_osi.jpg](..\Resource\computer_works_intro_6_osi.jpg)

- **The physical layer:**
    - Concerned with transmitting raw bits over a communication channel.
- **The data link layer:**
    - Mainly to transform a raw transmission facility into a line that appears free of undetected transmission errors to the network layer.
    - Medium access control sublayer
- **The network layer:**
    - A key design issue is determining how packets are routed from source to destination
    - Congestion control
- **The transport layer:**
    - The basic function is to accept data from above, split it up into smaller units  if need be, pass to the network layer, and ensure that the pieces all arrive correctly at the other end.
    - The transport layer is a true end-to-end layer, all the way from the source to the destination.
- **The session layer:**
    - To establish session: for dialog control, token management, and synchronization
- **The presentation layer:**
    - Is concerned with the syntax and semantics of the information transmitted
- **The application layer:**
    - Contains a variety of protocols that are commonly needed by users


transmitting $.$ /  congestion $.$ / session $.$ / syntax $.$ / semantics $.$ /

## The TCP/IP Reference Model
![Resource\computer_works_intro_7_tcpip.jpg](..\Resource\computer_works_intro_7_tcpip.jpg)

| Layer(OSI name) |            |   | TCP/IP|
|---|:-:|---|---|
| **Application + Presentation + Seesion**       | TELNET, FTP, SMTP, DNS  | ↓Protocols |  **Application**
| **Transport**             |  TCP, UDP         || **Transport**
| **Network**               |     IP        ||**Internet**|
| **Physical + Data link** | ARPNET, SATNET, Packet radio, LAN | Networks | **Host-to-network** |
Protocols and networks in the TCP/IP model initially.


- **The Host-to-Network layer:**
    - The TCP/IP reference model does not really say much about what happens below the internet layer.
- **The Internet layer:**
    - To permit hosts to inject packets into any network and have them travel independently to the destination (potentially on a different network).
    - The internet layer defines an official packet format and protocol called IP (Internet Protocol).
- **The transport layer:**
    - Two end-to-end transport protocols have been defined: **TCP** (Transmission Control Protocol), and **UDP** (User Datagram Protocol)
    - Is designed to allow peer entities on the source and destination hosts to carry on a conversation, just as in the OSI transport layer.
- **The application layer:**
    - Telnet, FTP, SMTP, DNS

inject $v.$ 注入/ permit  $v.$ 允许/ potentially  $adv.$ 潜在 /


## A Comparison of OSI and TCP/IP
1. The OSI model made the distinction between services, interfaces, and protocols explicit, while the TCP/IP model did not originally clearly distinguish between these three concepts.
2. The OSI reference model was devised before the corresponding protocols were invented. With TCP/IP the reverse was true.

distinction devised invented reverse explicit

## A Critique of the OSI Model and Protocols
- Why OSI did not take over the world
  - Bad timing
  - Bad technology
  - Bad implementations
  - Bad politics

Critique
## A Critique of the TCP/IP Reference Model
- Problems:
    - Service, interface, and protocol not distinguished
    - Not a general model
    - Host-to-network “layer” not really a layer
    - No mention of physical and data link layers
    - Minor protocols deeply entrenched, hard to replace

# Architecture of the Internet
![Resource\computer_works_intro_8.jpg][8]
Overview of the Internet

[8]:..\Resource\computer_works_intro_8.jpg
