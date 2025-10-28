#  Outgoing Emails: Sender Sent to 40+ Recipients
```yaml

index="MailServer" deviceDirection=1  suser!="Uname@email.com" msg!="*Mailer-Daemon*" 
| stats  count by msg ,suser   
| where  count > 50  
| table  suser msg count   | sort  - count
