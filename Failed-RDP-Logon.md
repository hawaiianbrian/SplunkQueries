#  Failed RDP Logon
```yaml

index=INDEX source=WinEventLog:Security sourcetype=WinEventLog:security Logon_Type=10 EventCode=4625 
| eval Date=strftime(_time, "%Y/%m/%d") 
| rex "Failed:\s+.*\s+Account\sName:\s+(?<TargetAccount>\S+)\s" 
| stats count by Date, TargetAccount, Failure_Reason, host 
| sort - Date
