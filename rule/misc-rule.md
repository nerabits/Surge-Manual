# 其他规则

#### DEST-PORT

此规则匹配对应端口的入站请求。

```
DEST-PORT,80,DIRECT
```

#### SRC-IP

此规则匹配对应 IP 的入站请求。

```
SRC-IP,192.168.20.100,DIRECT
```


#### IN-PORT

此规则匹配对应端口的出站请求。在Surge监听多个端口时较实用。

```
IN-PORT,6152,DIRECT
```


#### PROTOCOL 

此规则匹配对应请求的协议。可选值：HTTP、HTTPS、TCP、UDP、DOH。

```
PROTOCOL,HTTP,DIRECT
```

#### SCRIPT

使用 JavaScript 脚本判断是否匹配。

```
SCRIPT,ScriptName,DIRECT
```


#### CELLULAR-RADIO（仅限 iOS）

此规则匹配当前网络的蜂窝无线电技术。可选值：GPRS, Edge, WCDMA, HSDPA, HSUPA, CDMA1x, CDMAEVDORev0, CDMAEVDORevA, CDMAEVDORevB, eHRPD, HRPD, LTE, NRNSA, NR

```
CELLULAR-RADIO,LTE,DIRECT
```


#### CELLULAR-CARRIER（仅限 iOS）

此规则匹配当前网络的运营商。可选值为 MCC-MNC 移动设备网络代码。

```
CELLULAR-CARRIER,289-67,DIRECT
```


