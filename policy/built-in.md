# 内置策略

Surge 支持两种内置策略：DIRECT 和 REJECT。配置为 DIRECT 时，Surge 会将请求直接发送到服务端。配置为 REJECT 时，Surge 会直接拒绝请求。

DIRECT 和 REJECT 可直接用于规则和策略组。或者您也可以使用别名来定义这两个内置策略。

### 别名

```
[Proxy]
On = direct
Off = reject
```

之后，您就可以使用 'On' 和 'Off' 作为规则和策略组的策略名了。

