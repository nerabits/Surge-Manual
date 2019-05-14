# Header Rewrite

**This feature is only available in the beta version currently.**

Surge can rewrite request header sent by the clients before they are forwarded to the server.

Example:

```
[Header Rewrite]
^http://example.com header-add DNT 1
^http://example.com header-del Cookie
^http://example.com header-replace User-Agent Unknown
```

The rewrite rule consists 4 parts: URL regular expression, action type, header field and value.

### header-add

Append an new header line to request header, even the header field already exists.

Example:

```
[Header Rewrite]
^http://example.com header-add DNT 1

Before:
GET /index.html HTTP/1.1
Host: example.com
Connection: keep-alive
User-Agent: Mozilla/5.0 (Macintosh; Intel Mac OS X 10_12_4) AppleWebKit/603.1.30 (KHTML, like Gecko) Version/10.1 Safari/603.1.30
Accept-Language: en-us
Accept-Encoding: gzip, deflate

After:
GET /index.html HTTP/1.1
Host: example.com
Connection: keep-alive
User-Agent: Mozilla/5.0 (Macintosh; Intel Mac OS X 10_12_4) AppleWebKit/603.1.30 (KHTML, like Gecko) Version/10.1 Safari/603.1.30
Accept-Language: en-us
Accept-Encoding: gzip, deflate
DNT: 1
```

### header-del

Delete a header line from the request header.

Example:

```
[Header Rewrite]
^http://example.com header-del DNT

Before:
GET /index.html HTTP/1.1
Host: example.com
Connection: keep-alive
User-Agent: Mozilla/5.0 (Macintosh; Intel Mac OS X 10_12_4) AppleWebKit/603.1.30 (KHTML, like Gecko) Version/10.1 Safari/603.1.30
Accept-Language: en-us
Accept-Encoding: gzip, deflate
DNT: 1

After:
GET /index.html HTTP/1.1
Host: example.com
Connection: keep-alive
User-Agent: Mozilla/5.0 (Macintosh; Intel Mac OS X 10_12_4) AppleWebKit/603.1.30 (KHTML, like Gecko) Version/10.1 Safari/603.1.30
Accept-Language: en-us
Accept-Encoding: gzip, deflate
```

### header-replace

Replace a header value in the request header. If the header field doesn't exist, nothing happens.

Example:

```
[Header Rewrite]
^http://example.com header-replace DNT 1

Before:
GET /index.html HTTP/1.1
Host: example.com
Connection: keep-alive
User-Agent: Mozilla/5.0 (Macintosh; Intel Mac OS X 10_12_4) AppleWebKit/603.1.30 (KHTML, like Gecko) Version/10.1 Safari/603.1.30
Accept-Language: en-us
Accept-Encoding: gzip, deflate
DNT: 0

After:
GET /index.html HTTP/1.1
Host: example.com
Connection: keep-alive
User-Agent: Mozilla/5.0 (Macintosh; Intel Mac OS X 10_12_4) AppleWebKit/603.1.30 (KHTML, like Gecko) Version/10.1 Safari/603.1.30
Accept-Language: en-us
Accept-Encoding: gzip, deflate
DNT: 1
```

If you would like to add or replace a header line whenever the field exists. You may use header-add and header-del together.

```
[Header Rewrite]
^http://example.com header-del DNT
^http://example.com header-add DNT 1
```