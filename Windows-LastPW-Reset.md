#  Windows PW last reset
```yaml
index=windows* EventCode=4738 
| table _time,Account_Name,Password_Last_Set,signature,EventCode,Message 
| sort -_time
