# 本地 DNS 映射

Surge 支持本地自定义的 DNS 映射。它相当于 /etc/hosts，但具有更强大的功能，包括通配符、别名和指定 DNS 服务器。

```
[Host]
abc.com = 1.2.3.4
*.dev = 6.7.8.9
foo.com = bar.com
bar.com = server:8.8.8.8
```

## 通配符

你可以使用 \* 前缀来匹配所有子域名。请注意，Surge 使用简单字符串匹配。例如，\*google.com 将匹配 google.com, foo.google.com 和 bargoogle.com。而 \*.google.com 将**不**匹配 google.com.

```
[Host]
*.dev = 6.7.8.9
```

## 别名

相当于 CNAME 记录。

```
[Host]
foo.com = bar.com
```

## 指定 DNS 服务器

你可以为一个或多个域名指定一个 DNS 服务器。

```
[Host]
bar.com = server:8.8.8.8
```

由于 Surge 有自己的 DNS 客户端实现，一些主机名可能无法解析。你可以使用 "server:system" 来让系统解析。

```
[Host]
Macbook = server:system
```

默认情况下，所有后缀为 '.local' 的主机名都将由系统解析。

## 为代理使用本地 DNS 结果


```
[General]
use-local-host-item-for-proxy=true
```

默认情况下，因为 Surge 总是发送含有域名的代理请求，所以，请求的 DNS 解析由远程代理服务器完成。

启用此选项后，对于匹配本地 DNS 映射记录的请求，Surge 将使用本地映射的 IP 地址，而不是域名来发送代理请求。

此选项仅适用于使用 IP 地址的本地 DNS 映射。