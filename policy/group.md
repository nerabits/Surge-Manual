# 策略组

一个策略组可以包含多个策略，其中的策略可以是代理策略、其他策略组或内置策略 \(DIRECT 和 REJECT\)。

策略组有五个类型：‘select‘、’url-test‘、’fallback‘、’load-balance‘ 和 ’subnet‘。片段 \[Proxy Group\] 用于声明策略组。

## 手动选择策略组

在图形界面中选择需要使用的策略。

`SelectGroup = select, ProxyHTTP, ProxyHTTPS, DIRECT, REJECT`

> 在 iOS 版本中，你可以使用小组件来快速选择第一个手动选择策略组中的策略。
> 在 macOS 版本中，你可以在菜单栏的下拉菜单中选择策略。

## URL 自动测试策略组

通过对测试URL的延迟进行基准测试，自动选择使用的策略。你可以在一般设置中更改测试 URL，或者覆盖某个策略的测试 URL。

`AutoTestGroup = url-test, ProxySOCKS5, ProxySOCKS5TLS`

### 参数

#### interval：可选，单位为秒 \(默认：600秒\).

超过此时间间隔，将不再测试。除非重新使用此策略组。

#### tolerance：可选，单位为毫秒 \(默认：100毫秒\).

每次重新测试时，当此次测试的最低延迟比上一组测试的最低延迟少对应的设置值时，才会应用新策略。

此选项可防止具有相似延迟的策略不断自动切换。

#### timeout：可选，单位为秒 \(默认：5秒\).

测试时在超过设定时间仍无响应，则自动放弃对应策略。

## Fallback 策略组

按优先级和可用性来选择一个可用的策略，通过访问一个URL来测试其可用性，就像 URL 自动测试策略组一样。优先级从前到后依次降低。

`FallbackGroup = fallback, ProxySOCKS5, ProxySOCKS5TLS`

### 参数

#### interval：可选，单位为秒 \(默认：600秒\).

超过此时间间隔，将不再测试。除非重新使用此策略组。

#### timeout：可选，单位为秒 \(默认：5秒\).

测试时在超过设定时间仍无响应，则自动放弃对应策略。

## 负载均衡策略组

负载均衡组从可用的子策略中随机选择一个策略来使用。


### 参数

#### persistent：可选

当 persistent=true，尽可能对同一目标主机名使用相同的策略。避免因出口 IP 不同而触发目标站点的风险控制。但是，当可用性发生变化时，策略可能会发生变化。


## Subnet 策略组

自 Surge iOS 4.12.0 和 Surge Mac 4.5.0，SSID 策略组被重命名为 Subnet 策略组。在此情况下，你可以使用 [subnet expression](../rule/subnet.md) 

虽然仍被称为 SSID 策略组，但它已经扩展到包括根据当前网络的 SSID、BSSID、路由 IP 地址等选择子策略的能力。iOS 版本还可以为数据网络指定策略。

`Subnet Group = subnet, default = ProxyHTTP, cellular = ProxyHTTP, SSIDName = ProxySOCKS5`

目前仍然支持 SSID 组的旧语法。您可以使用组类型关键字 `subnet` 或 `ssid` 来实现多版本兼容。

### 参数

#### default：必需

没有找到匹配的 subnet 选项时的策略。

#### cellular：可选 (已废弃，使用 TYPE:CELLULAR 替代)

蜂窝网络下的策略。如果没有提供，将使用默认策略。

## 外置策略组

从 Surge Mac v3.0 和 Surge iOS v3.4 开始，可向策略组中导入在外部文件或 URL 中定义的策略。

`egroup = select, policy-path=proxies.txt`

该文件包含一个策略列表，就像主配置文件中的定义一样。

```
Proxy-A = https, example1.com, 443
Proxy-B = https, example2.com, 443
```

#### update-interval: 可选，单位为秒

如果路径是一个URL，则为更新间隔。

#### policy-regex-filter: 可选，

使用正则表达式与外部文件中的策略名匹配后，仅使用匹配的策略。

## 其他通用参数

#### no-alert

不显示该组策略变化通知。

#### hidden

不要在菜单（Surge Mac）和策略组标签（Surge iOS）中显示该组。


## 策略包含

从 Surge iOS 4.12.0 和 Surge Mac 4.5.0 开始，你可以使用 include-all-proxies 和 include-other-group 参数来包含全部代理策略或重用其他策略组的定义的策略。

#### include-all-proxies

参数 include-all-proxies=true 包含在 [Proxy] 段中定义的全部代理策略。可使用 policy-regex-filter 参数对策略进行筛选。

#### include-other-group

参数 include-other-group="group1,group2" 包含其他策略组中的策略，可以包含多个策略组（使用逗号分隔），也可使用 policy-regex-filter 参数对策略进行筛选。

一些说明：
- include-all-proxies、include-other-group 和 policy-path 参数允许同时在一个策略组中使用。policy-regex-filter 参数适用于以上所有参数。
- 对于 include-other-group 参数，各策略组之间有优先顺序。但 include-all-proxies、include-other-group 和 policy-path 参数之间没有优先顺序。对于子策略的顺序有意义的情况（例如，Fallback 策略组），则可使用该策略组与 include-other-group 嵌套。


