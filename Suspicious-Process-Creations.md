#  Suspicious Process Creations in SentinelOne
```yaml

index=sentinelone sourcetype=sentinelone:process
| search actionType=EXECUTED
| table _time, agentComputerName, userName, parentProcess, processName, commandLine
| sort - _time
