# 子网规则

### 子网表达式

子网表达式可以表示为如下形式：
  - 使用 SSID:value 匹配 Wi-Fi SSID，支持通配符。
  - 使用 BSSID:value 匹配 Wi-Fi BSSID，支持通配符。
  - 使用 ROUTER:value 匹配路由器 IP 地址。
  - 使用 TYPE:WIFI 匹配全部 Wi-Fi 网络。
  - 使用 TYPE:WIRED 匹配全部有线网络。
  - 使用 TYPE:CELLULAR 匹配全部蜂窝网络。
  - 使用 MCCMNC:100-200 匹配特定蜂窝网络。
  - 如果没有提供前缀，为保证兼容性，Surge 将尝试匹配 SSID/BSSID/ROUTER 规则。

#### SUBNET 规则

如果子网表达式匹配，则规则匹配。

```
SUBNET,TYPE:WIRED,DIRECT
SUBNET,SSID:MyHome,Proxy
```
