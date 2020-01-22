### event

Evaluates script while the specified event occurs. The value is the event name. Only one event is supported currently: network-changed.

Please invoke $done() to complete.

A simple example:

```
// event network-changed script-path=network-changed.js

$notification.post('DNS Update', $network.dns.join(', '));

$done();
```

