# Header Rewrite

**此功能目前只在测试版中提供。**

Surge 可以在被转发到服务器之前重写 Request Header 或 Response Header。

示例:

```
[Header Rewrite]
http-request ^http://example.com header-add DNT 1
http-request ^http://example.com header-del Cookie
http-request ^http://example.com header-replace User-Agent Unknown
http-response ^http://example.com header-replace-regex Date 2022 2023
```

Rewrite 规则包含多个部分：
1. HTTP 方向：`http-request` 或 `http-response`。 老版本只支持修改请求，此部分可以省略，例如：

    ```
    [Header Rewrite]
    ^http://example.com header-add DNT 1
    ```

2. URL 正则表达式
3. 模式类型
4. Header 字段
5. 值 (header-del 动作不支持)
6. 替换模板 (仅限 header-replace-regex)

### header-add

在头中添加一个新字段，即使该字段已经存在。

示例:

```
[Header Rewrite]
http-request ^http://example.com header-add DNT 1

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

在头中删除一行。

示例:

```
[Header Rewrite]
http-request ^http://example.com header-del DNT

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

在头中更改一个 Header 字段的值。当这个字段不存在时，将不处理。

示例:

```
[Header Rewrite]
http-request ^http://example.com header-replace DNT 1

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


### header-replace-regex

基于正则表达式和模板在头中更改一个 Header 字段的值。当这个字段不存在时，将不处理。
```
[Header Rewrite]
http-request ^http://example.com header-replace-regex User-Agent Safari Chrome

更改前:
GET /index.html HTTP/1.1
Host: example.com
Connection: keep-alive
User-Agent: Mozilla/5.0 (Macintosh; Intel Mac OS X 10_12_4) AppleWebKit/603.1.30 (KHTML, like Gecko) Version/10.1 Safari/603.1.30
Accept-Language: en-us
Accept-Encoding: gzip, deflate
DNT: 0

更改后:
GET /index.html HTTP/1.1
Host: example.com
Connection: keep-alive
User-Agent: Mozilla/5.0 (Macintosh; Intel Mac OS X 10_12_4) AppleWebKit/603.1.30 (KHTML, like Gecko) Version/10.1 Chrome/603.1.30
Accept-Language: en-us
Accept-Encoding: gzip, deflate
DNT: 0
```

