#  Account Deleted within 24 hours of Creation
```yaml

index=Index sourcetype=WinEventLog:Security (EventCode=4726 OR EventCode=4720) 
| eval Date=strftime(_time, "%Y/%m/%d") 
| rex "Subject:\s+\w+\s\S+\s+\S+\s+\w+\s\w+:\s+(?<SourceAccount>\S+)" 
| rex "Target\s\w+:\s+\w+\s\w+:\s+\S+\s+\w+\s\w+:\s+(?<DeletedAccount>\S+)" 
| rex "New\s\w+:\s+\w+\s\w+:\s+\S+\s+\w+\s\w+:\s+(?<NewAccount>\S+)" 
| eval SuspectAccount=coalesce(DeletedAccount,NewAccount) 
| transaction SuspectAccount startswith="EventCode=4720" endswith="EventCode=4726" 
| eval duration=round(((duration/60)/60)/24, 2) 
| eval Age=case(duration<=1, "Critical", duration>1 AND duration<=7, "Warning", duration>7, "Normal")
| table Date, index, host, SourceAccount, SuspectAccount, duration, Age 
| rename duration as "Days Account was Active" 
| sort + "Days Account was Active"
