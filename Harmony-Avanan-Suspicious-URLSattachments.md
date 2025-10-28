#  Checks for suspicious URLs or Attachments in Avanan/Harmony
```yaml

index=avanan sourcetype=avanan:email
| search (attachmentType="exe" OR attachmentType="js" OR ESAURLDetails.malicious=true)
| table _time, sender, recipient, subject, attachmentName, ESAURLDetails
