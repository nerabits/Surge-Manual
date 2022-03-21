### 计划任务

可配置 Surge 在特定的时间执行脚本，触发时间配置使用 crontab 的样式。该类型下第二参数为 crontab 表达式，常见的 crontab 为五位表示，即 * * * * * 表示每分钟执行一次，Surge 兼容五位表示和六位表示，可用 * * * * * * 表示每秒钟执行一次。但不支持 @daily 这样的别名。

crontab 表达式撰写方法请参见相关文档，一些样例如下：
* at 2am daily: 0 2 * * * 
* at 5 AM and 5 PM daily: 0 5,17 * * *
* on every minutes: * * * * *
* on every seconds: * * * * * *
* on every Sunday at 5 PM: 0 17 * * sun
* every 10 minutes: \*/10 * * * *

Just one incoming parameter: $cronexp.

脚本任务执行完毕后请调用 $done() 退出

一个简单样例：

```
// cron "0 2 * * *" script-path=cron.js
$surge.setSelectGroupPolicy('Group', 'Proxy');
$done();
```

### 额外的 API

- `$cronexp`：cron表达式字符串。

