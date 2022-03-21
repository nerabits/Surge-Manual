### HTTP 请求

用于修改 HTTP 请求体，该类型下第二参数为匹配 URL 的正则表达式，被匹配到的请求会被执行脚本。

传入参数为 $request，字段为

* `$request.url<String>`：请求的 URL
* `$request.method<String>`：请求的 HTTP 方法
* `$request.headers<Object>`：请求的 Header
* `$request.body<String or Uint8Array>`：请求的 Body，类型为 String 或 Unit8Array，仅当 requires-body = true 时有效
* `$request.id<String>`：一个特有的ID，以便在脚本之间保持连续性。

应执行 $done 返回一个对象，可选包含字段：
* `url<String>`：使用该 URL 覆盖原请求的 URL，注意使用脚本修改 URL 时不会像 URL Rewrite 那样自动调整 Header 的 Host 字段，如果需要调整需要手动返回新的 headers 字段
* `headers<Object>`：使用该 headers 词典完全覆盖原来的 headers，注意部分 HTTP 特殊字段不可被修改，如 Content-Length
* `body<String or Uint8Array>`：使用该 body 覆盖原来的请求 body，仅当 requires-body = true 时有效。

* `response<Object>`：如果返回了该字段，则表示应直接返回该结果而不进行实际的网络请求，仅当 requires-body = false 时有效。可包含三个字段：
    * `$status<Number>`：响应的 HTTP 状态码。
    * `$headers<Object>`：响应的 HTTP Headers（可选）
    * `$body<String or Uint8Array>`：响应的 HTTP Body（可选）

使用 $done(); 表示终止该请求，使用 $done({}); 表示不对该请求进行修改。

当前版本的一些限制：
* 当请求使用 chunked encoding 上传 body 时，不可以进行 body 修改。
* 当 Expect: 100-continue 存在时，不可以进行 body 修改。

一个简单的示例：

```
let headers = $request.headers;
headers['X-Modified-By'] = 'Surge';

$done({headers});
```

