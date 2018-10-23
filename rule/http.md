# HTTP Rule

There are 2 HTTP rule types. HTTP rule is for HTTP requests or HTTPS requests. It won't effect TCP connections.

#### USER-AGENT

```
USER-AGENT,Instagram*,DIRECT
```

Rule matches if the user agent of the request matches. Wildcard characters * and ? are supported.

#### URL-REGEX

`URL-REGEX,^http://google\.com,DIRECT`

Rule matches if the URL matches the regular expression.