# Header Rewrite

**此功能目前只在测试版中提供。**

Surge 可以在被转发到服务器之前重写由客户端发送的 Request Header。

示例:

```
[Header Rewrite]
^http://example.com header-add DNT 1
^http://example.com header-del Cookie
^http://example.com header-replace User-Agent Unknown
```

Rewrite 规则包含4个部分：URL 正则表达式、模式、字段和值。

### header-add

在请求头中添加一个新行，即使该字段已经存在。

示例:

```
[Header Rewrite]
^http://example.com header-add DNT 1

更改前：
GET /index.html HTTP/1.1
Host: example.com
Connection: keep-alive
User-Agent: Mozilla/5.0 (Macintosh; Intel Mac OS X 10_12_4) AppleWebKit/603.1.30 (KHTML, like Gecko) Version/10.1 Safari/603.1.30
Accept-Language: en-us
Accept-Encoding: gzip, deflate

更改后：
GET /index.html HTTP/1.1
Host: example.com
Connection: keep-alive
User-Agent: Mozilla/5.0 (Macintosh; Intel Mac OS X 10_12_4) AppleWebKit/603.1.30 (KHTML, like Gecko) Version/10.1 Safari/603.1.30
Accept-Language: en-us
Accept-Encoding: gzip, deflate
DNT: 1
```

### header-del

在请求头中删除一行。

示例:

```
[Header Rewrite]
^http://example.com header-del DNT

更改前：
GET /index.html HTTP/1.1
Host: example.com
Connection: keep-alive
User-Agent: Mozilla/5.0 (Macintosh; Intel Mac OS X 10_12_4) AppleWebKit/603.1.30 (KHTML, like Gecko) Version/10.1 Safari/603.1.30
Accept-Language: en-us
Accept-Encoding: gzip, deflate
DNT: 1

更改后：
GET /index.html HTTP/1.1
Host: example.com
Connection: keep-alive
User-Agent: Mozilla/5.0 (Macintosh; Intel Mac OS X 10_12_4) AppleWebKit/603.1.30 (KHTML, like Gecko) Version/10.1 Safari/603.1.30
Accept-Language: en-us
Accept-Encoding: gzip, deflate
```

### header-replace

在请求头中更改一个 Header 值。当这个字段不存在时，将不处理。

示例:

```
[Header Rewrite]
^http://example.com header-replace DNT 1

更改前：
GET /index.html HTTP/1.1
Host: example.com
Connection: keep-alive
User-Agent: Mozilla/5.0 (Macintosh; Intel Mac OS X 10_12_4) AppleWebKit/603.1.30 (KHTML, like Gecko) Version/10.1 Safari/603.1.30
Accept-Language: en-us
Accept-Encoding: gzip, deflate
DNT: 0

更改后：
GET /index.html HTTP/1.1
Host: example.com
Connection: keep-alive
User-Agent: Mozilla/5.0 (Macintosh; Intel Mac OS X 10_12_4) AppleWebKit/603.1.30 (KHTML, like Gecko) Version/10.1 Safari/603.1.30
Accept-Language: en-us
Accept-Encoding: gzip, deflate
DNT: 1
```

如果你想在字段存在的时候添加或替换一个 Header 行，你可以同时使用 header-add 和 header-del。

```
[Header Rewrite]
^http://example.com header-del DNT
^http://example.com header-add DNT 1
```