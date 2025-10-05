---
{"dg-publish":true,"dg-path":"网络/网络学习/ab-WLAN频段介绍.md","permalink":"/网络/网络学习/ab-WLAN频段介绍/"}
---

# 一、频段与信道介绍
## 1.ISM频段
ISM频段，此频段主要是开放给工业、科学、医学三个主要机构使用，该频段是依据美国联邦通讯委员会（FCC）所定义出来，并没有所谓使用授权的限制。
![../../../../Extras/Media/media-ab-WLAN频段介绍-1.png|300](/img/user/Extras/Media/media-ab-WLAN%E9%A2%91%E6%AE%B5%E4%BB%8B%E7%BB%8D-1.png)
## 2.WLAN频段与信道
WLAN技术被 802.11b/g/n 定义工作在 2.4GHz 的频段中，在其中 2.4GHz 频段被划分为14个交叠的、错列的20MHz 无线载波信道，它们的中心频率间隔分别为 5MHz。802.11a/n/ac 工作在有更多信道的 5GHz 频段中。
# 二、2.4GHz频段
- 支持802.11b/g/n
- 802.11b每个信道需要占用22MHz
- 802.11g、802.11n每个信道需要占用20MHz
- 802.11n完全兼容802.11b 和802. 11g
![../../../../Extras/Media/media-ab-WLAN频段介绍-2.png](/img/user/Extras/Media/media-ab-WLAN%E9%A2%91%E6%AE%B5%E4%BB%8B%E7%BB%8D-2.png)
## 1.主要国家工作频率

|信道|频率(MHz)|中国|美国、加拿大|欧洲|日本|澳大利亚|
|:-:|:-:|:-:|:-:|:-:|:-:|:-:|
|1|2412|是|是|是|是|是|
|2|2417|是|是|是|是|是|
|3|2422|是|是|是|是|是|
|4|2427|是|是|是|是|是|
|5|2432|是|是|是|是|是|
|6|2437|是|是|是|是|是|
|7|2442|是|是|是|是|是|
|8|2447|是|是|是|是|是|
|9|2452|是|是|是|是|是|
|10|2457|是|是|是|是|是|
|11|2462|是|是|是|是|是|
|12|2467|是|否|是|是|是|
|13|2472|是|否|是|是|是|
|14|2484|否|否|否|802.11b only|否|

## 2.信道绑定
信道绑定技术通过将相邻的两个20MHz信道绑定成40MHz，使传输速率成倍提高。
![../../../../Extras/Media/media-ab-WLAN频段介绍-3.png](/img/user/Extras/Media/media-ab-WLAN%E9%A2%91%E6%AE%B5%E4%BB%8B%E7%BB%8D-3.png)
2.4GHz频段一般常用的是1、6、11这三个不重叠的信道。
# 三、5GHz 频段
- 支持802.11a/n/ac/ax/be
- 802.11a/n每个信道需要占用20MHz
- 802.11ac每个信道支持20MHz、40MHz、80MHz

<table>
	<tr>
		<th align="center">信道编号Nch</th>
		<th align="center">频段GHz</th>
		<th align="center">中心频率MHz</th>
		<th align="center">美国</th>
		<th align="center">中国</th>
	</tr>
	<tr>
		<td align="center">36</td>
		<td align="center" rowspan="4">5.15~5.25<br>UNII低频段</td>
		<td align="center">5180</td>
		<td align="center">是</td>
		<td align="center">仅室内</td>
	</tr>
	<tr>
		<td align="center">40</td>
		<td align="center">5200</td>
		<td align="center">是</td>
		<td align="center">仅室内</td>
	</tr>
	<tr>
		<td align="center">44</td>
		<td align="center">5220</td>
		<td align="center">是</td>
		<td align="center">仅室内</td>
	</tr>
	<tr>
		<td align="center">48</td>
		<td align="center">5240</td>
		<td align="center">是</td>
		<td align="center">仅室内</td>
	</tr>
	<tr>
		<td align="center">52</td>
		<td align="center" rowspan="4">5.25~5.35<br>UNII中频段</td>
		<td align="center">5260</td>
		<td align="center">是</td>
		<td align="center">仅室内</td>
	</tr>
	<tr>
		<td align="center">56</td>
		<td align="center">5280</td>
		<td align="center">是</td>
		<td align="center">仅室内</td>
	</tr>
	<tr>
		<td align="center">60</td>
		<td align="center">5300</td>
		<td align="center">是</td>
		<td align="center">仅室内</td>
	</tr>
	<tr>
		<td align="center">64</td>
		<td align="center">5320</td>
		<td align="center">是</td>
		<td align="center">仅室内</td>
	</tr>
	<tr>
		<td align="center">149</td>
		<td align="center" rowspan="4">5.725~5.825<br>UNII高频段</td>
		<td align="center">5745</td>
		<td align="center">是</td>
		<td align="center">是</td>
	</tr>
	<tr>
		<td align="center">153</td>
		<td align="center">5765</td>
		<td align="center">是</td>
		<td align="center">是</td>
	</tr>
	<tr>
		<td align="center">157</td>
		<td align="center">5785</td>
		<td align="center">是</td>
		<td align="center">是</td>
	</tr>
	<tr>
		<td align="center">161</td>
		<td align="center">5805</td>
		<td align="center">是</td>
		<td align="center">是</td>
	</tr>
	<tr>
		<td align="center">165</td>
		<td align="center">~5.850</td>
		<td align="center">5825</td>
		<td align="center">是</td>
		<td align="center">是</td>
	</tr>
</table>

## 1.中国的5.8GHz信道
在中国，5.8GHz频段内有5个非重叠信道，分别为：149，153，157，161，165，如下图：
![../../../../Extras/Media/media-ab-WLAN频段介绍-4.png](/img/user/Extras/Media/media-ab-WLAN%E9%A2%91%E6%AE%B5%E4%BB%8B%E7%BB%8D-4.png)
## 2.信道绑定
标准建议配置：149，157或者153，161；采用149，157配置时，表示主信道在前；采用153，161配置时，表示主信道在后，配置范围其实是一样的。
![../../../../Extras/Media/media-ab-WLAN频段介绍-5.png](/img/user/Extras/Media/media-ab-WLAN%E9%A2%91%E6%AE%B5%E4%BB%8B%E7%BB%8D-5.png)
***
# 参考文献
[1] 华为技术有限公司.WLAN频段介绍[PPT].(2025)[2025-09-17]