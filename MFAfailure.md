index=o365 sourcetype=azure:signin
| search status="failure"
| stats count by user
| where count > 10
