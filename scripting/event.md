### 事件

在发生特定事件时执行脚本，该类型下第二参数为事件名称，目前只有 network-changed 一个事件。

脚本任务执行完毕后请调用 $done() 退出。

一个简单样例：

```
// event network-changed script-path=network-changed.js

$notification.post('DNS Update', $network.dns.join(', '));

$done();
```

