#  Disabled Account Re-enabled
```yaml

index=INDEX sourcetype=WinEventLog:Security (EventCode=4722) 
| eval Date=strftime(_time, "%Y/%m/%d") 
|rex "ID:\s+\w+\\\(?<sourceaccount>\S+)\s+" 
| rex "Account:\s+Security\sID:\s+\w+\\\(?<targetaccount>\S+)\s+" 
| stats count by Date, sourceaccount, targetaccount, Keywords, host 
| rename sourceaccount as "Source Account" 
| rename targetaccount as "Target Account" 
| sort - Date
