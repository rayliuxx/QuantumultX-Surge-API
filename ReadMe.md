## I. 关于

本API旨在将各种服务器订阅，转换成可用于 QuantumultX & Surge 两个优秀的iOS客户端的格式，具体来说：

- **QuantumultX**：从 ***SS订阅/SSD订阅/SSR订阅/V2rayN 订阅/Surge(conf&list)/QuanX*** 转换成 **QuantumultX** 格式的订阅，并提供正则过滤，以及UDP/TFO参数的修改，以及多个订阅（托管）的合并等，以及emoji旗帜添加/删除，以及简单的节点重命名；
- **Surge**：从 ***Surge(conf&list)/SS订阅/SSD订阅/V2rayN订阅***，转换成 **Surge list**的格式链接，并提供正则过滤，多个订阅（托管）链接合并，以及emoji旗帜添加/删除，以及简单的节点重命名等

-----

**更新说明：**

- 2019-10-15: 增加对emoji旗帜的支持
- 2019-10-18: 增加rename参数，进行简单重命名
- 2019-10-19: 增加对SSD订阅的转换支持
- 2019-10-25: 增加对quantumult X 类型的自我转换(正则过滤，emoji rename 等)
- 2019-10-29: emoji的json文件，有问题请指出
- 2019-10-30: 增加emoji旗帜删除参数，&emoji=-1
- 2019-11-03: rename 功能增强：节点名 前/后 增加字符

------

----

## II. 使用说明

### A. QuantumultX

| QuantumultX API     | 参数      | 说明                    | 要求                                                         | 状态 |
| ------------------- | --------- | ----------------------- | ------------------------------------------------------------ | ---- |
| 路径                | sub2quanx | NA                      | https://dove.589669.xyz/sub2quanx?                           | NA   |
| 类型                | type      | 必须                    | ss/ssd/ssr/v2/surge/quanx (surge的托管conf与list均可)        | ✅    |
| 订阅链接            | sub       | 必须，请先**urlencode** | 务必先对链接**urlencode**，多个订阅用 + 连接                 | ✅    |
| 正则过滤节点        | filter    | 可选，请先**urlencode** | 务必先对参数**urlencode**，从开头开始匹配，所以建议从  .* 开始 | ✅    |
| UDP强制更改         | udp       | 可选                    | 参数为1，或0 （默认为0，关闭），对surge/quanx类型无效        | ✅    |
| TFO强制更改         | tfo       | 可选                    | 参数为1，或0（默认为0，关闭），对surge/quanx类型无效         | ✅    |
| emoji 国家/地区符号 | emoji     | 可选                    | 参数为 -1(删除旗帜)，1，2(用于国行手机，解决无法显示台湾地区旗帜🇹🇼的问题)；<br />另有参数 11， 22，将emoji添加在节点名尾部（如：日本 IPLC 🇯🇵） | ✅    |
| 节点重命名          | rename    | 可选，请先**urlencode** | 1. 格式为 rename=oldname@newname，多个rename可用+链接：<br />- 例如将 香港替换成HK，日本替换成JP，则参数为：香港@HK+日本@JP (记得拿去urlencode)<br /> 2. 在名字前/后增加字符，可分别用 A@ 跟 @B等单参数，例如：<br />- 在节点前增加 [SS]，节点名尾增加 [IPLC], 则rename参数为：[SS]@+@[IPLC]<br />1跟2当然是可以混用的，比如 “[SS]@+@[IPLC]+香港@HK+日本@JP” | ✅    |

> 完整示范：将dler的ss订阅链接转换，并只取其中名字含 “**日本**” 的节点，并添加 emoji，以及将节点名中的“日本”替换为“JP”

```
`https://dove.589669.xyz/sub2quanx?type=ss&tfo=1&udp=1&emoji=2&sub=https%3A%2F%2Fdler.cloud%2Flink%2Fxxxx%3Fmu%3Dss&filter=.%2A%E6%97%A5%E6%9C%AC&rename=%E6%97%A5%E6%9C%AC%40JP`
```

如果你想过滤多个参数，比如 **日本** 或者 韩国 可以使用  .*(日本|韩国)

 更多更灵活的操作，自行学习 正则：https://github.com/ziishaned/learn-regex/blob/master/translations/README-cn.md

参数请去此网站进行URLEncode：https://www.urlencoder.org

---------



### B. Surge 3

| Surge API           | 参数      | 说明                    | 要求                                                         | 状态 |
| ------------------- | --------- | ----------------------- | ------------------------------------------------------------ | ---- |
| 路径                | Mix2Surge | NA                      | https://dove.589669.xyz/Mix2Surge?                           | NA   |
| 类型                | type      | 必须                    | ss/ssd/v2/surge   （其中，surge参数对conf托管跟list通用）    | ✅    |
| 订阅(托管)链接      | sub       | 必须，请先**urlencode** | 务必先对链接**urlencode**，多个订阅用 + 号连接               | ✅    |
| 正则过滤节点        | filter    | 可选，请先**urlencode** | 务必先对参数**urlencode**，从开头开始匹配，所以建议从  .* 开始 | ✅    |
| v2订阅的header host | hd        | 可选                    | hd=1，0 （为解决某些v2ray订阅在surge中不可用的情况，为0时，忽略header参数） | ✅    |
| UDP/TFO参数         | udp/tfo   | 可选                    | 仅对type为ss的类型有效（tfo=1/0，udp=1/0 来开启/关闭，默认关闭） | ✅    |
| emoji 国家/地区符号 | emoji     | 可选                    | 参数为 -1(删除旗帜)，1，2(用于国行手机，解决无法显示台湾地区旗帜🇹🇼的问题)；<br />另有参数 11， 22，将emoji添加在节点名尾部（如：日本 IPLC 🇯🇵） | ✅    |
| 节点重命名          | rename    | 可选，请先urlencode     | 1. 格式为 rename=oldname@newname，多个rename可用+链接：<br />- 例如将 香港替换成HK，日本替换成JP，则参数为：香港@HK+日本@JP (记得拿去urlencode)<br /> 2. 在名字前/后增加字符，可分别用 A@ 跟 @B等单参数，例如：<br />- 在节点前增加 [SS]，节点名尾增加 [IPLC], 则rename参数为：[SS]@+@[IPLC]<br />1跟2当然是可以混用的，比如 “[SS]@+@[IPLC]+香港@HK+日本@JP” | ✅    |

> 完整示范： 将某两个V2订阅合并转换成surge的list，并只选择其中的 **CHT ** 节点路线

```
https://dove.589669.xyz/Mix2Surge?type=v2&sub=https%3A%2F%2Fdler.cloud%2Fsubscribe%2Fxxx%3Fmu%3Dav2%2Bhttps%3A%2F%2Fytoo.xyz%2Fmodules%2Fservers%2FV2raySocks%2Fosubscribe.php%3Fsid%3D372%26token%3Dxxxo&filter=.%2ACHT
```



---

---

### 0⃣️ 请咖啡☕️名单

🙏感谢🙏

- 鸡儿硬梆梆
- 🐔哥｜法外 伉俪
- 旺仔弟| 旺仔哥
- 守夜人
- Big Cat
- Xin
- 锄禾
- 弥彦
- Miao ~ socloud
- 非主流 李克斯 关下门
- yumemi

**如果觉得有用，请大胆请喝咖啡☕️**

<img src="https://tva1.sinaimg.cn/large/006y8mN6gy1g7t6di3i9oj30gg0g240w.jpg" style="height:300px" />



