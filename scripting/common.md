_脚本功能需要 Surge iOS 4 或 Surge Mac 3.3.0以上版本_

# 脚本

使用 JavaScript 随心所欲地拓展 Surge 功能。

## Script 配置段

```
[Script]
script1 = type=http-response,pattern=^http://www.example.com/test script-path=test.js,max-size=16384,debug=true
scropt2 = type=cron,cronexp="* * * * *",script-path=fired.js
scropt3 = type=http-request,pattern=^http://httpbin.org script-path=http-request.js,max-size=16384,debug=true,requires-body=true
scropt4 = type=dns,script-path=dns.js,debug=true
```

每行配置含有两个部分：脚本名和参数。
常见参数：
 
* `type`：脚本的类型：`http-request`, `http-response`, `cron`, `event`, `dns`, `rule`, `generic`。
* `script-path`：脚本所在目录，可以是配置文件的相对路径、绝对路径，或一个 URL。
* `script-update-interval`：使用URL作为脚本路径时的更新间隔，以秒为单位。
* `debug`：启用调试模式，启用后将产生以下影响：
  1. 每次在评估脚本之前，都会从文件系统中加载该脚本。
  2. 对于 `http-request` 和 `http-response` 脚本，当您使用 `console.log()` 记录消息时，这些消息也会出现在请求的提示中。
* `timeout`：脚本的最长运行时间，默认值为 10 秒。
* `argument`：脚本可以用 `$argument` 来取值。

`http-request` 和 `http-response` 脚本类型的参数：

* `pattern`：用于匹配 URL 的正则表达式。

* `requires-body`：允许脚本修改请求/响应 Body，默认值为 false。此行为开销较大，建议仅在必要时启用。

* `max-size`：表示该脚本最大允许处理的 body 大小，若超过则放弃处理，默认值为 131072 (128KB)。

* `binary-mode`：仅在 iOS 15 和 macOS 上生效。原始的二进制 body 数据将以 Uint8Array 的形式传递给脚本，而非字符串值。

脚本需要 Surge 将整个 body 数据加载到内存。因为 iOS 系统限制了网络扩展所能占用的最大内存量，所以一个巨大的 body 可能会导致 Surge iOS 崩溃。

请只对必要的 URL 启用脚本。

如果响应 body 超过了 `max-size` 值，Surge 将回退到直通模式，并跳过此请求对应脚本的执行。

## 基本定义

所有脚本允许异步操作，使用 $done(value<Object>) 方法表示完成并返回相应结果。即使是不要求返回结果的脚本类型也应当在完成任务后调用 $done() 退出，否则脚本会因为超时而产生警告。

## 性能

JS Script 的执行效率极高，不必担心因使用脚本而带来性能问题。

## 公共 API

### 基本信息

* **`$network`**

此对象包含当前网络状态的基本信息。

* **`$script`**

  - `$script.name<String>`：当前执行的脚本的文件名
  - `$script.startTime<Date>`：当前执行的脚本的开始时间
  - `$script.type<String>`：当前脚本类型

* **`$environment`**

  - `$environment.system<String>`：iOS 或 macOS
  - `$environment.surge-build<String>`：Surge 当前的 build 编号
  - `$environment.surge-version<String>`：Surge 当前的版本号
  - `$environment.language<String>`：Surge 当前的图形界面语言

### 持久化保存

* **`$persistentStore.write(data<String>, [key<String>])`**

持久化保存数据，返回 bool 值表示是否成功，仅支持传入 string。

* **`$persistentStore.read([key<String>])`**

读取保存的持久化数据，返回 string 或 Null。

不传入 key 时，同一个 script-path 的脚本共享一个存储池。可传入一个固定的 key 以在多个脚本间共享数据。

提示：Surge Mac 写入 $persistentStore 数据到目录 `~/Library/Application Support/com.nssurge.surge-mac/SGJSVMPersistentStore/`。您可以直接在此处编辑文件以进行调试。

### 控制 Surge

* **`$httpAPI(method<String>, path<String>, body<String>, callback<Function>(result<Object>))`**

你可以使用 $httpAPI 来调用所有的 HTTP API 来控制 Surge 的功能。不需要认证参数。关于可用的功能，见 HTTP API 部分。


### 工具

* **`console.log(message<String>)`**

记录到 Surge 日志文件中。

* **`setTimeout(function[, delay])`**

与浏览器中的 setTimeout 相同。

* **`$httpClient.post(URL<String> or options<Object>, callback<Function>)`**

执行一个 HTTP POST 请求，第一位参数可以是一个 URL，或者参数表，参数表为

```
{
  url: "http://www.example.com/",
    headers: {
    Content-Type: "application/json"
    },
  body: "{}"
}
```

当使用参数表时，`url` 参数必填，其余选填，`headers` 字段存在将覆盖默认的所有 headers，`body` 可以为 string 或者 object，为 object 时将自动进行 JSON 编码并设置 Content-Type 为 `application/json`。

你可以指定执行请求的策略：
   - `policy`：使用现有策略及其名称。 {{book.BETA}}
   - `policy-descriptor`：使用具有完整描述符的临时策略。 {{book.BETA}}

你必须预先声明 `ability=http-client-policy` 才能使用此选项。

callback 定义为 callback(error<String>, response<Object>, data<String>)

error 为 null 表示请求成功，response 对象包含 status 和 headers 两个字段。

其余类似的方法有：**$httpClient.get**, **$httpClient.put**，**$httpClient.delete**, **$httpClient.head**, **$httpClient.options**, **$httpClient.patch**.

请求超时时间为 5 秒。

* **`$notification.post(title<String>, subtitle<String>, body<String>)`**

向通知中心发送通知，Surge iOS 上需开启通知总开关。

* **`$utils.geoip(ip<String>)`**

进行 GeoIP 查询，返回结果为 ISO 3166 的国家编码。

* **`$utils.ipasn(ip<String>)`**

查询 IP 地址的 ASN。

* **`$utils.ipaso(ip<String>)`**

查询 IP 地址的 ASO。

* **`$utils.ungzip(binary<Uint8Array>)`**

解压 gzip 数据。结果也是一个 Uint8Array。

### 手动触发

你可以通过长按脚本或使用系统的快捷指令 App 在 Surge iOS 上手动触发一个脚本。

如果你使用快捷指令来触发一个脚本，可以选择将参数传递给脚本，并且使用 `$intent.parameter` 来检索它。

