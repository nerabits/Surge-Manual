# Snell 协议 {{book.BETA}}

Snell 是一个由 Surge 团队开发的加密代理协议，以下是此协议的一些亮点：

- 优秀的性能。
- 支持通过 TCP 传输 UDP 数据。
- 单一二进制文件，无任何依赖 (除 glibc 外)。
- 完善的向导机制，帮助你使用协议。
- 如果遇到错误，代理服务端将向客户端报告远程错误。客户端可以根据不同情况选择合适的对策。

> Snell 协议仅适用于 Surge 用户，请不要尝试对协议进行反向分析并开发兼容客户端。我们希望保持较小的用户群，感谢您的理解。

你可以在这里下载独立的服务端二进制文件：

https://dl.nssurge.com/snell/snell-server-v4.0.0-linux-amd64.zip

https://dl.nssurge.com/snell/snell-server-v4.0.0-linux-i386.zip

https://dl.nssurge.com/snell/snell-server-v4.0.0-linux-aarch64.zip

https://dl.nssurge.com/snell/snell-server-v4.0.0-linux-armv7l.zip


Snell 的最新版本是 v4，与之前不同的是，此版本不向下兼容旧版本协议。请同时升级客户端（Surge iOS & Surge Mac）和服务端程序。

```
[Proxy]
Proxy = snell, 1.2.3.4, 6333, psk=RANDOM_KEY_HERE, version=4
```

## 使用 Surge Mac 作为 Snell 代理服务端

你也可以使用 Surge Mac（3.1.0 之后版本）作为 Snell 代理服务端。你可以在配置文件中添加以下配置：

```
[Snell Server]
interface = 0.0.0.0
port = 6160
psk = RANDOM_KEY_HERE
```

Surge 内置的 Snell 服务端采用 Snell V1 版本协议。


