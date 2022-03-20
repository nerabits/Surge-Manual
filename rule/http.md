# HTTP 规则

HTTP 规则有 2 种类型。HTTP 规则只针对 HTTP 和 HTTPS 请求，不会影响 TCP 连接。

#### USER-AGENT

```
USER-AGENT,Instagram*,DIRECT
```

此规则用于匹配对应请求的 USER-AGENT。支持通配符 * 和 ?。

#### URL-REGEX

`URL-REGEX,^http://google\.com,DIRECT`

如果 URL 与正则表达式匹配，则规则匹配。