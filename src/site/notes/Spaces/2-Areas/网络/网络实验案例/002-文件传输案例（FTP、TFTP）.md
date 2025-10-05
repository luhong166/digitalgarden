---
{"dg-publish":true,"dg-path":"网络/网络实验案例/002-文件传输案例（FTP、TFTP）.md","permalink":"/网络/网络实验案例/002-文件传输案例（FTP、TFTP）/"}
---

# 一、FTP
FTP（File Transfer Protocol）是一个用于从一台主机传送文件到另一台主机的协议，用于文件的“下载”和“上传”，它采用C/S（Client/Server）结构。

**FTP使用端口号：**
- **使用TCP的20端口于数据传输**
- **使用TCP的21端口于程序连接**

下载：

<font class="code">[Huawei-ftp] **get** *source-filename destination-filename*</font>

上传：

<font class="code">[Huawei-ftp] **put** *source-filename destination-filename*</font>

## 实验拓扑
<style> .container {font-family: sans-serif; text-align: center;} .button-wrapper button {z-index: 1;height: 40px; width: 100px; margin: 10px;padding: 5px;} .excalidraw .App-menu_top .buttonList { display: flex;} .excalidraw-wrapper { height: 800px; margin: 50px; position: relative;} :root[dir="ltr"] .excalidraw .layer-ui__wrapper .zen-mode-transition.App-menu_bottom--transition-left {transform: none;} </style><script src="https://cdn.jsdelivr.net/npm/react@17/umd/react.production.min.js"></script><script src="https://cdn.jsdelivr.net/npm/react-dom@17/umd/react-dom.production.min.js"></script><script type="text/javascript" src="https://cdn.jsdelivr.net/npm/@excalidraw/excalidraw@0/dist/excalidraw.production.min.js"></script><div id="excalidraw-001-远程登录案例&002-文件传输案例（FTP、TFTP）-1excalidraw.md1"></div><script>(function(){const InitialData={"type":"excalidraw","version":2,"source":"https://github.com/zsviczian/obsidian-excalidraw-plugin/releases/tag/2.15.3","elements":[{"id":"KV3t_WM5CdFJEr0Dqdy66","type":"line","x":-211.50003390402821,"y":-17.48036095876833,"width":356.13189072661714,"height":2.811959928262155,"angle":0,"strokeColor":"#1e1e1e","backgroundColor":"transparent","fillStyle":"solid","strokeWidth":2,"strokeStyle":"solid","roughness":1,"opacity":100,"groupIds":[],"frameId":null,"index":"Zz","roundness":{"type":2},"seed":808637997,"version":124,"versionNonce":477571013,"isDeleted":false,"boundElements":[],"updated":1758350902281,"link":null,"locked":false,"points":[[0,0],[356.13189072661714,-2.811959928262155]],"lastCommittedPoint":null,"startBinding":null,"endBinding":null,"startArrowhead":null,"endArrowhead":null,"polygon":false},{"id":"DgB6ShynldpLL494wdK-H","type":"image","x":-246.5,"y":-47,"width":70,"height":57.68518518518518,"angle":0,"strokeColor":"transparent","backgroundColor":"transparent","fillStyle":"solid","strokeWidth":2,"strokeStyle":"solid","roughness":1,"opacity":100,"groupIds":[],"frameId":null,"index":"a0","roundness":null,"seed":219638275,"version":108,"versionNonce":1987715075,"isDeleted":false,"boundElements":[],"updated":1758259122830,"link":null,"locked":false,"status":"pending","fileId":"6c703edecb4ca756d27f7772455f0ed845f19131","scale":[1,1],"crop":null},{"id":"ukeQ__NKqGDFoa1KGhwGi","type":"image","x":110.25,"y":-49.717592592592595,"width":70,"height":57.68518518518518,"angle":0,"strokeColor":"transparent","backgroundColor":"transparent","fillStyle":"solid","strokeWidth":2,"strokeStyle":"solid","roughness":1,"opacity":100,"groupIds":[],"frameId":null,"index":"a2","roundness":null,"seed":240194723,"version":239,"versionNonce":374709955,"isDeleted":false,"boundElements":[],"updated":1758259164480,"link":null,"locked":false,"status":"pending","fileId":"6c703edecb4ca756d27f7772455f0ed845f19131","scale":[1,1],"crop":null},{"id":"0hp4FrO9","type":"text","x":-173.33491914161448,"y":-48.92454675250394,"width":73.97996520996094,"height":25,"angle":0,"strokeColor":"#1e1e1e","backgroundColor":"transparent","fillStyle":"solid","strokeWidth":2,"strokeStyle":"solid","roughness":1,"opacity":100,"groupIds":[],"frameId":null,"index":"a5","roundness":null,"seed":1678972045,"version":69,"versionNonce":956479821,"isDeleted":false,"boundElements":[],"updated":1758259249964,"link":null,"locked":false,"text":"10.1.1.1","rawText":"10.1.1.1","fontSize":20,"fontFamily":6,"textAlign":"left","verticalAlign":"top","containerId":null,"originalText":"10.1.1.1","autoResize":true,"lineHeight":1.25},{"id":"9j1qhVFc","type":"text","x":32.66508085838552,"y":-48.42454675250394,"width":73.97996520996094,"height":25,"angle":0,"strokeColor":"#1e1e1e","backgroundColor":"transparent","fillStyle":"solid","strokeWidth":2,"strokeStyle":"solid","roughness":1,"opacity":100,"groupIds":[],"frameId":null,"index":"a6","roundness":null,"seed":1464537837,"version":21,"versionNonce":1378114179,"isDeleted":false,"boundElements":[],"updated":1758259247630,"link":null,"locked":false,"text":"10.1.1.2","rawText":"10.1.1.2","fontSize":20,"fontFamily":6,"textAlign":"left","verticalAlign":"top","containerId":null,"originalText":"10.1.1.2","autoResize":true,"lineHeight":1.25},{"id":"sNfT33In","type":"text","x":-172.83491914161448,"y":-18.424546752503943,"width":73.89994812011719,"height":25,"angle":0,"strokeColor":"#1e1e1e","backgroundColor":"transparent","fillStyle":"solid","strokeWidth":2,"strokeStyle":"solid","roughness":1,"opacity":100,"groupIds":[],"frameId":null,"index":"a7","roundness":null,"seed":138053859,"version":51,"versionNonce":1570344355,"isDeleted":false,"boundElements":[],"updated":1758259469482,"link":null,"locked":false,"text":"GE0/0/0","rawText":"GE0/0/0","fontSize":20,"fontFamily":6,"textAlign":"left","verticalAlign":"top","containerId":null,"originalText":"GE0/0/0","autoResize":true,"lineHeight":1.25},{"id":"4S4rW2Cx","type":"text","x":34.9650991689324,"y":-17.924546752503943,"width":73.89994812011719,"height":25,"angle":0,"strokeColor":"#1e1e1e","backgroundColor":"transparent","fillStyle":"solid","strokeWidth":2,"strokeStyle":"solid","roughness":1,"opacity":100,"groupIds":[],"frameId":null,"index":"a8","roundness":null,"seed":1320930413,"version":97,"versionNonce":564951171,"isDeleted":false,"boundElements":[],"updated":1758259460817,"link":null,"locked":false,"text":"GE0/0/0","rawText":"GE0/0/0","fontSize":20,"fontFamily":6,"textAlign":"left","verticalAlign":"top","containerId":null,"originalText":"GE0/0/0","autoResize":true,"lineHeight":1.25},{"id":"8w28XEu4","type":"text","x":-232.34985368033585,"y":14.441698868348283,"width":40.11997985839844,"height":25,"angle":0,"strokeColor":"#1e1e1e","backgroundColor":"transparent","fillStyle":"solid","strokeWidth":2,"strokeStyle":"solid","roughness":1,"opacity":100,"groupIds":[],"frameId":null,"index":"a9","roundness":null,"seed":1907823715,"version":20,"versionNonce":1392078125,"isDeleted":false,"boundElements":[],"updated":1758259442101,"link":null,"locked":false,"text":"AR1","rawText":"AR1","fontSize":20,"fontFamily":6,"textAlign":"left","verticalAlign":"top","containerId":null,"originalText":"AR1","autoResize":true,"lineHeight":1.25},{"id":"sNNkYZZk","type":"text","x":125.15014631966415,"y":11.941698868348283,"width":40.11997985839844,"height":25,"angle":0,"strokeColor":"#1e1e1e","backgroundColor":"transparent","fillStyle":"solid","strokeWidth":2,"strokeStyle":"solid","roughness":1,"opacity":100,"groupIds":[],"frameId":null,"index":"aA","roundness":null,"seed":1342341197,"version":26,"versionNonce":1017608515,"isDeleted":false,"boundElements":[],"updated":1758259452700,"link":null,"locked":false,"text":"AR2","rawText":"AR2","fontSize":20,"fontFamily":6,"textAlign":"left","verticalAlign":"top","containerId":null,"originalText":"AR2","autoResize":true,"lineHeight":1.25}],"appState":{"theme":"light","viewBackgroundColor":"#ffffff","currentItemStrokeColor":"#1e1e1e","currentItemBackgroundColor":"transparent","currentItemFillStyle":"solid","currentItemStrokeWidth":2,"currentItemStrokeStyle":"solid","currentItemRoughness":1,"currentItemOpacity":100,"currentItemFontFamily":6,"currentItemFontSize":20,"currentItemTextAlign":"left","currentItemStartArrowhead":null,"currentItemEndArrowhead":"arrow","currentItemArrowType":"round","currentItemFrameRole":null,"scrollX":257.730306063296,"scrollY":225.99275474603732,"zoom":{"value":1},"currentItemRoundness":"round","gridSize":20,"gridStep":5,"gridModeEnabled":false,"gridColor":{"Bold":"rgba(217, 217, 217, 0.5)","Regular":"rgba(230, 230, 230, 0.5)"},"currentStrokeOptions":null,"frameRendering":{"enabled":true,"clip":true,"name":true,"outline":true,"markerName":true,"markerEnabled":true},"objectsSnapModeEnabled":false,"activeTool":{"type":"selection","customType":null,"locked":false,"fromSelection":false,"lastActiveTool":null}},"files":{}};InitialData.scrollToContent=true;App=()=>{const e=React.useRef(null),t=React.useRef(null),[n,i]=React.useState({width:void 0,height:void 0});return React.useEffect(()=>{i({width:t.current.getBoundingClientRect().width,height:t.current.getBoundingClientRect().height});const e=()=>{i({width:t.current.getBoundingClientRect().width,height:t.current.getBoundingClientRect().height})};return window.addEventListener("resize",e),()=>window.removeEventListener("resize",e)},[t]),React.createElement(React.Fragment,null,React.createElement("div",{className:"excalidraw-wrapper",ref:t},React.createElement(ExcalidrawLib.Excalidraw,{ref:e,width:n.width,height:n.height,initialData:InitialData,viewModeEnabled:!0,zenModeEnabled:!0,gridModeEnabled:!1})))},excalidrawWrapper=document.getElementById("excalidraw-001-远程登录案例&002-文件传输案例（FTP、TFTP）-1excalidraw.md1");ReactDOM.render(React.createElement(App),excalidrawWrapper);})();</script>
## 实验需求
1. 命名并配置IP地址
2. 在AR1上开启FTP服务，FTP文件夹为`flash:/123`，要有AAA认证，创建用户`admin`，密码`12345`用于身份验证
3. 在AR2通过FTP上传文件statemach.efs，并再次下载为123.efs
## 实验解析
命名AR1：
```
<Huawei>system-view
Enter system view, return user view with Ctrl+Z.
[Huawei]sysname AR1
```
AR1配置IP地址：
```
[AR1]int g0/0/0
[AR1-GigabitEthernet0/0/0]ip add 10.1.1.1 24
Sep 19 2025 21:22:24-08:00 AR1 01IFNET/4/LINK_STATE(l)[0]:The line protocol IP on the interface GigabitEthernet0/0/0 has entered the UP state. 
[AR2-GigabitEthernet0/0/0]return
```
查看AR2此时有哪些文件：
```
<AR2>dir
Directory of flash:/

  Idx  Attr     Size(Byte)  Date        Time(LMT)  FileName 
    0  drw-              -  Sep 19 2025 13:21:12   dhcp
    1  -rw-        121,802  May 26 2014 09:20:58   portalpage.zip
    2  -rw-          2,263  Sep 19 2025 13:21:08   statemach.efs
    3  -rw-        828,482  May 26 2014 09:20:58   sslvpn.zip

1,090,732 KB total (784,460 KB free)
```
AR2 FTP连接AR1：
```
<AR2>ftp 10.1.1.1
Trying 10.1.1.1 ...

Press CTRL+K to abort
Connected to 10.1.1.1.
220 FTP service ready.
User(10.1.1.1:(none)):admin
331 Password required for admin.
Enter password:
230 User logged in.
```
查看此时AR1的FTP文件夹内有哪些文件（文件夹为空）：
```
[AR2-ftp]dir
200 Port command okay.
150 Opening ASCII mode data connection for *.
drwxrwxrwx   1 noone    nogroup         0 Sep 19 13:22 ..
drwxrwxrwx   1 noone    nogroup         0 Sep 19 13:22 .
226 Transfer complete.
FTP: 117 byte(s) received in 0.070 second(s) 1.67Kbyte(s)/sec.
```
AR2上传一个文件到AR1的FTP文件夹：
```
[AR2-ftp]put statemach.efs
200 Port command okay.
150 Opening ASCII mode data connection for statemach.efs.

 100%     
226 Transfer complete.
FTP: 2263 byte(s) sent in 0.180 second(s) 12.57Kbyte(s)/sec.
[AR2-ftp]dir
200 Port command okay.
150 Opening ASCII mode data connection for *.
drwxrwxrwx   1 noone    nogroup         0 Sep 19 13:22 ..
-rwxrwxrwx   1 noone    nogroup      2263 Sep 19 13:34 statemach.efs
drwxrwxrwx   1 noone    nogroup         0 Sep 19 13:34 .
226 Transfer complete.
FTP: 187 byte(s) received in 0.070 second(s) 2.67Kbyte(s)/sec.
```
AR2再将这个文件下载到本地，下载后名称改为123.efs
```
[AR2-ftp]get statemach.efs 123.efs
200 Port command okay.
150 Opening ASCII mode data connection for statemach.efs.
226 Transfer complete.
FTP: 2263 byte(s) received in 0.150 second(s) 15.08Kbyte(s)/sec.
<AR2>dir
Directory of flash:/

  Idx  Attr     Size(Byte)  Date        Time(LMT)  FileName 
    0  drw-              -  Sep 19 2025 13:21:12   dhcp
    1  -rw-        121,802  May 26 2014 09:20:58   portalpage.zip
    2  -rw-          2,263  Sep 19 2025 13:34:43   123.efs
    3  -rw-          2,263  Sep 19 2025 13:21:08   statemach.efs
    4  -rw-        828,482  May 26 2014 09:20:58   sslvpn.zip

1,090,732 KB total (784,460 KB free)
```
# 二、TFTP
TFTP：非重要性的文件传输协议
**使用UDP的69端口。**
<div id="excalidraw-002-文件传输案例（FTP、TFTP）-2excalidraw.md2"></div><script>(function(){const InitialData={"type":"excalidraw","version":2,"source":"https://github.com/zsviczian/obsidian-excalidraw-plugin/releases/tag/2.15.3","elements":[{"id":"flCJbP3wVhTUrzlfOFkOi","type":"line","x":-316.25,"y":-15.875,"width":619.5,"height":4.5,"angle":0,"strokeColor":"#1e1e1e","backgroundColor":"transparent","fillStyle":"solid","strokeWidth":4,"strokeStyle":"solid","roughness":0,"opacity":100,"groupIds":[],"frameId":null,"index":"Zz","roundness":null,"seed":930858697,"version":77,"versionNonce":143996457,"isDeleted":false,"boundElements":null,"updated":1758292282753,"link":null,"locked":false,"points":[[0,0],[619.5,-4.5]],"lastCommittedPoint":null,"startBinding":null,"endBinding":null,"startArrowhead":null,"endArrowhead":null,"polygon":false},{"id":"R7p8oQ6Z9t7wDRHgSzVFo","type":"image","x":-373.5,"y":-60.5,"width":108,"height":89,"angle":0,"strokeColor":"transparent","backgroundColor":"transparent","fillStyle":"solid","strokeWidth":2,"strokeStyle":"solid","roughness":1,"opacity":100,"groupIds":[],"frameId":null,"index":"a0","roundness":null,"seed":1797661671,"version":219,"versionNonce":662889799,"isDeleted":false,"boundElements":null,"updated":1758292271903,"link":null,"locked":false,"status":"pending","fileId":"195e72ac07acb67ddb11666178dca9adcedf5995","scale":[1,1],"crop":null},{"id":"1SVqrxVOqPf-pFbV6TjDX","type":"image","x":252,"y":-64.5,"width":108,"height":89,"angle":0,"strokeColor":"transparent","backgroundColor":"transparent","fillStyle":"solid","strokeWidth":2,"strokeStyle":"solid","roughness":1,"opacity":100,"groupIds":[],"frameId":null,"index":"a2","roundness":null,"seed":1244990729,"version":90,"versionNonce":1909714569,"isDeleted":false,"boundElements":null,"updated":1758292275637,"link":null,"locked":false,"status":"pending","fileId":"6c703edecb4ca756d27f7772455f0ed845f19131","scale":[1,1],"crop":null},{"id":"KxaWwJAf","type":"text","x":-351.75,"y":-99.375,"width":60.47996520996094,"height":35,"angle":0,"strokeColor":"#1e1e1e","backgroundColor":"transparent","fillStyle":"solid","strokeWidth":4,"strokeStyle":"solid","roughness":0,"opacity":100,"groupIds":[],"frameId":null,"index":"a3","roundness":null,"seed":163933319,"version":57,"versionNonce":1112909353,"isDeleted":false,"boundElements":null,"updated":1758292360206,"link":null,"locked":false,"text":"Host","rawText":"Host","fontSize":28,"fontFamily":6,"textAlign":"left","verticalAlign":"top","containerId":null,"originalText":"Host","autoResize":true,"lineHeight":1.25},{"id":"NjAER2Ee","type":"text","x":-361.75,"y":29.625,"width":84,"height":35,"angle":0,"strokeColor":"#1e1e1e","backgroundColor":"transparent","fillStyle":"solid","strokeWidth":4,"strokeStyle":"solid","roughness":0,"opacity":100,"groupIds":[],"frameId":null,"index":"a4","roundness":null,"seed":1534518215,"version":54,"versionNonce":539236201,"isDeleted":false,"boundElements":null,"updated":1758292355540,"link":null,"locked":false,"text":"服务器","rawText":"服务器","fontSize":28,"fontFamily":6,"textAlign":"left","verticalAlign":"top","containerId":null,"originalText":"服务器","autoResize":true,"lineHeight":1.25},{"id":"tyaXfpJI","type":"text","x":210.75,"y":-102.875,"width":179.1158905029297,"height":35,"angle":0,"strokeColor":"#1e1e1e","backgroundColor":"transparent","fillStyle":"solid","strokeWidth":4,"strokeStyle":"solid","roughness":0,"opacity":100,"groupIds":[],"frameId":null,"index":"a5","roundness":null,"seed":447417033,"version":58,"versionNonce":1428519815,"isDeleted":false,"boundElements":null,"updated":1758292379940,"link":null,"locked":false,"text":"Router/Switch","rawText":"Router/Switch","fontSize":28,"fontFamily":6,"textAlign":"left","verticalAlign":"top","containerId":null,"originalText":"Router/Switch","autoResize":true,"lineHeight":1.25},{"id":"JM757iwk","type":"text","x":266.75,"y":27.625,"width":84,"height":35,"angle":0,"strokeColor":"#1e1e1e","backgroundColor":"transparent","fillStyle":"solid","strokeWidth":4,"strokeStyle":"solid","roughness":0,"opacity":100,"groupIds":[],"frameId":null,"index":"a6","roundness":null,"seed":2086332999,"version":37,"versionNonce":1930064905,"isDeleted":false,"boundElements":null,"updated":1758292407591,"link":null,"locked":false,"text":"客户端","rawText":"客户端","fontSize":28,"fontFamily":6,"textAlign":"left","verticalAlign":"top","containerId":null,"originalText":"客户端","autoResize":true,"lineHeight":1.25},{"id":"AwyQOpZJwy61pSu476L-K","type":"image","x":-104.09878048780489,"y":-73.5,"width":178.42195121951224,"height":95.50000000000001,"angle":0,"strokeColor":"transparent","backgroundColor":"transparent","fillStyle":"solid","strokeWidth":4,"strokeStyle":"solid","roughness":0,"opacity":100,"groupIds":[],"frameId":null,"index":"aB","roundness":null,"seed":1173610439,"version":301,"versionNonce":2052165673,"isDeleted":false,"boundElements":null,"updated":1758292557966,"link":null,"locked":false,"status":"pending","fileId":"a7c0aa33232204571a2b69beea6e8157003bc7af","scale":[1,1],"crop":null},{"id":"mEgu8q79","type":"text","x":-67.25,"y":-40.875,"width":104.36398315429688,"height":45,"angle":0,"strokeColor":"#1e1e1e","backgroundColor":"transparent","fillStyle":"solid","strokeWidth":4,"strokeStyle":"solid","roughness":0,"opacity":100,"groupIds":[],"frameId":null,"index":"aE","roundness":null,"seed":46078729,"version":114,"versionNonce":355562537,"isDeleted":false,"boundElements":null,"updated":1758292553982,"link":null,"locked":false,"text":"IP网络","rawText":"IP网络","fontSize":36,"fontFamily":6,"textAlign":"left","verticalAlign":"top","containerId":null,"originalText":"IP网络","autoResize":true,"lineHeight":1.25},{"id":"ux35KOersusEpdyAVX51W","type":"image","x":-105,"y":-60.5,"width":176,"height":89,"angle":0,"strokeColor":"transparent","backgroundColor":"transparent","fillStyle":"solid","strokeWidth":2,"strokeStyle":"solid","roughness":1,"opacity":100,"groupIds":[],"frameId":null,"index":"aC","roundness":null,"seed":1412138729,"version":132,"versionNonce":2058241095,"isDeleted":true,"boundElements":null,"updated":1758292512638,"link":null,"locked":false,"status":"pending","fileId":"17092df89cd25f704190b5a2e5f6555ecdaf5305","scale":[1,1],"crop":null},{"id":"8p5IZphM","type":"text","x":-58.25,"y":48.125,"width":7.3079986572265625,"height":35,"angle":0,"strokeColor":"#1e1e1e","backgroundColor":"transparent","fillStyle":"solid","strokeWidth":4,"strokeStyle":"solid","roughness":0,"opacity":100,"groupIds":[],"frameId":null,"index":"aD","roundness":null,"seed":236463273,"version":5,"versionNonce":24922025,"isDeleted":true,"boundElements":null,"updated":1758292512638,"link":null,"locked":false,"text":"","rawText":"","fontSize":28,"fontFamily":6,"textAlign":"left","verticalAlign":"top","containerId":null,"originalText":"","autoResize":true,"lineHeight":1.25}],"appState":{"theme":"light","viewBackgroundColor":"#ffffff","currentItemStrokeColor":"#1e1e1e","currentItemBackgroundColor":"transparent","currentItemFillStyle":"solid","currentItemStrokeWidth":4,"currentItemStrokeStyle":"solid","currentItemRoughness":0,"currentItemOpacity":100,"currentItemFontFamily":6,"currentItemFontSize":36,"currentItemTextAlign":"left","currentItemStartArrowhead":null,"currentItemEndArrowhead":"arrow","currentItemArrowType":"round","currentItemFrameRole":null,"scrollX":396.75,"scrollY":390.125,"zoom":{"value":1},"currentItemRoundness":"sharp","gridSize":20,"gridStep":5,"gridModeEnabled":false,"gridColor":{"Bold":"rgba(217, 217, 217, 0.5)","Regular":"rgba(230, 230, 230, 0.5)"},"currentStrokeOptions":null,"frameRendering":{"enabled":true,"clip":true,"name":true,"outline":true,"markerName":true,"markerEnabled":true},"objectsSnapModeEnabled":false,"activeTool":{"type":"selection","customType":null,"locked":false,"fromSelection":false,"lastActiveTool":null}},"files":{}};InitialData.scrollToContent=true;App=()=>{const e=React.useRef(null),t=React.useRef(null),[n,i]=React.useState({width:void 0,height:void 0});return React.useEffect(()=>{i({width:t.current.getBoundingClientRect().width,height:t.current.getBoundingClientRect().height});const e=()=>{i({width:t.current.getBoundingClientRect().width,height:t.current.getBoundingClientRect().height})};return window.addEventListener("resize",e),()=>window.removeEventListener("resize",e)},[t]),React.createElement(React.Fragment,null,React.createElement("div",{className:"excalidraw-wrapper",ref:t},React.createElement(ExcalidrawLib.Excalidraw,{ref:e,width:n.width,height:n.height,initialData:InitialData,viewModeEnabled:!0,zenModeEnabled:!0,gridModeEnabled:!1})))},excalidrawWrapper=document.getElementById("excalidraw-002-文件传输案例（FTP、TFTP）-2excalidraw.md2");ReactDOM.render(React.createElement(App),excalidrawWrapper);})();</script>
下载、上传：

<font class="code">\<Huawei\> **tftp** *server-address* { **get** | **put** } *source-filename* *destination-filename*</font>

## 实现eNSP与真机联网
### 实验拓扑
<div id="excalidraw-002-文件传输案例（FTP、TFTP）-3excalidraw.md3"></div><script>(function(){const InitialData={"type":"excalidraw","version":2,"source":"https://github.com/zsviczian/obsidian-excalidraw-plugin/releases/tag/2.15.3","elements":[{"id":"PG-1GhpkDXq4uXG35MDLu","type":"line","x":-229.75,"y":-40.875,"width":397,"height":2.5,"angle":0,"strokeColor":"#1e1e1e","backgroundColor":"transparent","fillStyle":"solid","strokeWidth":2,"strokeStyle":"solid","roughness":1,"opacity":100,"groupIds":[],"frameId":null,"index":"Zz","roundness":{"type":2},"seed":228260265,"version":68,"versionNonce":1422305865,"isDeleted":false,"boundElements":null,"updated":1758293542266,"link":null,"locked":false,"points":[[0,0],[397,-2.5]],"lastCommittedPoint":null,"startBinding":null,"endBinding":null,"startArrowhead":null,"endArrowhead":null,"polygon":false},{"id":"KCA-pXDnGIlGg5mk2fO3i","type":"image","x":-283,"y":-86,"width":108,"height":89,"angle":0,"strokeColor":"transparent","backgroundColor":"transparent","fillStyle":"solid","strokeWidth":2,"strokeStyle":"solid","roughness":1,"opacity":100,"groupIds":[],"frameId":null,"index":"a0","roundness":null,"seed":1300629577,"version":26,"versionNonce":302109191,"isDeleted":false,"boundElements":null,"updated":1758293511126,"link":null,"locked":false,"status":"pending","fileId":"6c703edecb4ca756d27f7772455f0ed845f19131","scale":[1,1],"crop":null},{"id":"MTY7b8xO-Q7xwGCNmSp78","type":"image","x":88,"y":-89.5,"width":154,"height":88,"angle":0,"strokeColor":"transparent","backgroundColor":"transparent","fillStyle":"solid","strokeWidth":2,"strokeStyle":"solid","roughness":1,"opacity":100,"groupIds":[],"frameId":null,"index":"a1","roundness":null,"seed":1212412553,"version":43,"versionNonce":2136285161,"isDeleted":false,"boundElements":null,"updated":1758293528442,"link":null,"locked":false,"status":"pending","fileId":"bcb6299ef5dd11b772f18372f935ff5037837946","scale":[1,1],"crop":null},{"id":"aDT0dPsg","type":"text","x":-248.25,"y":12.125,"width":40.11997985839844,"height":25,"angle":0,"strokeColor":"#1e1e1e","backgroundColor":"transparent","fillStyle":"solid","strokeWidth":2,"strokeStyle":"solid","roughness":1,"opacity":100,"groupIds":[],"frameId":null,"index":"a3","roundness":null,"seed":1186203495,"version":30,"versionNonce":272842953,"isDeleted":false,"boundElements":null,"updated":1758293574959,"link":null,"locked":false,"text":"AR1","rawText":"AR1","fontSize":20,"fontFamily":6,"textAlign":"left","verticalAlign":"top","containerId":null,"originalText":"AR1","autoResize":true,"lineHeight":1.25},{"id":"qSeDXnhP","type":"text","x":128.75,"y":-67.375,"width":72,"height":45,"angle":0,"strokeColor":"#ffffff","backgroundColor":"transparent","fillStyle":"solid","strokeWidth":2,"strokeStyle":"solid","roughness":1,"opacity":100,"groupIds":[],"frameId":null,"index":"a4","roundness":null,"seed":1791835559,"version":56,"versionNonce":1093148137,"isDeleted":false,"boundElements":null,"updated":1758293622326,"link":null,"locked":false,"text":"真机","rawText":"真机","fontSize":36,"fontFamily":6,"textAlign":"left","verticalAlign":"top","containerId":null,"originalText":"真机","autoResize":true,"lineHeight":1.25},{"id":"aMI5CP1b","type":"text","x":-265.25,"y":-111.875,"width":8,"height":25,"angle":0,"strokeColor":"#1e1e1e","backgroundColor":"transparent","fillStyle":"solid","strokeWidth":2,"strokeStyle":"solid","roughness":1,"opacity":100,"groupIds":[],"frameId":null,"index":"a2","roundness":null,"seed":2016277767,"version":9,"versionNonce":1504919047,"isDeleted":true,"boundElements":null,"updated":1758293561484,"link":null,"locked":false,"text":"","rawText":"","fontSize":20,"fontFamily":5,"textAlign":"left","verticalAlign":"top","containerId":null,"originalText":"","autoResize":true,"lineHeight":1.25}],"appState":{"theme":"light","viewBackgroundColor":"#ffffff","currentItemStrokeColor":"#ffffff","currentItemBackgroundColor":"transparent","currentItemFillStyle":"solid","currentItemStrokeWidth":2,"currentItemStrokeStyle":"solid","currentItemRoughness":1,"currentItemOpacity":100,"currentItemFontFamily":6,"currentItemFontSize":36,"currentItemTextAlign":"left","currentItemStartArrowhead":null,"currentItemEndArrowhead":"arrow","currentItemArrowType":"round","currentItemFrameRole":null,"scrollX":396.75,"scrollY":390.125,"zoom":{"value":1},"currentItemRoundness":"round","gridSize":20,"gridStep":5,"gridModeEnabled":false,"gridColor":{"Bold":"rgba(217, 217, 217, 0.5)","Regular":"rgba(230, 230, 230, 0.5)"},"currentStrokeOptions":null,"frameRendering":{"enabled":true,"clip":true,"name":true,"outline":true,"markerName":true,"markerEnabled":true},"objectsSnapModeEnabled":false,"activeTool":{"type":"selection","customType":null,"locked":false,"fromSelection":false,"lastActiveTool":null}},"files":{}};InitialData.scrollToContent=true;App=()=>{const e=React.useRef(null),t=React.useRef(null),[n,i]=React.useState({width:void 0,height:void 0});return React.useEffect(()=>{i({width:t.current.getBoundingClientRect().width,height:t.current.getBoundingClientRect().height});const e=()=>{i({width:t.current.getBoundingClientRect().width,height:t.current.getBoundingClientRect().height})};return window.addEventListener("resize",e),()=>window.removeEventListener("resize",e)},[t]),React.createElement(React.Fragment,null,React.createElement("div",{className:"excalidraw-wrapper",ref:t},React.createElement(ExcalidrawLib.Excalidraw,{ref:e,width:n.width,height:n.height,initialData:InitialData,viewModeEnabled:!0,zenModeEnabled:!0,gridModeEnabled:!1})))},excalidrawWrapper=document.getElementById("excalidraw-002-文件传输案例（FTP、TFTP）-3excalidraw.md3");ReactDOM.render(React.createElement(App),excalidrawWrapper);})();</script>
### 实验需求
1. 命名并配置AR1的IP地址
2. 在真机上开启TFTP服务
3. 在AR1通过TFTP向真机上传文件，然后删除该文件并再次从真机下载文件
### 实验解析
搭好实验拓扑：
![../../../../Extras/Media/media-002-文件传输案例（FTP、TFTP）-1.png|300](/img/user/Extras/Media/media-002-%E6%96%87%E4%BB%B6%E4%BC%A0%E8%BE%93%E6%A1%88%E4%BE%8B%EF%BC%88FTP%E3%80%81TFTP%EF%BC%89-1.png)
打开Cloud1，添加UDP和VMware Network Adapter VMnet1（或者换成其他网卡也行，但要有一个UDP网卡）两个网卡，并设置端口映射：
![../../../../Extras/Media/media-002-文件传输案例（FTP、TFTP）-2.png](/img/user/Extras/Media/media-002-%E6%96%87%E4%BB%B6%E4%BC%A0%E8%BE%93%E6%A1%88%E4%BE%8B%EF%BC%88FTP%E3%80%81TFTP%EF%BC%89-2.png)
由图得知，在这条链路上，真机端的IP地址为192.168.198.1。

命名AR1：
```
<Huawei>system-view
Enter system view, return user view with Ctrl+Z.
[Huawei]sysname AR1
```
AR1设置IP地址：
```
[AR1]int g0/0/0
[AR1-GigabitEthernet0/0/0]ip add 192.168.198.2 24
Sep 20 2025 14:28:43-08:00 AR1 %%01IFNET/4/LINK_STATE(l)[0]:The line protocol IP on the interface GigabitEthernet0/0/0 has entered the UP state. 
[AR1-GigabitEthernet0/0/0]return
```
打开3CDaemon，点击设置TFTP服务器：
![../../../../Extras/Media/media-002-文件传输案例（FTP、TFTP）-3.png](/img/user/Extras/Media/media-002-%E6%96%87%E4%BB%B6%E4%BC%A0%E8%BE%93%E6%A1%88%E4%BE%8B%EF%BC%88FTP%E3%80%81TFTP%EF%BC%89-3.png)
进行TFTP设置：
![../../../../Extras/Media/media-002-文件传输案例（FTP、TFTP）-4.png](/img/user/Extras/Media/media-002-%E6%96%87%E4%BB%B6%E4%BC%A0%E8%BE%93%E6%A1%88%E4%BE%8B%EF%BC%88FTP%E3%80%81TFTP%EF%BC%89-4.png)
向真机上传文件：
```
<AR1>dir
Directory of flash:/

  Idx  Attr     Size(Byte)  Date        Time(LMT)  FileName 
    0  drw-              -  Sep 20 2025 06:20:49   dhcp
    1  -rw-        121,802  May 26 2014 09:20:58   portalpage.zip
    2  -rw-          2,263  Sep 20 2025 06:20:45   statemach.efs
    3  -rw-        828,482  May 26 2014 09:20:58   sslvpn.zip

1,090,732 KB total (784,464 KB free)
<AR1>tftp 192.168.198.1 put statemach.efs
Info: Transfer file in binary mode.
Uploading the file to the remote TFTP server. Please wait...

 22%     

 45%     

 67%     

 90%      TFTP: Uploading the file successfully.
    2263 bytes send in 1 second.
```
确认已上传：
![../../../../Extras/Media/media-002-文件传输案例（FTP、TFTP）-5.png](/img/user/Extras/Media/media-002-%E6%96%87%E4%BB%B6%E4%BC%A0%E8%BE%93%E6%A1%88%E4%BE%8B%EF%BC%88FTP%E3%80%81TFTP%EF%BC%89-5.png)
再下载该文件，下载为123.efs：
```
<AR1>tftp 192.168.198.1 get statemach.efs 123.efs
Info: Transfer file in binary mode.
Downloading the file from the remote TFTP server. Please wait...

 22%     

 45%     

 67%     

 90%     

 100%          2263 bytes received in 1 second.
TFTP: Downloading the file successfully.
<AR1>dir
Directory of flash:/

  Idx  Attr     Size(Byte)  Date        Time(LMT)  FileName 
    0  drw-              -  Sep 20 2025 06:20:49   dhcp
    1  -rw-        121,802  May 26 2014 09:20:58   portalpage.zip
    2  -rw-          2,263  Sep 20 2025 06:39:53   123.efs
    3  -rw-          2,263  Sep 20 2025 06:20:45   statemach.efs
    4  -rw-        828,482  May 26 2014 09:20:58   sslvpn.zip

1,090,732 KB total (784,456 KB free)
```