#  Checking for New Local Admin Accounts
```yaml
index=windows* (EventCode=4720 OR EventCode=4732)
| table _time, ComputerName, TargetUserName, SubjectUserName, Message
| sort - _time
