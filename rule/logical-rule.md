# 逻辑规则

使用逻辑运算符来组合多个规则，以应对复杂的情况。你可以将一个逻辑规则包含在另一个逻辑规则中。


#### AND 规则

如果全部子规则匹配，则该规则匹配。

```
AND,((#Rule1), (#Rule2), (#Rule3)...),Policy
```

示例：
```
AND,((SRC-IP,192.168.1.110), (DOMAIN, example.com)),DIRECT
```

#### OR 规则

只要有子规则匹配，则该规则匹配。

`OR,((#Rule1), (#Rule2), (#Rule3)...),Policy`

示例：
```
OR,((SRC-IP,192.168.1.110), (SRC-IP,192.168.1.111)),DIRECT
```

#### NOT 规则

反转原始规则的评估结果。

```
NOT,((#Rule1)),Policy
```


示例：
```
AND,((NOT,((SRC-IP,192.168.1.110))),(DOMAIN, example.com)),DIRECT
```

