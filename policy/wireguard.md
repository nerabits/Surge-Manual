# WireGuard

你可以将 Surge 作为 WireGuard 客户端，转换这个 L3 VPN 为一个代理策略。

```
[Proxy]
wireguard-home = wireguard, section-name = HomeServer

[WireGuard HomeServer]
private-key = sDEZLACT3zgNCS0CyClgcBC2eYROqYrwLT4wdtAJj3s=
self-ip = 10.0.2.2
dns-server = 223.5.5.5
mtu = 1280
peer = (public-key = fWO8XS9/nwUQcqnkfBpKeqIqbzclQ6EKP20Pgvzwclg=, allowed-ips = 0.0.0.0/0, endpoint = 192.168.20.6:51820)
```

配置说明：

- 所有的 key 可使用 base64 或 HEX 形式。
- `self-ip` 字段必须提供，请注意每个设备的 `self-ip` 必须不同，否则或造成 IP 抢占。
- 字段可以配置多个节点，以逗号分隔，用 () 表示为一个节点的配置。
- `preshared-key` 和 `keepalive` 是 peer 的可选参数。
- Peer 的 Endpoint 可以使用域名。请注意 endpoint 的解析过程由 [General] 配置的 DNS 解析器完成，与本段中的 `dns-server` 参数无关。
- `allowed-ips` 配置为 0.0.0.0/0 时，意味着该策略可以用于访问任何地址，也可以配置为特定内网地址。
- 如果需要通过该策略使用域名访问主机，则必须配置 `dns-server`，Surge 将通过 WireGuard 的 VPN 去该服务器执行 DNS 解析。可配置多个 DNS 地址，用逗号分隔。
- [WireGuard NAME] 段可拆分到 Detached Profile Section 文件中。
- 可以同时配置和使用多个Wireguard实例。

使用说明：

- WireGuard 是 L3 VPN，所以处理过程中的开销明显高于其他的一般代理协议。它适用于对带宽要求较低的场景。
- Surge 支持连接到 IPv6 节点，但是仍未支持 IPv6 隧道。
- 目前 Tunnel 只支持 TCP 和 UDP 协议，另外做了非常简单的 ICMP 响应。当 WireGuard 握手成功后，可从服务端 ping 客户端 tunnel IP 进行测试。
- 由于 WireGuard 本身没有异常机制，绝大多数情况下，WireGuard 出错的表现为超时（如密钥错误、防护墙阻挡、未配置服务端 NAT 等等），请自行通过抓包的方式分析原因。

