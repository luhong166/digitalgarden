---
{"dg-publish":true,"permalink":"/Spaces/2-Areas/网络/WLAN概述/"}
---

# 一、无线网络介绍
- 无线网络分类：
	- Wireless Personal Area Network（个人无线网络）
	- Wireless Local Area Network （无线局域网络）
	- Wireless Metro Area Network （无线城域网络）
	- Wireless Wide Area Network （无线广域网络）

![../../../Extras/Media/media-WLAN历史概述-1.png](/img/user/Extras/Media/media-WLAN%E5%8E%86%E5%8F%B2%E6%A6%82%E8%BF%B0-1.png)
- 无线传输技术：
	- Ir DA（红外线点对点通讯）
	- Blue Tooth
	- Home RF
	- WiFi（无线高保真Wireless Fidelity，使用无线技术如IEEE802.11a/b/g/n等为局域网提供无线连接）
	- GSM、UMTS、LTE（主要应用于移动网络数据传输，使用频段有900M，1800M，1900M，2100M等，用于无线广域网的覆盖）
# 二、什么是WLAN
**WLAN （Wireless Local Area Network）无线局域网是计算机网络与无线通信技术相结合的产物。**

大家经常说Wi-Fi，那么Wi-Fi和WLAN有什么关系？Wi-Fi＝采用802.11技术的WLAN

|版本|年份|频段|速率|
|:-:|:-:|:-:|:-:|
|802.11|1997|2.4 GHz|2 Mbps|
|802.11 a|1999|5 GHz|54 Mbps|
|802.11 b|1999|2.4 GHZ|11 Mbps|
|802.11 g|2003|2.4 GHz|54 Mbps|
|802.11 n|2009|2.4 GHz<br>5 GHz|600 Mbps|
|802.11 ac Wave1|2013|5 GHz|1.3Gbps|
|802.11 ac Wave2|2015|5 GHz|3.47Gbps|
|802.11ax|2019|2.4GHz<br>5GHz|9.6Gbps|
|802.11 be|2023|2.4GHz<br>5GHz<br>6GHz|30or46.1Gbps|
# 三、WLAN的基础配置案例（华为）
![../../../Extras/Media/media-WLAN历史概述-2.png](/img/user/Extras/Media/media-WLAN%E5%8E%86%E5%8F%B2%E6%A6%82%E8%BF%B0-2.png)
LSW1命名：
```
<Huawei>system-view
Enter system view, return user view with Ctrl+Z.
[Huawei]sysname LSW1
```
LSW1创建VLAN并配置接口为trunk：
```
[LSW1]vlan batch 10 20
Info: This operation may take a few seconds. Please wait for a moment...done.
[LSW1-GigabitEthernet0/0/1]interface GigabitEthernet0/0/1
[LSW1-GigabitEthernet0/0/1]port link-type trunk
[LSW1-GigabitEthernet0/0/1]port trunk allow-pass vlan all
[LSW1-GigabitEthernet0/0/1]interface GigabitEthernet0/0/2
[LSW1-GigabitEthernet0/0/2]port link-type trunk
[LSW1-GigabitEthernet0/0/2]port trunk pvid vlan 10
[LSW1-GigabitEthernet0/0/2]port trunk allow-pass vlan all
```
LSW1配置vlanif接口地址并配置DHCP：
```
[LSW1-GigabitEthernet0/0/2]quit
[LSW1]dhcp enable
Info: The operation may take a few seconds. Please wait for a moment.done.
[LSW1]interface Vlanif10
[LSW1-Vlanif10]ip address 192.168.10.1 255.255.255.0
[LSW1-Vlanif10]dhcp select interface
[LSW1-Vlanif10]dhcp server excluded-ip-address 192.168.10.10
[LSW1-Vlanif10]interface Vlanif20
[LSW1-Vlanif20]ip address 192.168.20.1 255.255.255.0
[LSW1-Vlanif20]dhcp select interface
[LSW1-Vlanif20]dhcp server dns-list 8.8.8.8
[LSW1-Vlanif20]quit
```
LSW1配置默认路由：
```
[LSW1]ip route-static 0.0.0.0 0.0.0.0 192.168.10.10
```
AC1命名：
```
<AC6005>system-view
Enter system view, return user view with Ctrl+Z.
[AC6005]sysname AC1
```
AC1创建VLAN并配置接口为trunk：
```
[AC1]vlan batch 10 20
Info: This operation may take a few seconds. Please wait for a moment...done.
[AC1]interface GigabitEthernet0/0/1
[AC1-GigabitEthernet0/0/1]port link-type trunk
[AC1-GigabitEthernet0/0/1]port trunk allow-pass vlan all
```
AC1配置vlanif接口地址：
```
[AC1-GigabitEthernet0/0/1]interface Vlanif10
[AC1-Vlanif10]ip address 192.168.10.10 255.255.255.0
[AC1-Vlanif10]interface Vlanif20
[AC1-Vlanif20]ip address 192.168.20.10 255.255.255.0
[AC1-Vlanif20]quit
```
AC1配置默认路由：
```
[AC1]ip route-static 0.0.0.0 0.0.0.0 192.168.10.1
```
AC1配置CAPWAP源接口：
```
[AC1]capwap source interface vlanif10
```
AC1配置验证模式：
```
[AC1]wlan
[AC1-wlan-view]ap auth-mode no-auth
Warning: It is insecure to configure none authentication mode.
```
AC1配置三大模板：
SSID模板（其中设置SSID为office）：
```
[AC1-wlan-view]ssid-profile name office
[AC1-wlan-ssid-prof-office]ssid office
Info: This operation may take a few seconds, please wait.done.
```
安全模板（其中设置密码为1234,abcd）：
```
[AC1-wlan-ssid-prof-office]security-profile name office
[AC1-wlan-sec-prof-office]security wpa2 psk pass-phrase 1234,abcd aes
```
VAP模板——虚拟接入点VAP(Virtual Access Point)：
```
[AC1-wlan-sec-prof-office]vap-profile name office
[AC1-wlan-vap-prof-office]ssid-profile office
Info: This operation may take a few seconds, please wait.done.
[AC1-wlan-vap-prof-office]security-profile office
Info: This operation may take a few seconds, please wait.done.
[AC1-wlan-vap-prof-office]service-vlan vlan-id 20
Info: This operation may take a few seconds, please wait.done.
[AC1-wlan-vap-prof-office]forward-mode direct-forword
```
AC1配置AP组：
```
[AC1-wlan-vap-prof-office]quit
[AC1-wlan-view]ap-group name default
[AC1-wlan-ap-group-default]vap-profile office wlan 1 radio all
Info: This operation may take a few seconds, please wait...done.
```

***
# 参考文献
[1] 华为技术有限公司.WLAN历史概述[PPT].(2025)[2025-09-12]