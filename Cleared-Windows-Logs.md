#  Cleared Windows Logs
```yaml

index="your index name here" source=WinEventLog:security (EventCode=1102 OR EventCode=517) 
| eval Date=strftime(_time, "%Y/%m/%d") 
| stats count by Client_User_Name, host, index, Date 
| sort - Date 
| rename Client_User_Name as "Account Name"
