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


#### PROTOCOL 

Rule matches if the protocol of the request matches. The possible values are HTTP, HTTPS, TCP, UDP, DOH.

```
PROTOCOL,HTTP,DIRECT
```

#### SCRIPT

Use a Javascript script to determine whether it matches.

```
SCRIPT,ScriptName,DIRECT
```


#### CELLULAR-RADIO (iOS Only)

Rule matches if the cellular radio technology of the current network matches. The possible values are GPRS, Edge, WCDMA, HSDPA, HSUPA, CDMA1x, CDMAEVDORev0, CDMAEVDORevA, CDMAEVDORevB, eHRPD, HRPD, LTE, NRNSA, NR

```
CELLULAR-RADIO,LTE,DIRECT
```


#### CELLULAR-CARRIER (iOS Only)

Rule matches if the cellular carrier of the current network matches. The value should be in MCC-MNC code style.

```
CELLULAR-CARRIER,289-67,DIRECT
```


