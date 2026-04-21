index=wineventlog EventCode=4688
| search NewProcessName IN ("*psexec.exe","*wmic.exe","*winrm.cmd")
| table _time, host, user, NewProcessName
