#  File Deletion Attempts
```yaml

index=Index sourcetype="WinEventLog:Security" EventCode=564 
| eval Date=strftime(_time, "%Y/%m/%d") 
| stats count by Date, Image_File_Name, Type, host 
| sort - Date
