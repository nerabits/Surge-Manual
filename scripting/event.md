### 事件

在发生特定事件时执行脚本，该类型下第二参数为事件名称。

脚本任务执行完毕后请调用 $done() 退出。


#### 事件类型

- `network-changed`: 当系统网络发生变化时触发。
```
// network-changed = script-path=network-changed.js,type=event,event-name=network-changed

$notification.post('DNS Update', $network.dns.join(', '));

$done();
```

- `notification`：当 Surge 显示通知时触发。即使通知类别为 off，脚本仍然可以获取消息。

```
// notification = script-path=notification.js,type=event,event-name=notification
console.log($event.data);
$done();
```
