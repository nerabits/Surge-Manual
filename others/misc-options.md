# [General] 配置段的其他选项

由于选项经常变化，你可以在应用程序中查找 [General] 部分选项的最新解释。

- Surge Mac: 主窗口 -> 帮助 -> 配置文件符号
- Surge iOS: "更多" 标签 -> 帮助 -> 配置文件符号


```
[General]
ipv6 = false
loglevel = notify
skip-proxy = 127.0.0.1, 192.168.0.0/16, 10.0.0.0/8, 172.16.0.0/12, 100.64.0.0/10, localhost, *.local
tun-excluded-routes = 192.168.0.0/16, 10.0.0.0/8, 172.16.0.0/12
tun-included-routes = 192.168.1.12/32
```

### loglevel

日志级别。可选值包含 verbose, info, notify 和 warning。不建议在日常使用中启用 verbose 模式，因为会大大降低性能。

### ipv6

开启完整 IPv6 支持。

### ipv6-vif {{book.BETA}}

允许 IPv6 通过 Surge VIF。此选项用于处理连接到 IPv6 地址的原始 TCP 连接。

- `off`: 关闭 Surge VIF 的 IPv6 功能。
- `auto`: 当你的本地网络支持 IPv6 时，启动 Surge VIF 的 IPv6 功能。
- `always`: 永远开启 Surge VIF 的 IPv6 功能。

### dns-server

上级 DNS 服务器的 IP 地址。

### skip-proxy

在 iOS 版本中，该选项将使得发往这些域名或者 IP 段的请求由 Surge VIF 进行处理（而不是 Surge Proxy）；在 macOS 版本中，当“设置为系统代理”开启时，该选项中的设置将会被提交到系统。该选项用于修正和某些应用的兼容性问题。

  - 指定单一域名，输入域名 - 例如，apple.com。

  - 指定一个域名上的所有网站，在域名前使用星号 - 例如，\*apple.com。

  - 指定一个域的特定子域名，输入完整域名 - 例如，store.apple.com。

  - 要通过IP地址指定主机或网络，请输入一个特定的IP地址，如 192.168.2.11 或一个地址范围，如 192.168.2.* 或 192.168.2.0/24。

注意：如果你指定了 IP 地址或地址范围，你只能在使用该地址或地址范围直接连接到该主机时绕过代理；而在使用这些IP或IP段对应的域名连接时，则不能绕过代理。

### exclude-simple-hostnames

和 skip-proxy 参数类似，该选项允许使用简单的主机名（没有.）的请求由 Surge VIF 而不是 Surge Proxy 进行处理。

### external-controller-access

该选项允许外部控制器来控制 Surge，例如 Surge 请求查看器（macOS）和 Surge iOS 远程控制器（iOS）。例如：key@0.0.0.0:6165

### http-api

该选项允许使用 HTTP API 来控制 Surge。例如：key@0.0.0.0:6166

### http-api-tls

使用 HTTPS 协议替代HTTP。必须先配置 MitM CA 证书。你需要在客户端设备上手动安装该证书。

### http-api-web-dashboard

你可以在启用该功能后，使用浏览器控制 Surge。

### show-error-page-for-reject

如果请求时普通的 HTTP 请求，则为 REJECT 策略显示一个错误网页。

### tun-excluded-routes

Surge VIF 仅可处理 TCP 和 UDP 协议。使用此功能来绕过特定的 IP 范围，来允许所有流量通过。

注意。这个选项只适用于Surge VIF。由 Surge Proxy 处理的请求不受影响。你可以结合 "skip-proxy" 和 "tun-excluded-routes" 选项来确保特定的 HTTP 流量绕过 Surge。

### tun-included-routes

默认情况下，Surge VIF 将自己定义为默认路由。然而，由于 Wi-Fi 网卡有一个较小的路由，一些流量可能不会通过 Surge VIF。使用这个选项可以添加一个较小的路由。

### internet-test-url

用于测试互联网连接性的 URL，同时也用于 DIRECT 策略的网络测试。

### proxy-test-url

代理策略的默认测试 URL。

### test-timeout

连接测试的超时时间。

### always-real-ip

当 Surge VIF 处理 DNS 查询时，该选项要求 Surge 返回真实的 IP 地址，而不是 fake IP。

DNS 数据包将被转发至上游 DNS 服务器。

### hijack-dns

默认情况下，Surge 只返回发送至 Surge DNS 地址（198.18.0.2）的 DNS 查询的虚假 IP 地址。发送到标准 DNS 的查询将被转发。

有些设备或软件总是使用一个固定的的 DNS 服务器 (例如，Google Speakers 总是使用8.8.8.8）。你可以使用这个选项来劫持查询，以获得一个虚假地址。

你可以使用 hijack-dns = \*:53 来劫持全部 DNS 查询。

### force-http-engine-hosts

使 Surge 将 TCP 连接视为 HTTP 请求。Surge HTTP 引擎将处理这些请求，所有的高级功能都可以使用，如抓取流量、Rewrite 和脚本。

支持通配符 \* 和 ?。

  - 使用前缀 - 来排除一个主机名。

  - 默认情况下，只有对80端口的请求才会被解密。

  - 使用后缀 :port 来允许其他端口。

  - 使用后缀 :0 来允许全部端口

Example:

  - -\*.apple.com: 排除所有发送到80端口的 \*.apple.com 的请求。

  - www.google.com: 对80端口的 www.google.com 请求采用强制HTTP处理。

  - www.google.com:8080: 对8080端口的 www.google.com 请求采用强制HTTP处理。

  - www.google.com:0: 对全部端口的 www.google.com 请求采用强制HTTP处理。

  - \*:0: 对所有端口上的所有主机名使用强制HTTP处理。


### debug-cpu-usage

启用CPU调试模式。这可能会降低性能。

### debug-memory-usage

启用内存调试模式。这可能会降低性能。

### doh-follow-outbound-mode

默认情况下，Surge 直接连接到 DoH 服务器进行查询。启用该选项使 DoH 遵循出站模式的设置和规则。

### doh-server

DNS-over-HTTPS 服务器的 URL。

### use-local-host-item-for-proxy

默认情况下，如果使用代理策略，DNS 查询总是在远程服务器上进行。启用此选项后，如果目标域的本地 DNS 映射结果存在，Surge 会使用 IP 地址而不是域名来建立代理连接。

### geoip-maxmind-url

用于更新 GeoIP 数据库的URL。

### disable-geoip-db-auto-update

关闭 GeoIP 数据库的自动更新。

### allow-dns-svcb

iOS system might perform an SVCB record DNS lookup instead of a standard A record lookup. This causes Surge to fail to return a virtual IP address. So by default, the SVCB record lookup is forbidden to force the system to perform an A record lookup.

### udp-policy-not-supported-behaviour

当 UDP 流量符合某项代理策略，而该代理不支持 UDP 转发时的回退行为。可用值：DIRECT, REJECT。

### proxy-test-udp

### compatibility-mode（仅限 iOS）

### allow-wifi-access（仅限 iOS）

允许从局域网中的其他设备访问 Surge 代理服务。

### wifi-access-http-port（仅限 iOS）

Surge HTTP 代理服务的端口号。

### wifi-access-socks5-port（仅限 iOS）

Surge SOCKS5 代理服务的端口号。

### wifi-access-http-auth（仅限 iOS）

对 Surge HTTP 代理服务进行认证。例如：username:password

### include-all-networks（仅限 iOS）

在默认情况下，一些请求可能不会被 Surge 接管。例如，应用程序可以绑定到物理网络接口，以绕过 Surge VIF。启用包括所有网络的选项，以确保所有的请求都由 Surge 处理而不泄漏。当你使用 Surge 作为防火墙时，这个选项很有用。(需要iOS 14.0或以上版本)

启用该选项可能会导致 AirDrop 和 Xcode 调试问题，在使用 USB 连接到 Surge 请求查看器时不工作，以及其他意想不到的副作用。请慎重使用。

### include-local-networks（仅限 iOS）

启用此选项，允许 Surge VIF 处理发送到局域网的请求。(需要iOS 14.2或以上版本)

启用该选项可能会导致 AirDrop 和 Xcode 调试问题，在使用 USB 连接到 Surge 请求查看器时不工作，以及其他意想不到的副作用。请慎重使用。

### wifi-assist（仅限 iOS）

开启增强版 Wi-Fi 助理。

### hide-vpn-icon（仅限 iOS）

隐藏状态栏的 VPN 图标。

### all-hybrid（仅限 iOS）

### allow-hotspot-access（仅限 iOS）

当个人热点开启时，允许从其他设备访问 Surge 代理服务。

### use-default-policy-if-wifi-not-primary（仅限 macOS）

如果禁用，即使 Wi-Fi 不是主网络接口，SSID/BSSID 模式仍然可以匹配。

### read-etc-hosts（仅限 macOS）

遵循 /etc/hosts 中的本地 DNS 映射项。

### http-listen（仅限 macOS）

HTTP 代理服务的监听参数。例如：0.0.0.0:6152

### socks5-listen（仅限 macOS）

SOCKS5 代理服务的监听参数。例如：0.0.0.0:6153


