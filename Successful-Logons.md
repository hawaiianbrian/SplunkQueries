#  Successful Logons
```yaml

index=INDEX source="WinEventLog:security" EventCode=4624 Logon_Type IN (2,7,10,11) NOT user IN ("DWM-*", "UMFD-*")
| eval Workstation_Name=lower(Workstation_Name)
| eval host=lower(host)
| eval hammer=_time 
| bucket span=12h hammer 
| stats values(Logon_Type) as "Logon Type" count sparkline by user host, hammer, Workstation_Name
| rename hammer as "12 hour blocks" host as "Target Host" Workstation_Name as "Source Host"
| convert ctime("12 hour blocks")
| sort - "12 hour blocks"
