# Snell 服务端

Snell 是一个新的由 Surge 团队开发的加密代理协议。您可以在这里下载独立的服务端二进制文件：https://github.com/surge-networks/snell

您也可以使用 Surge Mac 作为 Snell 代理服务器（仅在 3.1.0 及以后版本支持）。需要添加以下字段到您的配置文件中：

```
[Snell Server]
interface = 0.0.0.0
port = 6160
psk = RANDOM_KEY_HERE
obfs = off
```

Surge 内置的 Snell 服务端采用 Snell V1 版本协议。


