---
{"dg-publish":true,"dg-path":"网络/网络实验案例/009-DHCP配置案例.md","permalink":"/网络/网络实验案例/009-DHCP配置案例/"}
---

# 实验拓扑
<style> .container {font-family: sans-serif; text-align: center;} .button-wrapper button {z-index: 1;height: 40px; width: 100px; margin: 10px;padding: 5px;} .excalidraw .App-menu_top .buttonList { display: flex;} .excalidraw-wrapper { height: 800px; margin: 50px; position: relative;} :root[dir="ltr"] .excalidraw .layer-ui__wrapper .zen-mode-transition.App-menu_bottom--transition-left {transform: none;} </style><script src="https://cdn.jsdelivr.net/npm/react@17/umd/react.production.min.js"></script><script src="https://cdn.jsdelivr.net/npm/react-dom@17/umd/react-dom.production.min.js"></script><script type="text/javascript" src="https://cdn.jsdelivr.net/npm/@excalidraw/excalidraw@0/dist/excalidraw.production.min.js"></script><div id="excalidraw-009-DHCP配置案例-1excalidraw.md1"></div><script>(function(){const InitialData={"type":"excalidraw","version":2,"source":"https://github.com/zsviczian/obsidian-excalidraw-plugin/releases/tag/2.15.3","elements":[{"id":"xm4grVKm5LuIeccNWjTZZ","type":"line","x":-105.19672789900716,"y":37.426687392850795,"width":262.5040568808791,"height":293.86817796275034,"angle":0,"strokeColor":"#1e1e1e","backgroundColor":"transparent","fillStyle":"solid","strokeWidth":4,"strokeStyle":"solid","roughness":0,"opacity":100,"groupIds":[],"frameId":null,"index":"Zx","roundness":null,"seed":126194308,"version":64,"versionNonce":1522242052,"isDeleted":false,"boundElements":null,"updated":1758897294304,"link":null,"locked":false,"points":[[0,0],[262.5040568808791,293.86817796275034]],"lastCommittedPoint":null,"startBinding":null,"endBinding":null,"startArrowhead":null,"endArrowhead":null,"polygon":false},{"id":"wTRRAhVXWRmvzfnsZE_K-","type":"line","x":-102.46941302232267,"y":38.79034483119301,"width":195.00301368293873,"height":268.6405153534191,"angle":0,"strokeColor":"#1e1e1e","backgroundColor":"transparent","fillStyle":"solid","strokeWidth":4,"strokeStyle":"solid","roughness":0,"opacity":100,"groupIds":[],"frameId":null,"index":"Zy","roundness":null,"seed":6937860,"version":81,"versionNonce":1362994052,"isDeleted":false,"boundElements":null,"updated":1758897283858,"link":null,"locked":false,"points":[[0,0],[-195.00301368293873,268.6405153534191]],"lastCommittedPoint":null,"startBinding":null,"endBinding":null,"startArrowhead":null,"endArrowhead":null,"polygon":false},{"id":"dgBnO6ubLONsftpL-r8hi","type":"line","x":-107.92404277569159,"y":-259.8506341657551,"width":2.7273148766844315,"height":298.6409789969481,"angle":0,"strokeColor":"#1e1e1e","backgroundColor":"transparent","fillStyle":"solid","strokeWidth":4,"strokeStyle":"solid","roughness":0,"opacity":100,"groupIds":[],"frameId":null,"index":"Zz","roundness":null,"seed":617904516,"version":46,"versionNonce":981609860,"isDeleted":false,"boundElements":null,"updated":1758897259033,"link":null,"locked":false,"points":[[0,0],[2.7273148766844315,298.6409789969481]],"lastCommittedPoint":null,"startBinding":null,"endBinding":null,"startArrowhead":null,"endArrowhead":null,"polygon":false},{"id":"9Tko7dUr","type":"image","x":103.11915716660923,"y":287.1843939619149,"width":108,"height":89,"angle":0,"strokeColor":"transparent","backgroundColor":"transparent","fillStyle":"hachure","strokeWidth":1,"strokeStyle":"solid","roughness":1,"opacity":100,"roundness":null,"seed":22661,"version":161,"versionNonce":848783492,"updated":1758897217358,"isDeleted":false,"groupIds":[],"boundElements":[],"link":null,"locked":false,"frameId":null,"fileId":"65646de17f2b9d455b81072e794fdd6eaa588560","scale":[1,1],"crop":null,"index":"a0","status":"pending"},{"id":"KpqJilpy","type":"text","x":129.61915716660923,"y":380.1843939619149,"width":56.16796875,"height":35,"angle":0,"strokeColor":"#1e1e1e","backgroundColor":"transparent","fillStyle":"solid","strokeWidth":4,"strokeStyle":"solid","roughness":0,"opacity":100,"groupIds":[],"frameId":null,"index":"a2","roundness":null,"seed":2046689028,"version":106,"versionNonce":1478473732,"isDeleted":false,"boundElements":[],"updated":1758897217358,"link":null,"locked":false,"text":"AR1","rawText":"AR1","fontSize":28,"fontFamily":6,"textAlign":"left","verticalAlign":"top","containerId":null,"originalText":"AR1","autoResize":true,"lineHeight":1.25},{"id":"5ICL1BoJ","type":"text","x":-166.37478802370953,"y":-184.61279656510362,"width":120.79989624023438,"height":25,"angle":0,"strokeColor":"#1e1e1e","backgroundColor":"transparent","fillStyle":"solid","strokeWidth":4,"strokeStyle":"solid","roughness":0,"opacity":100,"groupIds":[],"frameId":null,"index":"a7","roundness":null,"seed":597827972,"version":274,"versionNonce":1402459012,"isDeleted":false,"boundElements":[],"updated":1758897190841,"link":null,"locked":false,"text":"DHCP Server","rawText":"DHCP Server","fontSize":20,"fontFamily":6,"textAlign":"left","verticalAlign":"top","containerId":null,"originalText":"DHCP Server","autoResize":true,"lineHeight":1.25},{"id":"pw07C4cG","type":"image","x":-160.09737718269628,"y":-303.10547199722464,"width":108,"height":89,"angle":0,"strokeColor":"transparent","backgroundColor":"transparent","fillStyle":"hachure","strokeWidth":1,"strokeStyle":"solid","roughness":1,"opacity":100,"roundness":null,"seed":51248,"version":53,"versionNonce":137450628,"updated":1758897168724,"isDeleted":false,"groupIds":[],"boundElements":[],"link":null,"locked":false,"frameId":null,"fileId":"805d1e1650d1576de888983f84d258dd11815cea","scale":[1,1],"crop":null,"index":"a8"},{"id":"nwX1rbpk","type":"text","x":-145.42462233010298,"y":-213.03165150875043,"width":79.5479736328125,"height":35,"angle":0,"strokeColor":"#1e1e1e","backgroundColor":"transparent","fillStyle":"solid","strokeWidth":4,"strokeStyle":"solid","roughness":0,"opacity":100,"groupIds":[],"frameId":null,"index":"a9","roundness":null,"seed":1770285956,"version":28,"versionNonce":1563511996,"isDeleted":false,"boundElements":null,"updated":1758897187908,"link":null,"locked":false,"text":"LSW1","rawText":"LSW1","fontSize":28,"fontFamily":6,"textAlign":"left","verticalAlign":"top","containerId":null,"originalText":"LSW1","autoResize":true,"lineHeight":1.25},{"id":"Pry46DGl","type":"image","x":-158.37936799435414,"y":-4.846693195758348,"width":109,"height":89,"angle":0,"strokeColor":"transparent","backgroundColor":"transparent","fillStyle":"hachure","strokeWidth":1,"strokeStyle":"solid","roughness":1,"opacity":100,"roundness":null,"seed":21614,"version":82,"versionNonce":1328731324,"updated":1758897219775,"isDeleted":false,"groupIds":[],"boundElements":[],"link":null,"locked":false,"frameId":null,"fileId":"bc6f0c239a8ab1242ddc00f300414adaea6269b8","scale":[1,1],"crop":null,"index":"aA"},{"id":"gyUoZIeC","type":"image","x":-383.3828453208219,"y":301.97623043124315,"width":111.27705579178685,"height":85.63495163107075,"angle":0,"strokeColor":"transparent","backgroundColor":"transparent","fillStyle":"hachure","strokeWidth":1,"strokeStyle":"solid","roughness":1,"opacity":100,"roundness":null,"seed":55333,"version":196,"versionNonce":1728911364,"updated":1758897273374,"isDeleted":false,"groupIds":[],"boundElements":[],"link":null,"locked":false,"frameId":null,"fileId":"d66aa843651f0fd19b005987f0ee56baa2792171","scale":[1,1],"crop":null,"index":"aB"},{"id":"cdGwWkcH","type":"text","x":-143.3791361725896,"y":85.83652645400002,"width":79.5479736328125,"height":35,"angle":0,"strokeColor":"#1e1e1e","backgroundColor":"transparent","fillStyle":"solid","strokeWidth":4,"strokeStyle":"solid","roughness":0,"opacity":100,"groupIds":[],"frameId":null,"index":"aC","roundness":null,"seed":1109796612,"version":33,"versionNonce":485098428,"isDeleted":false,"boundElements":null,"updated":1758897242474,"link":null,"locked":false,"text":"LSW2","rawText":"LSW2","fontSize":28,"fontFamily":6,"textAlign":"left","verticalAlign":"top","containerId":null,"originalText":"LSW2","autoResize":true,"lineHeight":1.25},{"id":"EOIeJYk6","type":"text","x":-354.0642103964639,"y":389.25030648514576,"width":53.33998107910156,"height":35,"angle":0,"strokeColor":"#1e1e1e","backgroundColor":"transparent","fillStyle":"solid","strokeWidth":4,"strokeStyle":"solid","roughness":0,"opacity":100,"groupIds":[],"frameId":null,"index":"aD","roundness":null,"seed":1463897404,"version":20,"versionNonce":172640900,"isDeleted":false,"boundElements":null,"updated":1758897248491,"link":null,"locked":false,"text":"PC1","rawText":"PC1","fontSize":28,"fontFamily":6,"textAlign":"left","verticalAlign":"top","containerId":null,"originalText":"PC1","autoResize":true,"lineHeight":1.25},{"id":"ONxqeIYe","type":"text","x":-103.15124174149383,"y":-158.71278476262796,"width":103.77995300292969,"height":25,"angle":0,"strokeColor":"#1e1e1e","backgroundColor":"transparent","fillStyle":"solid","strokeWidth":4,"strokeStyle":"solid","roughness":0,"opacity":100,"groupIds":[],"frameId":null,"index":"aE","roundness":null,"seed":747668540,"version":42,"versionNonce":991804860,"isDeleted":false,"boundElements":null,"updated":1758897329358,"link":null,"locked":false,"text":"10.1.1.1/24","rawText":"10.1.1.1/24","fontSize":20,"fontFamily":6,"textAlign":"left","verticalAlign":"top","containerId":null,"originalText":"10.1.1.1/24","autoResize":true,"lineHeight":1.25},{"id":"1up69BKT","type":"text","x":-189.06166035705422,"y":-158.9399837284302,"width":73.89994812011719,"height":25,"angle":0,"strokeColor":"#1e1e1e","backgroundColor":"transparent","fillStyle":"solid","strokeWidth":4,"strokeStyle":"solid","roughness":0,"opacity":100,"groupIds":[],"frameId":null,"index":"aF","roundness":null,"seed":43814148,"version":20,"versionNonce":1100693308,"isDeleted":false,"boundElements":null,"updated":1758897327208,"link":null,"locked":false,"text":"GE0/0/1","rawText":"GE0/0/1","fontSize":20,"fontFamily":6,"textAlign":"left","verticalAlign":"top","containerId":null,"originalText":"GE0/0/1","autoResize":true,"lineHeight":1.25},{"id":"0JMmipxY","type":"text","x":-157.69753927518298,"y":-31.438013243431726,"width":125.21987915039062,"height":25,"angle":0,"strokeColor":"#1e1e1e","backgroundColor":"transparent","fillStyle":"solid","strokeWidth":4,"strokeStyle":"solid","roughness":0,"opacity":100,"groupIds":[],"frameId":null,"index":"aG","roundness":null,"seed":1106708868,"version":43,"versionNonce":802209340,"isDeleted":false,"boundElements":null,"updated":1758897344608,"link":null,"locked":false,"text":"Ethernet0/0/1","rawText":"Ethernet0/0/1","fontSize":20,"fontFamily":6,"textAlign":"left","verticalAlign":"top","containerId":null,"originalText":"Ethernet0/0/1","autoResize":true,"lineHeight":1.25},{"id":"NHwUzDjY","type":"text","x":-334.85470367112555,"y":268.3395401369386,"width":125.21987915039062,"height":25,"angle":0,"strokeColor":"#1e1e1e","backgroundColor":"transparent","fillStyle":"solid","strokeWidth":4,"strokeStyle":"solid","roughness":0,"opacity":100,"groupIds":[],"frameId":null,"index":"aH","roundness":null,"seed":254427780,"version":52,"versionNonce":714899076,"isDeleted":false,"boundElements":[],"updated":1758897346807,"link":null,"locked":false,"text":"Ethernet0/0/1","rawText":"Ethernet0/0/1","fontSize":20,"fontFamily":6,"textAlign":"left","verticalAlign":"top","containerId":null,"originalText":"Ethernet0/0/1","autoResize":true,"lineHeight":1.25},{"id":"u4djKkYe","type":"text","x":-286.56316719852356,"y":91.29115620736889,"width":125.21987915039062,"height":25,"angle":0,"strokeColor":"#1e1e1e","backgroundColor":"transparent","fillStyle":"solid","strokeWidth":4,"strokeStyle":"solid","roughness":0,"opacity":100,"groupIds":[],"frameId":null,"index":"aI","roundness":null,"seed":1512135940,"version":32,"versionNonce":700577084,"isDeleted":false,"boundElements":null,"updated":1758897356324,"link":null,"locked":false,"text":"Ethernet0/0/2","rawText":"Ethernet0/0/2","fontSize":20,"fontFamily":6,"textAlign":"left","verticalAlign":"top","containerId":null,"originalText":"Ethernet0/0/2","autoResize":true,"lineHeight":1.25},{"id":"IHbQC9Xm","type":"text","x":-44.51397189277793,"y":83.79104029648659,"width":125.21987915039062,"height":25,"angle":0,"strokeColor":"#1e1e1e","backgroundColor":"transparent","fillStyle":"solid","strokeWidth":4,"strokeStyle":"solid","roughness":0,"opacity":100,"groupIds":[],"frameId":null,"index":"aJ","roundness":null,"seed":2096216964,"version":33,"versionNonce":1530365756,"isDeleted":false,"boundElements":null,"updated":1758897364875,"link":null,"locked":false,"text":"Ethernet0/0/3","rawText":"Ethernet0/0/3","fontSize":20,"fontFamily":6,"textAlign":"left","verticalAlign":"top","containerId":null,"originalText":"Ethernet0/0/3","autoResize":true,"lineHeight":1.25},{"id":"65rrXzzJ","type":"text","x":75.4878826813383,"y":258.3391924042919,"width":73.89994812011719,"height":25,"angle":0,"strokeColor":"#1e1e1e","backgroundColor":"transparent","fillStyle":"solid","strokeWidth":4,"strokeStyle":"solid","roughness":0,"opacity":100,"groupIds":[],"frameId":null,"index":"aK","roundness":null,"seed":914587836,"version":54,"versionNonce":886758532,"isDeleted":false,"boundElements":null,"updated":1758897378924,"link":null,"locked":false,"text":"GE0/0/0","rawText":"GE0/0/0","fontSize":20,"fontFamily":6,"textAlign":"left","verticalAlign":"top","containerId":null,"originalText":"GE0/0/0","autoResize":true,"lineHeight":1.25},{"id":"QUyA4cjK","type":"text","x":-392.2466186700463,"y":415.8416265328194,"width":115.21990966796875,"height":25,"angle":0,"strokeColor":"#1e1e1e","backgroundColor":"transparent","fillStyle":"solid","strokeWidth":4,"strokeStyle":"solid","roughness":0,"opacity":100,"groupIds":[],"frameId":null,"index":"aL","roundness":null,"seed":324303620,"version":61,"versionNonce":1695269052,"isDeleted":false,"boundElements":null,"updated":1758897407758,"link":null,"locked":false,"text":"DHCP Client","rawText":"DHCP Client","fontSize":20,"fontFamily":6,"textAlign":"left","verticalAlign":"top","containerId":null,"originalText":"DHCP Client","autoResize":true,"lineHeight":1.25},{"id":"antvouZ7","type":"text","x":94.92457311368969,"y":408.79625628618817,"width":115.21990966796875,"height":25,"angle":0,"strokeColor":"#1e1e1e","backgroundColor":"transparent","fillStyle":"solid","strokeWidth":4,"strokeStyle":"solid","roughness":0,"opacity":100,"groupIds":[],"frameId":null,"index":"aM","roundness":null,"seed":37439492,"version":69,"versionNonce":700527748,"isDeleted":false,"boundElements":[],"updated":1758897411025,"link":null,"locked":false,"text":"DHCP Client","rawText":"DHCP Client","fontSize":20,"fontFamily":6,"textAlign":"left","verticalAlign":"top","containerId":null,"originalText":"DHCP Client","autoResize":true,"lineHeight":1.25}],"appState":{"theme":"light","viewBackgroundColor":"#ffffff","currentItemStrokeColor":"#1e1e1e","currentItemBackgroundColor":"transparent","currentItemFillStyle":"solid","currentItemStrokeWidth":4,"currentItemStrokeStyle":"solid","currentItemRoughness":0,"currentItemOpacity":100,"currentItemFontFamily":6,"currentItemFontSize":20,"currentItemTextAlign":"left","currentItemStartArrowhead":null,"currentItemEndArrowhead":"arrow","currentItemArrowType":"round","currentItemFrameRole":null,"scrollX":596.7952344213807,"scrollY":494.740627920204,"zoom":{"value":1},"currentItemRoundness":"sharp","gridSize":20,"gridStep":5,"gridModeEnabled":false,"gridColor":{"Bold":"rgba(217, 217, 217, 0.5)","Regular":"rgba(230, 230, 230, 0.5)"},"currentStrokeOptions":null,"frameRendering":{"enabled":true,"clip":true,"name":true,"outline":true,"markerName":true,"markerEnabled":true},"objectsSnapModeEnabled":false,"activeTool":{"type":"selection","customType":null,"locked":false,"fromSelection":false,"lastActiveTool":null}},"files":{}};InitialData.scrollToContent=true;App=()=>{const e=React.useRef(null),t=React.useRef(null),[n,i]=React.useState({width:void 0,height:void 0});return React.useEffect(()=>{i({width:t.current.getBoundingClientRect().width,height:t.current.getBoundingClientRect().height});const e=()=>{i({width:t.current.getBoundingClientRect().width,height:t.current.getBoundingClientRect().height})};return window.addEventListener("resize",e),()=>window.removeEventListener("resize",e)},[t]),React.createElement(React.Fragment,null,React.createElement("div",{className:"excalidraw-wrapper",ref:t},React.createElement(ExcalidrawLib.Excalidraw,{ref:e,width:n.width,height:n.height,initialData:InitialData,viewModeEnabled:!0,zenModeEnabled:!0,gridModeEnabled:!1})))},excalidrawWrapper=document.getElementById("excalidraw-009-DHCP配置案例-1excalidraw.md1");ReactDOM.render(React.createElement(App),excalidrawWrapper);})();</script>
# 实验需求
以LSW1为DHCP Server，以AR1和PC1为DHCP Client，自动分配IP地址，网关为10.1.1.1/24，分配10.1.1.0网段，DNS设置为8.8.8.8，地址租期为3天。注：PC1的MAC地址为54-89-98-F8-05-26
# 实验解析
## 第一种方法：基于接口地址池
1. 设备命名略
2. LSW2配置VLAN都能通过：
```
[LSW2]vlan 10
[LSW2-vlan10]quit
[LSW2]port-group group-member e0/0/1 to e0/0/3
[LSW2-port-group]port link-type trunk
[LSW2-Ethernet0/0/1]port link-type trunk
[LSW2-Ethernet0/0/2]port link-type trunk
[LSW2-Ethernet0/0/3]port link-type trunk
[LSW2-port-group]port trunk allow-pass vlan all
[LSW2-Ethernet0/0/1]port trunk allow-pass vlan all
[LSW2-Ethernet0/0/2]port trunk allow-pass vlan all
[LSW2-Ethernet0/0/3]port trunk allow-pass vlan all
```
3. LSW1使能DHCP：
```
[LSW1]dhcp enable
Info: The operation may take a few seconds. Please wait for a moment.done.
```
4. LSW1建立VLAN：
```
[LSW1]vlan 10
[LSW1-vlan10]quit
```
5. LSW1配置DHCP：
```
[LSW1]int vlanif 10
[LSW1-Vlanif10]ip add 10.1.1.1 24
[LSW1-Vlanif10]dhcp select interface     #使能接口采用接口地址池的DHCP服务器功能，缺省未使能
[LSW1-Vlanif10]dhcp server excluded-ip-address 10.1.1.2 10.1.1.10     #排除地址
[LSW1-Vlanif10]dhcp server dns-list 8.8.8.8     #配置DNS
[LSW1-Vlanif10]dhcp server lease day 3 hour 0 minute 0     #配置DHCP租期
[LSW1-Vlanif10]dhcp server static-bind ip-address 10.1.1.11 mac-address 5489-98f8-0526                             #为PC1分配固定的IP地址
[LSW1-Vlanif10]dhcp server domain-name huawei.com   #分配域名
```
6. LSW1将VLANIF10绑定GE0/0/1
```
[LSW1-Vlanif10]int g0/0/1
[LSW1-GigabitEthernet0/0/1]port link-type access
[LSW1-GigabitEthernet0/0/1]port default vlan 10
[LSW1-GigabitEthernet0/0/1]quit
```
7. 将PC1设为DHCP自动获取地址后，查询PC的IP地址：
```
PC>ipconfig

Link local IPv6 address...........: fe80::5689:98ff:fef8:526
IPv6 address......................: :: / 128
IPv6 gateway......................: ::
IPv4 address......................: 10.1.1.11
Subnet mask.......................: 255.255.255.0
Gateway...........................: 10.1.1.1
Physical address..................: 54-89-98-F8-05-26
DNS server........................: 8.8.8.8
```
8. 在AR1上获取IP地址： 
```
[AR1]dhcp enable
Info: The operation may take a few seconds. Please wait for a moment.done.
[AR1]int g0/0/0
[AR1-GigabitEthernet0/0/0]ip address dhcp-alloc
Sep 26 2025 22:27:43-08:00 AR1 %%01IFNET/4/LINK_STATE(l)[0]:The line protocol IP on the interface GigabitEthernet0/0/0 has entered the UP state. 
```
9. 在AR1上查询IP地址获取情况，已获取10.1.1.254/24：
```
[AR1-GigabitEthernet0/0/0]display ip interface brief
*down: administratively down
^down: standby
(l): loopback
(s): spoofing
The number of interface that is UP in Physical is 2
The number of interface that is DOWN in Physical is 2
The number of interface that is UP in Protocol is 2
The number of interface that is DOWN in Protocol is 2

Interface                         IP Address/Mask      Physical   Protocol  
GigabitEthernet0/0/0              10.1.1.254/24        up         up        
GigabitEthernet0/0/1              unassigned           down       down      
GigabitEthernet0/0/2              unassigned           down       down      
NULL0                             unassigned           up         up(s)
```
10. 在LSW1上查询IP地址池使用情况：
```
[LSW1]display ip pool interface vlanif10 
  Pool-name      : vlanif10
  Pool-No        : 0
  Lease          : 3 Days 0 Hours 0 Minutes
  Domain-name    : huawei.com
  DNS-server0    : 8.8.8.8         
  NBNS-server0   : -               
  Netbios-type   : -               
  Position       : Interface       Status           : Unlocked
  Gateway-0      : 10.1.1.1        
  Mask           : 255.255.255.0
  VPN instance   : --
 -----------------------------------------------------------------------------
         Start           End     Total  Used  Idle(Expired)  Conflict  Disable
 -----------------------------------------------------------------------------
        10.1.1.1      10.1.1.254   253     2        242(0)         0        9
 -----------------------------------------------------------------------------
```
## 第二种方法：基于全局地址池
1. 设备命名略
2. LSW2配置VLAN都能通过：
```
[LSW2]vlan 10
[LSW2-vlan10]quit
[LSW2]port-group group-member e0/0/1 to e0/0/3
[LSW2-port-group]port link-type trunk
[LSW2-Ethernet0/0/1]port link-type trunk
[LSW2-Ethernet0/0/2]port link-type trunk
[LSW2-Ethernet0/0/3]port link-type trunk
[LSW2-port-group]port trunk allow-pass vlan all
[LSW2-Ethernet0/0/1]port trunk allow-pass vlan all
[LSW2-Ethernet0/0/2]port trunk allow-pass vlan all
[LSW2-Ethernet0/0/3]port trunk allow-pass vlan all
```
3. LSW1使能DHCP：
```
[LSW1]dhcp enable
Info: The operation may take a few seconds. Please wait for a moment.done.
```
4. LSW1配置VLAN和VLANIF：
```
[LSW1]vlan 10
[LSW1-vlan10]quit
[LSW1]int g0/0/1
[LSW1-GigabitEthernet0/0/1]port link-type access
[LSW1-GigabitEthernet0/0/1]port default vlan 10
[LSW1-GigabitEthernet0/0/1]int vlanif 10
[LSW1-Vlanif10]ip add 10.1.1.1 24
[LSW1-Vlanif10]quit
```
5. LSW1配置全局地址池：
```
[LSW1]ip pool pool1
Info:It's successful to create an IP address pool.
[LSW1-ip-pool-pool1]network 10.1.1.0 mask 255.255.255.0       #配置地址范围
[LSW1-ip-pool-pool1]dns-list 8.8.8.8           #配置DNS
[LSW1-ip-pool-pool1]gateway-list 10.1.1.1              #设置网关
[LSW1-ip-pool-pool1]excluded-ip-address 10.1.1.2 10.1.1.10       #排除地址
[LSW1-ip-pool-pool1]lease day 3 hour 0 minute 0      #配置DHCP租期
[LSW1-ip-pool-pool1]quit
```
6. 应用全局地址池：
```
[LSW1]int vlanif 10
[LSW1-Vlanif10]dhcp select global
```
7. 将PC1设为DHCP自动获取地址后，查询PC的IP地址：
```
PC>ipconfig

Link local IPv6 address...........: fe80::5689:98ff:fef8:526
IPv6 address......................: :: / 128
IPv6 gateway......................: ::
IPv4 address......................: 10.1.1.254
Subnet mask.......................: 255.255.255.0
Gateway...........................: 10.1.1.1
Physical address..................: 54-89-98-F8-05-26
DNS server........................: 8.8.8.8
```
8. 在AR1上获取IP地址：
```
[AR1]dhcp enable
Info: The operation may take a few seconds. Please wait for a moment.done.
[AR1]int g0/0/0
[AR1-GigabitEthernet0/0/0]ip address dhcp-alloc
```
9. 在AR1上查询IP地址获取情况，已获取10.1.1.253/24：
```
[AR1]display ip interface brief
*down: administratively down
^down: standby
(l): loopback
(s): spoofing
The number of interface that is UP in Physical is 2
The number of interface that is DOWN in Physical is 2
The number of interface that is UP in Protocol is 2
The number of interface that is DOWN in Protocol is 2

Interface                         IP Address/Mask      Physical   Protocol  
GigabitEthernet0/0/0              10.1.1.253/24        up         up        
GigabitEthernet0/0/1              unassigned           down       down      
GigabitEthernet0/0/2              unassigned           down       down      
NULL0                             unassigned           up         up(s)
```
10. 在LSW1上查询IP地址池使用情况：
```
[LSW1]display ip pool name pool1 
  Pool-name      : pool1
  Pool-No        : 0
  Lease          : 3 Days 0 Hours 0 Minutes
  Domain-name    : -
  DNS-server0    : 8.8.8.8         
  NBNS-server0   : -               
  Netbios-type   : -               
  Position       : Local           Status           : Unlocked
  Gateway-0      : 10.1.1.1        
  Mask           : 255.255.255.0
  VPN instance   : --
 -----------------------------------------------------------------------------
         Start           End     Total  Used  Idle(Expired)  Conflict  Disable
 -----------------------------------------------------------------------------
        10.1.1.1      10.1.1.254   253     2        251(0)         0        0
 -----------------------------------------------------------------------------
```