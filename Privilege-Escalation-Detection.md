#  Privilege Escalation Detection
```yaml

index=Index sourcetype="WinEventLog:Security" (EventCode=576 OR EventCode=4672 OR EventCode=577 OR EventCode=4673 OR EventCode=578 OR EventCode=4674) 
| stats count by user
