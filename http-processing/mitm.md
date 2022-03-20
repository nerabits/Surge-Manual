# HTTPS 解密 (中间人攻击 Man-in-the-Middle Attack, MitM)

Surge 可以使用 MitM 解密 HTTPS 请求。 请参阅 [Wikipedia 文章](https://en.wikipedia.org/wiki/Man-in-the-middle_attack) 获取更多信息。

证书生成器可以帮助你生成一个新的CA证书进行调试，并使系统信任此证书。此功能在 Surge 主窗口（Mac版）和 Surge iOS 配置编辑器中可用。这个证书是在本地生成的，只保存在你你的配置文件和系统钥匙串中。新证书的密钥是使用 OpenSSL 随机生成的。

你也可以使用自己的 CA 证书。请将证书转化为含有密码的 PKCS#12 格式 (.p12)。 请注意，由于系统限制，密码不能为空。使用 "base64" 命令编码为 base64 字符串，并将下面这些设置添加到你的配置文件中。

```
[MITM]
enable = true
ca-p12 = MIIJtQ.........
ca-passphrase = password
hostname = *google.com
```

Surge 仅会解密这里指定的主机名的请求。

- 可使用通配符 * 和 ? 。
- 可使用前缀 - 将特定主机名排除。
- 默认仅解密发往 443 端口的请求
  - 可使用后缀 :port 解密特定端口
  - 可使用后缀 :0 解密所有端口

示例:
- `-*.apple.com`: 排除所有发往 *.apple.com 端口 443 的请求。
- `www.google.com`: 允许对 www.google.com 端口 443 进行 MitM。
- `www.google.com:8080`: 允许对 www.google.com 端口 8080 进行 MitM。
- `www.google.com:0`: 允许对 www.google.com 的全部端口进行 MitM。
- `*:0`: 允许对全部主机名和端口进行 MitM。

一个一般配置：

`hostname = -*.apple.com, -*.icloud.com, *`

> 一些应用具有严格的安全策略，仅信任某些特定的证书，对这些域名启动解密可能导致问题。


## 选项

### tcp-connection

默认情况仅会对使用 HTTP 代理服务的 HTTPS 请求进行解密。启用该选项，Surge 将对通过 Surge VIF（增强模式）的原始 TCP 连接进行解密。

### skip-server-cert-verify

在执行 MitM 是不验证远程主机的证书。

