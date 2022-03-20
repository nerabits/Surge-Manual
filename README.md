# Surge 概述

Surge 是一个网络开发和代理工具。由于它是为开发者设计的，在使用时，你需要掌握一定的专业知识。

Surge 的核心能力有四项：

* 接管：可以将设备发出的网络连接进行接管。Surge 支持代理服务和虚拟网卡两种方式接管。

* 处理：可以对被接管的网络请求和响应进行修改。包括 URL 重定向、本地文件映射、使用 JavaScript 自定义修改等多种方式。

* 转发：可以将被接管的网络请求转发给其他代理服务器。可以是全局转发，也可以按照非常灵活的规则系统确定出口策略。

* 截获：可以截获并保存网络请求和响应的具体数据，同时可对 HTTPS 加密流量进行 MITM 解密。


## 特性

* 高性能、稳定、高效率：Surge 可以在耗费极小系统资源的情况下，在保证工业级稳定性的同时，流畅地处理全部网络数据。
* 灵活的规则体系：你可以编写基于域名、IP CIDR、GeoIP 等的转发规则。Surge 可以使用 HTTP/HTTPS/SOCKS5/SOCKS5-TLS/Trojan/Vmess/Shadowosocks 协议自动处理网络请求。
* HTTPS 解密：使用中间人攻击解密 HTTPS 流量。你可以使用证书生成器生成证书，安装到操作系统并信任来实现调试目的。
* 本地 DNS 映射：Surge 支持本地自定义 DNS 映射。其中包含多种功能：通配符、别名和自定义 DNS 服务器，可以满足你的多种需求。
* 代理组：你可以将多个代理放进一个代理组中，并根据分组情况来采用相应的策略。代理组有以下几种类型：自动测速\(基于 URL 测速选择代理\)、SSID \(根据当前连接的 Wi-Fi 的 SSID 选择代理\) 和手动选择。
* HTTP 重写：你可以使用自定义的规则，将 HTTP/HTTPS 请求重写到其他 URL 或阻止这些请求。
* 远程请求查看器：Surge 请求查看器可以通过 USB 或网络连接至 Surge iOS 或 Surge Mac 示例，查看目标设备的网络请求。
* 完整的 IPv6 支持：全部功能均可以在 IPv6 网络环境下正常运行。


### Surge Mac 独有的特性

* 增强模式：Surge 可以设置一个虚拟网络接口，用于处理不支持 Web Proxy 的应用程序的全部网络请求。
* 计费网络模式：你可以控制可访问互联网的应用程序和进程，这在连接到流量计费的网络时非常有用。
* 网关模式：Surge Mac可以被配置为第三层网关，为同一网络中的其他设备处理网络流量。


### Surge iOS 独有的特性

* 全部功能均可以在蜂窝网络环境下正常运行。
* 不论 App 是否遵循系统代理设置，Surge 均可捕获设备上所有的 HTTP/HTTPS/TCP 流量，并按照高度可配置的规则重定向到 HTTP/HTTPS/SOCKS5/SOCKS5-TLS/Trojan/Vmess/Shadowosocks 代理服务器。
* 即使在蜂窝网络上也可覆盖系统 DNS 设置，并同时查询所有 DNS 服务器来提高网络连接性能。
* 通过 Wi-Fi 或 USB 线缆将 Surge 请求查看器连接到 Surge iOS，监测和分析 iOS 设备的网络请求。通过 USB 线缆连接时，你甚至可以查看蜂窝网络请求。

### 理解 Surge

我们发布了官方指南，以便你更好地理解 Surge。

* 英文版本：https://manual.nssurge.com/book/understanding-surge/en/

* 中文版本：https://manual.nssurge.com/book/understanding-surge/cn/


