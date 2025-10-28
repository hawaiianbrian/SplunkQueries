#  Successful file access (must have object access auditing enabled)
```yaml

index=INDEX sourcetype=WinEventLog (Relative_Target_Name!="\\""" Relative_Target_Name!="*.ini") user!="*$" 
| bucket span=1d _time 
| stats count by Relative_Target_Name, user, _time, status 
| rename _time as Day 
| convert ctime(Day)
