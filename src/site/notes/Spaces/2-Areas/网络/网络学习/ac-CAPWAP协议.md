---
{"dg-publish":true,"dg-path":"网络/网络学习/ac-CAPWAP协议.md","permalink":"/网络/网络学习/ac-CAPWAP协议/"}
---

# 一、开发背景
传统的WLAN体系结构已经没有办法解决大规模组网需求，所以IETF成立CAPWAP工作小组，从而要解决大规模组网的要求，以实现各个厂商控制器与AP之间的互通。

CAPWAP：Control And Provisioning of Wireless Access Points（无线接入点控制和配置协议）
# 二、CAPWAP介绍
## 1.CAPWAP基本的结构：
用于无线AP和无线网络控制器（AC）之间通信，实现AC对其关联的AP集中管理和控制。主要包含以下的内容：
1. AP对AC的自动发现及AP&AC的运行状态机以及维护
2. AC对AP进行管理以及业务配置的下发
3. STA（工作站）数据封装的方式（直接转发、隧道方式）
## 2.WLAN的转发模型
- **直接转发**：对于AP进行管理，业务数据都本地直接转发即AP管理流量是被CAPWAP协议进行封装的，其他的用户业务流量是不经过 CAPWAP 封装的
- **隧道转发**：流量集中转发。业务数据报文统一由AP进行封装，当到达AC后。由AC实现转发。所以这种模式下AC的作用不但对AP进行管理，还要对业务流量时行转发。即AP的管理流量和数据流量都封装在CAPWAP隧道中到达AC

**两者的比较：**
<table>
	<tr>
		<th></th>
		<th>优点</th>
		<th>缺点</th>
	</tr>
	<tr>
		<td rowspan="3">直接转发</td>
		<td>AC处理数据量小</td>
		<td>安全性不高</td>
	</tr>
	<tr>
		<td>转发效率高</td>
		<td>中间网络可以解析用户报文</td>
	</tr>
	<tr>
		<td>业务报文不要多次封装</td>
		<td>业务数据不便于集中管理和控制</td>
	</tr>
	<tr>
		<td rowspan="4">隧道转发</td>
		<td>安全性高</td>
		<td>故障不容易定位</td>
	</tr>
	<tr>
		<td>AC集中转发业务流量</td>
		<td>业务流量必须经过AC转发</td>
	</tr>
	<tr>
		<td>方便集中管理和控制</td>
		<td>数据报文需要经过封装在CAPWAP隧道报文中</td>
	</tr>
	<tr>
		<td>经过加密，数据不易泄漏</td>
		<td>AC所受压力大</td>
	</tr>
</table>

## 3.CAPWAP原理结构：
CAPWAP是基于UDP端口的应用层协议，主要负责对数据，封装转发无线帧。

- CAPWAP数据和控制报文是基于不同的UDP端口：
	- 控制报文端口为UDP端口号：5246
	- 数据报文端口为UDP端口号：5247

### （1）瘦AP发现AC
AP上电以后，先从它自身的AC IP列表中去查找，如果没有此列表，则会启动AP动态发现AC机制，执行DHCP/DNS/广播发现流程与AC连接。
#### ①广播方式
这个也是它默认方式。此方式不需要进行配置的，通过发送广播地址：255.255.255.255，进行查找。如果有AC，那么这个AC就会响应。从而建立CAPWAP控制报文连接。它的局限AP与AC在同一个广播域中。
#### ②跨三层网络的AP发现AC
在这种拓扑中，AP与AC处于不同的VLAN（即不同IP子网中），AP发送广播包是没有办法到达AC，核心的原因是由于广播包被路由器或者交换机隔离，无法自动跨越VLAN边界。因此，AP需要一个明确的方向来查找AC。

**核心技术**：通过一种叫做“DHCP Option 43”扩展字段来实现
通过43字段来告知AC的具体IP地址，这样AP就可以直接使用单播与AC进行通信

**实现过程**：
1. DHCP中通过配置 option 43 字段，DHCP服务器在给AP的offer或ack，会包含这个特殊的option 43字段。所以AP不光通过DHCP获得IP地址，还能从 Option 43 解析出AC的IP地址。
2. 一旦AP得到AC的IP地址后，就不再发送广播，而使用单播（Unicast）直接向AC发起CAPWAP连接请求。
3. AC收到AP的连接请求后，进行身份验证（MAC或者SN号），随后完成AP注册和管理（AP上线）nor=normal

命令的使用方法：
1. DHCP Option43（在DHCP服务器配置中）

<font class="code">[Huawei-Vlanif20] **dhcp server option 43 sub-option 3 ascii** *ascii-string*</font>

其中*ascii-string*是AC的IP地址，如执行命令option 43 sub-option 3 ascii 192.168.0.1,192.168.0.2配置设备为AP指定AC的IP地址为192.168.0.1和192.168.0.2。

2. 查看AC的AP组（在AC上写）

<font class="code">\<Huawei\> **display ac all**