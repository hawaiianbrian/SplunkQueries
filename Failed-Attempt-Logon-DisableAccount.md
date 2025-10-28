#  Failed Attempted Logon Disabled Accounts
```yaml

index=Index source="WinEventLog:security" EventCode=4625 (Sub_Status="0xc0000072" OR Sub_Status="0xC0000072") Security_ID!="NULL SID" Account_Name!="*$" 
| eval Date=strftime(_time, "%Y/%m/%d")
| rex "Which\sLogon\sFailed:\s+\S+\s\S+\s+\S+\s+Account\sName:\s+(?<facct>\S+)" 
| eval Date=strftime(_time, "%Y/%m/%d") 
| stats count by Date, facct, host, Keywords 
| rename facct as "Target Account" host as "Host" Keywords as "Status" count as "Count"
