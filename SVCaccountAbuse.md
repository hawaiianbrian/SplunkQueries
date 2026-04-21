index=wineventlog EventCode=4624
| search user="svc_*"
| stats count by user, host
