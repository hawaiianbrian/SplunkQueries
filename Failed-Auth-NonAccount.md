#  Failed Authentication to Non-Existing Account
```yaml

index=Index source="WinEventLog:security" sourcetype="WinEventLog:Security" EventCode=4625 Sub_Status=0xC0000064 
| eval Date=strftime(_time, "%Y/%m/%d") 
| rex "Which\sLogon\sFailed:\s+Security\sID:\s+\S.*\s+\w+\s\w+\S\s.(?<uacct>\S.*)" 
| stats count by Date, uacct, host 
| rename count as "Attempts" 
| sort - Attempts
