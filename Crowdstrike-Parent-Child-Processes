#  Crowdstrike Parent-Child Processes
```yaml

index=crowdstrike event_simpleName=ProcessRollup2
| search ParentBaseFileName=winword.exe OR ParentBaseFileName=excel.exe OR ParentBaseFileName=powershell.exe
| table _time, aid, ComputerName, ParentBaseFileName, FileName, CommandLine, userName
| sort - _time
