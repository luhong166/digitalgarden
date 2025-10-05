---
{"dg-publish":true,"dg-path":"网络/网络学习/006-生成树STP（Spanning Tree Protocol）.md","permalink":"/网络/网络学习/006-生成树STP（Spanning Tree Protocol）/"}
---

# 一、生成树技术概述
## 1.技术背景
1. 二层交换机网络的冗余性与环路
	1. 一个缺乏冗余性设计的网络，如果发生故障，那么下联的PC将会断网。
	2. 引入冗余性的同时也引入了二层环路
2. 人为错误导致的二层环路

**二层环路带来的问题**：
1. 广播风暴
2. [[Spaces/2-Areas/网络/网络学习/003-以太网交换基础#2.MAC地址\|MAC地址]]漂移

**问答：二层及三层环路**：
1. 三层环路（Layer 3 Loop）
	- 常见根因：路由环路；
	- 动态路由协议有一定的防环能力；
	- IP报文头部中的TTL字段可用于防止报文被无止尽地转发。
2. 二层环路（Layer 2 Loop）
	- 常见根因：网络中部署了二层冗余环境，或人为的误接线缆导致；
	- 需借助特定的协议或机制实现二层防环；
	- 二层帧头中并没有任何信息可用于防止数据帧被无止尽地转发。
## 2.初识生成树协议
在网络中部署生成树后，交换机之间会进行生成树协议报文的交互并进行无环拓扑计算，最终将网络中的某个（或某些）接口进行阻塞（Block），从而打破环路。

![../../../../Extras/Media/media-006-生成树STP（Spanning Tree Protocol）-1.png](/img/user/Extras/Media/media-006-%E7%94%9F%E6%88%90%E6%A0%91STP%EF%BC%88Spanning%20Tree%20Protocol%EF%BC%89-1.png)

交换机上运行的生成树协议会持续监控网络的拓扑结构，当网络拓扑结构发生变化时，生成树能感知到这些变化，并且自动做出调整。
因此，生成树既能解决二层环路问题，也能为网络的冗余性提供一种方案。

![../../../../Extras/Media/media-006-生成树STP（Spanning Tree Protocol）-2.png](/img/user/Extras/Media/media-006-%E7%94%9F%E6%88%90%E6%A0%91STP%EF%BC%88Spanning%20Tree%20Protocol%EF%BC%89-2.png)

**生成树协议在园区网络中的应用位置**：
![../../../../Extras/Media/media-006-生成树STP（Spanning Tree Protocol）-3.png](/img/user/Extras/Media/media-006-%E7%94%9F%E6%88%90%E6%A0%91STP%EF%BC%88Spanning%20Tree%20Protocol%EF%BC%89-3.png)
# 二、STP的基本概念及工作原理
## 1.STP的基本概念
### （1）桥ID（Bridge ID，BID）
- 桥ID由16位的桥优先级（Bridge Priority）和48位的MAC地址构成。在STP网络中，桥优先级是可以配置的，取值范围是0～61440，默认值为32768,可以修改但是修改值必须为4096的倍数。
- 在STP网络中，BID最小的设备会被选举为根桥。

![../../../../Extras/Media/media-006-生成树STP（Spanning Tree Protocol）-4.png|300](/img/user/Extras/Media/media-006-%E7%94%9F%E6%88%90%E6%A0%91STP%EF%BC%88Spanning%20Tree%20Protocol%EF%BC%89-4.png)
### （2）根桥（Root Bridge）
- 在STP网络中，桥ID最小的设备会被选举为根桥。
- 在BID的比较过程中，首先比较桥优先级，优先级的值越小，则越优先，拥有最小优先级值的交换机会成为根桥；如果优先级相等，那么再比较MAC地址，拥有最小MAC地址的交换机会成为根桥。
- 对于一个STP网络，根桥在全网中只有一个，它是整个网络的逻辑中心，但不一定是物理中心。根桥会根据网络拓扑的变化而动态变化。
### （3）开销（Cost）
- 每一个激活了STP的接口都维护着一个Cost值，接口的Cost主要用于计算根路径开销，也就是到达根的开销。
- 接口的缺省Cost除了与其速率、工作模式有关，还与交换机使用的STP Cost计算方法有关。
- 接口带宽越大，则Cost值越小。
- 用户也可以根据需要通过命令调整接口的Cost。

开销默认值：
![../../../../Extras/Media/media-006-生成树STP（Spanning Tree Protocol）-5.png](/img/user/Extras/Media/media-006-%E7%94%9F%E6%88%90%E6%A0%91STP%EF%BC%88Spanning%20Tree%20Protocol%EF%BC%89-5.png)
### （4）根路径开销（Root Path Cost，RPC）
- 在STP的拓扑计算过程中，一个非常重要的环节就是“丈量”交换机某个接口到根桥的“成本”，也即RPC。
- 一台设备从某个接口到达根桥的RPC等于从根桥到该设备沿途所有入方向接口的Cost累加。
- 非根桥通过对比多条路径的路径开销，选出到达根桥的最短路径，这条最短路径的路径开销被称为RPC，并生成无环树状网络。根桥的根路径开销是0。

![../../../../Extras/Media/media-006-生成树STP（Spanning Tree Protocol）-6.png|300](/img/user/Extras/Media/media-006-%E7%94%9F%E6%88%90%E6%A0%91STP%EF%BC%88Spanning%20Tree%20Protocol%EF%BC%89-6.png)
在本例中，SW3从GE0/0/1接口到达根桥的RPC等于接口1的Cost加上接口2的Cost。
### （5）接口ID（Port ID，PID）
- 运行STP的交换机使用接口ID来标识每个接口，接口ID主要用于在特定场景下选举指定接口。
- 接口ID由两部分构成的，高4 bit是接口优先级，低12 bit是接口编号。
- 端口优先级取值范围是0到240，步长为16，即取值必须为16的整数倍。缺省情况下，端口优先级是128。端口ID可以用来确定端口角色。用户可以根据实际需要，通过命令修改该优先级。

![../../../../Extras/Media/media-006-生成树STP（Spanning Tree Protocol）-7.png|300](/img/user/Extras/Media/media-006-%E7%94%9F%E6%88%90%E6%A0%91STP%EF%BC%88Spanning%20Tree%20Protocol%EF%BC%89-7.png)
### （6）BPDU（Bridge Protocol Data Unit，网桥协议数据单元）
- 为了计算生成树，交换机之间需要交换相关的信息和参数，这些信息和参数被封装在BPDU中。
- BPDU分为两种类型：
	- 配置BPDU（Configuration BPDU）
	- TCN BPDU（Topology Change Notification（拓扑改变通告） BPDU）
- 配置BPDU是STP进行拓扑计算的关键；TCN BPDU只在网络拓扑发生变更时才会被触发。
- 在初始化过程中，每个桥都主动发送配置BPDU。在网络拓扑稳定以后，只有根桥主动发送配置BPDU，其他交换机在收到上游传来的配置BPDU后，才会发送自己的配置BPDU。
#### ①配置BPDU的报文格式
|PID|PVI|BPDU Type|Flags|Root ID|RPC|Bridge ID|Port ID|Message Age|Max Age|Hello Time|Forward Delay|
|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|

|字节|字段|描述|
|:-:|:-:|:-:|
|2|PID|协议ID ，对于STP而言，该字段的值总为0|
|1|PVI|协议版本ID，对于STP而言，该字段的值总为0|
|1|BPDU Type|指示本BPDU的类型，若值为0x00，则表示本报文为配置BPDU；若值为0x80，则为TCN BPDU|
|1|Flags|标志，STP只使用了该字段的最高及最低两个比特位，最低位是TC（Topology Change，拓扑变更）标志，最高位是TCA（Topology Change Acknowledgment，拓扑变更确认）标志|
|8|Root ID|根网桥的桥ID|
|4|RPC|根路径开销，到达根桥的STP Cost|
|8|Bridge ID|BPDU发送桥的ID|
|2|Port ID|BPDU发送网桥的接口ID（优先级+接口号）|
|2|Message Age|消息寿命，从根网桥发出BPDU之后的秒数，每经过一个网桥都加1，所以它本质上是到达根桥的跳数|
|2|Max Age|最大寿命，当一段时间未收到任何BPDU，生存期到达最大寿命时，网桥认为该接口连接的链路发生故障。默认20s|
|2|Hello Time|根网桥连续发送的BPDU之间的时间间隔，默认2s|
|2|Forward Delay|转发延迟，在侦听和学习状态所停留的时间间隔，默认15s|

#### ②配置BPDU的转发过程
交换机在刚启动时都认为自己是根桥，互相发送配置BPDU进行STP运算。
![../../../../Extras/Media/media-006-生成树STP（Spanning Tree Protocol）-8.png](/img/user/Extras/Media/media-006-%E7%94%9F%E6%88%90%E6%A0%91STP%EF%BC%88Spanning%20Tree%20Protocol%EF%BC%89-8.png)

### （7）STP的基本工作原理
|字段|
|:-:|
|协议ID|
|协议版本ID|
|类型|
|标志|
|<font color="red">根桥ID</font>|
|<font color="red">根路径开销</font>|
|<font color="red">网桥ID</font>|
|<font color="red">接口ID</font>|
|消息寿命|
|最大寿命|
|Hello时间|
|转发延迟|

**STP按照如下顺序选择最优的配置BPDU**：
1. 最小的根桥ID
2. 最小的RPC
3. 最小的网桥ID
4. 最小的接口ID

**STP操作**：
1. 选举一个根桥。
2. 每个非根交换机选举一个根端口。
3. 每个网段选举一个指定端口。
4. 阻塞非根、非指定端口。

**STP中定义了三种端口角色：指定端口，根端口和预备端口。**
- 指定端口是交换机向所连网段转发配置BPDU的端口，每个网段有且只能有一个指定端口。一般情况下，根桥的每个端口总是指定端口。
- 根端口是非根交换机去往根桥路径最优的端口。在一个运行STP协议的交换机上最多只有一个根端口，但根桥上没有根端口。
- 如果一个端口既不是指定端口也不是根端口，则此端口为预备端口。预备端口将被阻塞。

## 2.STP的计算过程
### （1）在交换网络中选举一个根桥
- STP交换机初始启动之后，都会认为自己是根桥，并在发送给其他交换机的BPDU中宣告自己为根桥。因此，此时BPDU中的根桥ID为各自设备的网桥ID。当交换机收到网络中其他设备发送来的BPDU后，会比较BPDU中的根桥ID和自己的BID。
- 网络中拥有最小桥ID的交换机成为根桥。
- 在一个连续的STP交换网络中只会存在一个根桥。
- 根桥的角色是可抢占的。
- 为了确保交换网络的稳定，建议提前规划STP组网，并将规划为根桥的交换机的桥优先级设置为最小值0。
- 根桥是整个交换网络的逻辑中心，但不一定是它的物理中心。
### （2）在每台非根桥上选举一个根接口
- 什么是根端口？答：由根端口来作为该非根桥设备与根桥设备之间进行报文交互的端口。
- 非根桥交换机上有且只会有一个根接口。
- 当非根桥交换机有多个接口接入网络中时，根接口是其收到最优配置BPDU的接口。
- 可以形象地理解为，根接口是每台非根桥上“朝向”根桥的接口。
- 选举过程比较：RPC-->上行交换机的BID-->上行交换机的PID-->本地交换机的PID（均为值越小，越优选）
	- 上行交换机，即交换机各个端口收到的BPDU来源的交换机
	- 本端交换机各个端口
### （3）在每条链路上选举一个指定接口
- 什么是指定端口？网络中的每个链路与根桥之间的工作路径必须是唯一的且最优的，与该链路相连的交换机（可能不止一台）就必须确定出一个唯一的指定端口。因此，每个链路（Link）选举一个指定端口，用于向这个链路发送BPDU。
- 注意：一般情况下，根桥上不存在任何根端口，只存在指定端口。
- 选举过程比较：RPC-->链路两端交换机的BID-->链路两端端口的PID（均为值越小，越优选）
### （4）非指定接口被阻塞
- 什么是非指定端口（预备端口）？一台交换机上，既不是根接口，又不是指定接口的接口被称为非指定接口。阻塞网络中的非指定接口。这一步完成后，网络中的二层环路就此消除。
- 注意：
	- 非指定端口不能转发由终端计算机产生并发送的帧（用户数据帧），但可以接收并处理BPDU。
	- 根端口和指定端口既可以接收和发送BPDU，也可以转发用户数据帧。
## 3.STP的接口状态
|状态名称|状态描述|
|:-:|:-:|
|禁用（Disable）|该接口不能收发BPDU，也不能收发业务数据帧，例如接口为down|
|阻塞（Blocking）|该接口被STP阻塞。处于阻塞状态的接口不能发送BPDU，但是会持续侦听BPDU，而且不能收发业务数据帧，也不会进行MAC地址学习|
|侦听（Listening）|当接口处于该状态时，表明STP初步认定该接口为根接口或指定接口，但接口依然处于STP计算的过程中，此时接口可以收发BPDU，但是不能收发业务数据帧，也不会进行MAC地址学习|
|学习（Learning）|当接口处于该状态时，会侦听业务数据帧（但是不能转发业务数据帧），并且在收到业务数据帧后进行MAC地址学习|
|转发（Forwarding）|处于该状态的接口可以正常地收发业务数据帧，也会进行BPDU处理。接口的角色需是根接口或指定接口才能进入转发状态|

### STP的接口状态迁移
![../../../../Extras/Media/media-006-生成树STP（Spanning Tree Protocol）-9.png](/img/user/Extras/Media/media-006-%E7%94%9F%E6%88%90%E6%A0%91STP%EF%BC%88Spanning%20Tree%20Protocol%EF%BC%89-9.png)
## 4.拓扑变化
### （1）直连链路故障
![../../../../Extras/Media/media-006-生成树STP（Spanning Tree Protocol）-10.png|300](/img/user/Extras/Media/media-006-%E7%94%9F%E6%88%90%E6%A0%91STP%EF%BC%88Spanning%20Tree%20Protocol%EF%BC%89-10.png)
**直连链路故障，备用端口会经过30s后恢复转发状态。**
- 当两台交换机间用两条链路互连时，其中一条是主用链路，另一条为备用链路。
- 当交换机SW2网络稳定时检测到根端口的链路发生故障，则其备用端口会经过两倍的Forward Delay（15s）时间进入用户流量转发状态。
### （2）非直连链路故障
![../../../../Extras/Media/media-006-生成树STP（Spanning Tree Protocol）-11.png](/img/user/Extras/Media/media-006-%E7%94%9F%E6%88%90%E6%A0%91STP%EF%BC%88Spanning%20Tree%20Protocol%EF%BC%89-11.png)
**非直连链路故障后，SW3的备用端口恢复到转发状态，非直连故障会导致50s左右的恢复时间。**
- 非直连故障
	1. 在稳定的STP网络，非根桥会定期收到来自根桥的BPDU报文。
	2. 若SW1与SW2之间的链路发生了某种故障（非物理故障），因此SW2一直收不到来自根桥SW1的BPDU报文，Max Age计时器（缺省: 20 s）就会超时，从而导致已经收到的BPDU报文失效。
	3. 此时，非根桥SW2会认为根桥失效，并且认为自己是根桥，从而发送自己的配置BPDU给SW3，通知SW3自己是新的根桥。
	4. 在此期间，SW3的预备端口一直收不到包含根桥ID的BPDU，Max Age计时器超时后，端口进入到Listening状态，开始向SW2“转发”从上游发来的包含根桥ID的BPDU。
	5. 因此，Max Age定时器超时后，SW2和SW3几乎同时收到对方发来的BPDU，再进行STP重新计算，SW2发现SW3发来的BPDU更优，就放弃宣称自己是根桥并重新确定端口角色。
- 端口状态：
	- SW3预备端口20s后会从Blocking状态进入到Listening状态，再进入Learning状态，最终进入到Forwarding状态，进行用户流量的转发。
### （3）拓扑改变导致MAC地址表错误
![../../../../Extras/Media/media-006-生成树STP（Spanning Tree Protocol）-12.png](/img/user/Extras/Media/media-006-%E7%94%9F%E6%88%90%E6%A0%91STP%EF%BC%88Spanning%20Tree%20Protocol%EF%BC%89-12.png)
在交换网络中，交换机依赖MAC地址表转发数据帧。**缺省情况下，MAC地址表项的老化时间是300秒**。如果生成树拓扑发生变化，交换机转发数据的路径也会随着发生改变，此时MAC地址表中未及时老化掉的表项会导致数据转发错误，因此在拓扑发生变化后需要及时更新MAC地址表项。
![../../../../Extras/Media/media-006-生成树STP（Spanning Tree Protocol）-13.png](/img/user/Extras/Media/media-006-%E7%94%9F%E6%88%90%E6%A0%91STP%EF%BC%88Spanning%20Tree%20Protocol%EF%BC%89-13.png)
- 拓扑变化过程中，根桥通过TCN BPDU报文获知生成树拓扑里发生了故障。根桥生成TC用来通知其他交换机加速老化现有的MAC地址表项。
- 拓扑变更以及MAC地址表项更新的具体过程如下：
	1. SW3感知到网络拓扑发生变化后，会不间断地向SWB发送TCN BPDU报文。
	2. SW2收到SW3发来的TCN BPDU报文后，会把配置BPDU报文中的Flags的TCA位设置1，然后发送给SW3，告知SW3停止发送TCN BPDU报文。
	3. SW2向根桥转发TCN BPDU报文。
	4. SW1把配置BPDU报文中的Flags的TC位设置为1后发送，通知下游设备把MAC地址表项的老化时间由默认的300 s修改为Forward Delay的时间（默认为15 s）。
	5. **最多等待15 s**之后，SW2中的错误MAC地址表项会被自动清除。此后，SW2就能重新开始MAC表项的学习及转发操作。
# 三、STP的基础配置命令（华为）
1. 配置生成树工作模式

<font class="code">[Huawei] **stp mode** { **stp** | **rstp** | **mstp** }</font>

交换机支持STP、RSTP和MSTP（Multiple Spanning Tree Protocol）三种生成树工作模式，默认情况工作在MSTP模式。

2. （可选）配置根桥

<font class="code">[Huawei] **stp root primary**</font>

配置当前设备为根桥。缺省情况下，交换机不作为任何生成树的根桥。配置后该设备优先级数值自动为0，并且不能更改设备优先级。

3. （可选）备份根桥

<font class="code">[Huawei] **stp root secondary**</font>

配置当前交换机为备份根桥。缺省情况下，交换机不作为任何生成树的备份根桥。配置后该设备优先级数值为4096，并且不能更改设备优先级。

4. （可选）配置交换机的STP优先级

<font class="code">[Huawei] **stp priority** *priority*</font>

缺省情况下，交换机的优先级取值是32768。

5. （可选）配置接口路径开销

<font class="code">[Huawei] **stp pathcost-standard** { **dot1d-1998** | **dot1t** | **legacy** }</font>

配置接口路径开销计算方法。缺省情况下，路径开销值的计算方法为IEEE 802.1t（dot1t）标准方法。
同一网络内所有交换机的接口路径开销应使用相同的计算方法。

<font class="code">[Huawei-GigabitEthernet0/0/1] **stp cost** *cost*</font>

设置当前接口的路径开销值。

6. （可选）配置接口优先级

<font class="code">[Huawei-GigabitEthernet0/0/1] **stp port priority** *priority*</font>

配置接口的优先级。缺省情况下，交换机接口的优先级取值是128。

7. 启用STP/RSTP/MSTP

<font class="code">[Huawei] **stp enable**</font>

使能交换机的STP/RSTP/MSTP功能。缺省情况下，设备的STP/RSTP/MSTP功能处于启用状态。
# 四、生成树技术进阶
- [[快速生成树RSTP（Rapid Spanning-Tree Protocol）\|快速生成树RSTP（Rapid Spanning-Tree Protocol）]]
- [[多生成树MSTP（Multiple Spanning Tree Protocol）\|多生成树MSTP（Multiple Spanning Tree Protocol）]]

***
# 参考文献
[1] 朱仕耿/z00261992（华为技术有限公司）.生成树[PPT].(2019-11-11)[2025-09-11]
