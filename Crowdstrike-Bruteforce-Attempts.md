#  Crowdstrike Bruteforce Attempts (evt/5m)
```yaml

index=crowdstrike event_simpleName=AuthFailed 
| bin _time span=5m
| stats count by userName, src_ip, _time
| where count > 5
| table _time, userName, src_ip, count
