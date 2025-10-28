#  Mailserver Changes

```yaml
index=MailServerAudit "*changes*" |  table _time user desc 
| timechart span=24h count
