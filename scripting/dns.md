### DNS

使用脚本去执行 DNS 解析操作，该类型下第二参数为脚本名。

`dns dnspod script-path=dnspod.js`

之后需要在 [Host] 中对相应域名进行配置。

```
[Host]
example.com = script:dnspod
*.example.com = script:dnspod
```

传入参数为 $domain，当前查询的域名。

返回结果可为以下结果中的任意一个：

* `address<String>`：直接使用该 IP 地址作为结果，必须是一个有效的 IPv4 或 IPv6 地址的字符串表示。
* `addresses<Array>`：使用多个 IP 地址作为结果。
* `server<String>`：表示 Surge 应交给特定的一个 DNS 服务器进行查询，必须是一个有效的 IPv4 或 IPv6 地址的字符串表示。
* `servers<Array>`：表示 Surge 应交给特定的多个 DNS 服务器进行查询。

当返回 `address<String>` 或 `addresses<Array>`时，可以额外返回 ttl 字段，将本次的结果记入 DNS 缓存避免重复查询，单位为秒。

以下样例使用了 DNSPod 的公开 HTTP DNS API，通过脚本扩展的方式让 Surge 可以随意支持各种协议的 DNS 查询

```
$httpClient.get('http://119.29.29.29/d?dn=' + $domain, function(error, response, data){
  if (error) {
    $done({}); // Fallback to standard DND query
  } else {
    $done({addresses: data.split(';'), ttl: 600});
  }
});
```


