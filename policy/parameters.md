# 通用策略参数

### 出口参数

所有这些参数对内置和代理策略都是可用的。

#### interface （默认：自动）

强制使用一个指定的出站网卡。

```
ProxyHTTP = http, 1.2.3.4, 443, username, password, interface = en2
```

像代理策略一样，direct 策略别名支持 interface 参数。

```
[Proxy]
Crop-VPN = direct, interface = utun0
WiFi = direct, interface = en2, allow-other-interface=true
```

请确保该网卡拥有一个对目标地址有效的路由表。

#### allow-other-interface

当该选项为 true 时，如果所需的网卡不可用，则允许 Surge 使用默认接口来处理网络连接。否则，连接会直接失败。

```
ProxyHTTP = http, 1.2.3.4, 443, username, password, interface = en2, allow-other-interface=true
```

#### ip-version

在 IPv4 和 IPv6 协议间进行选择

- dual（默认，使用更快的连接）
- v4-only
- v6-only
- prefer-v4
- prefer-v6

#### hybrid （布尔型，仅限 iOS，默认值：off）

尝试并发使用蜂窝数据和 Wi-Fi 进行连接，然后选择使用更快的连接。

#### tfo （布尔型，默认值：off）

启用 TCP Fast Open。

#### mptcp （布尔型，仅限 iOS，默认值：off）

启用 MultiPath TCP。（需要启用 Network.framework）

#### tos （十进制或十六进制，默认：0）

自定义 IP TOS 值。

### 测试

#### test-url

覆盖全局设置的测试 URL。该 URL 用于可用性和基准测试。

#### test-timeout（单位：秒）
 
覆盖全局设置的测试超时时间。

