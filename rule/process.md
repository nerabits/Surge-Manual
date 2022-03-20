# 进程规则

你可以为指定的进程配置策略，进程规则仅适用于 Surge Mac，Surge iOS 会自动忽略这些规则。

#### PROCESS-NAME

```
PROCESS-NAME,Telegram,Proxy
```

如果发出网络请求的进程名与 PROCESS-NAME 中的名称匹配，则规则匹配。

> 你可以指定文件名或可执行文件的完整路径。对于 macOS 应用程序包，它的路径是 .app/Contents/MacOS。