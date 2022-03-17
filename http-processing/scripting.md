# 脚本

*Surge Mac 3.2.0 / Surge iOS 3.8 及以后版本可用*

您可以使用 JavaScript 来修改 HTTP 响应。

```
[Script]
http-response .* script-path=script.js
```

每行包含 3 个部分：

1. 脚本类型。当前只支持 'http-response'。
2. URL正则表达式。该脚本只适用于匹配的请求。
3. 参数表，用逗号分隔。
   - script-path: 脚本路径，可以是相对路径（在配置文件的同一目录下）、绝对路径或者 URL。
   - script-update-interval: 当脚本路径为 URL 时的自动更新频率，单位为秒。默认值：86400 秒。
   - max-size: 表示该脚本最大允许处理的 body 大小，若超过则放弃处理，默认值为 131072 (128KB)。

由于进行脚本修改会需要 Surge 先将 response body 完全下载到内存后再进行处理，如果遇到了较大的数据将导致内存占用量暴增，Surge iOS 受系统对 Network Extension 内存限制，在该情况下进程极易被直接终止。（iOS 12 最大为 20MB）

所以请仅对需要的 URL 进行处理。

当返回的数据长度超过 max-size 设定值后，Surge 将放弃对该请求执行脚本并回退到 passthrough 模式。

## 编写脚本

Surge 会将几个全局变量传递给JS上下文。

- body[String]: HTTP 响应体
- status[Number]: HTTP 状态码
- method[String]: HTTP 方法
- headers[Object]: HTTP 返回头
- url[String]: 完整的 URL 地址

Surge 使用脚本生成的最后一个值作为结果。以下是对结果类型的定义：

- String: 使用它作为新的响应体。
- Null: 中止请求。
- undefined: 不处理相映。
- Object: 复杂修改
    - 如果 'body' 属性存在，就用其作为新的响应体。
    - 如果 'headers' 属性存在，则使用它们作为新的响应头。请注意，"Content-Length"、"Transfer-Encoding "和 "Content-Encoding "不能被改写。
    - 如果'status' 属性存在，则将其作为新的HTTP状态码。

一个简单的示例：

```
var obj = JSON.parse(body);
obj['surge'] = 'OK';
JSON.stringify(obj);
```

## 杂项

- 由于JavaScript的限制，其只支持对UTF-8编码的响应体进行脚本处理。
- 默认情况下，每个脚本的执行都会被创建一个新的 JS 上下文。您可以配置 "shared-jsvm-context"，让所有脚本共享 JS 上下文，这样可以让脚本共享全局变量的数据。

```
[General]
shared-jsvm-context=true
```

- 你可以使用 'console.log' 来记录到 Surge 的日志文件。
- Surge 请求查看器中的响应头和响应体为修改过的版本。您可以在‘计时 & 日志’标签中检查脚本的执行状态。


