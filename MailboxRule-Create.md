index=o365 sourcetype=exchange
| search operation="New-InboxRule" OR operation="Set-InboxRule"
| table _time, user, operation
