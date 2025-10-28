# Username guessing brute force attack
```yaml

index=<your_index> sourcetype=WinEventLog:Security EventCode IN (4624,4625)
| bin _time span=5m
| rex field=_raw "Account Name:\s+(?<username>[^\r\n]+)\s+Account Domain:"
| eval username=lower(trim(username))
| where username!="" AND username!="-" AND NOT like(username,"%$")
| stats count AS Attempts
        sum(eval(EventCode=4625)) AS Failed
        sum(eval(EventCode=4624)) AS Success
      by _time username
| where Failed>=4
| stats dc(username) AS Total by _time
| where Total>5
| sort _time
