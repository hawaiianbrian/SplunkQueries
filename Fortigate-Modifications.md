#  Fortigate Modifications
```yaml

index=fortigate  logdesc="Object attribute configured" AND NOT ui=ha_daemon
| table _time user src_ip action cfgpath msg cfgattr
| timechart span=1d count ,values(action) 
| sort _time
