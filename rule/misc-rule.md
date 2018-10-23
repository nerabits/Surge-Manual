# Miscellaneous Rule

#### DEST-PORT

Rule matches if the target port of the request matches.

```
DEST-PORT,80,DIRECT
```

#### SRC-IP

Rule matches if the client IP address of the request matches. Only for remote machines.

```
SRC-IP,192.168.20.100,DIRECT
```


#### IN-PORT

Rule matches if the incoming port of the request matches. Useful while Surge listening on multiple ports.

```
IN-PORT,6152,DIRECT
```