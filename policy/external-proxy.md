# 外部代理

为使 Surge 更简单地与其他代理软件配合使用，Surge Mac 支持外部代理策略。

以下为一个 SSH 示例。

首先，策略的类型为 `external`。

```
[Proxy]
external = external, exec = "/usr/bin/ssh", args = "11.22.33.44", args = "-D", args = "127.0.0.1:1080", local-port = 1080, addresses = 11.22.33.44
```

其中，`args` 和 `addresses` 字符段为可选，`exec` 和 `local-port` 为必需。`args` 和 `addresses` 可重复追加。

由以上策略，Surge 将进行以下操作：

1. 当使用策略时，Surge 使用 exec 和 args 字段启动外部进程，并将请求定向到 SOCKS5 代理 127.0.0.1:[local-port]。
2. 当使用策略时，如果外部进程被中止，其会被自动重启。
3. 启用增强模式时，Surge 将自动从 VIF 路由中排除 addresses 参数中的地址。(因此请在此字段中填写代理服务器 IP 地址，此功能不支持主机名和域名。)
4. Surge 总是对外部进程的请求使用 DIRECT 策略。（为处理像 obfs-local 一类的插件程序，外部进程的子进程也采用类似处理方式。）
5. Surge 退出时将自动关闭所有外部进程，Enhanced Mode 关闭时将自动清除全部路由表项.

一些提示：

1. 以上操作中，3 和 4 中存在功能重叠，请使用地址声明以排除VIF处理，由此可减少处理开销。4的功能为附加保护。
2. 外部进程的 stdout 和 stderr 将保存到 /tmp/Surge-External-xxxxxx.log，以进行故障排查。
3. 由于外部进程需要一定时间才可启动，如果转发到 127.0.0.1:[local-port] 时遇到连接被拒绝的错误，Surge将在 500ms 后进行自动重试，每个请求最多重试 6 次。
4. 由于 iOS 版本不支持外部代理，Surge iOS 会将外部代理策略设置为 REJECT。

