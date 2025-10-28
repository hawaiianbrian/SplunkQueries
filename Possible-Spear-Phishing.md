#  Outgoing Emails: Possible Spear Phishing Campaign
```yaml

index="Mailserver" deviceDirection=1   suser!="Uname@email.com" 
| eval to_list=split(duser, ";") 
| eval num_recipients=mvcount(to_list) 
| stats  sum(num_recipients) as total_recipients by suser, msg
| where  total_recipients > 40 
| sort - total_recipients
