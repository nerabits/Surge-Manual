# URL 重写

Surge 可以以两种不同的方式重定向URL，或基于 URL 拒绝特定请求。

示例:

```
[URL Rewrite]
^http://www\.google\.cn http://www.google.com header
^http://yachen\.com https://yach.me 302
^http://ad\.com/ad\.png _ reject
```

Rewrite 规则包含 3 个部分：正则表达式、替代文本和类型。

### Header 模式
Surge 将会修改请求的 Header，客户端将不会感知到这次重定向。

请求头中的 "Host" 字段将被修改为新的 URL。

```
[URL Rewrite]
^http://www\.google\.cn http://www.google.com header
```

> 你不能重定向到一个 HTTPS 标志符的 URL。你也不能重定向一个 HTTPS 请求。


### 302 模式
Surge 将简单地返回一个 302 重定向响应。当 HTTPS 解密对对应的主机名开启时，可以对 HTTPS 请求重定向。

```
[URL Rewrite]
^http://yachen\.com https://yach.me 302
```


### Reject 模式
当 URL 匹配时拒绝该请求，该规则下替代文本参数无效。当 HTTPS 解密对对应的主机名开启时，可以对 HTTPS 请求使用。

```
[URL Rewrite]
^http://ad\.com/ad\.png _ reject
```

