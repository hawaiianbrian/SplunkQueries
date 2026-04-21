index=wineventlog EventCode=4624 LogonType=10 OR LogonType=3
| search user IN ("*admin*","*adm*")
| stats count by _time, host, user, LogonType
