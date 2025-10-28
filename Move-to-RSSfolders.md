#  Exchange Inbox Rules: Move to RSS Folders
```yaml

(index=* sourcetype="MSExchange:InboxRules" RedirectTo!="" OR (MoveToFolder="rss*")) OR (index="MSexchange" action=NewInboxRule AND X_Forwarded_For!="10.*") 
| timechart span=24h count
