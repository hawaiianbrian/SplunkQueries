#  User Logon, Logoff, and Duration
```yaml

index=Index source="wineventlog:security" action=success Logon_Type=2 (EventCode=4624 OR EventCode=4634 OR EventCode=4779 OR EventCode=4800 OR EventCode=4801 OR EventCode=4802 OR EventCode=4803 OR EventCode=4804 ) user!="anonymous logon" user!="DWM-*" user!="UMFD-*" user!=SYSTEM user!=*$ (Logon_Type=2 OR Logon_Type=7 OR Logon_Type=10)
| convert timeformat="%a %B %d %Y" ctime(_time) AS Date 
| streamstats earliest(_time) AS login, latest(_time) AS logout by Date, host
| eval session_duration=logout-login 
| eval h=floor(session_duration/3600) 
| eval m=floor((session_duration-(h*3600))/60) 
| eval SessionDuration=h."h ".m."m " 
| convert timeformat=" %m/%d/%y - %I:%M %P" ctime(login) AS login 
| convert timeformat=" %m/%d/%y - %I:%M %P" ctime(logout) AS logout 
| stats count AS auth_event_count, earliest(login) as login, max(SessionDuration) AS sesion_duration, latest(logout) as logout, values(Logon_Type) AS logon_types by Date, host, user
