### 策略组

使用脚本去决定 policy-group，该类型下第二参数为脚本名。

`policy-group jsgroup script-path=group.js`

然后在 [Policy Group] 配置段中加入规则：

```
[Policy Group]
sgroup = script, policyA, policyB, policyC, script-name=jsgroup
```

传入参数为 $policyNames<Array>，指定的可用策略名数组。

返回结果为 {selected: "policy-name"}，选定的策略名称。


