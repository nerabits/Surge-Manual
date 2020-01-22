### policy-group

Uses a script as a policy group. The value field will be used as a name.

`policy-group jsgroup script-path=group.js`

Then add a line in [Policy Group] section:

```
[Policy Group]
sgroup = script, policyA, policyB, policyC, script-name=jsgroup
```

The incoming parameter is $policyNames<Array>, which is an array of available policy names.

The script should return a policy name like this: {selected: "policy-name"}


