#  Find PWs Entered as Usernames
```yaml

index=Index source=WinEventLog:Security TaskCategory=Logon Keywords="Audit Failure" 
| eval password=if(match(User_Name, "^(?=.*[a-z])(?=.*[A-Z])(?=.*[0-9])(?=.*[\W])(?=.{10,})"), "Yes", "No") 
| stats count by password User_Name 
| search password=Yes
